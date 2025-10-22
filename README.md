# 🧠 Leitner Box CLI App

A **command-line flashcard review system** based on the **Leitner method** — built with **Python** and **PostgreSQL**.  
This app allows users to register, log in, add flashcards, and review them over time using spaced repetition.

---

## 📁 Project Structure

Leitner Box/

│                                                         
├── main.py              → Entry point of the program  
├── auth.py              → User registration and login  
├── database.py          → PostgreSQL operations  
├── dashboard.py         → Main dashboard (CLI)  
├── review.py            → Leitner spaced repetition logic  
├── schemas.sql          → Database schema  
├── .gitignore           → Git ignore rules  
└── README.md            → Project documentation

---

## 🚀 Features

✅ **User Authentication**  
- Register and login with hashed passwords (`bcrypt`)  
- Prevent duplicate usernames  

✅ **Flashcard Management**  
- Add, edit, and delete cards  
- Automatically assigned to one of **6 Leitner slots**  

✅ **Card Addition Process**
- Below is a visual flow of how a new flashcard is added to the system:

<p align="left">
  <img src="1.PNG" alt="Leitner Box Flowchart" width="200"/>
</p>

✅ **Leitner Review System (Spaced Repetition)**  
- Reviews only **due cards** (`last_review <= today`)  
- Each slot defines a specific review interval:  

| Slot | Interval (days) | Meaning            |
|------|-----------------|--------------------|
| 1    | 1               | New card           |
| 2    | 3               | Learning           |
| 3    | 7               | Short-term memory  |
| 4    | 14              | Medium-term memory |
| 5    | 30              | Long-term memory   |
| 6    | 60              | Mastered ✅        |

📌 **Rules:**  
- Correct answer → move card up one slot (max slot 6)  
- Wrong answer → move card back to slot 1  
- Missed review by **more than 2 days** → move card **down one slot**

✅ **CLI Interface**  
- Clean terminal UI  
- Screen automatically clears after each user input (`os.system("cls" or "clear")`)  
- Works on **Windows, macOS, and Linux**

---

## 🧩 Requirements

- **Python 3.10+**
- **PostgreSQL 15+**
- Install dependencies:
  ```bash
  pip install psycopg2-binary bcrypt

---

## ⚙️ Database Setup

1. Open PostgreSQL (terminal or pgAdmin)

2. Create the database:
   ```bash
   CREATE DATABASE leitner_db;

3. Run the schema file:
   ```bash
   \i schemas.sql

---

## ▶️ How to Run

1. Open your project folder

2. Run the app in terminal:
   ```bash
   python main.py

3. Main menu:
   ```bash
   === LEITNER BOX ===
   1) Register
   2) Login
   3) Exit

4. After login:
   ```bash
   === DASHBOARD ===
   1) Show Box
   2) Add Card
   3) Modify Card
   4) Review Cards
   5) Logout

---

## 🗄️ Database Schema

- Table: users:

| Column   | Type         | Description     |
|----------|--------------|-----------------|
| id	   | SERIAL	User  | ID              |
| username | VARCHAR(100) | Unique username |
| password | TEXT         | Hashed password |


- Table: cards:

| Column      | Type    | Description            |
|-------------|---------|------------------------|
| id          | SERIAL  | Card ID                |
| user_id     | INTEGER | Linked user            |
| slot        | INTEGER | Leitner box slot (1–6) |
| question    | TEXT    | Card question          |
| answer      | TEXT    | Card answer            |
| last_review | DATE    | Last review date       |

---

## 🧩 Technical Notes

- Database operations use a @db_connection decorator for safety and cleaner code.
- Passwords are securely hashed using bcrypt.
- Modular design improves maintainability and testing:
 . auth.py: registration & login
 . database.py: database logic
 • dashboard.py: main user menu
 • review.py: Leitner logic

---

## 💡 Future Improvements

- Add review progress tracking
- Export/import flashcards (CSV/JSON)
- Add category/tag system for cards
- Build a web version (Django) or GUI app

---

## 👨‍💻 Authors

Mohammad Moghanloo
📧 Email: mohamad.mgn.89@gmail.com
🐙 GitHub: mohamad-mgn

Parisa Khosravi
📧 Email: pkhosravi21@gmail.com
🐙 GitHub: parisa-khosravi