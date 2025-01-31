import random
import time
import tkinter as tk
from tkinter import *
from tkinter import messagebox, simpledialog
from PIL import Image, ImageTk
from tkinter import font
from tkinter import Label, Tk
from tkinter import ttk
from tkinter import Tk, StringVar, Entry, Button, Toplevel, Label

def center_window(window, width, height):
    screen_width = window.winfo_screenwidth()
    screen_height = window.winfo_screenheight()
    x_coordinate = int((screen_width / 2) - (width / 2))
    y_coordinate = int((screen_height / 2) - (height / 2))
    window.geometry(f"{width}x{height}+{x_coordinate}+{y_coordinate}")

def open_start_window():
    start_window = Tk()
    start_window.geometry('600x800')
    start_window.title("Welcome to Math-Rumble-GUI!")
    
    window_width = 600
    window_height = 800
    start_window.geometry(f"{window_width}x{window_height}")
    
    center_window(start_window, window_width, window_height)
                          
    lm = Image.open(r"Math 6")                                                #Add 'Math 6' image source here:)
    lm = lm.resize((600, 800), Image.LANCZOS) 
    lm_image = ImageTk.PhotoImage(lm)
    lm_label = Label(start_window, image=lm_image, bg="white")
    lm_label.grid(row=0, column=0, columnspan=2)
    lm_label.place(x=0, y=0, anchor='nw')# position of image

    def exit_window():
        start_window.destroy()
        
    font_style = font.Font(family='Arial bold', size=15, weight='bold')
    exit_button = tk.Button(text='Start', bg='dodgerblue1', fg='white',command=exit_window)
    exit_button['font'] = font_style
    exit_button.config(height=5, width=20)
    exit_button.place(x=180, y=600)

    start_window.mainloop()
open_start_window()

#=================================================================================================================
#Backend
tasks_list = []
counter = 1

def inputError():
    if enterTaskField.get() == "":
        messagebox.showerror("Input Error", "Please enter a calculation.")
        return 0
    return 1
        
#=================================================================================================================
#Timer

time_left = 0
running = False  # Tracks if the timer is running
timer_id = None

def countdowntimer():
    times = int(hrs.get()) * 3600 + int(mins.get()) * 60 + int(sec.get())
#---
def update_timer():
    global time_left, running, timer_id
    if running and time_left >= 0:
        minute, second = divmod(time_left, 60)
        hour = minute // 60
        sec.set(f"{second:02d}")
        mins.set(f"{minute % 60:02d}")
        hrs.set(f"{hour:02d}")
        time_left -= 1
        timer_id = win.after(1000, update_timer)
    else:
        running = False  # Stop timer
        sec.set('00')
        mins.set('00')
        hrs.set('00')
    
#pause/stop timer function
def countdowntimer():
    global time_left, running
    if running:
        return  

    try:
        time_left = int(hrs.get()) * 3600 + int(mins.get()) * 60 + int(sec.get())
        running = True
        update_timer()
    except ValueError:
        messagebox.showerror("Input Error", "Please enter valid numbers for hours, minutes, and seconds.")

def pause_timer():
    global running, timer_id
    if running:
        running = False
        if timer_id is not None:
            win.after_cancel(timer_id)
            timer_id = None  
#---
def generate_math_problem():
    pattern = enterMathField.get()
    if '+' in pattern:
        op = '+'
    elif '-' in pattern:
        op = '-'
    elif '*' in pattern:
        op = '*'
    elif '/' in pattern:
        op = '/'
    else:
        messagebox.showerror("Input Error", "Please enter a valid operation.")
        return
#---
    left_limit = int(pattern.split(op)[0].strip())
    right_limit = int(pattern.split(op)[1].strip())
    rights = wrongs = 0
#---
    while True:
        a = random.randint(0 if op != '/' else 1, left_limit)
        b = random.randint(0 if op != '/' else 1, right_limit)
        if op in ['-', '/']:
            a, b = max(a, b), min(a, b)

        result = eval(f"{a} {op} {b}")
        answer = simpledialog.askinteger("Math Problem", f"{a} {op} {b} = ?")
        
        if answer is None:  # User cancelled the dialog
            break
        
        if answer == result:
            rights += 1
            messagebox.showinfo("Result", "Right!")
        else:
            wrongs += 1
            messagebox.showinfo("Result", "Wrong!")
        
        again = messagebox.askyesno("Continue?", "Do you want to solve another problem?")
        if not again:
            score = f"{rights} right, {wrongs} wrong."
            messagebox.showinfo("Your Score", score)
            break
#========================================================================================================
#Frontend

#---
win = Tk()
win.title("Math-Rumble-GUI")
win.geometry("600x800")
win.configure(background="white")

#---

window_height = 800
window_width = 600

def center_screen():
    """ gets the coordinates of the center of the screen """
    global screen_height, screen_width, x_cordinate, y_cordinate

    screen_width = win.winfo_screenwidth()
    screen_height =win.winfo_screenheight()
# Coordinates of the upper left corner of the window to make the window appear in the center
    x_cordinate = int((screen_width/2) - (window_width/2))
    y_cordinate = int((screen_height/2) - (window_height/2))
    win.geometry("{}x{}+{}+{}".format(window_width, window_height, x_cordinate, y_cordinate))
    
center_screen()   
#---

logo = Image.open("")                                                                           #I added my logo for the GUI here:)
logo = logo.resize((100, 100), Image.LANCZOS) 
logo_image = ImageTk.PhotoImage(logo)
logo_label = Label(win, image=logo_image, bg="white")
logo_label.grid(row=0, column=0, columnspan=2)
logo_label.place(x=0, y=0, anchor='nw')# position of logo
#-
label = tk.Label(win)
Label(win, text="Enter Math Pattern (+,-,*,/) To Practice like (10 + 10)", bg="light blue").grid(row=20, column=1)
label.place(x=225, y=300)# position of text field
enterMathField = Entry(win)
enterMathField.grid(row=9, column=1)
enterMathField.place(x=225, y=300, anchor='nw')# position of text field
#-
MathButton = Button(win, text="Generate Math Problem", command=generate_math_problem, bg="light yellow")
MathButton.grid(row=14, column=1)
MathButton.place(x=225, y=250)# position of text field
#-
Label(win, text="Set Timer (Hour:Min:Sec)", bg="light blue").grid(row=10, column=1)
hrs = StringVar(value='00')
mins = StringVar(value='00')
sec = StringVar(value='00')
#setting position of the time display
hrs_enter = tk.Entry(label, textvariable=hrs, width=3)
mins_enter = tk.Entry(label, textvariable=mins, width=3)
sec_enter = tk.Entry(label, textvariable=sec, width=3)

hrs_enter.place(relx=0.4, rely=0.5, anchor="center") 
mins_enter.place(relx=0.5, rely=0.5, anchor="center")
sec_enter.place(relx=0.6, rely=0.5, anchor="center")

Entry(label, textvariable=hrs, width=2).grid(row=16, column=0)
Entry(label, textvariable=mins, width=2).grid(row=16, column=1)
Entry(label, textvariable=sec, width=2).grid(row=16, column=2)
#-

TimerButton = tk.Button(win, text="Start Timer", foreground="white", command=countdowntimer, bg="dodgerblue1")
TimerButton.grid(row=13, column=1)
TimerButton.config(height=5, width=20)
TimerButton.place(x=320, y=600)
#pause
PauseButton = tk.Button(win, text="Pause Timer", foreground="white", command=pause_timer, bg="red")
PauseButton.grid(row=14, column=1)
PauseButton.config(height=5, width=20)
PauseButton.place(x=120, y=600)

# Configure grid to center the label
win.columnconfigure(0, weight=1)
win.columnconfigure(1, weight=1)
win.columnconfigure(2, weight=1)
label.grid(row=0, column=1)

#=====================================================================================================================
#simple calculator 

def open_calc():
    cal = Toplevel(win)
    cal.title("Calculator Rumble")
    cal.geometry("270x150")
    cal.configure(background="white")
    
    global expression
    expression =""
    
    def press(num):
        global expression
        expression += str(num)
        equation.set(expression)
    def equal_press():
        global expression
        try:
            total = str(eval(expression))
            equation.set(total)
            expression =""
        except:
            equation.set("error")
            expression =""
    def clear(num):
        global expression
        expression =""
        equation.set("")
    
    equation = StringVar()
    expression_field = Entry(cal, textvariable=equation) 
    expression_field.grid(columnspan=4, ipadx=70)
    expression = "" 
    
    button1 = Button(cal, text=' 1 ', fg='white', bg='red', 
                    command=lambda: press(1), height=1, width=7) 
    button1.grid(row=2, column=0) 
 
    button2 = Button(cal, text=' 2 ', fg='white', bg='red', 
                    command=lambda: press(2), height=1, width=7) 
    button2.grid(row=2, column=1) 
 
    button3 = Button(cal, text=' 3 ', fg='white', bg='red', 
                    command=lambda: press(3), height=1, width=7) 
    button3.grid(row=2, column=2) 
 
    button4 = Button(cal, text=' 4 ', fg='white', bg='red', 
                    command=lambda: press(4), height=1, width=7) 
    button4.grid(row=3, column=0) 
 
    button5 = Button(cal, text=' 5 ', fg='white', bg='red', 
                    command=lambda: press(5), height=1, width=7) 
    button5.grid(row=3, column=1) 
 
    button6 = Button(cal, text=' 6 ', fg='white', bg='red', 
                    command=lambda: press(6), height=1, width=7) 
    button6.grid(row=3, column=2) 
 
    button7 = Button(cal, text=' 7 ', fg='white', bg='red', 
                    command=lambda: press(7), height=1, width=7) 
    button7.grid(row=4, column=0) 
 
    button8 = Button(cal, text=' 8 ', fg='white', bg='red', 
                    command=lambda: press(8), height=1, width=7) 
    button8.grid(row=4, column=1) 
 
    button9 = Button(cal, text=' 9 ', fg='white', bg='red', 
                    command=lambda: press(9), height=1, width=7) 
    button9.grid(row=4, column=2) 
 
    button0 = Button(cal, text=' 0 ', fg='white', bg='red', 
                    command=lambda: press(0), height=1, width=7) 
    button0.grid(row=5, column=0) 
 
    plus = Button(cal, text=' + ', fg='white', bg='red', 
                command=lambda: press("+"), height=1, width=7) 
    plus.grid(row=2, column=3) 
 
    minus = Button(cal, text=' - ', fg='white', bg='red', 
                command=lambda: press("-"), height=1, width=7) 
    minus.grid(row=3, column=3) 
 
    multiply = Button(cal, text=' * ', fg='white', bg='red', 
                    command=lambda: press("*"), height=1, width=7) 
    multiply.grid(row=4, column=3) 
 
    divide = Button(cal, text=' / ', fg='white', bg='red', 
                    command=lambda: press("/"), height=1, width=7) 
    divide.grid(row=5, column=3) 
 
    equal = Button(cal, text=' = ', fg='white', bg='red', 
                command=equal_press, height=1, width=7) 
    equal.grid(row=5, column=2) 
 
    clear = Button(cal, text='Clear', fg='white', bg='red', 
                command=clear, height=1, width=7) 
    clear.grid(row=5, column='1') 
 
    Decimal= Button(cal, text='.', fg='white', bg='red', 
                    command=lambda: press('.'), height=1, width=7) 
    Decimal.grid(row=6, column=0)
        
    buttons = [
        ('1', 2, 0), ('2', 2, 1), ('3', 2, 2),
        ('4', 3, 0), ('5', 3, 1), ('6', 3, 2),
        ('7', 4, 0), ('8', 4, 1), ('9', 4, 2),
        ('0', 5, 0), ('+', 2, 3), ('-', 3, 3),
        ('*', 4, 3), ('/', 5, 3), ('=', 5, 2),
        ('Clear', 5, 1), ('.', 6, 0)
    ]
    
    for (text, row, col) in buttons:
        if text == '=':
            Button(cal, text=text, fg='white', bg='red', command=equal_press, height=1, width=7).grid(row=row, column=col)
        elif text == 'Clear':
            Button(cal, text=text, fg='white', bg='red', command=clear, height=1, width=7).grid(row=row, column=col)
        else:
            Button(cal, text=text, fg='white', bg='red', command=lambda t=text: press(t), height=1, width=7).grid(row=row, column=col)
    
    cal.mainloop()
               
open_calc_button = Button(win, text="Open Calculator", fg='white', bg='blue', command=open_calc, height=2, width=15)
open_calc_button.place(x=225, y=500)

win.mainloop()
