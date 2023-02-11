import pygame, sys, random
from pygame.locals import*

pygame.init()
pygame.time.delay(1000)
X = 1200
Y = 800
S = pygame.display.set_mode((X, Y))
pygame.display.set_caption('Hello World')


#            R    G    B
GREY     = (100, 100, 100)
BLUE     = (  0,   0, 255)
NAVYBLUE = ( 60,  60,  60)
WHITE    = (255, 255, 255)
RED      = (255,   0,   0)
GREEN    = (  0, 255,   0)
YELLOW   = (255, 255,   0)
ORANGE   = (255, 128,   0)
PURPLE   = (255,   0, 255)
CYAN     = (  0, 255, 255)
PINK     = (255, 128, 128)
BLACK    = (  0,   0,   0)
BROWN    = (222, 184, 135)
myfont = pygame.font.SysFont('Comic Sans MS', 30)


def turnCtoN(charactor):
    for i in range(len(charactor) - 1, -1, -1):
        a = len(charactor[i]) - 1
        num = 0
        for j in range(len(charactor[i]) - 1, -1, -1):
            c = charactor[i][j]
            if c == '1':
                num += 1 * (10 ** (a - j))
            elif c == '2':
                num += 2 * (10 ** (a - j))
            elif c == '3':
                num += 3 * (10 ** (a - j))
            elif c == '4':
                num += 4 * (10 ** (a - j))
            elif c == '5':
                num += 5 * (10 ** (a - j))
            elif c == '6':
                num += 6 * (10 ** (a - j))
            elif c == '7':
                num += 7 * (10 ** (a - j))
            elif c == '8':
                num += 8 * (10 ** (a - j))
            elif c == '9':
                num += 9 * (10 ** (a - j))
            elif c == '0':
                num += 0 * (10 ** (a - j))
            charactor[i].pop(j)
        charactor.pop(i)
        charactor.append(num)
    print(charactor)
    for i in range(int(len(charactor)/2)):
        a = charactor[i]
        b = charactor[len(charactor) - i - 1]
        charactor[i] = b
        charactor[len(charactor) - i - 1] = a
    return()


t = 0
last_time1 = 0
last_time2 = 0
last_time3 = 0
last_time4 = 0
plant_type = 0
plant = 0
price = 0
blood = 0
sun = []
board = []
zombie_data = []
zombie_working = []
bullet = []
file = open('zombie.txt', 'r')
for line in file:
    data = [[]]
    count = 0
    for i in range(len(line)):
        if line[i] == ' ':
            count += 1
            data.append([])
        elif line[i] != '\n':
            data[count].append(line[i])
    turnCtoN(data)
    zombie_data.append(data)
sun_point = 3000
actor_type = False
for i in range(5):
    board.append([])
    for j in range(9):
        board[i].append([0, 0, 0])
time_init = pygame.time.get_ticks()


def score(x, y, s, color):
    digit = 0
    while True:
        digit += 1
        j = int(s/(10**digit))
        if j == 0:
            break
    for i in range(digit):
        a = 10**(digit-i-1)
        b = int(s/a)
        if b == 1:
            PRINT = '1'
        elif b == 2:
            PRINT = '2'
        elif b == 3:
            PRINT = '3'
        elif b == 4:
            PRINT = '4'
        elif b == 5:
            PRINT = '5'
        elif b == 6:
            PRINT = '6'
        elif b == 7:
            PRINT = '7'
        elif b == 8:
            PRINT = '8'
        elif b == 9:
            PRINT = '9'
        elif b == 0:
            PRINT = '0'
        text = myfont.render(PRINT, False, color)
        S.blit(text, (x, y))
        x += 20
        s -= a * b


def draw_board():
    width = 125
    pygame.draw.rect(S, BLACK, ((0, 0), (X, Y)), 0)
    pygame.draw.rect(S, (255, 80, 50), ((0, 0), (800, width)), 0)
    for i in range(5):
        for j in range(9):
            x = width * j + 50
            y = width * (i + 1)
            if (x + y) % 2 == 1:
                pygame.draw.rect(S, (75, 150, 75), ((x, y), (width, width)), 0)
            else:
                pygame.draw.rect(S, (100, 200, 100), ((x, y), (width, width)), 0)
    for i in range(9):
        x = 100 + i * 70
        y = 5
        pygame.draw.rect(S, (255, 255, 255), ((x, y), (65, 115)), 0)


def sun_production():
    global last_time1, last_time2, sun_point, actor_type, t
    mouse_x, mouse_y = pygame.mouse.get_pos()
    if last_time1 + 5000 <= t:
        last_time1 = t
        x = random.randint(50, X - 50)
        y = 0
        sun.append([x, y, Y])
    if t - last_time2 >= 20:
        last_time2 += 20
        if len(sun) > 0:
            for i in range(len(sun) - 1, -1, -1):
                x, y, end = sun[i]
                if y <= Y - 50 and y < end:
                    y += 1
                    sun[i][1] = y
    if len(sun) > 0:
        for i in range(len(sun) - 1, -1, -1):
            x, y, end = sun[i]
            pygame.draw.circle(S, YELLOW, (x, y), 20, 0)
            if actor_type and -50 < mouse_x - x < 50 and -50 < mouse_y - y < 50:
                sun.pop(i)
                sun_point += 50
    score(10, 80, sun_point, BLUE)


def game():
    global actor_type, time_init, t
    t = pygame.time.get_ticks() - time_init
    draw_board()
    sun_production()
    plants()
    zombie()
    for i in range(len(zombie_data) - 1, -1, -1):
        if t - 20 <= zombie_data[i][0] <= t + 20:
            line = zombie_data[i][1]
            type = zombie_data[i][2]
            x = X
            zombie_working.append([x, line, type])
            zombie_data.pop(i)
    for ev in pygame.event.get():
        if ev.type == MOUSEBUTTONDOWN:
            if ev.button == 1:
                actor_type = True
        elif ev.type == MOUSEBUTTONUP:
            if ev.button == 1:
                actor_type = False
        if ev.type == QUIT:
            pygame.quit()
            sys.exit()


def zombie():
    global t, last_time3
    if len(zombie_working) != 0:
        for i in range(len(zombie_working) - 1, -1, -1):
            if len(zombie_working[i]) < 4:
                if zombie_working[i][2] == 1:
                    speed = random.randint(10, 15)
                    HP = 270
                    armor = 0
                    state = 'walking'
                    zombie_working[i].append(speed)
                    zombie_working[i].append(HP)
                    zombie_working[i].append(armor)
                    zombie_working[i].append(state)
                line = zombie_working[i][1]
                line -= 1
                zombie_working[i][1] = line
            x, line, type, speed, HP, armor, state = zombie_working[i]
            width = 125
            y = width * (line + 1) - 25
            if state == 'walking':
                pygame.draw.rect(S, NAVYBLUE, ((int(x), y), (30, width)), 0)
            elif state == 'eating':
                pygame.draw.rect(S, GREY, ((int(x), y), (30, width)), 0)
            column = int((x - 50) / 125)
            if column < 9:
                TYPE, HP_p, CD = board[line][column]
                if HP_p > 0 and TYPE != 0:
                    state = 'eating'
                    zombie_working[i][6] = state
                else:
                    state = 'walking'
                    zombie_working[i][6] = state
            if HP <= 0:
                zombie_working.pop(i)
        if last_time3 + 40 <= t:
            last_time3 = t
            for i in range(len(zombie_working) - 1, -1, -1):
                x, line, type, speed, HP_z, armor, state = zombie_working[i]
                if state == 'walking':
                    x -= speed/20
                zombie_working[i][0] = x
                column = int((x - 50) / 125)
                if column < 9:
                    TYPE, HP_p, CD = board[line][column]
                    if HP_p > 0 and TYPE != 0:
                        HP_p -= 4
                        board[line][column][1] = HP_p


def plants():
    global actor_type, plant_type, sun_point, plant, price, blood, last_time4
    x, y = pygame.mouse.get_pos()
    line = -1
    column = -1
    width = 125
    if plant_type > 0:
        pygame.draw.rect(S, WHITE, ((x - 30, y - 60), (65, 120)), 0)
        if 50 < x <= 1175 and 125 < y <= 750:
            line = int(y / 125) - 1
            column = int((x - 50) / 125)
    if actor_type:
        if 5 <= y <= 120 and 100 <= x <= 730 and plant_type == 0:
            plant_type = int((x - 100) / 70) + 1
            plant = 0
            price = 0
            blood = 0
            if plant_type == 1:
                plant = 'Peathshooter'
                price = 100
                blood = 300
            elif plant_type == 2:
                plant = 'Sunflower'
                price = 50
                blood = 300
            elif plant_type == 3:
                plant = 'Cherry Bomb'
                price = 150
                blood = 4000
            elif plant_type == 4:
                plant = 'Wall-nut'
                price = 50
                blood = 4000
    else:
        plant_type = 0
        if line != -1 and sun_point >= price:
            if board[line][column] == [0, 0, 0]:
                sun_point -= price
                CD_p = 0
                if plant == 'Peathshooter':
                    CD_p = random.randint(1360, 1500)
                elif plant == 'Sunflower':
                    CD_p = random.randint(22000, 26000)
                elif plant == 'Cherry Bomb':
                    CD_p = 1000
                board[line][column][0] = plant
                board[line][column][1] = blood
                board[line][column][2] = CD_p
    for i in range(5):
        for j in range(9):
            TYPE, HP, CD_p = board[i][j]
            x = width * j + 50
            y = width * (i + 1)
            if HP <= 0:
                board[i][j][0] = 0
                board[i][j][1] = 0
                board[i][j][2] = 0
            if TYPE == 'Peathshooter':
                pygame.draw.circle(S, GREEN, (x + 62, y + 62), 40)
            elif TYPE == 'Sunflower':
                pygame.draw.circle(S, YELLOW, (x + 62, y + 62), 40)
            elif TYPE == 'Cherry Bomb':
                pygame.draw.circle(S, RED, (x + 62, y + 62), 40)
            elif TYPE == 'Wall-nut':
                pygame.draw.circle(S, BROWN, (x + 62, y + 62), 40)
    if last_time4 + 40 <= t:
        last_time4 = t
        for i in range(5):
            for j in range(9):
                TYPE, HP, CD_p = board[i][j]
                x = width * j + 50
                y = width * (i + 1)
                if HP > 0:
                    if CD_p > 0:
                        CD_p -= 40
                    elif CD_p <= 0:
                        if TYPE == 'Sunflower':
                            sun.append([x, y - 20, y + 105])
                            CD_p = random.randint(22000, 26000)
                        elif TYPE == 'Peathshooter':
                            trigger = True
                            for q in range(len(zombie_working) - 1, -1, -1):
                                if len(zombie_working[q]) > 3 and trigger:
                                    x_z, line_z, type, speed, HP_z, armor, state = zombie_working[q]
                                    x_p = width * j + 50
                                    if line_z == i and x_z >= x_p:
                                        bullet.append([x + 10, i, 'Peath'])
                                        trigger = False
                                        CD_p = random.randint(1360, 1400)
                        elif TYPE == 'Cherry Bomb':
                            for q in range(len(zombie_working) - 1, -1, -1):
                                x_z, line_z, type, speed, HP_z, armor, state = zombie_working[q]
                                column = int((x - 50) / 125)
                                if i - 1 <=line_z <= i + 1 and j - 1 <=column <= j + 1:
                                    HP_z -= 1800
                                zombie_working[q][4] = HP_z
                            board[i][j][0] = 0
                            board[i][j][1] = 0
                            board[i][j][2] = 0
                        elif TYPE == 'Wall-nut':
                            CD_p = 0
                board[i][j][2] = CD_p
        if len(bullet) != 0:
            for i in range(len(bullet) - 1, -1, -1):
                x, line, TYPE = bullet[i]
                x += 10
                bullet[i][0] = x
    if len(bullet) != 0:
        for i in range(len(bullet) - 1, -1, -1):
            x_p, line_p, TYPE = bullet[i]
            y = width * (line_p + 1)
            if TYPE == 'Peath':
                pygame.draw.circle(S, GREEN, (x_p + 62, y + 62), 15)
                hit = True
                for j in range(len(zombie_working) - 1, -1, -1):
                    if len(zombie_working[j]) > 3 and hit:
                        x_z, line_z, type, speed, HP_z, armor, state = zombie_working[j]
                        if line_z == line_p and x_p < x_z < x_p + 50:
                            HP_z -= 20
                            zombie_working[j][4] = HP_z
                            bullet.pop(i)
                            hit = False
            if x_p > X + 50:
                bullet.pop(i)


while True:
    game()
    pygame.display.update()
