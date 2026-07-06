## Source code for Pong Game.

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


# Clock
clock = pygame.time.Clock()

# Ball setup
ball_radius = 15
x, y = WIDTH // 2, HEIGHT // 2
dx, dy = 5, 5

# Paddle setup
paddle_width, paddle_height = 120, 15
paddle_x = WIDTH // 2 - paddle_width // 2
paddle_y = HEIGHT - 40
paddle_speed = 7

# Score
score = 0
font = pygame.font.Font(None, 36)

# Game loop
running = True
while running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Move paddle with keys
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and paddle_x > 0:
        paddle_x -= paddle_speed
    if keys[pygame.K_RIGHT] and paddle_x < WIDTH - paddle_width:
        paddle_x += paddle_speed

    # Move ball
    x += dx
    y += dy

    # Bounce off walls
    if x - ball_radius <= 0 or x + ball_radius >= WIDTH:
        dx = -dx
    if y - ball_radius <= 0:
        dy = -dy

    # Ball hits paddle
    if (paddle_y <= y + ball_radius <= paddle_y + paddle_height and
        paddle_x <= x <= paddle_x + paddle_width):
        dy = -dy
        score += 1  # increase score

    # Ball falls below paddle → Game over
    if y + ball_radius >= HEIGHT:
        print("Game Over! Final Score:", score)
        running = False

    # Draw everything
    screen.fill(WHITE)
    pygame.draw.circle(screen, RED, (x, y), ball_radius)  # Ball
    pygame.draw.rect(screen, BLUE, (paddle_x, paddle_y, paddle_width, paddle_height))  # Paddle

    # Show score
    score_text = font.render(f"Score: {score}", True, (0, 0, 0))
    screen.blit(score_text, (10, 10))

    # Update display
    pygame.display.update()
    clock.tick(60)

pygame.quit()
sys.exit()
