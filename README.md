# contackbooks

from tkinter import messagebox
from tkinter import*
import random
import os
import webbrowser
root = Tk()
root.title('Contact book')
root.geometry('650x300')
root.config(bg ='#121212')
listbox = Listbox(root,width=40,height=15)
listbox.place(relx=0.75,rely=0.47,anchor='c')

def add_contact():
    contact_str = name_entry.get()+':'+phone_entry.get()
    listbox.insert(End,contact_str)
    name_entry.delete(0,End)
    phone_entry.delete(0,End)
    

def dell():
    listbox.delete(ANCHOR)

def Open():
    with open("save.txt", 'r') as F:
        for line in F:
            listbox.insert(End,line)

def save():
    with open("save.txt",'w') as F:
        list_tuple = listbox.get(0,End)
        for item in list_tuple:
            if item.endwith('\n'):
                F.writer(item)
            else:
                F.write(item + '\n')
def Open_dir():
    webbrowser.open("save.txt")
    
def copy():
    selected_contact = listbox.get(ANCHOR)
    number = selected_contact.split(':')
    pyperclip.copy(number[1])

def Exit():
    choice = messagebox.askquestion('Exit App are your sure?')
    if choice == 'yes':
        root.destroy
    else:
        return
name_label = Label(root,text ='ContactName',bg='#121212',
                  fg ='white',font=('Calibri',12),anchor='w',justify=LEFT)
name_label.place(relx=0.1,rely=0.1,anchor='c')

name_entry = Entry(root,text = 'ContactName',bg='#121212',
                  fg ='white',width =30,bd=2)
name_entry.place(relx=0.4,rely=0.1,anchor='c')
phone_label = Label(root,text ='ContactNumber',bg='#121212',
                  fg ='white',font=('Calibri',12),anchor='w',justify=LEFT)
phone_label.place(relx=0.1,rely=0.2,anchor='c')

phone_entry = Entry(root,text = 'ContactNumber',bg='#121212',
                  fg ='white',width =30,bd=2)
phone_entry.place(relx=0.4,rely=0.2,anchor='c')
add_btn = Button(root,text='Add Contact',bg='#121212',fg='white',
                 command = add_contact, bd =3,padx=125)
add_btn.place (relx=0.29,rely=0.35,anchor='c')

save_btn =  Button(root,text='Save list',bg='#121212',fg='white',
                 command = save, bd =3,padx=135)
save_btn.place(relx = 0.29,rely=0.5,anchor='c')

copy_btn = Button(root,text='Copy phone', bg='#121212',fg='white',
                 command = copy, bd =3,padx=10)
copy_btn.place(relx=0.15,rely=0.65,anchor='c')

del_btn = Button(root,text='Delete Phone',bg='#121212',fg='white',
                 command=dell, bd=3,padx=25)
del_btn.place(relx=0.15,rely=0.77,anchor='c')

open_btn = Button(root,text='Open Saved',bg='#121212',fg='white',
                  command=Open ,bd=3,padx=30)
open_btn.place(relx=0.42,rely=0.65,anchor='c')


exit_btn = Button(root,text='Exit App',bg='#121212',fg='white',
                  command=Exit,bd=3,padx=50)
exit_btn.place(relx=0.42,rely=0.77,anchor='c')
End =contact_str [::]
Open()
root.mainloop()

