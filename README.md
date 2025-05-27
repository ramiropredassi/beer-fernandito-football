# Beer, Fernandito and Football

### A Linguistic and Social Network Analysis on the Role of Football as Geographical, Cultural and Social Glue Using Twitch Data

**Technical Report**  
**Antonio Federico Barbano, Luciana Fazio, Daniela Lorieri, Ramiro Predassi, Miriana Somenzi**  
**July 2024**

---

## 🔗 Project Website

In addition to this report, the same authors developed a **static website** for the project submission, built with **Jekyll** and **Bootstrap**.

📍 Visit it here:  
👉 [https://ramiropredassi.github.io/g7-2024-website/](https://ramiropredassi.github.io/g7-2024-website/)

---

## 1. Goal

The project aims to assess whether football acts as a unifying or dividing factor. Mainly, we explore how communities form on Twitch, how they interact, and how they influence one another.

We focused on **Italy and Argentina** as case studies and worked across four main areas:

- Data collection  
- Data exploration and processing  
- Sentiment and emotion analysis  
- Social network analysis  

---

## 2. Data Collection

We gathered data from the top 10 Italian football Twitch channels, as ranked by Twitchmetrics.

- **Timeframe**: March to June 2024  
- **Data volume**:  
  - ~1.5 million messages (Italy)  
  - ~2.5 million messages (Argentina)

**Tools used:**

- `twitch-dl`: to download video URLs  
- `ChatDownloader`: to download and parse chat messages  

**Chat metadata collected:**

- Message ID, username, display name, timestamp, message, message type, color, badge info, etc.

---

## 3. Data Exploration and Processing

### Cleaning and Preprocessing:

1. Removed bots (automated messages)
2. Complied with GDPR (minimal necessary data)
3. Calculated basic metrics: unique users, average messages per user

### Interaction Analysis:

- Used regex to detect tagged users
- Calculated interaction counts per channel

### Cross-Country User Comparison:

- Merged datasets
- Built a correlation matrix (normalized with MinMaxScaler)
- Visualized with a heatmap and dendrogram using **Altair**

### Interaction Graphs:

- Built with **Pyvis**
- Edge weights based on user correlation
- Computed **closeness centrality** using NetworkX

### Word Frequency Analysis:

- Cleaned text with **NLTK**
- Removed Twitch-specific and common irrelevant words
- Plotted top 15 frequent words using **Altair**

---

## 4. Sentiment and Emotion Analysis

We used **Pysentimiento**, a multilingual NLP toolkit trained on Twitter data in Spanish and Italian.

### Why Pysentimiento?

- Supports both study languages
- Processes emojis and Twitch "emotes"
- Pre-trained on social network language

### Processing Steps:

1. Normalized text (emojis, repeated characters, laughter)
2. Extracted emotes into a separate column
3. Tokenized text and removed stopwords and null rows
4. Processed in batches of 15 messages

### User Labeling:

- Identified tagged interactions using regex
- Measured sentiment and emotion per message
- Aggregated sentiment/emotion scores per user

### Visualizations:

- Sentiment and emotion per channel shown in **Altair bar charts**
- Emote usage analyzed and associated with emotion

---

## 5. Social Network Analysis

We modeled user interactions as a network to analyze:

- **Social balance (triads)**  
- **Assortativity**

### Network Construction:

- Converted sentiment to numeric weights:
  - `+1` for positive, `-1` for negative  
  - Neutral values handled using confidence:  
    - If more positive → `+0.25`  
    - If more negative → `-0.25`

### Social Balance Analysis:

1. Created an undirected signed graph  
2. Computed:
   - Degree, betweenness, closeness centrality  
   - All possible triads using NetworkX  
3. Measured balance within triads  
4. Computed triad census (16 types of triads)

### Assortativity Analysis:

1. Converted to a directed graph  
2. Assigned sentiment signs to nodes  
3. Measured assortativity  
4. Visualized results using **Altair**

---

## References

1. Pérez, J. M., et al. (2021). *Pysentimiento: A python toolkit for opinion mining and social NLP tasks*. arXiv:2106.09462  
2. Terzi, E., & Winkler, M. (2011). *A Spectral Algorithm for Computing Social Balance*. In: WAW 2011, Lecture Notes in Computer Science, vol 6732, Springer.

---

## Table of Contents

- [🔗 Project Website](#-project-website)  
- [1. Goal](#1-goal)  
- [2. Data Collection](#2-data-collection)  
- [3. Data Exploration and Processing](#3-data-exploration-and-processing)  
- [4. Sentiment and Emotion Analysis](#4-sentiment-and-emotion-analysis)  
- [5. Social Network Analysis](#5-social-network-analysis)  

---

> “Beer, Fernandito and Football” — An academic exploration into the social language of football fans on Twitch.
