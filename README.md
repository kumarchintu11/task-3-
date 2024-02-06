# task-3 : Rock-Paper-Scissors Game

from tkinter import *
from PIL import Image,ImageTk
from random import randint


# Main Window
root = Tk()
root.title("Rock-Paper-Scissors")
root.configure(background="#9b59b6")


#store Pictures
rock_img=ImageTk.PhotoImage(Image.open("rock.png "))
paper_img=ImageTk.PhotoImage(Image.open("paper.png "))
scissors_img=ImageTk.PhotoImage(Image.open("scissors.png "))
crock_img=ImageTk.PhotoImage(Image.open("crock.png "))
cpaper_img=ImageTk.PhotoImage(Image.open("cpaper.png "))
cscissors_img=ImageTk.PhotoImage(Image.open("cscissors.png "))


#insert pictures
user_label = Label(root,image=rock_img, bg="#9b59b6")
comp_label = Label(root,image=crock_img, bg="#9b59b6")
comp_label.grid(row=1, column=0)
user_label.grid(row=1, column=4)


#indicators
user_indicators=Label(root, font= 50, text="USER",bg="#9b59b6",fg="white")
comp_indicators=Label(root, font= 50, text="COMPUTER",bg="#9b59b6",fg="white")
user_indicators.grid(row=0, column=3)
comp_indicators.grid(row=0, column=1)


#messages
msg = Label(root, font=50, bg="#9b59b6",fg="white")
msg.grid(row=3, column=2)

#updates messages
def updateMessage(x):
    msg["text"] = x

#update user score
def updateScore():
    score = int(playerScore["text"])
    score+=1
    playerScore["text"]= str(score)

def updateCompScore():
    score = int(computerScore["text"])
    score+=1
    computerScore["text"]= str(score)


#updates choices

choices = ["rock", "paper", "scissors"]
def updateChoice(x):

#for computer
    compChoice = choices[randint(0,2)]
    if compChoice == "rock":
        comp_label.configure(image= crock_img)
    elif compChoice == "paper":
        comp_label.configure(image= cpaper_img)
    else:
        comp_label.configure(image= cscissors_img)



#updates choices
    if x=="rock":
        user_label.configure(image= rock_img)
    elif x=="paper":
        user_label.configure(image= paper_img)
    else:
        user_label.configure(image= scissors_img)
    checkWin(x,compChoice)




#buttons creartion
rock = Button(root,width=20, height=2, text="ROCK", bg="#FF3E4D", fg="white",command=lambda:updateChoice("rock")).grid(row=2, column=1)
paper = Button(root,width=20, height=2, text="PAPER", bg="#FAD02E", fg="white",command=lambda:updateChoice("paper")).grid(row=2, column=2)
scissors = Button(root,width=20, height=2, text="SCISSORS", bg="#0ABDE3", fg="white",command=lambda:updateChoice("scissors")).grid(row=2, column=3)



#scores
playerScore= Label(root,text=0,font=100,bg="#9b59b6",fg="white")
computerScore= Label(root,text=0,font=100,bg="#9b59b6",fg="white")
computerScore.grid(row=1, column=1)
playerScore.grid(row=1, column=3)


#check winner
def checkWin(player,computer):
    if player == computer :
        updateMessage("its a tie")
    elif player == "rock":
        if computer == "paper":
            updateMessage("You Loose")
            updateCompScore()
        else:
            updateMessage("You Win")
            updateCompScore()
    elif player == "paper":
        if computer == "scissors":
            updateMessage("You Loose")
            updateCompScore()
        else:
            updateMessage("You Win")
            updateCompScore()
    elif player == "scissors":
        if computer == "rock":
            updateMessage("You Loose")
            updateCompScore()
        else:
            updateMessage("You Win")
            updateCompScore()
    else:
        pass

root.mainloop()
