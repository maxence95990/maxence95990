# Importer la bibliothèque pygame
import pygame

# Initialiser le jeu
pygame.init()
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Bing's Game")
clock = pygame.time.Clock()

# Créer une classe pour les objets du jeu
class GameObject(pygame.sprite.Sprite):
    def __init__(self, image, x, y):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.image.load(image)
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y

    def update(self):
        # Mettre à jour la position de l'objet
        pass

# Créer un groupe pour stocker les objets du jeu
objects = pygame.sprite.Group()

# Créer un objet joueur
player = GameObject("player.png", 400, 300)
objects.add(player)

# Créer une variable pour stocker le mode de création
creation_mode = False

# Créer une boucle principale
running = True
while running:
    # Gérer les événements
    for event in pygame.event.get():
        # Quitter le jeu
        if event.type == pygame.QUIT:
            running = False
        # Changer le mode de création
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_c:
                creation_mode = not creation_mode
                print("Creation mode:", creation_mode)
        # Créer un objet
        if event.type == pygame.MOUSEBUTTONDOWN and creation_mode:
            # Obtenir la position de la souris
            mouse_x, mouse_y = pygame.mouse.get_pos()
            # Créer un objet aléatoire
            image = pygame.image.load("object" + str(random.randint(1, 4)) + ".png")
            object = GameObject(image, mouse_x, mouse_y)
            objects.add(object)

    # Mettre à jour le jeu
    objects.update()

    # Dessiner le jeu
    screen.fill((135, 206, 235)) # Couleur du ciel
    objects.draw(screen)
    pygame.display.flip()

    # Contrôler le temps
    clock.tick(60)

# Quitter le jeu
pygame.quit()
