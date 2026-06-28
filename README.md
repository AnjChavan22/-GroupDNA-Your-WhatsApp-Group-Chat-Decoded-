# 🧬 GroupDNA — Your WhatsApp Group Chat, Decoded

GroupDNA is a lightweight behavioral analytics engine that parses raw WhatsApp group chat exports to uncover deep structural communication patterns and automatically assign distinct personality archetypes to group members.

The twist? **This engine is built entirely from scratch using core Python and NumPy.** Heavy dependencies like Pandas, collections.Counter, Matplotlib, or external NLP packages are deliberately avoided to emphasize lightweight, raw data engineering principles.

---

## 🎯 Key Objective
The goal of GroupDNA is to take unstructured, multi-line, timestamped conversational lines, cleanly normalize them, and map personal behaviors across several parameters:
* Message and attachment volumes.
* Chronological activity frequencies (by hour and day).
* Temporal gaps (response speed and continuous radio silence).
* Cleaned conversational vocabulary tracking.

---

## 🚀 Key System Features

### 1. Robust Raw Chat Parser
* **Multi-Line Handling:** Intelligently tokenizes strings by matching date-signature formats, combining lines split over text paragraphs into a single record without breaking indices.
* **System/Media Filtration:** Accurately isolates administrative system messages, logs `<Media omitted>` footprints, and tracks message deletion spikes separately.

### 2. Native Inline Terminal Bar Charts
* Generates proportional visual charts using block character rendering matrices (`██████░░░░`) directly inside the text terminal, removing the need for a GUI or rendering library.

### 3. $6 \times 24$ Activity Heatmap Grid (NumPy Core)
* Projects participant behavior across a multi-dimensional NumPy array tracking hours `00:00` through `23:00`.
* Utilizes ratio-based density shading characters (`.`, `░`, `▒`, `█`, `██`).
* **Behavioral Archetype Detection:** Implements automated heuristic flags. For instance, if an individual conducts more than 60% of their communication between 11 PM and 4 AM, the engine tags them with a **"Night Owl" Archetype**.

### 4. Custom Vocabulary Engine
* Implements a raw dictionary-based string frequency text processor.
* Strips punctuation, isolates individual tokens, filters single-character fragments, ignores numbers, and runs a custom-mapped list of common conversational stop words to locate distinct user keywords.

### 5. Interaction Delta Analytics
* Evaluates chronological time gaps between consecutive texts from distinct senders to isolate individual **Average Response Speeds**.
* Tracks calendar-day arrays across the entire timeline window to map the **Longest Silent Streak** (consecutive days with 0 messages logged) for each member.

---

## 📊 Sample Output Visuals (Terminal)

### Executive Summary & Leaderboard
```text
============================================================
         GROUP OVERVIEW — HOSTEL BOIS 4EVER
============================================================
  Chat duration         : 60 days
  From                  : 01 April 2024
  To                    : 30 May 2024
  Total messages        : 3,127

  --- Leaderboard ---

  Rahul           :   940 ████████████████████   2.6 words/msg   7 media   6 deleted
  Priya           :   712 ███████████████.....   5.0 words/msg   4 media   2 deleted
  Neha            :   624 █████████████.......   5.3 words/msg   8 media   3 deleted
  Aman            :   484 ██████████..........   5.0 words/msg   4 media   2 deleted
  Karan           :   345 ███████.............  57.0 words/msg   7 media   2 deleted
  Vikas           :    22 ....................   1.8 words/msg   2 media   0 deleted
============================================================

NumPy Shaded Hourly Heatmap Matrix
```
ACTIVITY HEATMAP (messages by hour of day)
  -------------------------------------------------------
  Person      00   03   06   09   12   15   18   21
  -------------------------------------------------------
  Rahul       ░  ░  ░  ░  █  █  ██ ██ 
  Priya       .  .  ░  ██ ██ ▒  █  █  
  Aman        █  █  .  .  .  ░  ░  ░    <- NIGHT OWL (80.4% after 11 PM)
  Karan       .  .  .  ▒  ██ █  █  ▒  
  Neha        .  .  ░  ██ █  ░  ██ ▒  
  Vikas       .  .  .  ▒  ▒  ▒  █  ▒  

  Shade key:  . = none   ░ = low   ▒ = medium   █ = high   ██ = peak
```
```
**🛠️ Project Requirements & Stack:**
- Python 3.x
- NumPy
- Core Standard Modules used: datetime, string

**⚙️ How To Run**
1. Export a WhatsApp chat history without media as a .txt file.

2. Place the export file into your local working directory or load it into your Jupyter environment.

3. Ensure the text file path name perfectly matches your target loading variable in the file loader string block:

" with open('your_chat_file.txt', 'r', encoding='utf-8') as chat_file: "

4. Run all notebook code frames to print out the group behavior graphs and archetype profiles
```
