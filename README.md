import random

class Player:
    def __init__(self, name):
        self.name = name
        self.health = 100
        self.inventory = []

    def take_damage(self, damage):
        self.health -= damage

    def heal(self, amount):
        self.health += amount

    def add_to_inventory(self, item):
        self.inventory.append(item)

def start_game():
    print("Welcome to the Text-Based Adventure Game!")
    player_name = input("Enter your character's name: ")
    player = Player(player_name)

    print(f"Hello, {player.name}! Your health is {player.health}.")

    # Game loop
    while player.health > 0:
        action = input("What do you want to do? (explore/quit): ").lower()

        if action == "explore":
            explore(player)
        elif action == "quit":
            print("Thanks for playing! Goodbye.")
            break
        else:
            print("Invalid action. Try again.")

def explore(player):
    # Simulating an encounter
    encounter = random.choice(["enemy", "treasure", "nothing"])

    if encounter == "enemy":
        enemy_health = random.randint(20, 50)
        print(f"You've encountered an enemy with {enemy_health} health!")
        combat(player, enemy_health)
    elif encounter == "treasure":
        treasure = random.choice(["sword", "health potion"])
        print(f"You found a {treasure}!")
        player.add_to_inventory(treasure)
    else:
        print("You found nothing of interest.")

def combat(player, enemy_health):
    while enemy_health > 0 and player.health > 0:
        print(f"Your health: {player.health} | Enemy health: {enemy_health}")
        attack = input("What do you want to do? (attack/run): ").lower()

        if attack == "attack":
            damage = random.randint(5, 15)
            enemy_health -= damage
            print(f"You dealt {damage} damage to the enemy!")
        elif attack == "run":
            print("You managed to escape from the enemy.")
            break
        else:
            print("Invalid action. Try again.")

        # Enemy's turn
        player.take_damage(random.randint(3, 10))
    
    if player.health <= 0:
        print("Game over! You were defeated.")
    elif enemy_health <= 0:
        print("You defeated the enemy!")

# Start the game
start_game()
