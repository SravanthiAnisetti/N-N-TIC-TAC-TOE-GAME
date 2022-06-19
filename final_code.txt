import sys
from tkinter import *
import tkinter.font as tkfont
import tkinter.messagebox
from tkinter import simpledialog
from tkinter import filedialog
from copy import deepcopy
import random

import pygame
pygame.init()
winner_sound = pygame.mixer.Sound("winner.wav")
boing = pygame.mixer.Sound("boing.wav")
song1 = pygame.mixer.music.load("song1.wav")
pygame.mixer.music.play()

root = tkinter.Tk()
root.title("Tic Tac Toe")
root.configure(background="powder blue")
font = tkfont.Font(font="Times 36 bold")

isPlayed = False
value_click = 0
value_1 = 0
value_2 = 0
win = 0
draw_game = 0
getentrance1 = ""
getentrance2 = ""
lst = []

lbl1 = tkinter.Label(root, text="Name player 1 with X ")
name1 = lbl1.grid(row=1,column=0)
name2 = tkinter.Label(root, text="Name player 2 with O ").grid(row=2,column=0)
size_ = tkinter.Label(root, text="Size of the Board").grid(row=3,column=0)
b1 = tkinter.Button(root, text="Computer vs Player",command=lambda:play1()).grid(row=6,column=0)
b2 = tkinter.Button(root, text="Player vs Player",command=lambda:play()).grid(row=6,column=1)
 


entrance1 = tkinter.Entry(root, bd =5)
entrance1.grid(row=1,column=1)
entrance2 = tkinter.Entry(root, bd =5)
entrance2.grid(row=2,column=1)
entrance3 = tkinter.Entry(root, bd =5)
entrance3.grid(row=3,column=1)

def check(table,button) :
    global value_click
    global win
    global draw_game
    global wins
    global value_1
    global value_2
    global draws
    global table_signs
    global final_matrix
    diagonal1 = ""
    diagonal2 = ""
    answer2 = entrance3.get()

    if button["text"]==" " and value_click == 0 :
        button.config(text="X")
        table_signs[table.index(button)]="X"
        value_click = 1
        value_1 = value_1 + 1
    if button["text"]==" " and value_click == 1 :
        button.config(text="O")
        table_signs[table.index(button)]="O"
        value_click = 0
        value_2 = value_2 + 1
    l = 0
    for i in range(int(answer2)) :
        for j in range(int(answer2)) :
            if l < len(table_signs) :
                final_matrix[i][j] = table_signs[l]
                l = l + 1

    for i in range(int(answer2)) :
        count = 0
        for j in range(int(answer2)-1) :
            if final_matrix[i][j] == "X" or final_matrix[i][j] == "O" :
               if final_matrix[i][j] == final_matrix[i][j+1] :
                   c = final_matrix[i][j]
                   count = count + 1
        if count==int(answer2)-1:
            if c=="X":
                winner = "congratulations "+getentrance1+" ,you've won the game"
            else :
                winner = "congratulations "+getentrance2+" ,you've won the game" 
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play()
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win))
            final_matrix = [['P' for j in range(int(answer2))]for i in range(int(answer2))]
            root.destroy()

    for j in range(int(answer2)) :
        count = 0
        for i in range(int(answer2)-1) :
            if final_matrix[i][j] == "X" or final_matrix[i][j] == "O" :
               if final_matrix[i][j] == final_matrix[i+1][j] :
                   c = final_matrix[i][j]
                   count = count + 1
        if count==int(answer2)-1:
            if c=="X":
                winner = "congratulations "+getentrance1+" ,you've won the game"
            else :
                winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win))
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            root.destroy()

    for i in range(int(answer2)):
        diagonal1 = diagonal1 + final_matrix[i][i]

    if (diagonal1.count("X") == int(answer2)) :
        winner = "congratulations "+getentrance1+" ,you've won the game" 
        winner_sound.play()
        pygame.mixer.music.load("winner.wav")
        pygame.mixer.music.play() 
        tkinter.messagebox.showinfo("Announcement",winner) 
        win = win + 1
        wins = tkinter.Label(root,text="Wins : "+str(win))
        final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
        diagonal1 = ""
        root.destroy()
    else :
        if (diagonal1.count("O") == int(answer2)) :
            winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()

        for i in range(int(answer2)):
            diagonal2 = diagonal2 + final_matrix[i][int(answer2)-i-1]

        if (diagonal2.count("X") == int(answer2)) :
            winner = "congratulations "+getentrance1+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()

        if (diagonal2.count("O") == int(answer2)) :
            winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()

        if value_1 + value_2 == int(answer2)**2 and win == 0 :
            draw = getentrance1+" and "+getentrance2+" ,you've made a draw. Please try again!"
            boing.play()
            pygame.mixer.music.load("boing.wav")
            pygame.mixer.music.play()
            tkinter.messagebox.showinfo("Draw",draw) 
            draw_game = draw_game + 1
            draws = tkinter.Label(root,text="Draws : "+str(draw_game)).grid(row=2,column=5)
            diagonal1 = ""
            diagonal2 = ""
            root.destroy()
            
def check1(table,button) :
    global win
    global draw_game
    global wins
    global value_1
    global value_2
    global draws
    global table_signs
    global final_matrix
    global lst
    global validClick
    diagonal1 = ""
    diagonal2 = ""
    answer2 = entrance3.get()
    
    if button["text"]==" ":
        button.config(text="X")
        table_signs[table.index(button)]="X"
        value_click = 1
        value_1 = value_1 + 1
        lst.remove(button)
        validClick = True
    l = 0
    for i in range(int(answer2)) :
        for j in range(int(answer2)) :
            if l < len(table_signs) :
                final_matrix[i][j] = table_signs[l]
                l = l + 1

    for i in range(int(answer2)) :
        count = 0
        for j in range(int(answer2)-1) :
            if final_matrix[i][j] == "X" or final_matrix[i][j] == "O" :
               if final_matrix[i][j] == final_matrix[i][j+1] :
                   c = final_matrix[i][j]
                   count = count + 1
        if count==int(answer2)-1:
            if c=="X":
                winner = "congratulations "+getentrance1+" ,you've won the game"
            else :
                winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play()  
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win))
            final_matrix = [['P' for j in range(int(answer2))]for i in range(int(answer2))]
            root.destroy()
            return

    for j in range(int(answer2)) :
        count = 0
        for i in range(int(answer2)-1) :
            if final_matrix[i][j] == "X" or final_matrix[i][j] == "O" :
               if final_matrix[i][j] == final_matrix[i+1][j] :
                   c = final_matrix[i][j]
                   count = count + 1
        if count==int(answer2)-1:
            if c=="X":
                winner = "congratulations "+getentrance1+" ,you've won the game"
            else :
                winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win))
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            root.destroy()
            return

    for i in range(int(answer2)):
        diagonal1 = diagonal1 + final_matrix[i][i]

    if (diagonal1.count("X") == int(answer2)) :
        winner = "congratulations "+getentrance1+" ,you've won the game" 
        winner_sound.play()
        pygame.mixer.music.load("winner.wav")
        pygame.mixer.music.play() 
        tkinter.messagebox.showinfo("Announcement",winner) 
        win = win + 1
        wins = tkinter.Label(root,text="Wins : "+str(win))
        final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
        diagonal1 = ""
        root.destroy()
        return
    else :
        if (diagonal1.count("O") == int(answer2)) :
            winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()
            return

        for i in range(int(answer2)):
            diagonal2 = diagonal2 + final_matrix[i][int(answer2)-i-1]

        if (diagonal2.count("X") == int(answer2)) :
            winner = "congratulations "+getentrance1+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()
            return

        if (diagonal2.count("O") == int(answer2)) :
            winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()
            return

        if value_1 + value_2 == int(answer2)**2 and win == 0 :
            draw = getentrance1+" and "+getentrance2+" ,you've made a draw. Please try again!"
            boing.play()
            pygame.mixer.music.load("boing.wav")
            pygame.mixer.music.play()
            tkinter.messagebox.showinfo("Draw",draw) 
            draw_game = draw_game + 1
            draws = tkinter.Label(root,text="Draws : "+str(draw_game)).grid(row=2,column=5)
            diagonal1 = ""
            diagonal2 = ""
            root.destroy()
            return
    
    diagonal1 = ""
    diagonal2 = ""
    if validClick:
        button = random.sample(lst, 1)[0]
        button.config(text="O")
        table_signs[table.index(button)]="O"
        value_click = 0
        value_2 = value_2 + 1
        lst.remove(button)
        validClick = False
    
    l = 0
    for i in range(int(answer2)) :
        for j in range(int(answer2)) :
            if l < len(table_signs) :
                final_matrix[i][j] = table_signs[l]
                l = l + 1

    for i in range(int(answer2)) :
        count = 0
        for j in range(int(answer2)-1) :
            if final_matrix[i][j] == "X" or final_matrix[i][j] == "O" :
               if final_matrix[i][j] == final_matrix[i][j+1] :
                   c = final_matrix[i][j]
                   count = count + 1
        if count==int(answer2)-1:
            if c=="X":
                winner = "congratulations "+getentrance1+" ,you've won the game"
            else :
                winner = "congratulations "+getentrance2+" ,you've won the game" 
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win))
            final_matrix = [['P' for j in range(int(answer2))]for i in range(int(answer2))]
            root.destroy()

    for j in range(int(answer2)) :
        count = 0
        for i in range(int(answer2)-1) :
            if final_matrix[i][j] == "X" or final_matrix[i][j] == "O" :
               if final_matrix[i][j] == final_matrix[i+1][j] :
                   c = final_matrix[i][j]
                   count = count + 1
        if count==int(answer2)-1:
            if c=="X":
                winner = "congratulations "+getentrance1+" ,you've won the game"
            else :
                winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win))
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            root.destroy()

    for i in range(int(answer2)):
        diagonal1 = diagonal1 + final_matrix[i][i]

    if (diagonal1.count("X") == int(answer2)) :
        winner = "congratulations "+getentrance1+" ,you've won the game" 
        winner_sound.play()
        pygame.mixer.music.load("winner.wav")
        pygame.mixer.music.play() 
        tkinter.messagebox.showinfo("Announcement",winner) 
        win = win + 1
        wins = tkinter.Label(root,text="Wins : "+str(win))
        final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
        diagonal1 = ""
        root.destroy()
    else :
        if (diagonal1.count("O") == int(answer2)) :
            winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()

        for i in range(int(answer2)):
            diagonal2 = diagonal2 + final_matrix[i][int(answer2)-i-1]

        if (diagonal2.count("X") == int(answer2)) :
            winner = "congratulations "+getentrance1+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()

        if (diagonal2.count("O") == int(answer2)) :
            winner = "congratulations "+getentrance2+" ,you've won the game"
            winner_sound.play()
            pygame.mixer.music.load("winner.wav")
            pygame.mixer.music.play() 
            tkinter.messagebox.showinfo("Announcement",winner) 
            win = win + 1
            wins = tkinter.Label(root,text="Wins : "+str(win)).grid(row=1,column=5)
            final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
            diagonal1 = ""
            root.destroy()

        if value_1 + value_2 == int(answer2)**2 and win == 0 :
            draw = getentrance1+" and "+getentrance2+" ,you've made a draw. Please try again!"
            boing.play()
            pygame.mixer.music.load("boing.wav")
            pygame.mixer.music.play()
            tkinter.messagebox.showinfo("Draw",draw) 
            draw_game = draw_game + 1
            draws = tkinter.Label(root,text="Draws : "+str(draw_game)).grid(row=2,column=5)
            diagonal1 = ""
            diagonal2 = ""
            root.destroy()

def play() :
    global getentrance1
    global getentrance2
    global final_matrix
    global answer2
    global table_signs
    global isPlayed
    global table_btn
    global lbl1
    answer2 = entrance3.get()
    answer2_conv = int(answer2)
    if answer2_conv <= 2:
       alert = "please enter size between 3-8" 
       tkinter.messagebox.showinfo("Announcement",alert)
       sys.exit("Execution terminated due to invalid board size.")
    if answer2_conv > 8:
       alert = "please enter size between 3-8" 
       tkinter.messagebox.showinfo("Announcement",alert)
       sys.exit("Execution terminated due to invalid board size.")
    table_signs = ['P' for i in range(int(answer2)**2)]
    final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
    getentrance1 = entrance1.get()
    getentrance2 = entrance2.get()
    button = tkinter.StringVar()
    if isPlayed:
        for btn in table_btn:
            btn.destroy()
    table_btn = []
    isPlayed = True
    total = 0
    h2 = lbl1.size()[1]
    for i in range(5,int(answer2)+5):
        for j in range(int(answer2)):
            m = font.measure("m")
            print((root.winfo_screenheight() - 4 * h2) // (int(answer2) * 36))
            btn = tkinter.Button(root,text=" ",font="Times 36 bold",height=1,width = root.winfo_screenwidth() // (int(answer2) * m),bg="black",fg="white")
            table_btn.append(btn)
            btn.grid(row=i,column=j)
            total = total +1
    for i in range(len(table_btn)):
        table_btn[i]["command"]=lambda x=table_btn,y=table_btn[i]:check(x,y)
        
def play1() :
    global getentrance1
    global getentrance2
    global final_matrix
    global answer2
    global table_signs
    global isPlayed
    global table_btn
    global lbl1
    global validClick
    global lst
    answer2 = entrance3.get()
    answer2_conv = int(answer2)
    if answer2_conv <= 2:
       alert = "please enter size greater than 2" 
       tkinter.messagebox.showinfo("Announcement",alert)
       sys.exit("Execution terminated due to invalid board size.")
    if answer2_conv > 8:
       alert = "please enter size between 3-8" 
       tkinter.messagebox.showinfo("Announcement",alert)
       sys.exit("Execution terminated due to invalid board size.")
    table_signs = ['P' for i in range(int(answer2)**2)]
    final_matrix = [['P' for j in range(int(answer2))] for i in range(int(answer2))]
    getentrance1 = entrance1.get()
    getentrance2 = entrance2.get()
    button = tkinter.StringVar()
    if isPlayed:
        for btn in table_btn:
            btn.destroy()
    table_btn = []
    isPlayed = True
    total = 0
    h2 = lbl1.size()[1]
    for i in range(5,int(answer2)+5):
        for j in range(int(answer2)):
            m = font.measure("m")
            print((root.winfo_screenheight() - 4 * h2) // (int(answer2) * 36))
            btn = tkinter.Button(root,text=" ",font="Times 36 bold",height=1,width = root.winfo_screenwidth() // (int(answer2) * m),bg="black",fg="white")
            table_btn.append(btn)
            btn.grid(row=i,column=j)
            total = total +1
    validClick = False
    lst = table_btn.copy()
    for i in range(len(table_btn)):
        table_btn[i]["command"]=lambda x=table_btn,y=table_btn[i]:check1(x,y)

root.mainloop()
pygame.quit()
