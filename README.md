Recursive Spectral Modularity Optimization

📖 Research Abstract

This repository contains a complete implementation of Spectral Modularity Maximization for community detection, applied to the canonical Zachary's Karate Club dataset. Developed for the DSC212: Graph Theory module, this project demonstrates how analyzing the spectrum (eigenvalues and eigenvectors) of a graph's modularity matrix allows for the unsupervised detection of network substructures.

The core algorithm employs recursive spectral bisection, systematically partitioning the graph to maximize modularity ($Q$) until no statistically significant communities remain.

🧠 Mathematical Methodology

The community detection process is grounded in linear algebra, specifically the properties of the Modularity Matrix ($B$).

1. The Modularity Matrix

We define the modularity matrix $B$ as the difference between the actual adjacency matrix $A$ and the expected edge distribution under a null model (configuration model):

$$B_{ij} = A_{ij} - \frac{k_i k_j}{2m}$$

Where $k$ represents node degrees and $m$ is the total number of edges.

2. Spectral Bisection

To divide the network, we solve the eigenvalue problem for $B$. The leading eigenvector (corresponding to the largest positive eigenvalue $\lambda_1$) provides a continuous relaxation of the discrete cluster indicators. The sign of the eigenvector components determines community membership.

3. Stopping Criterion

The recursion terminates when a subgraph is indivisible, defined mathematically when the leading eigenvalue of its modularity matrix is non-positive:


$$\lambda_1 \le 0$$

⚙️ Implementation Details

Algorithm Logic

Preprocessing: Construction of the modularity matrix using NumPy.

Decomposition: Utilization of scipy.linalg.eigh to extract the leading eigenpair.

Recursion: A Depth-First Search (DFS) approach is used to recursively split communities. If a split yields a positive modularity gain ($\Delta Q$), the subgraph is further bisected.

Network Analytics

The project computes and tracks the evolution of four key centrality metrics across the graph's partitioning history:

Degree Centrality: Connection volume.

Betweenness Centrality: Control over information flow.

Closeness Centrality: Average distance to other nodes.

Clustering Coefficient: Local neighborhood density.

📉 Visualization & Results

The output includes a detailed visual analysis of the community structure evolution:

Iterative Splits: A grid visualization displaying the graph state at each step of the recursion.

Stable Layouts: Uses a fixed spring layout to allow visual tracking of specific nodes across iterations.

Metric Evolution: Time-series plotting of centrality measures to identify "bridge" nodes and stable community cores.

💻 Technical Dependencies

Python 3.x

NetworkX: High-level graph abstraction and metric calculation.

NumPy: Vectorized matrix operations.

SciPy: Linear algebra solvers for eigen-decomposition.

Matplotlib: Plotting and sub-graph visualization.

🔍 Key Findings

The algorithm successfully recovers the ground-truth social divisions of the Karate Club. The analysis highlights how "bridge" nodes often possess high betweenness centrality initially but lose influence as the graph fragments into tightly knit modules.
