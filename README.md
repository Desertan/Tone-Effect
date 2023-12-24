# Tone-Effect
Tone effekt
# Code for Sound Effects using Python and Pygame
import pygame
import sys
import random

# Initialize Pygame and mixer
pygame.init()
pygame.mixer.init()

# Set up display
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("Sound Effects")

# Define colors
black = (0, 0, 0)
white = (255, 255, 255)

# Load sound effects
explosion_sound = pygame.mixer.Sound("explosion.wav")
coin_sound = pygame.mixer.Sound("coin.wav")

# Define Particle class
class Particle:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
        self.radius = random.randint(2, 5)

    def move(self):
        self.x += random.randint(-2, 2)
        self.y += random.randint(-2, 2)

    def draw(self):
        pygame.draw.circle(screen, self.color, (self.x, self.y), self.radius)

# Create a list of particles
particles = [Particle(width // 2, height // 2) for _ in range(100)]

# Main game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                explosion_sound.play()
            elif event.key == pygame.K_c:
                coin_sound.play()

    screen.fill(black)

    # Move and draw particles
    for particle in particles:
        particle.move()
        particle.draw()

    pygame.display.flip()
    pygame.time.Clock().tick(30)
