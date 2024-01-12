# Random-Projects

 Table of Contents
 
- [Hangman Game](#hangman_game)
- [Snake Game](#snake_game)

---

Hangman Game
---

```python
word = "Lauren"

allowed_errors = 6
guesses = []
done = False
while not done:
    for letter in word:
        if letter.lower() in guesses:
            print(letter, end="")
        else:
            print("_", end="")
    print("")
    done = True

    guess = input(f"Allowed Errors Left {allowed_errors}, Next Guess: ")
    guesses.append(guess.lower())
    if guess.lower() not in word.lower():
        allowed_errors -= 1
        if allowed_errors == 0:
            break

    done = True
    for letter in word:
        if letter.lower() not in guesses:
            done = False

if done:
    print(f"Congrats! It was {word}!")
else:
    print(f"Game over!")
```

<img width="351" alt="Screenshot 2024-01-11 180131" src="https://github.com/Laurenjohns/Random-Projects/assets/107310914/d9c5e263-51df-401f-be43-31e5e401e832">


---

### Snake Game
---

```python
import pygame
import time
import random

pygame.init()

white = (255, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)
orange = (255, 165, 0)

width, height = 600, 400

game_display = pygame.display.set_mode((width, height))
pygame.display.set_caption("Snake Game")

clock = pygame.time.Clock()

snake_size = 10  # Change to 10 or 15, choose one
snake_speed = 15  # Adjust the speed as needed

message_font = pygame.font.SysFont('ubuntu', 30)
score_font = pygame.font.SysFont('ubuntu', 25)


def print_score(score):
    text = score_font.render("Score: " + str(score), True, orange)
    game_display.blit(text, [0, 0])


def draw_snake(snake_size, snake_pixels):
    for pixel in snake_pixels:
        pygame.draw.rect(game_display, white, [pixel[0], pixel[1], snake_size, snake_size])


def run_game():
    game_over = False
    game_close = False
    x = width / 2
    y = height / 2

    x_speed = 0
    y_speed = 0

    snake_pixels = []
    snake_length = 1

    target_x = round(random.randrange(0, width - snake_size) / 10.0) * 10.0
    target_y = round(random.randrange(0, height - snake_size) / 10.0) * 10.0

    while not game_over:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
                game_close = False

            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x_speed = -snake_size
                    y_speed = 0
                elif event.key == pygame.K_RIGHT:
                    x_speed = snake_size
                    y_speed = 0
                elif event.key == pygame.K_UP:
                    x_speed = 0
                    y_speed = -snake_size
                elif event.key == pygame.K_DOWN:
                    x_speed = 0
                    y_speed = snake_size

        if x >= width or x < 0 or y >= height or y < 0:
            game_close = True

        x += x_speed
        y += y_speed

        game_display.fill(black)
        pygame.draw.rect(game_display, orange, [target_x, target_y, snake_size, snake_size])

        snake_pixels.append([x, y])

        if len(snake_pixels) > snake_length:
            del snake_pixels[0]

        for pixel in snake_pixels[:-1]:
            if pixel == [x, y]:
                game_close = True

        draw_snake(snake_size, snake_pixels)
        print_score(snake_length - 1)

        pygame.display.update()

        if x == target_x and y == target_y:
            target_x = round(random.randrange(0, width - snake_size) / 10.0) * 10.0
            target_y = round(random.randrange(0, height - snake_size) / 10.0) * 10.0
            snake_length += 1

        clock.tick(snake_speed)

    pygame.quit()
    quit()


run_game()
```
---
