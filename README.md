from tkinter import *
import threading
import time
import webbrowser


def countdown():
    global x, y, z
    while x > 0 or y > 0 or z > 0:
        if z == 0:
            if y == 0:
                if x > 0:
                    x -= 1
                    y = 59
                    z = 59
            else:
                y -= 1
                z = 59
        else:
            z -= 1
        
        x2 = f"{x:02}"
        y2 = f"{y:02}"
        z2 = f"{z:02}"
        
        label.config(text=f"{x2}:{y2}:{z2}")
        
        # Sleep for 1 second
        time.sleep(1)

    if True:
        webbrowser.open("https://www.youtube.com/watch?v=dQw4w9WgXcQ")



def start():
    global x, y, z
    try:
        x = int(entry.get())
        y = int(entry2.get())
        z = int(entry3.get())
    except ValueError:
        label.config(text="Invalid input")
        return
    
    thread = threading.Thread(target=countdown)
    thread.start()

root = Tk()
root.title("Timer")
default_text = "00"

label = Label(root, text="00:00:00")
label.place(x=65, y=30)

entry = Entry(root, width=2)
entry.insert(0, default_text)
entry.place(x=60, y=60)

entry2 = Entry(root, width=2)
entry2.insert(0, default_text)
entry2.place(x=80, y=60)

entry3 = Entry(root, width=2)
entry3.insert(0, default_text)
entry3.place(x=100, y=60)

label_h = Label(root, text="H")
label_h.place(x=60, y=80)

label_m = Label(root, text="M")
label_m.place(x=80, y=80)

label_s = Label(root, text="S")
label_s.place(x=103, y=80)

button = Button(root, text="Start", command=start)
button.place(x=70, y=100)

root.mainloop()
