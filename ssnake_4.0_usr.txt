import turtle
from time import sleep
from random import randint,choice
from gc import collect
delay = 0.04
score = 0
high_score = 0
b=True
wn = turtle.Screen()
wn.title("SSnake 4.0 -usr")
wn.bgcolor("black")
wn.setup(width=600, height=600)
wn.tracer(0)
head = turtle.Turtle()
head.speed(0)
head.shape("circle")
head.color("red")
head.penup()
head.goto(0, 0)
head.direction = "stop"
foods=[]
food1=turtle.Turtle()
food2=turtle.Turtle()
food3=turtle.Turtle()
food4=turtle.Turtle()
food5=turtle.Turtle()
food6=turtle.Turtle()
food7=turtle.Turtle()
foods.append(food1)
foods.append(food2)
foods.append(food3)
foods.append(food4)
foods.append(food5)
foods.append(food6)
foods.append(food7)
for food in foods:
 food.speed(0)
 food.shape("circle")
 food.color("yellow")
 food.penup()
 food.goto(0, 100)
foods[5].color("purple")
foods[6].color("purple")
segments = []
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0, 260)
pen.write("Score: 0          High Score: 0", align="center",font=("Lucida Console", 12, "normal"))
def go_up():
 if head.direction != "down":
  head.direction = "up"
def go_down():
 if head.direction != "up":
  head.direction = "down"
def go_left():
 if head.direction != "right":
  head.direction = "left"
def go_right():
 if head.direction != "left":
  head.direction = "right"
def stop():
 global b
 b=not(b)
def move():
 if head.direction == "up":
  y = head.ycor()
  head.sety(y + 10)
 if head.direction == "down":
  y = head.ycor()
  head.sety(y - 10)
 if head.direction == "left":
  x = head.xcor()
  head.setx(x - 10)
 if head.direction == "right":
  x = head.xcor()
  head.setx(x + 10)
def distance(head,obj,num1,num2):
 x1=head.xcor()
 y1=head.ycor()
 x2=obj.xcor()
 y2=obj.ycor()
 x3=x1-x2
 y3=y1-y2
 if x3>num1 or -x3>num1 or y3>num1 or -y3>num1:
  return False
 elif x3*x3+y3*y3>num2:
  return False
 return True
wn.listen()
wn.onkeypress(go_up, "w")
wn.onkeypress(go_down, "s")
wn.onkeypress(go_left, "a")
wn.onkeypress(go_right, "d")
wn.onkeypress(go_up, "Up")
wn.onkeypress(go_down, "Down")
wn.onkeypress(go_left, "Left")
wn.onkeypress(go_right, "Right")
wn.onkeypress(stop,"space")
while True:
 wn.update()
 if b:
  if head.xcor() > 290 or head.xcor() < -290 or head.ycor() > 290 or head.ycor() < -290:
   sleep(1)
   head.goto(0, 0)
   head.direction = "stop"
   for segment in segments:
     segment.goto(310,310)
   segments.clear()
   delay=0.04
   score = 0
   pen.clear()
   pen.write("Score: {}          High Score: {}".format(score, high_score),align="center", font=("Lucida Console", 12, "normal"))
   b=True
  for food in foods:
   if distance(head,food,20,400):
    x=randint(-270,270)
    y=randint(-270,270)
    food.goto(x,y)
    segment=turtle.Turtle()
    segment.speed(0)
    segment.shape("circle")
    segment.color("blue")
    segment.penup()
    segments.append(segment)
    delay -= 0.0002
    score += 10
    if score > high_score:
        high_score = score
    pen.clear()
    pen.write("Score: {}          High Score: {}".format(score, high_score),align="center", font=("Lucida Console", 12, "normal"))
    if food==foods[5] or food==foods[6]:
     segment = turtle.Turtle()
     segment.speed(0)
     segment.shape("circle")
     segment.color("blue")
     segment.penup()
     segments.append(segment)
     score += 10
     if score > high_score:
      high_score = score
     pen.clear()
     pen.write("Score: {}          High Score: {}".format(score, high_score),align="center", font=("Lucida Console", 12, "normal"))
     x1=randint(-290,-250)
     x2=randint(250,290)
     y1=randint(-290,-250)
     y2=randint(250,290)
     x=choice([x1,x2])
     y=choice([y1,y2])
     food.goto(x,y)
  if len(segments) > 0:
   x = head.xcor()
   y = head.ycor()
   segment=segments[len(segments)-1]
   segment.goto(x,y)
   for index in range(len(segments)-1, 0, -1):
    segments[index]=segments[index-1]
   segments[0]=segment
  move()
  for segment in segments:
   if distance(head,segment,5,25):
    sleep(1)
    head.goto(0, 0)
    head.direction = "stop"
    for segment in segments:
     segment.goto(310,310)
    segments.clear()
    score = 0
    delay = 0.04
    pen.clear()
    pen.write("Score: {}         High Score: {}".format(score, high_score), align="center", font=("Lucida Console", 12, "normal"))
    b=True
  if delay>=0:
   sleep(delay)
 else:
  sleep(0.2)
 collect()
wn.mainloop()
