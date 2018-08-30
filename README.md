# Kinematics-Calculator
This is a calculator that I created that can solve basic kinematics problems as well as projectile motion questions.
#This program is meant to give people help for grade 11 physics
#It covers the kinematics unit
#The user inputs variables and then inputs "solve" for the variable they want to solve
#The program outputs a detailed step by step solution


#Needed modules
from tkinter import*
import tkinter.messagebox
import math
import sys
import os


#Saving velocity as they change
VelocityInits = []


#Restarts the programs
def restart_program():
    python = sys.executable
    os.execl(python, python, * sys.argv)

#Method for the five kinematic equations
def big5():

    #Outputs the answers
    def Big5():
        try:
            displacement = dEnter.get()
            velocityInitial = v1Enter.get()
            velocityFinal = v2Enter.get()
            acceleration = aEnter.get()
            time = tEnter.get()
            directionPositive = directionEnter.get()

            VelocityInits.append(time)

            if not(displacement == "" or velocityInitial == "" or velocityFinal == "" or acceleration == "" or time == ""):
                tkinter.messagebox.showinfo("Error", "Please leave one box blank!")
                restart_program()

            if(displacement == "" and velocityInitial == "") or (displacement == "" and velocityFinal == "") or (displacement == "" and acceleration == "") or (displacement == "" and time == "") or (velocityInitial == "" and velocityFinal == "") or (velocityFinal == "" and acceleration == "") or (velocityFinal == "" and time == "") or (acceleration == "" and  time == ""):
                tkinter.messagebox.showinfo("Error", "Please fill out 4 boxes")
                restart_program()            

            if(displacement == "solve" and velocityInitial == "solve") or (displacement == "solve" and velocityFinal == "solve") or (displacement == "solve" and acceleration == "solve") or (displacement == "solve" and time == "solve") or (velocityInitial == "solve" and velocityFinal == "solve") or (velocityFinal == "solve" and acceleration == "solve") or (velocityFinal == "solve" and time == "solve") or (acceleration == "solve" and  time == "solve"):
                tkinter.messagebox.showinfo("Error", "You can only solve one problem at once!")
                restart_program() 
                
            dText.destroy()
            dEnter.destroy()
            v1Text.destroy()
            v1Enter.destroy()
            v2Text.destroy()
            v2Enter.destroy()
            tText.destroy()
            tEnter.destroy()
            aText.destroy()
            aEnter.destroy()
            directionText.destroy()
            directionEnter.destroy()
            solve.destroy()
            headerText.destroy()

            #Kinematic equation that does not use the final velocity variable
            def equation1(d, v1, a, t):
                t1 = 0
                t2 = 0   
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = v1 * t + 1/2a * t^2"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = (",v1,"*",t,") + (1/2",a,"*",t,"^2)"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = ", v1*t, "+ (", 1/2*a, "*", t**2))                    
                    return (v1 * t) + (1/2 * a * t ** 2)
                    
                elif solving == "v1":
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 = (d - (0.5 * a * t**2)) / t"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =(",d,"-(0.5 *",a,"*",t,"^2)) /",t,")"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =", d, "- (", 0.5*a,"*", t**2, ") /",t))
                    return (d - (0.5 * a * t**2)) / t
                  
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (2*(d - (v1 * t)) / t^2"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (2*(",d,"-(",v1,"*",t,"))) /",t,"^2"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",2,"* (",d, "-", v1 * t,")) /",t**2))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",2,"* (",d - v1*t,")) /",t**2))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",2 * (d - v1 *t),") /", t**2))
                    return (2*(d - (v1 * t))) / t ** 2
                 
                elif solving == "t":
                    try:
                        t1 = (-v1 + math.sqrt(v1**2 - (2*a*d))) / a
                    except (ValueError):
                        t1 = -99.224
                    try:
                        t2 = (-v1 - math.sqrt(v1**2 - (2*a*d))) / a
                    except (ValueError):
                        t2 = -99.224
                        
                    if t1 == -99.224 and t2 == -99.224:
                        print()
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END, "This is impossible, please recheck variables!")
                        #make them go to a fresh big 5 equation page please
                        return 0
                    elif t1 == -99.224:
                        answers = Text(master,height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (-v1 +",u"\u221a v1**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v1,"+", u"\u221a",v1,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v1,"+",u"\u221a",v1 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v1,"+",u"\u221a",round(v1 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v1 + math.sqrt(v1 ** 2 - 2 * a * d),3),"/",a))
                        return t2
                    elif t2 == -99.224:
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        ansewrs.insert(END,("t1 = (-v1 +",u"\u221a v1**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v1,"+", u"\u221a",v1,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v1,"+",u"\u221a",v1 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v1,"+",u"\u221a",round(v1 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v1 + math.sqrt(v1 ** 2 - 2 * a * d),3),"/",a))
                        return t1
                    elif t1 > t2:
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        ansewrs.insert(END,("t1 = (-v1 +",u"\u221a v1**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v1,"+", u"\u221a",v1,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v1,"+",u"\u221a",v1 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v1,"+",u"\u221a",round(v1 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v1 + math.sqrt(v1 ** 2 - 2 * a * d),3),"/",a))                        
                        return t1
                    elif t2 > t1:
                        answers = Text(master,height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (-v1 +",u"\u221a v1**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v1,"+", u"\u221a",v1,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v1,"+",u"\u221a",v1 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v1,"+",u"\u221a",round(v1 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v1 + math.sqrt(v1 ** 2 - 2 * a * d),3),"/",a))
                        return t2

            #KInematic equation that does not use the initial velocity variable
            def equation2 (d, v2, a, t):
                t1 = 0
                t2 = 0
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = v2 * t + 1/2a * t^2"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = (",v2,"*",t,") + (1/2",a,"*",t,"^2)"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = ", v2*t, "+ (", 1/2*a, "*", t**2))                     
                    return (v2 * t) + (0.5 * a * t ** 2)
                   
                elif solving == "v2":
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 = (d - (0.5 * a * t**2)) / t"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =(",d,"-(0.5 *",a,"*",t,"^2)) /",t,")"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =", d, "- (", 0.5*a,"*", t**2, ") /",t))
                    return (d - (0.5 * a * t**2)) / t
                    
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (2*(d - (v2 * t)) / t^2"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (2*(",d,"-(",v2,"*",t,"))) /",t,"^2"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",2,"* (",d, "-", v2 * t,")) /",t**2))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",2,"* (",d - v2*t,")) /",t**2))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",2 * (d - v2 *t),") /", t**2))                    
                    return (2*(d - (v2 * t))) / t ** 2
                
                elif solving == "t":
                    try:
                        t1 = (-v2 + math.sqrt(v2**2 - (2*a*d))) / a
                    except (ValueError):
                        t1 = -99.224
                    try:
                        t2 = (-v2 - math.sqrt(v2**2 - (2*a*d))) / a
                    except (ValueError):
                        t2 = -99.224

                    if t1 == -99.224 and t2 == -99.224:
                        print()
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END, "This is impossible, please recheck variables!")
                        #make them go to a fresh big 5 equation page please
                    elif t1 == -99.224:
                        answers = Text(master,height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (-v2 +",u"\u221a v2**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v2,"+", u"\u221a",v2,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v2,"+",u"\u221a",v2 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v2,"+",u"\u221a",round(v2 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v2 + math.sqrt(v2 ** 2 - 2 * a * d),3),"/",a))
                        return t2
                    elif t2 == -99.224:
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        ansewrs.insert(END,("t1 = (-v2 +",u"\u221a v2**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v2,"+", u"\u221a",v2,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v2,"+",u"\u221a",v2 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v2,"+",u"\u221a",round(v2 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v2 + math.sqrt(v2 ** 2 - 2 * a * d),3),"/",a))                        
                        return t1
                    elif t1 > t2:
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        ansewrs.insert(END,("t1 = (-v2 +",u"\u221a v2**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v2,"+", u"\u221a",v2,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v2,"+",u"\u221a",v2 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t1 = (",-v2,"+",u"\u221a",round(v2 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v2 + math.sqrt(v2 ** 2 - 2 * a * d),3),"/",a))                         
                        return t1
                    elif t2 > t1:
                        answers = Text(master,height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (-v2 +",u"\u221a v2**2 - (2*a*d)) / a"))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v2,"+", u"\u221a",v2,"** 2 - (2*",a,"*",d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v2,"+",u"\u221a",v2 ** 2,"-","(", 2 * a * d,")) /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = (",-v2,"+",u"\u221a",round(v2 ** 2 - 2 * a * d,3),") /",a))
                        answers = Text(master, height = 1, width = 50)
                        answers.pack()
                        answers.insert(END,("t2 = ",round(-v2 + math.sqrt(v2 ** 2 - 2 * a * d),3),"/",a))
                        return t2

            #Kinematic equation that does not use the displacement variable
            def equation3(v1, v2, a, t):
                if solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 = -v2 + a * t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =",-v2,"+",a,"*",t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =",-v2,"+",a*t))
                    return v2 - a * t
                    
                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 = -v1 + a * t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =",-v1,"+",a,"*",t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =",-v1,"+",a*t))
                    return  v1 + a * t
                    
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (v2 - v1) / t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (",v2, "-", v1,") /", t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = (", v2 - v1,") /", t))
                    return (v2 - v1) / t
                    
                elif solving == "t":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("t = (v2 - v1) / a"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("t = (", v2,"-",v1,") /",a))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("t =(",v2-v1,") /",a))
                    return (v2 - v1) / a
                    

            #Kinematic equation that does not use the acceleration variable
            def equation4(d, v1, v2, t):
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = 0.5 * (v1 + v2) * t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = 0.5 * (v1 + v2) * t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = 0.5 * (",v1 + v2,")*t"))
                    return 0.5 * (v1 + v2) * t
                    
                elif solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 = (2*d - (v2 * t)) / t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 = ( 2*", d, "(",v2,"*",t,")) /", t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 = (", 2*d, "- (", v2 *t,")) /", t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 = ", 2*d - v2 * t ,"/", t))
                    return (2*d - (v2 * t)) / t

                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 = (2*d - (v1 * t)) / t"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 = ( 2*", d, "(",v1,"*",t,")) /", t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 = (", 2*d, "- (", v1 *t,")) /", t))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 = ", 2*d - v1 * t ,"/", t))
                    return (2*d - (v1 * t)) / t
                    
                elif solving == "t":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("t = (2 * d) / (v1 + v2)"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("t = ( 2 *", d,") / (",v1, "+", v2,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("t = (", 2 * d,") / (",v1 + v2,")"))
                    return (2 * d) / (v1 + v2)
                    

            #Kinematic equation that does not use the time variable 
            def equation5 (d, v1, v2, a):    
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = ((v2 ** 2) - (v1 ** 2)) / (2 * a)"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = ((", v2,"** 2) - (",v1,"** 2)) / (2 *", a,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = ((", v2**2,") - (", v1**2,")) / (", 2*a,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("d = ", v2**2 - v1**2,"/ (", 2*a,")"))
                    return ((v2 ** 2) - (v1 ** 2)) / (2 * a)

                elif solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =",u"\u221a","(-v2 ^2) + (2 * a * d)"))
                    answers = Text(master,height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =",u"\u221a","(",-v2,"** 2) + (2 *",a,"/",d,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =",u"\u221a","(",(-v2**2),") + (", (2 * a / d),")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v1 =",u"\u221a","(",(-v2**2) + (2 * a / d),")"))
                    return math.sqrt((-v2**2) + (2 * a / d))
                
                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =",u"\221a","(-v1**2) + (2 * a / d)"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =",u"\211a","(",-v1,"** 2) + (2 *",a,"/",d,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =",u"\221a","(",(-v1**2),") + (", (2 * a / d),")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("v2 =",u"\221a","(",(-v1**2) + (2 * a / d),")"))
                    return math.sqrt((v1**2) + (2 * a * d))
                    
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = ((v2 ** 2) - (v1 ** 2)) / (2 * d)"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = ((", v2,"** 2) - (",v1,"**2)) / (2 *",d,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = ((", v2**2,"- (",v1**2,")) /(", 2*d,")"))
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("a = ", v2**2 - v1**2,"/ (", 2*d,")"))
                    return ((v2**2) - (v1**2))/ (2*d)
                    

            def vectorDirection(direction):
                if directionPositive == "forward" and direction > 0 or directionPositive == "fwd" and direction > 0:
                    return "[FWD]"
                elif directionPositive == "forward" and direction < 0 or directionPositive == "fwd" and direction < 0:
                    return "[BKWD]"
                elif directionPositive == "backward" and direction > 0 or directionPositive == "bkwd" and direction > 0:
                    return "[BKWD]"
                elif directionPositive == "backward" and direction < 0 or directionPositive == "bkwd" and direction < 0:
                    return "[FWD]"
                elif directionPositive == "up" and direction > 0:
                    return "[UP]"
                elif directionPositive == "up" and direction < 0:
                    return "[DOWN]"
                elif directionPositive == "down" and direction > 0:
                    return "[DOWN]"
                elif directionPositive == "down" and direction < 0:
                    return "[UP]"
                elif directionPositive == "north" and direction > 0:
                    return "[NORTH]"
                elif directionPositive == "north" and direction < 0:
                    return "[SOUTH]"
                elif directionPositive == "south" and direction > 0:
                    return "[SOUTH]"
                elif directionPositive == "south" and direction < 0:
                    return "[NORTH]"
                elif directionPositive == "east" and direction > 0:
                    return "[EAST]"
                elif directionPositive == "east" and direction < 0:
                    return "[WEST]"
                elif directionPositive == "west" and direction > 0:
                    return "[WEST]"
                elif directionPositive == "west" and direction < 0:
                    return "[EAST]"
                else:
                    return ""
                
            #Uses the solve string to find which of the potential variables is being solved for. Another variable is set
            #to keep the variable that needs to be solved stored and sets the original variable back to a number so that
            #a float can be take from that variable for calculation
            if displacement == "solve":
                displacement = 0
                solving = "d"    
            elif velocityInitial == "solve":
                velocityInitial = 0
                solving = "v1"    
            elif velocityFinal == "solve":
                velocityFinal = 0
                solving = "v2"    
            elif acceleration == "solve":
                acceleration = 0
                solving = "a"
            elif time == "solve":
                time = 0
                solving = "t"

            #Determines which equation to use based on the the variable that is not assigned a value when all variables are declared
            #the actual answer is then calculated and the appropriate vector is then assigned based on is the answer is positive or
            #negative. If the answer is negative it is then changed to positive because vectored number should be expressed as postiive
            #numbers only. Since time is not a vector it does not get a vector sign but time cannot be negative so it is also set to be positive.
                
                #Solving without the final velocity varaible
            if velocityFinal == "":
                answer = equation1(float(displacement), float(velocityInitial), float(acceleration), float(time))
     
                
                try:
                    vector = vectorDirection(answer)
                except (TypeError):
                    pass

                if answer < 0:
                    answer *= -1

                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("The displacement is", answer, "m", vector))
                    
                elif solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("The initial velocity is", answer, "m/s", vector))
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("The acceleration is", answer, "m/s^2", vector))
                elif solving == "t" and answer != 0:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The time taken is", answer, "s"))
                    
                #Solving without the initial velocity variable        
            elif velocityInitial == "":
                answer = equation2(float(displacement), float(velocityFinal), float(acceleration), float(time))
                vector = vectorDirection(answer)
                float(answer)
                if answer < 0:
                    answer *= -1
                    
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The dispalcement is", answer, "m", vector))
                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The final velocity is", answer,"m/s", vector, v2))
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The acceleration is", answer, "m/s^2", vector))
                elif solving == "t":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The time taken is", answer, "s"))
                    
                #Solving without the displacement variable
            elif displacement == "":
                answer = equation3(float(velocityInitial), float(velocityFinal), float(acceleration), float(time))
                vector = vectorDirection(answer)
                float(answer)
                if answer < 0:
                    answer *= -1
                    
                if solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The initial velocity is", answer, "m/s", vector))
                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The final velocity is", answer, "m/s", vector)   )             
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The acceleration is", answer, "m/s^2", vector))
                elif solving == "t":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The time taken is", answer, "s") )

                #Solving without the acceleration variable
            elif acceleration == "":
                answer = equation4(float(displacement), float(velocityInitial), float(velocityFinal), float(time))
                vector = vectorDirection(answer)
                float(answer)
                if answer < 0:
                    answer *= -1
                    
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The displacement is", answer, "m", vector) )
                elif solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The initial velocity is", answer,"m/s", vector) )
                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The final velocity", answer, "m/s", vector) )
                elif solving == "t":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The time taken is", answer, "s"))

                #Solving wihtout the time variable
            elif time == "":
                answer = equation5(float(displacement), float(velocityInitial), float(velocityFinal), float(acceleration))
                vector = vectorDirection(answer)
                float(answer)
                if answer < 0:
                    answer *= -1
                    
                if solving == "d":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The displacement is", answer, "m", vector))
                elif solving == "v1":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The initial velocity is", answer, "m/s", vector))
                elif solving == "v2":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The final velocity is", answer, "m/s", vector))
                elif solving == "a":
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END,("The acceleration is", answer, "m/s^2", vector))
                    
            reseter = Button(master, text = "Reset", command = restart_program)
            reseter.pack()
            
        except:
            tkinter.messagebox.showinfo("Error", "Error")
            restart_program()
            
    #Destroyed unneeded seeds
    equations.destroy()
    projectile.destroy()

    #Displays words and inputs

    headerText = Text(master, height = 1, width = 50)
    headerText.pack()
    headerText.insert(END, "Leave one variable blank, and write 'solve' for the variable you want to solve")
    
    dText = Text(master, height = 1, width = 50)
    dText.pack()
    dText.insert(END, "Enter the distance")

    dEnter = Entry(master)
    dEnter.pack()

    v1Text = Text(master, height = 1, width = 50)
    v1Text.pack()
    v1Text.insert(END, "Enter the initial velocity")

    v1Enter = Entry(master)
    v1Enter.pack()

    v2Text = Text(master, height = 1, width = 50)
    v2Text.pack()
    v2Text.insert(END, "Enter the final velocity")

    v2Enter = Entry(master)
    v2Enter.pack()

    tText = Text(master, height = 1, width = 50)
    tText.pack()
    tText.insert(END, "Enter the time")

    tEnter = Entry(master)
    tEnter.pack()

    aText = Text(master, height = 1, width = 50)
    aText.pack()
    aText.insert(END, "Enter the acceleration")

    aEnter = Entry(master)
    aEnter.pack()

    directionText = Text(master, height = 1, width = 50)
    directionText.pack()
    directionText.insert(END, "Which direciton is positive?")

    directionEnter = Entry(master)
    directionEnter.pack()

    solve = Button(master, text = "Solve the Equation!", command = Big5)
    solve.config(height = 10, width = 50)
    solve.pack()


#Method for projectile motion
def projectileMotion():

    #Outputs projectile motions answers
    def projectiles():
        try:

            #Gets all variables
            d = dEnter.get()
            v = vEnter.get()
            t = tEnter.get()
            a = aEnter.get()
            h = hEnter.get()

            timeAsk = 0
            velocityAsk = 0
            angleAsk = 0
            distanceAsk = 0
            heightAsk = 0

            #Initiliazes the solve
            if d == "solve":
                distanceAsk = 1
            elif v == "solve":
                velocityAsk = 1
            elif t == "solve":
                timeAsk = 1
            elif a == "solve":
                angleAsk = 1
            elif h == "solve":
                heightAsk = 1
            else:
                tkinter.messagebox.showinfo("Error", "You must input something to solve")
                restart_program()

            #Finds blank
            if d == "":
                distanceAsk = 2
            elif v == "":
                velocityAsk = 2
            elif t == "":
                timeAsk = 2
            elif a == "":
                angleAsk = 2
            elif h == "":
                heightAsk = 2
            else:
                tkinter.messagebox.showinfo("Error", "Please leave one box blank!")
                restart_program()

            #If there is a user input problem the program resets
            if(d == "" and v == "") or (d == "" and t == "") or (d == "" and a == "") or (d == "" and h == "") or (v == "" and t == "") or (v == "" and a == "") or (v == "" and h == "") or (t== "" and  a == "") or (t== "" and  h == "") or (a== "" and  h== "") :
                tkinter.messagebox.showinfo("Error", "Please fill out 4 boxes")
                restart_program()            

            if(d == "solve" and v == "solve") or (d == "solve" and t == "solve") or (d == "solve" and a == "solve") or (d == "solve" and h == "solve") or (v == "solve" and t == "solve") or (v == "solve" and a == "solve") or (v == "solve" and h == "solve") or (t == "solve" and  a == "solve") or (t == "solve" and  h == "solve") or (a == "solve" and  h == "solve") :
                tkinter.messagebox.showinfo("Error", "You can only solve one problem at once!")
                restart_program()

            #Turns all variables from str to float
            if timeAsk == 0:
                time = float(t)
            if velocityAsk == 0:
                velocity = float(v)
            if angleAsk == 0:
                angle = float(a)
            if distanceAsk == 0:
                distance = float(d)
            if heightAsk == 0:
                height = float(h)

            #Destroys unneeded
            dText.destroy()
            dEnter.destroy()
            vText.destroy()
            vEnter.destroy()
            tText.destroy()
            tEnter.destroy()
            aText.destroy()
            aEnter.destroy()
            hText.destroy()
            hEnter.destroy()
            headerText.destroy()
            solve.destroy()


            #First three words are inputs, the last wor dis the thing the function is solving
            def VelocityDistanceHeightSolveAngle(velocity, distance, height):
                velocity = int(input())
                distance = int(input())
                height = int(input())

                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is beyond the scope of my knowledge so we are guessing and checking it"))

                angle = 1
                time = 0
                distanc = -height

                while True:
                    timeprevious = time
                    velocityY = math.sin(math.radians(angle))*velocity
                    velocityX = math.cos(math.radians(angle))*velocity
                    time = distance/velocityX
                    timecheck =  ((-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc)))))/(2*(-9.8))
                    angle = angle+0.01
                    if time>timecheck:
                        time = (time+timecheck)/2
                        break
                if angle>90 or angle == 1:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("Unsolvable"))
                else:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("The angle is", angle))

            def VelocityDistanceHeightSolveTime(velocity, distance, height):

                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is beyond the scope of my knowledge so we are guessing and checking it"))

                angle = 1
                time = 0
                distanc = -height

                while True:
                    timeprevious = time
                    velocityY = math.sin(math.radians(angle))*velocity
                    velocityX = math.cos(math.radians(angle))*velocity
                    time = distance/velocityX
                    timecheck =  ((-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc)))))/(2*(-9.8))
                    angle = angle+0.01
                    if time>timecheck:
                        time = (time+timecheck)/2
                        break

                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The time is", time)) 

            def TimeDistanceHeightSolveAngle(time, distance, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find velocity on X axis using distance over time"))
                velocityX = distance/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find y axis velocity using the big 5 equations"))
                distanc = -height
                velocityY = (distanc-(1/2)*-9.8*(time**2))/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Finally, we use a tan funciton to find the angle"))
                angle = math.degrees(math.atan(velocityY/velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The angle is", angle))

            def TimeDistanceHeightSolveVelocity(time, distance, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find velocity on X axis using distance over time"))
                velocityX = distance/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find y axis velocity using the big 5 equations"))
                distanc = -height
                velocityY = (distanc-(1/2)*-9.8*(time**2))/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Finally, we use the pythagerrom theorm to find the total velocity"))
                velocity = math.sqrt(velocityX**2 + velocityY**2)
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The velocity is", velocity))

            def TimeAngleHeightSolveVelocity(time, angle, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find velocity on Y axis",))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We have time, height, and gravity so far, so we use distance - 1/2*a*time^2/time"))
                distanc = -height
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now that we have velocity on the vertical and angle, we find total velocity"))
                velocityY = (-height-0.5*9.8*(time**2))/time
                velocity = velocityY*(1/(math.sin(math.radians(angle))))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The velocity is", velocity))

            def TimeAngleHeightSolveDistance(time, angle, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find velocity on Y axis"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We have time, height, and gravity so far, so we use distance - 1/2*a*time^2/time"))
                distanc = -height
                velocityY = (distanc-(1/2)*-9.8*(time**2))/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now that we have velocity on the vertical and angle, we find total velocity"))
                velocity = velocityY*(1/(math.sin(math.radians(angle))))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The velocity is", velocity))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we use the pythagerom theorm to find velocity on x axis"))
                velocityX = math.sqrt((velocity**2)-(velocityY**2))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Velocity X is", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Time * VelocityX equals distance"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The distance is", velocityX*time))
                

            def TimeAngleDistanceSolveVelocity(time, angle, distance):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First, we find velocity on the x axis by dividing distance with time"))
                velocityX = distance/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we use secant of the angle to find the velocity"))
                velocity = velocityX * (1/(math.cos(math.radians(angle))))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The velocity is", velocity))

            def TimeAngleDistanceSolveHeight(time, angle, distance):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First, we find velocity on the x axis by dividing distance with time"))
                velocityX = distance/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we use secant of the angle to find the velocity"))
                velocity = velocityX * (1/(math.cos(math.radians(angle))))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The velocity is", velocity))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find the up velocity using the pythagerom thoerom"))
                velocityY = math.sqrt((velocity**2)-(velocityX**2))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Velocity on the y axis is", velocityY))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we use the big 5 equation to find the height, which is height = velocity*time+1/2acceleration*time^2"))
                height = (velocityY*time)+(-9.8)*0.5*(time**2)
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Remember to reverse the sign of height"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The height is", -height))


            def TimeVelocityAngleSolveDistance(time, velocity, angle):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find the horizontal velocity!"))
                velocityX = math.cos(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Cosine", angle, "then multiply with", velocity, "to get", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Since d = v*t, we multiply the velocity on the X axis with time to find distance"))
                distance = velocityX*time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, (time, "x", velocityX, "=", distance))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The distance is", distance, "!"))

            def TimeVelocityAngleSolveHeight(time, velocity, angle):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find vertical velocity!"))
                velocityY = math.sin(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("sin", angle, "then multiply with", velocity, "to get", velocityY))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Thankfully owen derived the equations for us."))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Substitute the variables into v*t + (1/2)*a*t^2"))
                height = (velocityY*time)+(-9.8)*0.5*(time**2)
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The displacement is", height, "However, we are looing for height! It is the opposite"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The height is", -height))

            def TimeVelocityDistanceSolveAngle(time, velocity, distance):
                velocityX = distance/time
                angle = math.degrees(math.acos(velocityX/velocity))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Finding the velocity on the horizontal axis is of upmost importance"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, (distance, "divided by", time, "equals", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Then we can find the angle using trigonomerty"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Divide horizontal velocity by velocity, then use inverse cos to find the angle!"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The angle is", angle))


            def TimeVelocityDistanceSolveHeight(time, velocity, distance):
                velocityX = distance/time
                angle = math.degrees(math.acos(velocityX/velocity))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Finding the velocity on the horizontal axis is of upmost importance"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, (distance, "divided by", time, "equals", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Then we can find the angle using trigonomerty"))        
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Divide horizontal velocity by velocity, then use inverse cos to find the angle!"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The angle is", angle))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find the velocity on the y axis"))
                velocityY = math.sin(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("sin", angle, "then multiply with", velocity, "to get", velocityY))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Thankfully owen derived the equations for us."))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Substitute the variables into v*t + (1/2)*a*t^2"))
                height = (velocityY*time)+(-9.8)*0.5*(time**2)
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The displacement is", height, "However, we are looing for height! It is the opposite"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The height is", -height))


            def TimeVelocityHeightSolveDistance(time, velocity, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We first find the velocity on vertical"))                            
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Thank owen for deriving the equation for us"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We currently have *gasp* time, height, and gravity"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Remember, we must make height negative because we are finding the end displacement"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("(v = d-1/2a*t^2)/t"))
                distanc = -height
                velocityY = (distanc-(1/2)*-9.8*(time**2))/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Vertical velocity is", velocityY))
                angle = math.degrees(math.asin(velocityY/velocity))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("sin(verticalvelocity/velocity) gives us", angle))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("To find distance, we find the vertical velocity"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("cos(angle)*velocity equals", velocityX))
                velocityX = math.cos(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("velocity*time gives us distance"))
                distance = velocityX*time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The distance is", distance))


            def TimeVelocityHeightSolveAngle(time, velocity, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We first find the velocity on vertical"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Thank owen for deriving the equation for us"))
                answers.pack()
                answers.insert(END, ("We currently have time, height, and gravity"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Remeber, we must make height negative because we are finding the end displacement"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("(v = d-1/2a*t^2)/t"))
                distanc = -height
                velocityY = (distanc-(1/2)*-9.8*(time**2))/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Vertical velocity is", velocityY))
                angle = math.degrees(math.asin(velocityY/velocity))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("sin(verticalvelocity/velocity) gives us", angle))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The angle is", angle))

            def VelocityDistanceAngleSolveTime(velocity, distance, angle):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We first find the velocity of the x component"))     
                velocityX = math.cos(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("cosine velocity to get", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we divide distance by velocity on the X axis to get time"))
                time = velocity/velocityX
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, (velocity, "divided by", velocityX, "is", time))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The time is", time))

            def VelocityDistanceAngleSolveHeight(velocity, distance, angle):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We first find the velocity of the x component"))
                velocityX = math.cos(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("cosine velocity to get", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we divide distance by velocity on the X axis to get time"))
                time = velocity/velocityX
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, (velocity, "divided by", velocityX, "is", time))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find velocity on the Y axis"))
                velocityY = math.sin(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Thankfull owen derived the equations, so we solve using the big 5"))
                height = velocityY*time+0.5*(-9.8)*(time**2)
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We make the distance negative, so the height is", height))            

            def VelocityDistanceHeightSolveAngle(velocity, distance, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is beyond the scope of my knowledge so we are guessing and checking it"))  

                angle = 1
                time = 0
                distanc = -height

                while True:
                    timeprevious = time
                    velocityY = math.sin(math.radians(angle))*velocity
                    velocityX = math.cos(math.radians(angle))*velocity
                    time = distance/velocityX
                    timecheck =  ((-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc)))))/(2*(-9.8))
                    angle = angle+0.01
                    if time>timecheck:
                        time = (time+timecheck)/2
                        break
                if angle>90 or angle == 1:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("Unsolvable"))  
                else:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("angle is", angle)) 

            def VelocityDistanceHeightSolveAngle(velocity, distance, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is beyond the scope of my knowledge so we are guessing and checking it")) 

                angle = 1
                time = 0
                distanc = -height

                while True:
                    timeprevious = time
                    velocityY = math.sin(math.radians(angle))*velocity
                    velocityX = math.cos(math.radians(angle))*velocity
                    time = distance/velocityX
                    timecheck =  ((-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc)))))/(2*(-9.8))
                    angle = angle+0.01
                    if time>timecheck:
                        time = (time+timecheck)/2
                        break
                if angle>90 or angle == 1:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("Unsolvable")) 
                else:
                    answers = Text(master, height = 1, width = 50)
                    answers.pack()
                    answers.insert(END, ("angle is", angle))     

            def VelocityDistanceHeightSolveTime(velocity, distance, height):
                velocity = int(input())
                distance = int(input())
                height = int(input())
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is beyond the scope of my knowledge so we are guessing and checking it"))   

                angle = 1
                time = 0
                distanc = -height

                while True:
                    timeprevious = time
                    velocityY = math.sin(math.radians(angle))*velocity
                    velocityX = math.cos(math.radians(angle))*velocity
                    time = distance/velocityX
                    timecheck =  ((-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc)))))/(2*(-9.8))
                    angle = angle+0.01
                    if time>timecheck:
                        time = (time+timecheck)/2
                        break
                    
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The time is", time))   

            def TimeDistanceHeightSolveAngle(time, distance, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("First we find velocity on X axis using distance over time"))
                velocityX = distance/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find y axis velocity using the big 5 equatiubtistute into a big 5"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We use v*t + 1/2a*t^2"))
                velocityY = (distance-0.5*(-9.8)*(time**2))/time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The angle is", math.degrees(math.atan(velocityY/velocityX))))

            def VelocityAngleHeightSolveTime(velocity, angle, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Remember to flip height since the projectile is going down"))
                distanc = -height
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("We first find the Y component velocity"))
                velocityY = math.sin(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("sin velocity to get", velocityY))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we substitute the variables into the equation"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("time = (-v+/-squareroot(v^2-2a(-d)))/21"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Since there are two values for time, we use the larger one"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is because the smaller velocity assumes the projectile is traveling up"))
                time = (-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc))))/(2*(-9.8))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The time is", time))

            def VelocityAngleHeightSolveDistance(velocity, angle, height):
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Remember to flip height since the projectile is going down"))
                distanc = -height
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                velocityY = math.sin(math.radians(angle))*velocity
                answers.insert(END, ("We first find the Y component velocity"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("sin velocity to get", velocityY))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we substitute the variables into the equation"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("time = (-v+/-squareroot(v^2-2a(-d)))/21"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Since there are two values for time, we use the larger one"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is because the smaller velocity assumes the projectile is traveling up"))
                time = (-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc))))/(2*(-9.8))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("This is because the smaller velocity assumes the projectile is traveling up"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The time is", time))
                velocityX = math.cos(math.radians(angle))*velocity            
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we find velocity on the horizontal axis"))
                velocityX = math.cos(math.radians(angle))*velocity
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("cos the velocity to get", velocityX))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Now we multiply velocity on the horizonal with time to get distance"))
                distance = velocityX*time
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The total distance is", distance))

            #Scary stuff
            def AngleDistanceHeightSolveTime(angle, distance, height):
                velocity = 0.001
                distanc = -height
                #Guess and check time
                while True:
                    #We can technically combine all of this into one line but it would be too tedious
                    velocityY = math.sin(math.radians(angle))*velocity
                    time = (-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc))))/(2*(-9.8))
                    velocityX = math.cos(math.radians(angle))*velocity
                    distanceTry = velocityX*time
                    if distanceTry<distance:
                        velocity = velocity*2
                    elif distanceTry>distance:
                        break


                change = velocity/2
                foward = False
                #Tries to be as accurate as possible
                while True:
                    if foward == True:
                        velocity += change
                    else:
                        velocity -= change
                        
                    velocityY = math.sin(math.radians(angle))*velocity
                    time = (-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc))))/(2*(-9.8))
                    velocityX = math.cos(math.radians(angle))*velocity
                    distanceTry = velocityX*time
                    if distanceTry>distance:
                        foward = False
                    elif distanceTry<distance:
                        foward = True
                    else:
                        break

                    if change<0.001:
                        break
                    
                    change = change/2

                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Unfortunately, solving this is beyond the scope of grade 11. This program guessed and checked"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The time is", time))

            def AngleDistanceHeightSolveVelocity(angle, distance, height):  
                velocity = 0.001
                distanc = -height
            #Guess and check time
                while True:
                    #We can technically combine all of this into one line but it would be too tedious
                    velocityY = math.sin(math.radians(angle))*velocity
                    time = (-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc))))/(2*(-9.8))
                    velocityX = math.cos(math.radians(angle))*velocity
                    distanceTry = velocityX*time
                    if distanceTry<distance:
                        velocity = velocity*2
                    elif distanceTry>distance:
                        break


                change = velocity/2
                foward = False
            #Makes it accurate
                while True:
                    if foward == True:
                        velocity += change
                    else:
                        velocity -= change
                        
                    velocityY = math.sin(math.radians(angle))*velocity
                    time = (-velocityY-math.sqrt((velocityY**2)-(2*(-9.8)*(-distanc))))/(2*(-9.8))
                    velocityX = math.cos(math.radians(angle))*velocity
                    distanceTry = velocityX*time
                    if distanceTry>distance:
                        foward = False
                    elif distanceTry<distance:
                        foward = True
                    else:
                        break

                    if change<0.001:
                        break
                    
                    change = change/2
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("Unfortunately, solving this is beyond the scope of grade 11. This program guessed and checked"))
                answers = Text(master, height = 1, width = 50)
                answers.pack()
                answers.insert(END, ("The velocity is", velocity))

            #Big block of code to check which function to call for
            if timeAsk == 0 and velocityAsk == 0 and angleAsk == 0 and distanceAsk == 1:
                TimeVelocityAngleSolveDistance(time, velocity, angle)

            if timeAsk == 0 and velocityAsk == 0 and angleAsk == 0 and heightAsk == 1:
                TimeVelocityAngleSolveHeight(time, velocity, angle)

            if timeAsk == 0 and velocityAsk == 0 and distanceAsk == 0 and angleAsk == 1:
                TimeVelocityDistanceSolveAngle(time, velocity, distance)

            if timeAsk == 0 and velocityAsk == 0 and distanceAsk == 0 and heightAsk == 1:
                TimeVelocityDistanceSolveHeight(time, velocity, distance)

            if timeAsk == 0 and velocityAsk == 0 and heightAsk == 0 and distanceAsk == 1:
                TimeVelocityHeightSolveDistance(time, velocity, height)

            if timeAsk == 0 and velocityAsk == 0 and heightAsk == 0 and angleAsk == 1:
                TimeVelocityHeightSolveAngle(time, velocity, height)

            if velocityAsk == 0 and distanceAsk == 0 and angleAsk == 0 and timeAsk == 1:
                VelocityDistanceAngleSolveTime(velocity, distance, angle)

            if velocityAsk == 0 and distanceAsk == 0 and angleAsk == 0 and heightAsk == 1:
                VelocityDistanceAngleSolveHeight(velocity, distance, angle)

            if velocityAsk == 0 and angleAsk == 0 and heightAsk == 0 and timeAsk == 1:
                VelocityAngleHeightSolveTime(velocity, angle, height)

            if velocityAsk == 0 and angleAsk == 0 and heightAsk == 0 and distanceAsk == 1:
                VelocityAngleHeightSolveDistance(velocity, angle, height)

            if angleAsk == 0 and distanceAsk == 0 and heightAsk == 0 and timeAsk == 1:
                AngleDistanceHeightSolveTime(angle, distance, height)

            if angleAsk == 0 and distanceAsk == 0 and heightAsk == 0 and velocityAsk == 1:
                AngleDistanceHeightSolveVelocity(angle, distance, height)

            if velocityAsk == 0 and distanceAsk == 0 and heightAsk == 0 and angleAsk == 1:
                VelocityDistanceHeightSolveAngle(velocity, distance, height)

            if velocityAsk == 0 and distanceAsk == 0 and heightAsk == 0 and timeAsk == 1:
                VelocityDistanceHeightSolveTime(velocity, distance, height)

            if timeAsk == 0 and distanceAsk == 0 and heightAsk == 0 and velocityAsk == 1:
                TimeDistanceHeightSolveVelocity(time, distance, height)

            if timeAsk == 0 and distanceAsk == 0 and heightAsk == 0 and angleAsk == 1:
                TimeDistanceHeightSolveAngle(time, distance, height)

            if timeAsk == 0 and angleAsk == 0 and heightAsk == 0 and velocityAsk == 1:
                TimeAngleHeightSolveVelocity(time, angle, height)

            if timeAsk == 0 and angleAsk == 0 and heightAsk == 0 and distanceAsk == 1:
                TimeAngleHeightSolveDistance(time, angle, height)

            if timeAsk == 0 and angleAsk == 0 and distanceAsk == 0 and velocityAsk == 1:
                TimeAngleDistanceSolveVelocity(time, angle, distance)

            if timeAsk == 0 and angleAsk == 0 and distanceAsk == 0 and heightAsk == 1:
                TimeAngleDistanceSolveHeight(time, angle, distance)

        #Try and except for error
        except:
            tkinter.messagebox.showinfo("Error", "Error")
            restart_program()
                
        reseter = Button(master, text = "Reset", command = restart_program)
        reseter.pack()


    #Clears the screen and remakes the things              
    equations.destroy()
    projectile.destroy()

    headerText = Text(master, height = 1, width = 50)
    headerText.pack()
    headerText.insert(END, "Leave one blank, and leave one with solve inside!")
        
    dText = Text(master, height = 1, width = 50)
    dText.pack()
    dText.insert(END, "Enter the distance")

    dEnter = Entry(master)
    dEnter.pack()

    vText = Text(master, height = 1, width = 50)
    vText.pack()
    vText.insert(END, "Enter the velocity")

    vEnter = Entry(master)
    vEnter.pack()

    tText = Text(master, height = 1, width = 50)
    tText.pack()
    tText.insert(END, "Enter the time")

    tEnter = Entry(master)
    tEnter.pack()

    aText = Text(master, height = 1, width = 50)
    aText.pack()
    aText.insert(END, "Enter the angle")

    aEnter = Entry(master)
    aEnter.pack()

    hText = Text(master, height = 1, width = 50)
    hText.pack()
    hText.insert(END, "Enter the height")

    hEnter = Entry(master)
    hEnter.pack()
        
    solve = Button(master, text = "Teach Me!!!", command = projectiles)
    solve.config(height = 10, width = 50)
    solve.pack()
    
    


    
#Initialize the window
master = Tk()

#Button for big 5 equations
equations = Button(master, text = "Kinematic Equations", command = big5)
equations.pack()
equations.config(height = 15, width = 50)

#Button for projectile motion
projectile = Button(master, text = "Projectile Motion", command = projectileMotion)
projectile.pack()
projectile.config(height = 15, width = 50)

#Initializes the loop
mainloop()


