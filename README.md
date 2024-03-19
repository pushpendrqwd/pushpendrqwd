<!---
pushpendrqwd/pushpendrqwd is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->import pygame
import sys

# Initialize pygame
pygame.init()

# Set up screen dimensions
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Simple Platformer Game")

# Colors
WHITE = (255, 255, 255)
BLUE = (0, 0, 255)
RED = (255, 0, 0)

# Player properties
player_width = 50
player_height = 50
player_x = 50
player_y = SCREEN_HEIGHT - player_height
player_speed = 5

# Enemy properties
enemy_width = 50
enemy_height = 50
enemy_x = SCREEN_WIDTH - enemy_width
enemy_y = SCREEN_HEIGHT - enemy_height
enemy_speed = 3

clock = pygame.time.Clock()

def draw_player(x, y):
    pygame.draw.rect(screen, BLUE, (x, y, player_width, player_height))

def draw_enemy(x, y):
    pygame.draw.rect(screen, RED, (x, y, enemy_width, enemy_height))

def game_loop():
    game_over = False

    while not game_over:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            player_x -= player_speed
        if keys[pygame.K_RIGHT]:
            player_x += player_speed

        # Update enemy position
        enemy_x -= enemy_speed
        if enemy_x <= 0:
            enemy_x = SCREEN_WIDTH - enemy_width

        # Collision detection
        if player_x < enemy_x + enemy_width and \
           player_x + player_width > enemy_x and \
           player_y < enemy_y + enemy_height and \
           player_y + player_height > enemy_y:
            game_over = True

        # Draw everything
        screen.fill(WHITE)
        draw_player(player_x, player_y)
        draw_enemy(enemy_x, enemy_y)
        pygame.display.update()

        clock.tick(60)

game_loop()

