# WebApp
# Event Planner interface
import tkinter as tk
from tkinter import messagebox
import sqlite3

# Database setup
conn = sqlite3.connect('events.db')
c = conn.cursor()
c.execute('''CREATE TABLE IF NOT EXISTS events
             (name TEXT, date TEXT, time TEXT, location TEXT, description TEXT)''')
conn.commit()

# Function to save event details to the database
def save_event():
    name = name_entry.get()
    date = date_entry.get()
    time = time_entry.get()
    location = location_entry.get()
    description = description_entry.get("1.0", tk.END)

    if name and date and time and location:
        c.execute("INSERT INTO events VALUES (?, ?, ?, ?, ?)", (name, date, time, location, description))
        conn.commit()
        messagebox.showinfo("Success", "Event saved successfully!")
    else:
        messagebox.showwarning("Error", "Please fill out all fields.")

# GUI setup
root = tk.Tk()
root.title("Event Planning Interface")

tk.Label(root, text="Event Name:").grid(row=0, column=0, padx=10, pady=10)
name_entry = tk.Entry(root)
name_entry.grid(row=0, column=1, padx=10, pady=10)

tk.Label(root, text="Date (YYYY-MM-DD):").grid(row=1, column=0, padx=10, pady=10)
date_entry = tk.Entry(root)
date_entry.grid(row=1, column=1, padx=10, pady=10)

tk.Label(root, text="Time (HH:MM):").grid(row=2, column=0, padx=10, pady=10)
time

