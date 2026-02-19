# 🕸️ Classroom Social Network Analysis
### *Mapping the invisible architecture of human connection using Graph Theory*

<div align="center">

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)
![NetworkX](https://img.shields.io/badge/NetworkX-Graph_Analysis-FF6B35?style=for-the-badge)
![Pandas](https://img.shields.io/badge/Pandas-Data_Wrangling-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

</div>

---

> **"Every friendship is an edge. Every person is a node. But not all nodes are equal."**
>
> This project applies **Graph Theory** and **Network Science** to a real-world classroom dataset — mapping social bonds, detecting hidden communities, and identifying the students who hold the network together.

---

## What This Project Does

Given a real dataset of friendships within a college classroom, this notebook constructs and analyzes a **social graph** to answer questions that no survey or spreadsheet could:

- Who is the **most influential** person in the room?
- Which students act as **bridges** between otherwise disconnected groups?
- What **hidden communities** exist beneath the surface?
- How does information **flow** through the class?

---

##  Key Findings at a Glance

| Metric | Value | Interpretation |
|---|---|---|
| **Nodes (Students)** | ~35+ | Full class representation |
| **Edges (Friendships)** | Multiple | All unique, undirected connections |
| **Network Density** | **0.23** | 23% of all possible friendships exist — realistic & healthy |
| **Graph Diameter** | **4** | Any two students are ≤ 4 hops apart (*Small World Effect* ✅) |
| **Avg. Clustering Coeff.** | **~0.59** | If A is friends with B & C → 59% chance B & C are also friends |
| **Isolated Students** | **0** | Every student has at least one connection |

---

## 🔬 Analysis Pipeline

```
Raw Excel Data
      │
      ▼
   Data Cleaning
  ├── Duplicate record removal (e.g., "Devanshu Sabhrawal" appeared 3×)
  └── Self-loop detection & elimination
      │
      ▼
  Graph Construction (NetworkX)
  └── Undirected Graph G with all valid friendship edges
      │
      ▼
 Centrality Analysis
  ├── Degree Centrality     → Who knows the most people?
  ├── Betweenness Centrality → Who connects disparate groups?
  ├── Closeness Centrality  → Who spreads info fastest?
  └── PageRank              → Who is most "influential"?
      │
      ▼
 Community Detection
  ├── Greedy Modularity (baseline)
  └── Girvan-Newman (divisive) → 5 distinct social circles identified
      │
      ▼
 Bridge Analysis
  └── Cross-community edges that prevent network fragmentation
```

---

##  Who Runs The Room? — Centrality Rankings

### Degree Centrality *(Most Popular)*
**ARUSH RANJAN** — directly connected to ~**57%** of the class. The drop-off to the next student (~40%) reveals a **centralized, hub-and-spoke** structure rather than a distributed one.

### Betweenness Centrality *(The Gatekeeper)*
**SIDDHESH BANSAL** — despite not being the most popular, he sits on the shortest path between more pairs than anyone else. He is a **critical information broker** bridging distinct social circles.

###  Closeness Centrality *(Fastest Information Spreader)*
**ARUSH RANJAN & BANOTU SANTHOSH** — positioned at the geometric center of the graph. A rumor starting with them reaches everyone with the fewest hops.

---

## Community Detection — 5 Distinct Social Circles

Using the **Girvan-Newman Divisive Clustering** algorithm (which outperformed Greedy Modularity for this dataset):

| Community | Identity | Binding Factor |
|---|---|---|
| 🟠 **Orange** | "The South Cluster" | Regional / geographic origin |
| 🟣 **Purple** | "The Hostel Cluster" | Residential proximity (hostel wing) |
| 🔵 **Blue** | "The Female Cluster" | Gender-based social cohesion |
| 🟢 **Green** | Sub-community | Mixed ties |
| 🔴 **Red** | Sub-community | Mixed ties |

> **Key Insight:** Social circles form primarily around **residence** (hostel wing) and **regional origin**, not academic performance or class seating — mirroring real-world sociological findings.

---

##  Network Bridges — The Students Who Hold It All Together

| Student | Function | Why It Matters |
|---|---|---|
| **Badagoni Sri Sahasra** | Connects the Female Cluster → South Cluster via Arush Ranjan | Prevents the structural isolation of the Female Cluster |
| **Madan Vishwakarma** | Bridges the Hostel Cluster ↔ South Cluster | Enables cross-group information flow between the two dominant subgroups |

> Remove these students from the graph, and the network **fractures**. They are structurally irreplaceable.

---

##  Limitations & Critical Reflections

This analysis acknowledges its own blind spots — because good data science always does:

1. **Overlapping Group Problem** — Girvan-Newman forces hard community boundaries. Real students can belong to multiple circles simultaneously (e.g., South Indian + Hostel resident).
2. **Static Snapshot** — Social networks evolve. This is a single point-in-time capture; friendship ties form and dissolve.
3. **Self-Reported Bias** — The source data reflects *perceived* friendships, not necessarily *mutual* ones.
4. **Undirected Graph Assumption** — All edges are treated as bidirectional, which may not always reflect reality.

---

##  Tech Stack

| Tool | Purpose |
|---|---|
| `pandas` | Data ingestion, cleaning, and manipulation |
| `networkx` | Graph construction and all centrality algorithms |
| `matplotlib` | Custom graph visualizations |
| `numpy` | Numerical operations |
| Greedy Modularity + Girvan-Newman | Community detection algorithms |
| PageRank (α=0.85) | Influence scoring |

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone <your-repo-url>

# 2. Install dependencies
pip install pandas networkx matplotlib numpy openpyxl

# 3. Add your data file to the project directory
# (Ensure 'Friendship Network.xlsx' is present)

# 4. Launch the notebook
jupyter notebook friendshipgraph.ipynb
```

---

##  Project Structure

```
 friendship-network-analysis
 ┣  friendshipgraph.ipynb     ← Main analysis notebook
 ┣  data/Friendship Network.xlsx   ← Source data (student friendship survey)
 └  README.md
```

---

##  Future Scope

- [ ] Build a **directed graph** to model asymmetric friendships (A considers B a friend, but not vice versa)
- [ ] Apply **temporal analysis** — how does the network change over a semester?
- [ ] Use **overlapping community detection** (e.g., BIGCLAM) to handle students belonging to multiple groups
- [ ] Build an **interactive visualization** using Gephi or Pyvis

---

<div align="center">

*Built with curiosity and NetworkX · Graph Theory applied to real human connection*

</div>
