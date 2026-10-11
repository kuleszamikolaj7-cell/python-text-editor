import PySimpleGUI as sg
import io
import os
script_dir = os.path.dirname(__file__)
currentSize =11
currentFont = 'Arial'
icon_path = os.path.join(script_dir, "favicon.ico")
icon = icon_path if os.path.isfile(icon_path) else None
menu = [["File",["New", "Open", "Save", "Save As", "Exit"]], ["Edit", ["Font",["Arial","Courier"],["Size",["8","11","22"]]]], ["Help", ["About",["Version 1.0"]]]]
filename=None
def about():
    sg.popup('Text Editor', 'Version 1.0', 'Created by MK', title='About')
def save(data):
    if filename!= '':

        with io.open(filename,'w',encoding='utf8') as f:
            f.write(data)
def save_as(data):
    global filename
    new_filename = sg.tk.filedialog.asksaveasfilename(
        defaultextension=".txt",
        filetypes=[("Text files", "*.txt"), ("All files", "*.*")],
        initialdir=script_dir,
        title="Save As"
    )
    if not new_filename:
        return False
    
    if new_filename != '':
         with io.open(new_filename,'w',encoding='utf8') as f:
             f.write(data)

    filename = new_filename
    window.TKroot.title(f"Text Editor - {os.path.basename(filename)}")
    return True

def new_file():
    global filename
    filename= None

    window['TEXT'].update('')
    window.TKroot.title("Text Editor - Untitled")
def open_file():
    fileopen=sg.popup_get_file("file to open", no_window=True)
    if not fileopen:
        return False
    try:
        with io.open( fileopen,"r",encoding="utf-8") as f:
            text=f.read()
    except (OSError, UnicodeError) as error:
        sg.popup_error(f"Cannot open file:\n{error}")
        return
    filename= fileopen
    window['TEXT'].update(value= text)
    window.TKroot.title(f"Text Editor - {os.path.basename(filename)}")

layout=[
    [sg.Menu(menu)],
    [sg.Multiline(size=(80, 20), font=(currentFont, currentSize),expand_x=True,expand_y=True, key='TEXT')]
]

window=sg.Window('Text Editor', layout,icon="favicon.ico", resizable=True, finalize=True)
while True:
    event, values = window.read()
    if event == sg.WINDOW_CLOSED or event == 'Exit':
        break
    if event == 'Courier':
        currentFont = 'Courier'
        font = ('Courier', currentSize)
        window['TEXT'].update(font=font)
    elif event == 'Arial':
        currentFont = 'Arial'
        font = ('Arial', currentSize)
        window['TEXT'].update(font=font)
    elif event == '8':
        currentSize = 8
        font = (currentFont, currentSize)
        window['TEXT'].update(font=font)
    elif event == '11':
        currentSize = 11
        font = (currentFont, currentSize)
        window['TEXT'].update(font=font)
    elif event == '22':
        currentSize = 22
        font = (currentFont, currentSize)
        window['TEXT'].update(font=font)
    if event == 'Version 1.0':
        about()
    if event == 'Save':
        if filename is None:
            save_as(values['TEXT'])
        else:
            save(values['TEXT']) 
    if event == 'Save As':
        save_as(values['TEXT'])
    if event == 'New':
        if sg.popup_yes_no(
        'Create a new file? Unsaved changes will be lost.',
         title='New File',
            keep_on_top=True
        ) == 'Yes':
            new_file()
    if event== 'Open':
        open_file()




window.close()

