# JatiMaps 🗺️

An interactive, graph-based city route visualiser for Indonesian cities. JatiMaps simulates a weighted road network of up to 10 major Indonesian cities and lets you find the **shortest path** between any two cities (Dijkstra's algorithm) and compute the **optimal tour** across all cities (Traveling Salesman Problem via brute-force). Every run generates a randomised graph and renders it visually using NetworkX and Matplotlib.

---

## Features

- **Shortest Path (Dijkstra)** — finds the fastest route between any two cities using a min-heap priority queue implementation
- **Traveling Salesman Problem (TSP)** — computes the minimum-distance tour visiting all 10 cities via brute-force permutation search
- **Randomised Graph Generation** — on each run, 10 cities and 30 edges with realistic weights (10–100 km) are generated randomly, keeping the simulation fresh
- **Interactive Graph Visualisation** — renders the full city graph with edge weights; highlights the Dijkstra route in red using NetworkX and Matplotlib
- **Real Indonesian City Names** — nodes map to actual major cities: Surabaya, Jakarta, Bandung, Yogyakarta, Semarang, Malang, Medan, Palembang, Makassar, and Bali

---

## City Reference

When prompted, use the `Kota_N` identifiers below:

| ID | City |
|---|---|
| `Kota_1` | Surabaya |
| `Kota_2` | Jakarta |
| `Kota_3` | Bandung |
| `Kota_4` | Yogyakarta |
| `Kota_5` | Semarang |
| `Kota_6` | Malang |
| `Kota_7` | Medan |
| `Kota_8` | Palembang |
| `Kota_9` | Makassar |
| `Kota_10` | Bali |

---

## Prerequisites

- **Python 3.8+**
- **pip**

---

## Installation

```bash
# 1. Clone the repository
git clone https://github.com/Masykster/JatiMaps.git
cd JatiMaps

# 2. Install dependencies
pip install networkx matplotlib
```

No virtual environment is strictly required, but one is recommended:

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install networkx matplotlib
```

---

## Usage

```bash
python index.py
```

**Example session:**

```
--- Daftar Kota ---
Kota_1: Surabaya
Kota_2: Jakarta
...

Masukkan kota asal (misal: Kota_1): Kota_1
Masukkan kota tujuan (misal: Kota_5): Kota_5

Jalur tercepat dari Surabaya ke Semarang: ['Surabaya', 'Yogyakarta', 'Semarang']
Total jarak tempuh: 87 km
```

After displaying the Dijkstra result, a **graph visualisation window** opens — the shortest path is drawn in red over the full city network. Close the window to continue.

```
Menjalankan TSP (brute-force)... Mohon tunggu beberapa saat...
Rute TSP terbaik: ['Surabaya', 'Malang', 'Bali', ...]
Total jarak tempuh TSP: 512 km
```

> ⚠️ **TSP performance note:** Brute-force TSP has O(n!) time complexity. With 10 cities (10! = 3,628,800 permutations) and a randomly connected graph, computation can take **several minutes** depending on your hardware. This is expected behaviour — the terminal will display a waiting message.

---

## How It Works

```
index.py
│
├── nama_kota          — dict mapping Kota_N keys → Indonesian city names
│
├── Graph (class)
│   ├── add_vertex()   — register a node in the adjacency list
│   ├── add_edge()     — add an undirected weighted edge (bidirectional)
│   ├── dijkstra()     — min-heap shortest path; returns (path, total_distance)
│   └── tsp_brute_force() — exhaustive permutation search; returns (path, total_distance)
│
├── visualize_graph()  — draws the NetworkX graph via Matplotlib;
│                        highlights the Dijkstra path in red when provided
│
└── main (script)
    ├── Build graph: 10 vertices + 30 random edges (weight 10–100 km)
    ├── Prompt user for source and destination
    ├── Run Dijkstra → print result → visualise
    └── Run TSP → print optimal tour + total distance
```

---

## Dependencies

| Package | Purpose |
|---|---|
| `networkx` | Graph data structure, layout, and drawing utilities |
| `matplotlib` | Rendering the graph visualisation window |
| `heapq` | Built-in — priority queue for Dijkstra |
| `itertools` | Built-in — `permutations` for brute-force TSP |
| `random` | Built-in — random edge generation |

---

## Project Structure

```
JatiMaps/
├── index.py   # Single-file application — all logic and visualisation
└── README.md
```
