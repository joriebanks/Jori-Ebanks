# Jori Ebanks
# Final Poject 2025
import tkinter as tk
from tkinter import Canvas


def letter_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

grade_counts = {"A": 0,"B": 0,"C": 0,"D": 0,"F": 0}

total = 0

file = open("grade.txt", "r")

file.readline()

line = file.readline()

while line != "":    
    grades = line.strip().split(",")    
    number = int(grades[0])    
    letter = letter_grade(number)    
    grade_counts[letter] += 1    
    total += number    
    line = file.readline()

file.close()


def draw_pie_chart(data):    
    window = tk.Tk()    
    window.title("Grade Distribution Pie Chart")    
    canvas = Canvas(window, width=400, height=400)    
    canvas.pack()
    total = sum(data.values())    
    start_angle = 0
        colors = {"A": "green", "B": "lime", "C": "yellow", "D": "orange", "F": "red"}
    for grade, count in data.items():    
        if count > 0:            
            extent = (count / total) * 360            
            canvas.create_arc(50, 50, 350, 350, start=start_angle, extent=extent, fill=colors[grade])            
            start_angle += extent
    window.mainloop() 

print("\nGrade Counts:")

for grade, count in grade_counts.items():    
    print(f"{grade}: {count}")


draw_pie_chart(grade_counts)

file_menu = tk.Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New", command=clear_graph)
file_menu.add_separator()
file_menu.add_command(label="Open", command=process_data)
file_menu.add_separator()
file_menu.add_command(label="Exit", command=exit_program)
menu_bar.add_cascade(label="File", menu=file_menu)

