<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Graph Theory — Topics, Theorems & Answers</title>
<link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,600;1,400;1,600&family=JetBrains+Mono:wght@400;500&family=Nunito+Sans:wght@300;400;600&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --bg: #0f1117;
  --surface: #181c27;
  --surface2: #1e2235;
  --border: #2a3050;
  --accent: #e8a838;
  --accent2: #5b8dee;
  --accent3: #52c98a;
  --accent4: #e85b6f;
  --accent5: #b07de8;
  --text: #dde3f0;
  --text-dim: #7a869e;
  --text-bright: #ffffff;
  --tag-pt: rgba(232,91,111,0.15);
  --tag-pt-b: #e85b6f;
  --tag-algo: rgba(232,168,56,0.15);
  --tag-algo-b: #e8a838;
  --tag-list: rgba(91,141,238,0.15);
  --tag-list-b: #5b8dee;
  --tag-ham: rgba(82,201,138,0.15);
  --tag-ham-b: #52c98a;
  --tag-digraph: rgba(176,125,232,0.15);
  --tag-digraph-b: #b07de8;
  --tag-state: rgba(232,91,111,0.15);
  --tag-state-b: #e85b6f;
}

body {
  background: var(--bg);
  font-family: 'Nunito Sans', sans-serif;
  color: var(--text);
  min-height: 100vh;
  padding: 2.5rem 1rem 4rem;
  background-image: radial-gradient(ellipse at 20% 10%, rgba(91,141,238,0.07) 0%, transparent 50%),
                    radial-gradient(ellipse at 80% 90%, rgba(232,168,56,0.06) 0%, transparent 50%);
}

.container {
  max-width: 820px;
  margin: 0 auto;
}

header {
  text-align: center;
  margin-bottom: 3rem;
  animation: fadeUp 0.6s both;
}

.header-eyebrow {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.65rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.8rem;
}

h1 {
  font-family: 'Lora', serif;
  font-size: 2.2rem;
  font-weight: 600;
  color: var(--text-bright);
  line-height: 1.2;
  margin-bottom: 0.5rem;
}

h1 em {
  font-style: italic;
  color: var(--accent2);
}

.header-sub {
  font-size: 0.82rem;
  color: var(--text-dim);
  font-weight: 300;
}

.hint {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.62rem;
  color: var(--text-dim);
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 5px 14px;
  margin-top: 1rem;
}

.hint::before { content: '▸'; color: var(--accent); }

/* Topic cards */
.topic-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  margin-bottom: 1rem;
  overflow: hidden;
  animation: fadeUp 0.5s both;
  transition: border-color 0.25s, box-shadow 0.25s;
}

.topic-card:nth-child(1) { animation-delay: 0.05s; }
.topic-card:nth-child(2) { animation-delay: 0.10s; }
.topic-card:nth-child(3) { animation-delay: 0.15s; }
.topic-card:nth-child(4) { animation-delay: 0.20s; }
.topic-card:nth-child(5) { animation-delay: 0.25s; }
.topic-card:nth-child(6) { animation-delay: 0.30s; }
.topic-card:nth-child(7) { animation-delay: 0.35s; }

.topic-card.open {
  border-color: var(--accent2);
  box-shadow: 0 0 0 1px var(--accent2), 0 8px 40px rgba(91,141,238,0.12);
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}

.topic-header {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.2rem 1.4rem;
  cursor: pointer;
  user-select: none;
  position: relative;
}

.topic-header:hover { background: rgba(255,255,255,0.02); }

.topic-number {
  font-family: 'Lora', serif;
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--accent);
  min-width: 2rem;
  line-height: 1;
  padding-top: 4px;
}

.topic-meta { flex: 1; }

.topic-tag {
  display: inline-block;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.58rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding: 3px 8px;
  border-radius: 4px;
  margin-bottom: 0.4rem;
  font-weight: 500;
  border: 1px solid transparent;
}

.tag-pt    { background: var(--tag-pt);      color: var(--tag-pt-b);      border-color: var(--tag-pt-b); }
.tag-list  { background: var(--tag-list);    color: var(--tag-list-b);    border-color: var(--tag-list-b); }
.tag-algo  { background: var(--tag-algo);    color: var(--tag-algo-b);    border-color: var(--tag-algo-b); }
.tag-ham   { background: var(--tag-ham);     color: var(--tag-ham-b);     border-color: var(--tag-ham-b); }
.tag-digraph { background: var(--tag-digraph); color: var(--tag-digraph-b); border-color: var(--tag-digraph-b); }
.tag-state { background: var(--tag-state);   color: var(--tag-state-b);   border-color: var(--tag-state-b); }

.badge {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.56rem;
  background: var(--accent);
  color: #000;
  padding: 2px 6px;
  border-radius: 3px;
  margin-left: 6px;
  vertical-align: middle;
  font-weight: 500;
}

.topic-title {
  font-family: 'Lora', serif;
  font-size: 1.0rem;
  font-weight: 600;
  color: var(--text-bright);
  line-height: 1.3;
}

.toggle-icon {
  font-size: 0.75rem;
  color: var(--text-dim);
  transition: transform 0.3s;
  padding-top: 6px;
  min-width: 20px;
  text-align: right;
}

.topic-card.open .toggle-icon { transform: rotate(180deg); color: var(--accent2); }

/* Answer panel */
.answer-panel {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.45s cubic-bezier(0.4, 0, 0.2, 1);
}

.topic-card.open .answer-panel { max-height: 2000px; }

.answer-inner {
  border-top: 1px solid var(--border);
  padding: 1.4rem 1.4rem 1.6rem 1.4rem;
  background: var(--surface2);
}

.answer-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent3);
  margin-bottom: 0.8rem;
  display: flex;
  align-items: center;
  gap: 8px;
}

.answer-label::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--border);
}

.answer-body {
  font-size: 0.85rem;
  line-height: 1.75;
  color: var(--text);
  font-weight: 300;
}

.answer-body p { margin-bottom: 0.8rem; }
.answer-body p:last-child { margin-bottom: 0; }

.answer-body strong {
  color: var(--text-bright);
  font-weight: 600;
}

.answer-body em {
  color: var(--accent2);
  font-style: italic;
}

.math-block {
  background: var(--bg);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent2);
  border-radius: 6px;
  padding: 0.8rem 1rem;
  margin: 0.8rem 0;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.78rem;
  color: var(--accent);
  line-height: 1.6;
}

.proof-step {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.5rem 0.8rem;
  margin: 0.6rem 0;
  align-items: start;
}

.step-num {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.7rem;
  color: var(--accent3);
  background: rgba(82,201,138,0.1);
  border: 1px solid rgba(82,201,138,0.3);
  border-radius: 3px;
  padding: 2px 7px;
  white-space: nowrap;
  margin-top: 2px;
}

.step-text {
  font-size: 0.83rem;
  line-height: 1.65;
  color: var(--text);
}

.definition-grid {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  margin: 0.6rem 0;
}

.def-row {
  display: grid;
  grid-template-columns: 180px 1fr;
  gap: 0.8rem;
  align-items: start;
  padding: 0.6rem 0.8rem;
  background: var(--bg);
  border-radius: 6px;
  border: 1px solid var(--border);
}

.def-term {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.73rem;
  color: var(--accent5);
  font-weight: 500;
  padding-top: 1px;
}

.def-desc {
  font-size: 0.81rem;
  line-height: 1.55;
  color: var(--text);
}

.theorem-box {
  background: rgba(91,141,238,0.07);
  border: 1px solid rgba(91,141,238,0.3);
  border-radius: 8px;
  padding: 0.9rem 1rem;
  margin: 0.7rem 0;
}

.theorem-box .th-name {
  font-family: 'Lora', serif;
  font-size: 0.85rem;
  font-style: italic;
  color: var(--accent2);
  font-weight: 600;
  margin-bottom: 0.4rem;
}

.theorem-box .th-body {
  font-size: 0.81rem;
  line-height: 1.6;
  color: var(--text);
}

.section-divider {
  height: 1px;
  background: var(--border);
  margin: 0.9rem 0;
}

footer {
  text-align: center;
  margin-top: 3rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  color: var(--text-dim);
  text-transform: uppercase;
  animation: fadeUp 0.5s 0.5s both;
}
</style>
</head>
<body>
<div class="container">

  <header>
    <div class="header-eyebrow">Graph Theory · Exam Preparation</div>
    <h1>Topics, Theorems<br><em>& Full Answers</em></h1>
    <div class="header-sub">Click any topic to reveal the complete answer</div>
    <div class="hint">Click a card to expand</div>
  </header>

  <!-- 1 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">1</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-pt">Prove That · PT</span></div>
        <div class="topic-title">The distance between two vertices is a metric.</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p>Let <strong>G</strong> be a connected graph and <strong>d(u, v)</strong> denote the length of the shortest path between vertices <em>u</em> and <em>v</em>. We must verify all four metric axioms:</p>

          <div class="proof-step">
            <span class="step-num">M1</span>
            <span class="step-text"><strong>Non-negativity:</strong> d(u, v) ≥ 0 for all u, v, since path length counts edges (a non-negative quantity). d(u, v) = 0 if and only if u = v (the trivial path of length zero).</span>
          </div>
          <div class="proof-step">
            <span class="step-num">M2</span>
            <span class="step-text"><strong>Identity of indiscernibles:</strong> d(u, v) = 0 ⟺ u = v. If u ≠ v, any path between them uses at least one edge, so d(u, v) ≥ 1 > 0.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">M3</span>
            <span class="step-text"><strong>Symmetry:</strong> d(u, v) = d(v, u). Any shortest path from u to v can be traversed in reverse to give a path from v to u of equal length. Hence the minimum lengths must be equal.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">M4</span>
            <span class="step-text"><strong>Triangle inequality:</strong> d(u, w) ≤ d(u, v) + d(v, w). Concatenating a shortest u–v path with a shortest v–w path yields a (not necessarily shortest) u–w walk of length d(u,v)+d(v,w). The shortest path d(u,w) cannot exceed this length. ∎</span>
          </div>
          <p style="margin-top:0.8rem;">Since all four axioms hold, <strong>d is a metric</strong> on the vertex set of G.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- 2 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">2</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-list">List & Define</span></div>
        <div class="topic-title">Binary Tree Properties</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p>A <strong>binary tree</strong> is a rooted tree in which every vertex has <em>at most two children</em> (a left child and a right child).</p>
          <div class="definition-grid">
            <div class="def-row">
              <div class="def-term">Degree constraint</div>
              <div class="def-desc">Each internal node has at most 2 children; the root has no parent; leaves have 0 children.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Full binary tree</div>
              <div class="def-desc">Every node has exactly 0 or 2 children. If it has <em>i</em> internal nodes, it has exactly <em>i + 1</em> leaves.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Complete binary tree</div>
              <div class="def-desc">All levels are fully filled except possibly the last, which is filled left to right.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Perfect binary tree</div>
              <div class="def-desc">All internal nodes have 2 children and all leaves are at the same depth <em>h</em>. Total nodes = 2^(h+1) − 1.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Height <em>h</em></div>
              <div class="def-desc">Longest path from root to a leaf. A perfect tree of height <em>h</em> has 2^h leaves.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Leaf count</div>
              <div class="def-desc">In a full binary tree: leaves = internal nodes + 1. In a perfect tree of height h: leaves = 2^h.</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 3 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">3</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-algo">Algorithm</span> <span class="badge">1Q</span></div>
        <div class="topic-title">Kruskal's Algorithm</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p><strong>Kruskal's Algorithm</strong> finds a <em>Minimum Spanning Tree (MST)</em> of a weighted connected graph using a greedy strategy.</p>

          <div class="section-divider"></div>

          <div class="proof-step">
            <span class="step-num">Step 1</span>
            <span class="step-text"><strong>Sort</strong> all edges of G in non-decreasing order of weight.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">Step 2</span>
            <span class="step-text">Initialize a forest T with all vertices and no edges.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">Step 3</span>
            <span class="step-text">For each edge (u, v) in sorted order: <strong>add it to T if it does not form a cycle</strong> (i.e., u and v are in different components). Otherwise discard it.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">Step 4</span>
            <span class="step-text">Stop when T has <em>n − 1</em> edges (where n = number of vertices). T is the MST.</span>
          </div>

          <div class="math-block">
            Complexity: O(E log E)  — dominated by the sorting step.<br>
            Uses Union-Find (Disjoint Set Union) for cycle detection: O(α(n)) per operation.
          </div>

          <p><strong>Correctness:</strong> By the cut property — at each step, adding the minimum weight edge that crosses some cut and doesn't create a cycle is always safe for the MST.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- 4 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">4</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-pt">Prove That · PT</span></div>
        <div class="topic-title">A tree has one or two centers.</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p>The <strong>center</strong> of a graph is the set of vertices that minimize the eccentricity (maximum distance to any other vertex).</p>

          <div class="section-divider"></div>

          <p><strong>Proof (by iterative leaf removal):</strong></p>

          <div class="proof-step">
            <span class="step-num">Step 1</span>
            <span class="step-text">If T has 1 or 2 vertices, the result is trivially true.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">Step 2</span>
            <span class="step-text">A leaf (degree-1 vertex) always has the <em>highest</em> eccentricity in a tree. Remove all leaves simultaneously to get a smaller tree T'.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">Step 3</span>
            <span class="step-text">The center of T equals the center of T'. Repeat the removal process.</span>
          </div>
          <div class="proof-step">
            <span class="step-num">Step 4</span>
            <span class="step-text">This process terminates when exactly <strong>1 or 2 vertices remain</strong>, which are the center(s). It cannot terminate with 3+ vertices because removing leaves from any path of length ≥ 2 reduces it further. ∎</span>
          </div>

          <div class="math-block">
            If 1 vertex remains → the tree has a unique center.<br>
            If 2 vertices remain → both are centers (they form the central edge).
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 5 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">5</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-ham">Hamiltonian Circuit</span> <span class="badge">2Q</span></div>
        <div class="topic-title">Hamiltonian Circuits, Theorems & the Traveling Salesman Problem</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p>A <strong>Hamiltonian circuit</strong> is a closed path in a graph that visits every vertex exactly once and returns to the starting vertex.</p>

          <div class="section-divider"></div>

          <div class="theorem-box">
            <div class="th-name">Dirac's Theorem (1952)</div>
            <div class="th-body">If G is a simple graph with <em>n ≥ 3</em> vertices and every vertex has degree <strong>deg(v) ≥ n/2</strong>, then G has a Hamiltonian circuit.<br><br>
            <em>Intuition:</em> High degree forces enough connectivity that a full circuit must exist.</div>
          </div>

          <div class="theorem-box">
            <div class="th-name">Ore's Theorem (1960)</div>
            <div class="th-body">If G is a simple graph with <em>n ≥ 3</em> vertices, and for every pair of <strong>non-adjacent</strong> vertices u, v: <strong>deg(u) + deg(v) ≥ n</strong>, then G has a Hamiltonian circuit.<br><br>
            <em>Note:</em> Ore's Theorem is a generalization — it implies Dirac's Theorem (Dirac's condition ⟹ Ore's condition).</div>
          </div>

          <div class="section-divider"></div>

          <p><strong>Application — Traveling Salesman Problem (TSP):</strong></p>
          <p>Given a complete weighted graph (cities and road costs), find the <em>minimum-weight Hamiltonian circuit</em>. TSP is <strong>NP-hard</strong> — no known polynomial-time exact algorithm exists. Common approaches:</p>
          <div class="definition-grid">
            <div class="def-row">
              <div class="def-term">Brute force</div>
              <div class="def-desc">Check all (n−1)!/2 Hamiltonian circuits. Exact but O(n!) time — infeasible for large n.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Nearest neighbour heuristic</div>
              <div class="def-desc">Greedy — always go to the closest unvisited city. Fast but not optimal.</div>
            </div>
            <div class="def-row">
              <div class="def-term">Dynamic programming</div>
              <div class="def-desc">Held-Karp algorithm: O(n² · 2ⁿ) — exact, faster than brute force.</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 6 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">6</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-digraph">Directed Graphs</span></div>
        <div class="topic-title">Digraphs — Complete, Symmetric & Asymmetric</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p>A <strong>digraph (directed graph)</strong> is a graph where every edge has a direction — denoted as an ordered pair (u → v), called an <em>arc</em>.</p>
          <div class="section-divider"></div>
          <div class="definition-grid">
            <div class="def-row">
              <div class="def-term">(i) Complete Digraph</div>
              <div class="def-desc">For every ordered pair of distinct vertices (u, v), there exists an arc <strong>u → v</strong>. A complete digraph on n vertices has <strong>n(n−1)</strong> arcs. Both u→v and v→u exist between any two vertices.</div>
            </div>
            <div class="def-row">
              <div class="def-term">(ii) Symmetric Digraph</div>
              <div class="def-desc">For every arc <strong>u → v</strong>, the reverse arc <strong>v → u</strong> also exists. The underlying undirected graph has an edge for each such pair. Essentially a digraph equivalent of an undirected graph.</div>
            </div>
            <div class="def-row">
              <div class="def-term">(iii) Asymmetric Digraph</div>
              <div class="def-desc">For every pair of vertices u, v, <strong>at most one</strong> of u→v or v→u exists — never both. No two vertices are mutually connected. Also called a <em>tournament</em> if for every pair exactly one direction exists.</div>
            </div>
          </div>
          <div class="math-block">
            Complete ⊇ Symmetric: every symmetric digraph is complete only if all pairs have arcs in both directions.<br>
            Asymmetric ∩ Symmetric = ∅ (they are mutually exclusive by definition).
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 7 -->
  <div class="topic-card" onclick="toggle(this)">
    <div class="topic-header">
      <div class="topic-number">7</div>
      <div class="topic-meta">
        <div><span class="topic-tag tag-state">State & Describe</span></div>
        <div class="topic-title">Theorem 6 and Theorem 3</div>
      </div>
      <div class="toggle-icon">▾</div>
    </div>
    <div class="answer-panel">
      <div class="answer-inner">
        <div class="answer-label">Answer</div>
        <div class="answer-body">
          <p><em>Note: "Theorem 6" and "Theorem 3" refer to specific theorems from your course textbook or lecture notes. The most commonly associated theorems in this context are:</em></p>

          <div class="theorem-box">
            <div class="th-name">Theorem 3 — (Characterization of Trees)</div>
            <div class="th-body">A graph G with n vertices is a <strong>tree</strong> if and only if it satisfies any two of the following three conditions:<br><br>
            (a) G is connected.<br>
            (b) G has no cycles (acyclic).<br>
            (c) G has exactly <strong>n − 1</strong> edges.<br><br>
            <em>Any two of these three conditions imply the third.</em></div>
          </div>

          <div class="theorem-box">
            <div class="th-name">Theorem 6 — (Euler's Formula / Handshaking Lemma for Digraphs)</div>
            <div class="th-body">In any digraph, the <strong>sum of all in-degrees equals the sum of all out-degrees</strong>, and both equal the total number of arcs <em>m</em>:<br><br>
            <strong>Σ indeg(v) = Σ outdeg(v) = m</strong><br><br>
            <em>Alternatively (if your course uses it for planar graphs):</em> For a connected planar graph: <strong>V − E + F = 2</strong> (Euler's formula), where V = vertices, E = edges, F = faces.</div>
          </div>

          <p style="margin-top:0.8rem; color: var(--text-dim); font-size:0.78rem; font-style:italic;">⚠ Please verify with your course notes — theorem numbering varies by textbook. The above covers the most likely candidates for this topic list.</p>
        </div>
      </div>
    </div>
  </div>

  <footer>Graph Theory · Topics & Answers · Study Guide</footer>
</div>

<script>
function toggle(card) {
  card.classList.toggle('open');
}
</script>
</body>
</html>
