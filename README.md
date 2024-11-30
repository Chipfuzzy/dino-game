import pgzrun
from random import randint
from time import time

HEIGHT = 500
WIDTH = 850

dinosaurs = []
lines = []
next_dinosaurs = 0

start_time = 0
total_time = 0
end_time = 0

number_of_dinosaur = 8

def create_dinosaurs():
    global start_time
    for count in range(0, number_of_dinosaur):
        dinosaur = Actor('stegoxbg')
        dinosaur.pos = randint(40, WIDTH-40), randint(40, HEIGHT-40)
        dinosaurs.append(dinosaur)
    start_time = time()
    
def draw():
    global total_time

    screen,blit("background", (0,0))
    number = 1
    for dinosaur in dinosaurs:
        screen.draw.text(str(number), (dinosaur.pos[0], dinosaur.pos[1]+20))
        dinosaur.draw()
        number = number + 1

    for line in lines:
        screen.draw.line(line[0], line[1], (255,255,255))

    if next_dinosaur < number_of_dinosaur:
        total_time = time() - start_time
        screen.draw.text(str(round(total_time,1)), (10,10), fontsize=30)
    else:
        screen.draw.text(str(round(total_time,1)), (10,10), fontsize=30)

def update():

    pass
def on_mouse_down(pos):
    global next_dinosaur, lines

    if next_dinosaur < number_of_dinosaur:
        if dinosaurs[next_dinosaur].collidepoint(pos):
            if next_dinosaur:
                lines.append((dinosaurs[next_dinosaur-1].pos, dinosaurs.pos))
            next_dinosaur = next_dinosaur + 1
        else:
            lines = []
            next_dinosaur = 0

create_dinosaurs()

pgzrun.go()
