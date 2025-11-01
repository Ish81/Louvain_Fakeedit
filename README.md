# 🧩 Louvain Community Detection on FakeEDDIT Dataset

## ✅ Overview
This project applies **Louvain community detection** on the **FakeEDDIT dataset** to identify groups of Reddit users posting **semantically similar content**.

---

## Text-based (Semantic) Similarity

Text-based (semantic) similarity, meaning the graph connects **users (authors)** whose post titles are textually similar.

### ⚙️ Implementation Logic

| Step | Description |
|------|--------------|
| 🧍‍♂️ **Node** | Each node represents a **user (author)** from the dataset. |
| 🧠 **Text Representation** | Computed **TF-IDF vectors** of users’ post titles (`clean_title`). |
| 📈 **Similarity Calculation** | Measured **cosine similarity** between these TF-IDF vectors. |
| 🔗 **Edge Creation** | Added an edge between two users if **similarity > 0.3** (configurable threshold). |
| ⚖️ **Edge Weight** | The **edge weight** equals the cosine similarity score between the two users. |
| 🧩 **Community Detection** | Applied the **Louvain algorithm** to detect groups of users posting semantically similar content. |

Thus, your graph and Louvain detection are based entirely on **content similarity**.

---

## 🧠 Technical Details

- **Dataset Used:** FakeEDDIT Reddit dataset  
- **Fields Utilized:** `author`, `clean_title`
- **Graph Type:** Undirected, weighted graph  
- **Weight Source:** TF-IDF cosine similarity  
- **Edge Threshold:** 0.3 (can be tuned for density control)  
- **Community Detection Algorithm:** Louvain (modularity optimization)  

---

## 📊 Visualization
- Communities are visualized as **color-coded clusters** in a **2D force-directed layout**.  
- Each node = a Reddit user.  
- Each edge = similarity link between semantically close users.  
- Colors = distinct Louvain communities.  

---

## 💡 Interpretation
- Users within the same color cluster post **textually similar content**, showing thematic alignment.  
- Highly connected clusters suggest **shared interests or topics**.  
- Sparse inter-community edges indicate **bridging users** linking different topics.  

---

## 🧰 Technologies Used
- **Python 3.x**
- **pandas** – data preprocessing  
- **scikit-learn** – TF-IDF vectorization & cosine similarity  
- **networkx** – graph construction & visualization  
- **community (python-louvain)** – Louvain modularity optimization  
- **matplotlib** – 2D graph visualization  

---
