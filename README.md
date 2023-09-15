import tkinter as tk

def click_button(event):
    current_text = display.get()
    button_text = event.widget.cget("text")
    
    if button_text == "=":
        try:
            result = eval(current_text)
            display.set(result)
        except Exception as e:
            display.set("Error")
    elif button_text == "C":
        display.set("")
    else:
        display.set(current_text + button_text)

root = tk.Tk()
root.title("Simple Calculator")

display = tk.StringVar()
entry = tk.Entry(root, textvar=display, font="Arial 20", bd=10, insertwidth=4, width=14, borderwidth=4, relief="ridge", justify="right")
entry.grid(row=0, column=0, columnspan=4)

buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    'C', '0', '=', '+'
]

row_val = 1
col_val = 0

for button in buttons:
    button_frame = tk.Frame(root)
    button_frame.grid(row=row_val, column=col_val)
    button_val = tk.Button(button_frame, text=button, padx=20, pady=20, font="lucida 15")
    button_val.pack()
    button_val.bind("<Button-1>", click_button)

    col_val += 1
    if col_val > 3:
        col_val = 0
        row_val += 1

root.mainloop()
