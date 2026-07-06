```
import pygame
import sys

# Initialize Pygame
pygame.init()

# Screen setup
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Pong Game")

# Colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
BLACK = (30, 30, 30)

# Clock
clock = pygame.time.Clock()

# Ball
ball_radius = 15
x, y = WIDTH // 2, HEIGHT // 2
dx, dy = 5, 5

# Paddle
paddle_width = 120
paddle_height = 15
paddle_x = WIDTH // 2 - paddle_width // 2
paddle_y = HEIGHT - 40
paddle_speed = 7

# Score
score = 0
font = pygame.font.Font(None, 36)
big_font = pygame.font.Font(None, 70)

running = True
game_over = False


def reset_game():
    global x, y, dx, dy, paddle_x, score

    x = WIDTH // 2
    y = HEIGHT // 2
    dx = 5
    dy = 5
    paddle_x = WIDTH // 2 - paddle_width // 2
    score = 0


# Main Game Loop
while running:

    # Events
    for event in pygame.event.get():

        if event.type == pygame.QUIT:
            running = False

        if game_over and event.type == pygame.KEYDOWN:

            if event.key == pygame.K_r:
                reset_game()
                game_over = False

            elif event.key == pygame.K_q:
                running = False

    if not game_over:

        # Paddle Movement
        keys = pygame.key.get_pressed()

        if keys[pygame.K_LEFT] and paddle_x > 0:
            paddle_x -= paddle_speed

        if keys[pygame.K_RIGHT] and paddle_x < WIDTH - paddle_width:
            paddle_x += paddle_speed

        # Ball Movement
        x += dx
        y += dy

        # Wall Collision
        if x - ball_radius <= 0 or x + ball_radius >= WIDTH:
            dx *= -1

        if y - ball_radius <= 0:
            dy *= -1

        # Paddle Collision
        if (paddle_y <= y + ball_radius <= paddle_y + paddle_height and
                paddle_x <= x <= paddle_x + paddle_width):

            dy *= -1
            score += 1

        # Game Over
        if y + ball_radius >= HEIGHT:
            game_over = True

        # Draw Game
        screen.fill(WHITE)

        pygame.draw.circle(screen, RED, (x, y), ball_radius)

        pygame.draw.rect(
            screen,
            BLUE,
            (paddle_x, paddle_y, paddle_width, paddle_height)
        )

        score_text = font.render(f"Score : {score}", True, BLACK)
        screen.blit(score_text, (20, 20))

    else:

        # Game Over Screen
        screen.fill(BLACK)

        title = big_font.render("GAME OVER", True, RED)
        score_text = font.render(f"Final Score : {score}", True, WHITE)
        restart = font.render("Press R to Play Again", True, WHITE)
        quit_game = font.render("Press Q to Quit", True, WHITE)

        screen.blit(title, (WIDTH//2 - title.get_width()//2, 170))
        screen.blit(score_text, (WIDTH//2 - score_text.get_width()//2, 260))
        screen.blit(restart, (WIDTH//2 - restart.get_width()//2, 320))
        screen.blit(quit_game, (WIDTH//2 - quit_game.get_width()//2, 370))

    pygame.display.flip()
    clock.tick(60)

pygame.quit()
sys.exit()
