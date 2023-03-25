import pygame, sys, random
from pygame.locals import *

pygame.init()
X = 1200
Y = 700
S = pygame.display.set_mode((X, Y))
pygame.display.set_caption('水果忍者')
FPS = 20
fpsClock = pygame.time.Clock()

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

state = 'SPLASH'
splash_text_tm = 0
splash_text_show = False
myfont = pygame.font.SysFont('Comic Sans MS', 30)
last_time1 = 0
last_time2 = 0
last_time3 = 0
last_time4 = 0
last_time5 = 0
last_time6 = 0
last_time7 = 0
last_time8 = 0
timing = False
obj = []
act = []
act_copy = []
split = []
lines = []
droplets = []
actor_type = False
score = 0
score1 = 0
v_move = 1
v_production = 500
key = True
rain = False
juice = []
bomb = []
laser = []
core = []
actor_life = 0
HP_boss = 200
boss_move = 0
boss_word = 0
boss_x = 0
boss_y = 0
move_x = 0
move_y = 0
invincible_time = 0
stage = 1
skill = 0
event_move = True


def waiting(time):
    while True:
        t = pygame.time.get_ticks()
        if t > time:
            break
        actor()


def draw_board():
    S.fill(BLACK)


def velocity():
    global score, v_production, last_time5
    t = pygame.time.get_ticks()
    if score <= 0:
        v_production = 500 - score * 2
        last_time5 = t
    else:
        boss()


def time():
    global last_time4, timing, key, last_time1, last_time2, last_time3, actor_life
    t = pygame.time.get_ticks()
    mouse_x, mouse_y = pygame.mouse.get_pos()
    if timing:
        x1 = int(X / 3)
        y1 = int(Y / 2)
        x2 = int(X * 3 / 4)
        y2 = int(Y * 4 / 7)
        x3 = int(X * 2 / 3)
        y3 = int(Y * 5 / 7)
        pygame.draw.circle(S, YELLOW, (x1, y1), 40, 0)
        pygame.draw.circle(S, PINK, (x2, y2), 40, 0)
        pygame.draw.circle(S, BLUE, (x3, y3), 40, 0)
        if actor_type:
            if x1 - 20 < mouse_x < x1 + 20 and y1 - 20 < mouse_y < y1 + 20:
                last_time4 = 60000 + t
                key = True
                waiting(500 + t)
                actor_life = 3
            elif x2 - 20 < mouse_x < x2 + 20 and y2 - 20 < mouse_y < y2 + 20:
                last_time4 = 120000 + t
                key = True
                waiting(500 + t)
                actor_life = 3
            elif x3 - 20 < mouse_x < x3 + 20 and y3 - 20 < mouse_y < y3 + 20:
                last_time4 = 300000 + t
                key = True
                waiting(500 + t)
                actor_life = 3
            if key:
                last_time1 = 2000 + t
                last_time2 = 2000 + t
                last_time3 = 2000 + t


def actor():
    global actor_type
    x, y = pygame.mouse.get_pos()
    for ev in pygame.event.get():
        if ev.type == QUIT:
            pygame.quit()
            sys.exit()
        if ev.type == MOUSEBUTTONDOWN:
            if ev.button == 1:
                actor_type = True
        elif ev.type == MOUSEBUTTONUP:
            if ev.button == 1:
                actor_type = False
                if len(act) != 0:
                    for i in range(len(act) - 1, -1, -1):
                        act.pop()
    if actor_type:
        act.insert(0, [x, y])
        mouse_x, mouse_y = pygame.mouse.get_pos()
        if actor_type:
            pygame.draw.circle(S, WHITE, (mouse_x, mouse_y), 4)
        if len(act) != 0:
            for i in range(1, len(act)):
                x, y = act[i - 1]
                x1, y1 = act[i]
                if i <= int(len(act)/2):
                    width = int(3 + i/8)
                if i >= int(len(act)/2):
                    width = int(11 - i/8)
                pygame.draw.line(S, BLUE, (x, y), (x1, y1), width + 4)
                pygame.draw.line(S, WHITE, (x, y), (x1, y1), width)
            if len(act) >= 80:
                act.pop()


def object():
    global last_time1, last_time2, last_time3, last_time4, actor_type, score, v_move, X, Y, v_production, timing, state, actor_life
    mouse_x, mouse_y = pygame.mouse.get_pos()
    t = pygame.time.get_ticks()
    if timing:
        if t >= last_time4:
            state = 'END'
    if t - last_time1 >= v_production:
        last_time1 += v_production
        type = random.randint(0, 100)
        object_type = 0
        life = 1
        if 0 <= type <= 35:
            object_type = 'apple'
        elif 36 <= type <= 38:
            object_type = 'bread'
        elif 39 <= type <= 48:
            object_type = 'bomb'
        elif 49 <= type <= 79:
            object_type = 'peach'
        elif 80 <= type <= 85:
            object_type = 'orange'
            life = 10
            last_time1 += 1500
        elif 86 <= type <= 100:
            object_type = 'watermalon'
            life = 2
        object_x = random.randint(-350, 350)
        object_diraction = random.choice(['left', 'right'])
        k = random.randint(Y - 250, Y - 150)
        h = random.randint(X / -2 + 50, X / 2 - 50)
        if 0 <= object_x - h <= 100:
            object_x += 100
        elif -100 <= object_x - h <= 0:
            object_x -= 100
        a = k / (object_x - h) / (object_x - h)
        waiting = 0
        obj.append([object_type, object_x, Y + 100, a, h, k, object_diraction, life, waiting])
    if t - last_time2 >= 10:
        last_time2 += 10
        if len(obj) != 0:
            for i in range(len(obj)-1, -1, -1):
                type, x, y, a, h, k, diraction, life, waiting = obj[i]
                beginning_y = Y + 100
                move_x = 1
                if diraction == 'left':
                    x -= move_x
                    y = a * (x - h) * (x - h) - k + beginning_y#f(x)
                else:
                    x += move_x
                    y = a * (x - h) * (x - h) - k + beginning_y#f(x)
                if waiting >= 0:
                    waiting -= 1
                obj[i][1] = x
                obj[i][2] = y
                obj[i][8] = waiting
        if len(juice) != 0:
            for i in range(len(juice)):
                x, y, v, color = juice[i]
                y += v + random.randint(-1, 1)
                juice[i][1] = y
        if len(bomb) != 0:
            for i in range(len(bomb)):
                x, y, waiting = bomb[i]
                bomb[i][2] = waiting - 1
    if t - last_time3 >= 20:
        last_time3 += 20
        if len(split) != 0:
            for i in range(len(split)):
                object = split[i]
                for j in range(1, -1, -1):
                    type, x, y, a, h, k, diraction = object[j]
                    beginning_y = Y + 100
                    move_x = 2
                    if diraction == 'left':
                        x -= move_x
                        y = a * (x - h) * (x - h) - k + beginning_y  # f(x)
                    else:
                        x += move_x
                        y = a * (x - h) * (x - h) - k + beginning_y  # f(x)
                    split[i][j][1] = x
                    split[i][j][2] = y
    if len(obj) != 0:
        for i in range(len(obj) - 1, -1, -1):
            type, x, y, a, h, k, diraction, life, waiting = obj[i]
            x += X / 2
            width = 0
            if type == 'apple':
                width = 50
                color = RED
                pygame.draw.rect(S, color, (x - width, y - width, width, width))
            elif type == 'peach':
                width = 50
                color = PINK
                pygame.draw.rect(S, color, (x - width, y - width, width, width))
            elif type == 'watermalon':
                width = 70
                color = GREEN
                pygame.draw.rect(S, color, (x - width, y - width, width, width))
            elif type == 'orange':
                width = 55
                color = ORANGE
                pygame.draw.rect(S, color, (x - width, y - width, width, width))
            elif type == 'bomb':
                width = 50
                color = GREY
                pygame.draw.rect(S, color, (x - width, y - width, width, width))
            elif type == 'bread':
                width = 55
                color = YELLOW
                pygame.draw.rect(S, color, (x - width, y - width, width, width))
            if 0 > mouse_x - x > -1 * width and 0 > mouse_y - y > -1 * width and actor_type:
                beginning_x = x - X / 2
                if waiting <= 0:
                    if type != 'bomb' and type != 'bread':
                        score += 1
                        for j in range(25):
                            x = random.randint(mouse_x - 20, mouse_x + 20)
                            y = random.randint(mouse_y - 20, mouse_y + 40)
                            v = 3
                            juice.append([x, y, v, color])
                    if life > 1:
                        life -= 1
                        waiting = 10
                        obj[i][8] = waiting
                        obj[i][7] = life
                    elif life <= 1 and type == 'watermalon':
                        obj.pop(i)
                        h1 = 2 * beginning_x - h
                        if diraction == 'left':
                            diraction1 = 'right'
                        else:
                            diraction1 = 'left'
                        split.append([[type, beginning_x - 15, y, a, h, k, diraction], [type, beginning_x - 15, y, a, h1, k, diraction1]])
                        split.append([[type, beginning_x + 15, y, a, h, k, diraction], [type, beginning_x + 15, y, a, h1, k, diraction1]])
                    elif life <= 1 and type == 'bomb':
                        obj.pop(i)
                        bomb.append([x, y, 80])
                        actor_life -= 1
                    elif type == 'bread' and actor_life < 3:
                        obj.pop(i)
                        actor_life += 1
                    else:
                        obj.pop(i)
                        h1 = 2 * beginning_x - h
                        if diraction == 'left':
                            diraction1 = 'right'
                        else:
                            diraction1 = 'left'
                        split.append([[type, beginning_x, y, a, h, k, diraction], [type, beginning_x, y, a, h1, k, diraction1]])
            if y >= Y + 200 or x > X + 100 or x < -100 + width:
                obj.pop(i)
    #            if type != 'bomb':
    #               actor_life -= 1
    if len(split) > 0:
        for i in range(len(split)):
            object = split[i]
            for j in range(1, -1, -1):
                type, x, y, a, h, k, diraction = object[j]
                x += X / 2
                if type == 'apple':
                    width = 30
                    pygame.draw.rect(S, RED, (x - width, y - width, width, width))
                elif type == 'peach':
                    width = 30
                    pygame.draw.rect(S, PINK, (x - width, y - width, width, width))
                elif type == 'watermalon':
                    width = 45
                    pygame.draw.rect(S, GREEN, (x - width, y - width, width, width))
                elif type == 'orange':
                    width = 35
                    pygame.draw.rect(S, ORANGE, (x - width, y - width, width, width))
        if len(juice) != 0:
            for i in range(len(juice) - 1, -1, -1):
                x, y, v, color = juice[i]
                pygame.draw.rect(S, color, (x, y, 2, 2), 2)
                if y > Y:
                    juice.pop(i)
        if len(bomb) != 0:
            for i in range(len(bomb) - 1, -1, -1):
                x, y, waiting = bomb[i]
                pygame.draw.rect(S, RED, (x, y, 10, 10), 0)
                if waiting <= 0:
                    bomb.pop(i)
        if actor_life <= 0:
            state = 'END'


def splash():
    global splash_text_tm, splash_text_show, state, last_time1, last_time2, last_time3, last_time4, X, Y, timing, key, actor_type, actor_life
    S.fill(BLACK)
    mouse_x, mouse_y = pygame.mouse.get_pos()
    t = pygame.time.get_ticks()
    x1 = int(X / 3)
    y1 = int(Y * 5 / 7)
    x2 = int(X * 2 / 3)
    y2 = int(Y * 4 / 7)
    pygame.draw.circle(S, GREEN, (x1, y1), 40, 0)
    pygame.draw.circle(S, RED, (x2, y2), 40, 0)
    if t - splash_text_tm > 500:
        splash_text_show = not splash_text_show
        splash_text_tm = t
    if splash_text_show:
        text = myfont.render('Fruit Ninja', False, RED)
        S.blit(text, (int(X / 2 - 50), int(Y / 4)))
    if actor_type:
        if x1 - 30 < mouse_x < x1 + 30 and y1 - 30 < mouse_y < y1:
            last_time1 = 2000 + t
            last_time2 = 2000 + t
            last_time3 = 2000 + t
            state = 'GAME'
            actor_life = 3
            waiting(500 + t)
        elif x2 - 30 < mouse_x < x2 + 30 and y2 - 30 < mouse_y < y2:
            last_time1 = 2000 + t
            last_time2 = 2000 + t
            last_time3 = 2000 + t
            timing = True
            key = False
            state = 'GAME'
            waiting(500 + t)
    actor()


def boss():
    global state, score, score1, HP_boss, boss_x, boss_y, v_production, last_time1, move_x, move_y, event_move, last_time5, last_time6, last_time8, boss_move, boss_key, boss_word, actor_type, actor_life, invincible_time, stage, skill, last_time7, rain
    mouse_x, mouse_y = pygame.mouse.get_pos()
    v_production = 114514
    t = pygame.time.get_ticks()
    w = 10
    if t > last_time5 + w and boss_move <= 200:
        last_time5 = t
        boss_move += 1
    width = 75
    w = 100
    if boss_word <= 3:
        boss_x = int(X/2)
        boss_y = -1 * width + boss_move * 1
    if t > last_time5 + w and boss_word <= 5:
        last_time5 = t
        boss_word += 1
    if boss_word == 0:
        text = myfont.render('I am the kin of fruit.', False, RED)
        S.blit(text, (int(X / 2 - 130), int(Y / 2 - 50)))
    elif boss_word == 1:
        text = myfont.render('Now, fight with me.', False, RED)
        S.blit(text, (int(X / 2 - 130), int(Y / 2 - 50)))
    elif boss_word == 2:
        text = myfont.render("Don't try to let the mouse leave the interface", False, RED)
        S.blit(text, (int(X / 2 - 300), int(Y / 2 - 50)))
    elif boss_word == 3:
        text = myfont.render("This is my advice.", False, RED)
        S.blit(text, (int(X / 2 - 150), int(Y / 2 - 50)))
    elif boss_word == 4:
        invincible_time = t + 2000
        last_time1 = t
        last_time5 = t
        rain = False
        score1 = score
        for i in range(2):
            for j in range(8):
                if i == 0:
                    lines.append(X / 8 * (j + 1))
                if i == 1:
                    lines.append(Y / 8 * (j + 1))
        boss_word += 1
    else:
        HP_boss = 200 + score1 - score
        if HP_boss <= 100:
            if t >= last_time8 + 15:
                boss_x += move_x
                boss_y -= move_y
                last_time8 = t
            if boss_x >= X - width or boss_x <= width:
                move_x *= -1
                if move_x >= 0:
                    move_x = random.choice((3, 4, 5))
                else:
                    move_x = random.choice((-3, -4, -5))
                boss_x += move_x * 2
            if boss_y >= Y - width or boss_y <= width:
                move_y *= -1
                boss_y -= move_y * 2
                if move_y >= 0:
                    move_y = random.choice((3, 4, 5))
                else:
                    move_y = random.choice((-3, -4, -5))
            if boss_x <= mouse_x <= boss_x + width and boss_y <= mouse_y <= boss_y + width and t >= invincible_time:
                actor_life -= 1
                invincible_time = t + 500
            if HP_boss <= 0:
                HP_boss = 0
                state = 'END'
        else:
            last_time8 = t
            move_x = random.choice((2, -2))
            move_y = random.choice((2, -2))
        pygame.draw.line(S, GREY, (50, Y - 50), (X - 50, Y - 50), 20)
        pygame.draw.line(S, RED, (50, Y - 50), (50 + int((X - 100) / 200 * HP_boss), Y - 50), 20)
        v_production = 600
        mouse_x, mouse_y = pygame.mouse.get_pos()
        if actor_type == False and invincible_time <= t:
            actor_life -= 1
            invincible_time = t + 2000
        if t >= last_time5 + 12000:
            skill = random.randint(1, 3)
            last_time7 = t + 500
            last_time6 = t
            last_time5 = t
            stage = 1
            rain = True
            if skill == 3:
                x = random.randrange(0, X, 20)
                y = Y - x
                for i in range(int(X/20)):
                    if i <= int(y/20):
                        laser.append([0, y - i * 20])
                    else:
                        laser.append([x - 20 * (40 - i), 0])
            elif skill == 4:
                core.append([10, 'left', boss_x, boss_y])
        if skill == 1:
            if stage % 2 == 1:
                w1 = 1000
            else:
                w1 = 2000
            if t >= last_time6 + w1:
                stage += 1
                last_time6 = t
            if stage == 1:
                for i in range(8):
                    x = lines[i]
                    pygame.draw.line(S, RED, (x, 0), (x, Y), 3)
            elif stage == 2:
                for i in range(8):
                    x = lines[i]
                    pygame.draw.line(S, WHITE, (x, 0), (x, Y), 20)
                    if x - 10 <= mouse_x <= x + 10 and invincible_time < t:
                        actor_life -= 1
                        invincible_time = t + 500
            elif stage == 3:
                for i in range(8):
                    y = lines[i + 7]
                    pygame.draw.line(S, RED, (0, y), (X, y), 3)
            elif stage == 4:
                for i in range(8):
                    y = lines[i + 7]
                    pygame.draw.line(S, WHITE, (0, y), (X, y), 20)
                    if y - 10 <= mouse_y <= y + 10 and invincible_time < t:
                        actor_life -= 1
                        invincible_time = t + 500
            elif stage == 5:
                for i in range(8):
                    x = lines[i]
                    pygame.draw.line(S, RED, (x, 0), (x, Y), 3)
                    y = lines[i + 7]
                    pygame.draw.line(S, RED, (0, y), (X, y), 3)
            elif stage == 6:
                for i in range(8):
                    x = lines[i]
                    pygame.draw.line(S, WHITE, (x, 0), (x, Y), 20)
                    y = lines[i + 7]
                    pygame.draw.line(S, WHITE, (0, y), (X, y), 20)
                    if x - 10 <= mouse_x <= x + 10 and invincible_time < t:
                        actor_life -= 1
                        invincible_time = t + 500
                    if y - 10 <= mouse_y <= y + 10 and invincible_time < t:
                        actor_life -= 1
                        invincible_time = t + 500
        elif skill == 2:
            if t - last_time5 >= 8000:
                rain = False
            if t >= last_time6 + 500 and rain:
                last_time6 = t
                for i in range(8):
                    x = random.randint(0, X)
                    v = random.randint(4, 7)
                    droplets.append([x, 0, v])
            if t >= last_time7 + 20 and len(droplets) >= 0:
                last_time7 = t
                for i in range(len(droplets)):
                    x, y, v = droplets[i]
                    droplets[i][1] = y + v
            for i in range(len(droplets) - 1, -1, -1):
                x, y, v = droplets[i]
                pygame.draw.circle(S, BLUE, (x, y), 10)
                if x - 10 <= mouse_x <= x + 10 and y - 10 <= mouse_y < y + 10 and t >= invincible_time:
                    actor_life -= 1
                    invincible_time = t + 500
                if y >= Y + 80:
                    droplets.pop(i)
        elif skill == 3:
            if t <= last_time6 + 1500:
                for i in range(len(laser)):
                    x1, y1 = laser[i]
                    x2 = boss_x
                    y2 = boss_y
                    pygame.draw.line(S, RED, (x1, y1), (x2, y2), 1)
            elif last_time6 + 8000 >= t >= last_time6 + 1500:
                for i in range(len(laser)):
                    x1, y1 = laser[i]
                    x2 = boss_x
                    y2 = boss_y
                    pygame.draw.line(S, WHITE, (x1, y1), (x2, y2), 1)
                    if x1 != x2:
                        k = (y1 - y2) / (x1 - x2)
                        b = (x1 * y2 - x2 * y1) / (x1 - x2)
                    else:
                        k = 0
                        b = 0
                    if t >= invincible_time:
                        if int(mouse_x * k + b) == mouse_y and k != 0:
                            if (k > 0 and y1 == 0 and mouse_x < boss_x and mouse_y < boss_y) or (k < 0 and x1 == 0 and mouse_x < boss_x and mouse_y > boss_y) or (k > 0 and y1 == Y and mouse_x > boss_x and mouse_y < boss_y) or (k < 0 and x1 == X and mouse_x >= boss_x and mouse_y >= boss_y):
                                actor_life -= 1
                                invincible_time = t + 1000
            else:
                for i in range(len(laser) - 1, -1, -1):
                    laser.pop(i)
            if last_time7 + 20 <= t and last_time6 + 8000 >= t >= last_time6 + 1500:
                last_time7 = t
                x1, y1 = laser[0]
                if x1 == 0:
                    if y1 <= Y - 20:
                        y1 += 20
                    else:
                        x1 = 20 - Y + y1
                        y1 = Y
                elif x1 == X:
                    if y1 >= 20:
                        y1 -= 20
                    else:
                        x1 = X - 20 + y1
                        y1 = 0
                elif y1 == 0:
                    if x1 >= 20:
                        x1 -= 20
                    else:
                        y1 = 20 - x1
                        x1 = 0
                elif y1 == Y:
                    if x1 <= X - 20:
                        x1 += 20
                    else:
                        y1 = 20 + x1 - X
                        x1 = X
                laser.insert(0, [x1, y1])
                laser.pop()
    pygame.draw.circle(S, YELLOW, (boss_x, boss_y), width)


def life():
    global actor_life
    if actor_life >= 0:
        for i in range(actor_life):
            pygame.draw.circle(S, RED, (30 + i * 100, 30), 30)


def game():
    global key
    draw_board()
    if key:
        object()
        velocity()
        life()
    else:
        time()
    actor()


def end():
    global last_time1, last_time2, last_time3, last_time4, timing, obj, act, act_copy, split, v_move, actor_type, v_production, key, score, state, HP_boss
    last_time1 = 0
    last_time2 = 0
    last_time3 = 0
    last_time4 = 0
    timing = False
    obj = []
    act = []
    act_copy = []
    split = []
    actor_type = False
    score = 0
    v_move = 1
    v_production = 500
    key = True
    pygame.draw.rect(S, NAVYBLUE, (X / 4, Y / 4, X / 2, Y / 2), 0)
    pygame.draw.rect(S, GREY, (X / 4 + 10, Y / 4 + 10, X / 2 - 20, Y / 2 - 20), 0)
    if HP_boss > 0:
        text = myfont.render('GAME OVER', False, RED)
    else:
        text = myfont.render('YOU WIN', False, RED)
    S.blit(text, (int(X / 2 - 80), int(Y / 2 - 40)))
    for ev in pygame.event.get():
        if ev.type == QUIT:
            pygame.quit()
            sys.exit()
        if ev.type == KEYDOWN:
            if ev.key == K_SPACE:
                state = 'SPLASH'


if __name__ == '__main__':
    fpsClock.tick(FPS)
    while True:
        if state == 'SPLASH':
            splash()
        elif state == 'GAME':
            game()
        elif state == 'END':
            end()
        pygame.display.update()
