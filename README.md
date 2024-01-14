import pygame
pygame.init()

# Vytvorenie okna s rozmermi 800x600
window = pygame.display.set_mode((800, 600))

# Nastavenie názvu okna
pygame.display.set_caption("Pygame Touch Example")

# Nastavenie farieb
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Hlavný cyklus programu
running = True
while running:
    # Spracovanie udalostí
    for event in pygame.event.get():
        # Ukončenie programu pri stlačení tlačidla X
        if event.type == pygame.QUIT:
            running = False
        # Spracovanie dotykových udalostí
        elif event.type == pygame.FINGERDOWN:
            # Získanie pozície a tlaku prsta
            x = event.x * 800
            y = event.y * 600
            pressure = event.pressure
            # Výpis informácií o dotyku
            print(f"Touch at ({x}, {y}) with pressure {pressure}")
    
    # Vymazanie okna
    window.fill(BLACK)

    # Získanie zoznamu aktívnych dotykov
    touches = pygame.sdl2.touch.get_num_touches()

    # Pre každý dotyk vykresliť kruh s farbou a veľkosťou závislou od tlaku
    for i in range(touches):
        touch = pygame.sdl2.touch.get_touch(i)
        x = touch.x * 800
        y = touch.y * 600
        pressure = touch.pressure
        color = (255 - pressure * 255, pressure * 255, 0)
        radius = pressure * 50
        pygame.draw.circle(window, color, (x, y), radius)

    # Aktualizácia okna
    pygame.display.flip()

# Ukončenie pygame
pygame.quit()

