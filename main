import pygame
import random
import math

#Initialize Pygame
pygame.init()

#Create a screen
screen = pygame.display.set_mode((800, 600))

#create a background
background = pygame.image.load("tlo2.png")

#Create caption and icon
pygame.display.set_caption("Space Invaders")
icon = pygame.image.load('ufo.png')
pygame.display.set_icon(icon)


#Create Enemy
enemyImg = pygame.image.load("alien.png")
enemyX = random.randint(0, 736)
enemyY = random.randint(0, 150)
enemyX_change = 5
enemyY_change = 40

#Create Player
playerImg = pygame.image.load("space-invaders.png")
playerX = 360
playerY = 480
playerX_change = 0
playerY_change = 0

#Score
score = 0

#Create Bullet
#Bullet state- 'ready' if not on screen, 'fire' if already shooted and on screen
bulletImg = pygame.image.load("bullet.png")
bulletX = 0
bulletY = 480
bulletX_change = 0
bulletY_change = -10
bullet_state = 'ready'

def player(x, y):
    screen.blit(playerImg, (x, y))

def enemy(x, y):
    screen.blit(enemyImg, (x, y))

def fire_bullet(x, y):
    global bullet_state
    global bulletX
    bullet_state = "fire"
    screen.blit(bulletImg, (x + 16, y + 10))

def is_collision(enemyX, enemyY, bulletX, bulletY):
    distance = math.sqrt(math.pow(enemyX - bulletX, 2) + math.pow(enemyY - bulletY, 2))
    return distance <= 28

#Create Game loop
running = True
while running:

    # RGB Colors
    screen.fill((0, 25, 60))
    screen.blit(background, (0, 0))

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                playerX_change = -5
            if event.key == pygame.K_RIGHT:
                playerX_change = 5
            if event.key == pygame.K_SPACE and bullet_state == 'ready':
                fire_bullet(playerX, playerY)
                bulletX = playerX + 16
                bulletY = playerY
        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                playerX_change = 0

    playerX += playerX_change
    #Check for boundaries so the playes doesn't go away:
    if playerX <= 0:
        playerX= 0
    elif playerX >= 736:
        playerX = 736

    #Enemy movement:
    enemyX += enemyX_change
    if enemyX <= 0:
        enemyX_change = 4
        enemyY += enemyY_change
    if enemyX >= 736:
        enemyX_change = -4
        enemyY += enemyY_change

    #Bullet movement
    if bullet_state == 'fire':
        bulletY += bulletY_change
        screen.blit(bulletImg, (bulletX, bulletY))
        if is_collision(enemyX, enemyY, bulletX, bulletY):
            bullet_state = 'ready'
            enemyX = random.randint(0, 736)
            enemyY = random.randint(0, 150)
            score += 1
        if bulletY <= 0:
            bullet_state = 'ready'

    enemy(enemyX, enemyY)
    player(playerX, playerY)
    pygame.display.update()

