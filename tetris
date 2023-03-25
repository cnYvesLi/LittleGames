import pygame, sys, random
from pygame.locals import *

S = pygame.display.set_mode((370, 670))
pygame.display.set_caption('hello world')
pygame.init()
pygame.mixer.init()
pygame.time.delay(1000)

audio_background = pygame.mixer.music.load("D:/python/snd/audio/background.mp3")
audio_down = pygame.mixer.Sound("D:/python/snd/audio/down.wav")
audio_gameover = pygame.mixer.Sound("D:/python/snd/audio/gameover.wav")
audio_remove = pygame.mixer.Sound("D:/python/snd/audio/remove.wav")

FPS = 30
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
x = 0
y = 0

ab1 = [(-1, 0), (0, 0), (1, 0), (2, 0), -1, 2, 0, 0]
bb1 = [(0, -1), (0, 0), (0, 1), (0, 2), 0, 0, -1, 2]
cb1 = [(1, 0), (0, 0), (-1, 0), (-2, 0), -2, 1, 0, 0]
db1 = [(0, -2), (0, -1), (0, 0), (0, 1), 0, 0, -2, 2]
b1 = [ab1, bb1, cb1, db1]
ab2 = [(-1, 0), (0, 0), (0, 1), (1, 1), -1, 1, 0, 1]
bb2 = [(0, -1), (0, 0), (-1, 0), (-1, 1), -1, 0, -1, 1]
cb2 = [(1, 0), (0, 0), (0, -1), (-1, -1), -1, 1, -1, 0]
db2 = [(0, 1), (0, 0), (1, 0), (1, -1), 0, 1, -1, 1]
b2 = [ab2, bb2, cb2, db2]
ab3 = [(1, 0), (0, 0), (0, 1), (-1,  1), -1, 1, 0, 1]
bb3 = [(0, 1), (0, 0), (-1, 0), (-1, -1), -1, 0, -1, 1]
cb3 = [(-1, 0), (0, 0), (0, -1), (1, -1), -1, 1, -1, 0]
db3 = [(0, -1), (0, 0), (1, 0), (1, 1), 0, 1, -1, 1]
b3 = [ab3, bb3, cb3, db3]
ab4 = [(-1, 0), (0, 0), (1, 0), (0, -1), -1, 1, -1, 0]
bb4 = [(0, -1), (0, 0), (0, 1), (1, 0), 0, 1, -1, 1]
cb4 = [(-1, 0), (0, 0), (1, 0), (0, 1), -1, 1, 0, 1]
db4 = [(0, -1), (0, 0), (0, 1), (-1, 0), -1, 0, -1, 1]
b4 = [ab4, bb4, cb4, db4]
ab5 = [(-1, 0), (0, 0), (-1, 1), (0, 1), -1, 0, 0, 1]
bb5 = [(-1, 0), (0, 0), (-1, 1), (0, 1), -1, 0, 0, 1]
cb5 = [(-1, 0), (0, 0), (-1, 1), (0, 1), -1, 0, 0, 1]
db5 = [(-1, 0), (0, 0), (-1, 1), (0, 1), -1, 0, 0, 1]
b5 = [ab5, bb5, cb5, db5]
ab6 = [(0, -1), (0, 0), (-1, 0), (-2, 0), -2, 0, -1, 0]
bb6 = [(1, 0), (0, 0), (0, -1), (0, -2), 0, 1, -2, 1]
cb6 = [(0, 1), (0, 0), (1, 0), (2, 0), 0, 2, -1, 1]
db6 = [(-1, 0), (0, 0), (0, 1), (0, 2), -1, 0, 0, 2]
b6 = [ab6, bb6, cb6, db6]
ab7 = [(0, -1), (0, 0), (1, 0), (2, 0), 0, 2, -1, 0]
bb7 = [(1, 0), (0, 0), (0, 1), (0, 2), 0, 1, 0, 2]
cb7 = [(0, 1), (0, 0), (-1, 0), (-2, 0), -2, 0, 0, 1]
db7 = [(-1, 0), (0, 0), (0, -1), (0, -2), -1, 0, -2, 1]
b7 = [ab7, bb7, cb7, db7]
b = [b1, b2, b3, b4, b5, b6, b7]

state = 'SPLASH'
current_block = -1
current_pos = None
current_board = []
current = 0
last_time = 0
color = (0, 0, 0)
form = 0
abject_by = 0
s = 0
board = []
point = 0
color = (0, 0, 0)
recort_block = []
myfont = pygame.font.SysFont('Comic Sans MS', 30)
for i in range(200):
    board.append(0)


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


def tetris_init():
    global state, current_block, current_pos, current_board, current, last_time, color, form, abject_by, s, board

    current_block = -1
    current_pos = None
    current_board = []
    current = 0
    last_time = 0
    color = (0, 0, 0)
    form = 0
    abject_by = 0
    s = 0
    board = []

splash_text_show = False
splash_text_tm = 0


def splash():
    global state, splash_text_show, splash_text_tm
    S.fill(BLACK)
    t = pygame.time.get_ticks()
    if t - splash_text_tm > 500:
        splash_text_show = not splash_text_show
        splash_text_tm = t

    if splash_text_show:
        text = myfont.render('Press SPACE to START', False, RED)
        S.blit(text, (20, 250))
    for ev in pygame.event.get():
        if ev.type == QUIT:
            pygame.quit()
            sys.exit()
        if ev.type == KEYDOWN:
            if ev.key == K_SPACE:
                state = 'GAME'
                tetris_init()
                pygame.mixer.music.play(loops=-1)


def end():
    global state
    draw_board()
    if len(current_board) != 0:
        for i in range(len(current_board)):
            x, y, z = current_board[i]
            pygame.draw.rect(S, z, (x, y, 30, 30))
    pygame.draw.rect(S, RED, pygame.Rect(83, 213, 224, 54))
    pygame.draw.rect(S, WHITE, pygame.Rect(85, 215, 220, 50))
    text = myfont.render('GAME OVER', False, RED)
    S.blit(text, (100, 220))
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == KEYDOWN:
            state = 'SPLASH'


def draw_board():
    S.fill(BLACK)
    for x in range(12):
        for y in range(22):
            if x == 0 or x == 11 or y == 0 or y == 21:
                pygame.draw.rect(S, NAVYBLUE, (x * 30 + 5, y * 30 + 5, 30, 30))
            else:
                pygame.draw.rect(S, WHITE, (x * 30 + 5, y * 30 + 5, 30, 30), 2)


def game():
    global current_block, current_pos, current, last_time, form, abject_by, s, color, state, point
    rect = []
    line = []
    delete = []
    if len(current_board) != 0:
        for i in range(len(current_board) -1, -1, -1):
            x, y, z = current_board[i]
            if y <= 95:
                state = 'END'
                current = 1
                pygame.mixer.music.stop()
                audio_gameover.play()
            line.append(y)
            pygame.draw.rect(S, z, (x, y, 30, 30))
        for i in range(len(current_board) -1, -1, -1):
            x, y, z = current_board[i]
            if line.count(y) == 10:
                key = True
                if len(delete) != 0:
                    for j in range(len(delete)):
                        y1 = delete[j]
                        if y == y1:
                            key = False
                if key:
                    delete.append(y)
            if len(delete) != 0:
                key = True
                for j in range(len(delete)):
                    y1 = delete[j]
                    if y == y1 and key:
                        current_board.pop(i)
                        key = False
        if len(delete) != 0:
            point += len(delete)
            for i in range(len(current_board)):
                x, y, z = current_board[i]
                print(len(delete))
                growth = 0
                for j in range(len(delete)):
                    ly = delete[j]
                    if y < ly:
                        growth += 30
                y += growth
                current_board[i] = (x, y, z)
                audio_remove.play()
    if current == 0:
        n = random.randint(3, 8)
        recort_block = random.choice(b)
        color = random.choice([YELLOW, BLUE, WHITE, GREEN, RED])
        s = 0
        current_block = n
        current_pos = recort_block
        current = 1
    elif current == 1:
        n = current_block
        recort_block = current_pos
    t = pygame.time.get_ticks()
    if (t-last_time) > 200 or current_block < 0:
        s += 1
        last_time = t
    block = recort_block[form]
    while True:
        if block[4] + n <= 0:
            n += 1
        elif block[5] + n >= 11:
            n -= 1
        else:
            break
    if block[6] + 2 <= 0:
        abject_by = 1
    elif block[6] + 2 >= 0:
        abject_by = 0
    k = 0
    j = 0
    for m in range(4):
        bx, by = block[m]
        rect_x = 5 + n * 30 + bx * 30
        rect_y = 65 + by * 30 + abject_by * 30 + s * 30
        rect.append((rect_x, rect_y, color))
        if j == 0:
            if len(current_board) != 0:
                for i in range(len(current_board)):
                    x, y, z = current_board[i]
                    if rect_x == x and rect_y == y:
                        j = 1
                        k = 1
            if block[7] + s > 18:
                j = 1
                k = 1
        if 11 >= n + bx >= 1:
            pygame.draw.rect(S, color, (rect_x, rect_y, 30, 30))

    if k == 1:
        audio_down.play()
        for j in range(len(rect)):
            x, y, z = rect[j]
            current_board.append((x, y - 30, z))
            current = 0


    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()
        if event.type == KEYDOWN:
            r = 0
            if event.key == K_LEFT or event.key == K_a:
                if len(current_board) != 0:
                    for i in range(len(current_board)):
                        x, y, z = current_board[i]
                        for j in range(len(rect)):
                            rx, ry, rz = rect[j]
                            if rx - 30 == x and ry == y:
                                r = 1
                if r != 1:
                    n -= 1
                    current_block = n
            elif event.key == K_RIGHT or event.key == K_d:
                if event.type == QUIT:
                    pygame.quit()
                    sys.exit()
                if event.type == KEYDOWN:
                    r = 0
                    if event.key == K_LEFT or event.key == K_a:
                        if len(current_board) != 0:
                            for i in range(len(current_board)):
                                x, y, z = current_board[i]
                                for j in range(len(rect)):
                                    rx, ry, rz = rect[j]
                                    if rx + 30 == x and ry == y:
                                        r = 1
                    if r != 1:
                        n += 1
                        current_block = n
                    print(r)
            if event.type == QUIT:
                pygame.quit()
                sys.exit()
            if event.type == KEYDOWN:
                r = 0
                if event.key == K_LEFT or event.key == K_a:
                    if len(current_board) != 0:
                        for i in range(len(current_board)):
                            x, y, z = current_board[i]
                            for j in range(len(rect)):
                                rx, ry, rz = rect[j]
                                if rx - 30 == x and ry == y:
                                    r = 1
                if r != 1:
                    n -= 1
                    current_block = n
                n += 1
                current_block = n
            if event.key == K_SPACE:
                if form < 3:
                    form += 1
                elif form == 3:
                    form = 0


if __name__ == '__main__':
    fpsClock.tick(FPS)
    while True:
        if state == 'SPLASH':
            splash()
        elif state == 'GAME':
            draw_board()
            game()
        elif state == 'END':
            end()
        pygame.display.update()
