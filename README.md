# Code-for-Satistical-calculator
from tkinter import *
import tkinter as tk

# Create functions for calculating measures of central tendency and dispersion

# Calculate Arithmetic Mean
def calculate_arithmetic_mean(numbers):
    return sum(numbers) / len(numbers)

# Calculate Harmonic Mean
def calculate_harmonic_mean(numbers):
    return len(numbers) / sum(1 / x for x in numbers)

# Calculate Geometric Mean
def calculate_geometric_mean(numbers):
    product = 1
    for num in numbers:
        product *= num
    return product**(1/len(numbers))

# Calculate Mode
def calculate_mode(numbers):
    from collections import Counter
    count = Counter(numbers)
    mode = count.most_common(1)
    return mode[0][0]

# Calculate Median
def calculate_median(numbers):
    numbers.sort()
    n = len(numbers)
    if n % 2 == 0:
        mid1 = numbers[n // 2]
        mid2 = numbers[n // 2 - 1]
        median = (mid1 + mid2) / 2
    else:
        median = numbers[n // 2]
    return median

# Calculate Range
def calculate_range(numbers):
    return max(numbers) - min(numbers)

# Calculate Variance
def calculate_variance(numbers):
    mean = calculate_arithmetic_mean(numbers)
    squared_diff = [(x - mean) ** 2 for x in numbers]  # Fixed the calculation
    variance = sum(squared_diff) / len(numbers)
    return variance

# Calculate Standard Deviation
def calculate_standard_deviation(numbers):
    variance = calculate_variance(numbers)
    return variance ** 0.5  # Fixed the calculation

# Calculate Mean Absolute Deviation (MAD)
def calculate_mean_absolute_deviation(numbers):
    mean = calculate_arithmetic_mean(numbers)
    mad = sum(abs(x - mean) for x in numbers) / len(numbers)
    return mad

# Create the main GUI
root = Tk()
root.title("Project-1: Measure of Central Tendency and Dispersion")
root.minsize(700, 500)
root.maxsize(1200, 988)

# Adding widgets to the Main window

title_label = Label(text='Title: Measure of Central Tendency and Dispersion', font=('Arial', 15))
author_label = Label(text='Author Details:  Khushi Panwar', font=('Arial', 10))
title_label.pack()
author_label.pack()

number_label = Label(text='Enter List of Nos. (space-separated):', font=('Arial', 12))
number_label.place(x=10, y=75)

number_text = Text(height=1, width=30)
number_text.place(x=270, y=75)

ctLabel = Label(text='Measure of Central Tendency', font=('Arial', 12))
ctLabel.place(x=10, y=150)

var = IntVar()
r1_ct = Radiobutton(text="Arithmetic Mean", variable=var, value=1)
r2_ct = Radiobutton(text="Harmonic Mean", variable=var, value=2)
r3_ct = Radiobutton(text="Geometric Mean", variable=var, value=3)
r4_ct = Radiobutton(text="Mode", variable=var, value=4)
r5_ct = Radiobutton(text="Median", variable=var, value=5)

r1_ct.place(x=10, y=200)
r2_ct.place(x=10, y=220)
r3_ct.place(x=10, y=240)
r4_ct.place(x=10, y=260)
r5_ct.place(x=10, y=280)

dispLabel = Label(text='Measure of Dispersion', font=('Arial', 12))
dispLabel.place(x=10, y=310)

var_dispersion = IntVar()
r1_dispersion = Radiobutton(text="Range", variable=var_dispersion, value=1)
r2_dispersion = Radiobutton(text="Variance", variable=var_dispersion, value=2)
r3_dispersion = Radiobutton(text="Standard Deviation", variable=var_dispersion, value=3)
r4_dispersion = Radiobutton(text="Mean Absolute Deviation (MAD)", variable=var_dispersion, value=4)

r1_dispersion.place(x=10, y=340)
r2_dispersion.place(x=10, y=360)
r3_dispersion.place(x=10, y=380)
r4_dispersion.place(x=10, y=400)

result_label = Label(font=('Arial', 12))
result_label.place(x=10, y=460)

def calculate_central_tendency():
    numbers_str = number_text.get("1.0", "end-1c")
    numbers = [float(x) for x in numbers_str.split()]
    choice = var.get()

    if choice == 1:  # Arithmetic Mean
        result_label.config(text=f"Arithmetic Mean: {calculate_arithmetic_mean(numbers)}")
    elif choice == 2:  # Harmonic Mean
        result_label.config(text=f"Harmonic Mean: {calculate_harmonic_mean(numbers)}")
    elif choice == 3:  # Geometric Mean
        result_label.config(text=f"Geometric Mean: {calculate_geometric_mean(numbers)}")
    elif choice == 4:  # Mode
        result_label.config(text=f"Mode: {calculate_mode(numbers)}")
    elif choice == 5:  # Median
        result_label.config(text=f"Median: {calculate_median(numbers)}")

def calculate_dispersion():
    numbers_str = number_text.get("1.0", "end-1c")
    numbers = [float(x) for x in numbers_str.split()]
    choice = var_dispersion.get()

    if choice == 1:  # Range
        result_label.config(text=f"Range: {calculate_range(numbers)}")
    elif choice == 2:  # Variance
        result_label.config(text=f"Variance: {calculate_variance(numbers)}")
    elif choice == 3:  # Standard Deviation
        result_label.config(text=f"Standard Deviation: {calculate_standard_deviation(numbers)}")
    elif choice == 4:  # Mean Absolute Deviation (MAD)
        result_label.config(text=f"Mean Absolute Deviation (MAD): {calculate_mean_absolute_deviation(numbers)}")

calculate_button = Button(text='Calculate Selected Option in Measures of Central Tendency', command=calculate_central_tendency)
calculate_button.place(x=200, y=200)

calculate_dispersion_button = Button(text='Calculate Selected Option in Measures of Dispersion', command=calculate_dispersion)
calculate_dispersion_button.place(x=200, y=350)

quitButton = Button(text='End Now', command=root.destroy)
quitButton.pack(padx=20, pady=20, side=tk.BOTTOM)

root.mainloop()
