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
```

## Explaination

Absolutely! Let's go through the code section by section. This is a great way to understand how a Pygame program works.

---

# 1. Import Libraries

```python
import pygame
import sys
```

### Explanation

* `pygame` → Used to create games.
* `sys` → Used to exit the program properly with `sys.exit()`.

---

# 2. Initialize Pygame

```python
pygame.init()
```

### Explanation

This initializes all the Pygame modules (display, sound, fonts, etc.).

Without this line, Pygame functions won't work correctly.

---

# 3. Create the Game Window

```python
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Pong Game")
```

### Explanation

```python
WIDTH = 800
HEIGHT = 600
```

The game window will be:

* Width = **800 pixels**
* Height = **600 pixels**

---

```python
screen = pygame.display.set_mode((WIDTH, HEIGHT))
```

Creates the game window.

---

```python
pygame.display.set_caption("Pong Game")
```

Changes the window title.

---

# 4. Colors

```python
WHITE = (255,255,255)
RED = (255,0,0)
BLUE = (0,0,255)
BLACK = (30,30,30)
```

### Explanation

Colors in Pygame are represented using **RGB** values.

```
(Red, Green, Blue)
```

Example

```
(255,0,0) → Red

(0,255,0) → Green

(0,0,255) → Blue

(255,255,255) → White
```

---

# 5. Clock

```python
clock = pygame.time.Clock()
```

### Explanation

The clock controls the game's **frame rate (FPS)**.

Later we write

```python
clock.tick(60)
```

which means

> Run the game at **60 frames per second**.

Without it, the game could run too fast.

---

# 6. Ball Variables

```python
ball_radius = 15
```

The ball's radius is **15 pixels**.

---

```python
x = WIDTH // 2
y = HEIGHT // 2
```

The ball starts in the **center** of the screen.

For an 800×600 window:

```
x = 400
y = 300
```

---

```python
dx = 5
dy = 5
```

These represent the ball's speed.

```
dx → Horizontal speed

dy → Vertical speed
```

Initially

```
x = x + 5
y = y + 5
```

So the ball moves diagonally.

---

# 7. Paddle Variables

```python
paddle_width = 120
paddle_height = 15
```

The paddle is

```
120 pixels wide

15 pixels tall
```

---

```python
paddle_x = WIDTH//2 - paddle_width//2
```

Places the paddle in the center.

```
800//2 = 400

400 - 60 = 340
```

So it begins at x = 340.

---

```python
paddle_y = HEIGHT - 40
```

Places the paddle near the bottom.

```
600 - 40 = 560
```

---

```python
paddle_speed = 7
```

Each key press moves the paddle **7 pixels**.

---

# 8. Score

```python
score = 0
```

Keeps track of the player's score.

---

```python
font = pygame.font.Font(None,36)
```

Creates a font for displaying text.

`None` means use Pygame's default font.

---

```python
big_font = pygame.font.Font(None,70)
```

Used for the **GAME OVER** title.

---

# 9. Game States

```python
running = True
game_over = False
```

These control the game's flow.

### running

```
True → Keep running

False → Close the game
```

---

### game_over

```
False → Game is being played

True → Show Game Over screen
```

---

# 10. Reset Function

```python
def reset_game():
```

This function restarts the game.

---

```python
global x,y,dx,dy,paddle_x,score
```

These variables are defined outside the function.

Without `global`, Python would create new local variables instead of updating the existing game variables.

---

```python
x = WIDTH//2
y = HEIGHT//2
```

Move the ball back to the center.

---

```python
dx = 5
dy = 5
```

Restore the ball's speed.

---

```python
paddle_x = WIDTH//2 - paddle_width//2
```

Move the paddle back to the center.

---

```python
score = 0
```

Reset the score.

---

# 11. Main Game Loop

```python
while running:
```

This loop keeps running until

```
running = False
```

Think of it as:

```
Game starts

↓

Repeat

↓

Check keyboard

↓

Move objects

↓

Draw objects

↓

Update screen

↓

Repeat
```

---

# 12. Event Handling

```python
for event in pygame.event.get():
```

Checks for events like:

* Keyboard
* Mouse
* Closing the window

---

```python
if event.type == pygame.QUIT:
```

If the player clicks **X**,

```python
running = False
```

so the game exits cleanly.

---

# 13. Restart Keys

```python
if game_over and event.type == pygame.KEYDOWN:
```

Only listen for keys **after the game ends**.

---

```python
if event.key == pygame.K_r:
```

Press **R**

↓

Restart the game.

---

```python
elif event.key == pygame.K_q:
```

Press **Q**

↓

Quit.

---

# 14. Paddle Movement

```python
keys = pygame.key.get_pressed()
```

Returns the current state of every key.

---

```python
if keys[pygame.K_LEFT]:
```

If the Left Arrow is held down,

```
paddle_x -= paddle_speed
```

Move left.

---

```python
if keys[pygame.K_RIGHT]:
```

Move right.

---

# 15. Ball Movement

```python
x += dx
y += dy
```

Every frame:

```
x = x + dx

y = y + dy
```

This creates the ball's motion.

---

# 16. Wall Collision

```python
if x-ball_radius <=0:
```

The ball has reached the left wall.

---

```python
dx *= -1
```

Reverse the horizontal direction.

If

```
dx = 5
```

then

```
dx = -5
```

The ball now moves left.

The same logic applies to the right and top walls.

---

# 17. Paddle Collision

```python
if (
paddle_y <= y+ball_radius <= paddle_y+paddle_height
and
paddle_x <= x <= paddle_x+paddle_width
):
```

This checks if the ball touches the paddle.

If true,

```python
dy *= -1
```

The ball bounces upward.

---

```python
score +=1
```

Increase the score.

---

# 18. Game Over

```python
if y+ball_radius >= HEIGHT:
```

If the ball reaches the bottom,

```
game_over = True
```

Instead of exiting, the game switches to the Game Over screen.

---

# 19. Drawing the Game

```python
screen.fill(WHITE)
```

Paint the background white.

This clears the previous frame so moving objects don't leave trails.

---

```python
pygame.draw.circle(...)
```

Draw the ball.

---

```python
pygame.draw.rect(...)
```

Draw the paddle.

---

```python
font.render(...)
```

Create the score text.

---

```python
screen.blit(score_text,(20,20))
```

Display the score at the top-left corner.

---

# 20. Game Over Screen

When

```python
game_over == True
```

this section runs instead of the gameplay.

It displays:

* **GAME OVER**
* Final Score
* Press **R** to Play Again
* Press **Q** to Quit

---

# 21. Update the Display

```python
pygame.display.flip()
```

Makes everything you've drawn appear on the screen.

Without this line, nothing would be visible.

---

# 22. Frame Rate

```python
clock.tick(60)
```

Limits the game to **60 FPS**, keeping the gameplay smooth and consistent across different computers.

---

# 23. Exit the Game

```python
pygame.quit()
sys.exit()
```

These lines:

* Close all Pygame resources.
* Exit the Python program cleanly.

---

## Overall Program Flow

```text
Start Program
      │
      ▼
Initialize Pygame
      │
      ▼
Create Window
      │
      ▼
Initialize Ball, Paddle, Score
      │
      ▼
──────── Main Loop ────────
│ Read Events             │
│ Move Paddle             │
│ Move Ball               │
│ Check Wall Collision    │
│ Check Paddle Collision  │
│ Update Score            │
│ Check Game Over         │
│ Draw Objects            │
│ Update Screen           │
└─────────────────────────┘
      │
      ▼
Game Over?
      │
   Yes ▼
Show Game Over Screen
      │
 ┌────┴────┐
 │         │
R Pressed  Q Pressed
 │         │
 ▼         ▼
Reset    Exit Game
```

This program introduces many core Pygame concepts you'll use in almost every game: the game loop, event handling, animation, collision detection, drawing shapes, rendering text, game states, and resetting the game. Mastering these concepts will make it much easier to build larger games such as Snake, Brick Breaker, Flappy Bird, Space Invaders, or platformers.
