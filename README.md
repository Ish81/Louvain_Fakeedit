# 🧩 Louvain Community Detection on FakeEDDIT + Interaction-Based Dataset

This repository demonstrates **two community detection pipelines**:

1. **Semantic (text-based) communities** using the FakeEDDIT dataset  
2. **Interaction-based communities** using a misinformation dataset (Sindhoor)

Both use the **Louvain algorithm**, but the meaning of communities differs:

- Semantic = similarity of *content*  
- Interaction = similarity of *user behavior*  


---

# 🔷 Part A — Semantic Communities (FakeEDDIT Dataset)

## 🧠 Overview
This section identifies communities based on **what users write**.

Users are connected if their **post titles are semantically similar** using TF-IDF + cosine similarity.

---

## 📘 A1. Text-Based Similarity Pipeline

### ⚙️ Implementation Logic

| Step | Description |
|------|------------|
| 🧍‍♂️ Node | Each node represents a Reddit **user (author)** |
| 🧠 Text Representation | TF-IDF vectors computed from `clean_title` |
| 📈 Similarity | Cosine similarity between TF-IDF embeddings |
| 🔗 Edge Rule | Create edge if similarity > **0.30** |
| ⚖️ Edge Weight | Cosine similarity score |
| 🧩 Community Detection | Louvain modularity optimization |

---

## 📊 A2. Interpretation

- Users in the same cluster → post **textually similar** content  
- Clusters represent **topic groups**  
- Sparse cross-links reveal **topic bridging users**  

---

## 🖼️ A3. Visualization

- Nodes = authors  
- Edges = semantic similarity  
- Colors = Louvain communities  
- Layout = force-directed (spring layout)  

---

# 🔶 Part B — Interaction-Based Communities (Sindhoor Misinformation Dataset)

## 🧠 Overview
This section finds communities based on **how users interact**, not what they post.

The graph reflects patterns of:
- commenting  
- co-commenting  
- mentions  
- keyword activity  
- hoax amplification  

---

## 📘 B1. Interaction Logic for Building the Graph

| Interaction Source | Meaning | Weight |
|--------------------|---------|--------|
| 💬 Co-commenting | Commenting on the same post | 1 |
| 🎯 Comment → Author | Direct reply | 1 |
| 🏷 Mentions | Explicit user reference | 2 |
| 🔥 Keyword “Sindhoor” match | Interaction on hoax content | 1 |
| ➕ Accumulation | Multiple interactions strengthen edge | ✔ |

All interactions are accumulated into **weighted edges** between users.

---

## 🧩 B2. Why Communities Form

### 🟥 Hoax Cluster  
Users with high interaction density:
- U1 (Alpha)  
- U2 (Bravo)  
- U3 (Charlie)  
- U7 (Gamma)  
- U6 (absorbed due to repeated interactions)

These users:
- frequently reply to each other  
- mention each other  
- post/comment on hoax content  
- co-comment across many posts  

→ Their nodes appear **close together** in the graph.

---

### 🟦 Neutral / Skeptic Cluster
Low-interaction users:
- U4 (Delta)  
- U5 (Echo)  
- U8 (Hotel)

They:
- do not engage with hoaxers  
- rarely mention others  
- interact mostly inside their own group  

→ Their nodes drift **far from the hoax cluster**.

---

## 📊 B3. Modularity Score

- **Modularity ≈ 0.19**
- Indicates:
  - dataset is small  
  - interactions are semi-dense  
  - communities are *meaningful but not perfectly separated*
- 0.0 → random structure
- 0.3–0.6 → clear communities
- 0.8+ → extremely strong separation

Two distinct clusters still emerge clearly.

---

## 🎨 B4. Graph Visualization Interpretation

- **Spring layout** pushes weakly connected users outward  
- **Strongly connected users** cluster tightly  
- **Node color** = community  
- **Edge width** = strength of interaction  
- **Top-degree nodes** = influential hoax spreaders  

Visual patterns reflect real-world misinformation clusters.

---

# 🧠 Combined Understanding: Semantic vs Interaction Graphs

| Feature | FakeEDDIT Semantic Graph | Sindhoor Interaction Graph |
|--------|---------------------------|-----------------------------|
| Edge Meaning | Cosine similarity | Behavioral interaction |
| Weight | TF-IDF similarity | Interaction strength |
| Why Nodes Group | Similar content | Frequent interactions |
| Community Meaning | Topic groups | Social / influence clusters |
| Why Nodes Spread | Different topics | Few or no interactions |

Semantic = *what* users write.  
Interaction = *how* users behave.  

---

# 🧰 Technologies Used

- Python 3.x  
- pandas  
- scikit-learn (TF-IDF, cosine similarity)  
- networkx  
- python-louvain  
- matplotlib  
- NumPy  

---

# 🎯 Summary

This repository demonstrates **two fundamental types of social network communities**:

### 🔹 Semantic communities  
Users grouped by **text similarity** in FakeEDDIT.

### 🔸 Interaction communities  
Users grouped by **actual interaction behavior** in the Sindhoor dataset.

Together, these approaches give a complete view of both:
- **topic similarity**, and  
- **social interaction structure**  

in online networks.

