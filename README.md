import random
import time

# Fonction pour simuler une animation de texte
def animation_texte(texte):
    for char in texte:
        print(char, end="", flush=True)
        time.sleep(0.05)  # Ajuste la vitesse ici
    print()

# Création des classes de Pokémon
class Pokemon:
    def __init__(self, nom, points_de_vie, attaque):
        self.nom = nom
        self.points_de_vie = points_de_vie
        self.attaque = attaque
    
    def attaquer(self, cible):
        animation_texte(f"{self.nom} lance une attaque!")
        time.sleep(1)
        degats = random.randint(5, self.attaque)
        cible.points_de_vie -= degats
        animation_texte(f"{cible.nom} reçoit {degats} points de dégâts!")
        time.sleep(1)

    def est_vivant(self):
        return self.points_de_vie > 0

# Création des Pokémon du joueur et de l'adversaire
ton_pokemon = Pokemon("Pikachu", 50, 15)
pokemon_adversaire = Pokemon("Salamèche", 45, 12)

# Début du combat
animation_texte("Un combat Pokémon commence !")
time.sleep(1)
animation_texte(f"Ton Pokémon : {ton_pokemon.nom} (PV: {ton_pokemon.points_de_vie})")
animation_texte(f"Pokémon Adversaire : {pokemon_adversaire.nom} (PV: {pokemon_adversaire.points_de_vie})\n")

# Boucle de combat
while ton_pokemon.est_vivant() and pokemon_adversaire.est_vivant():
    # Tour du joueur
    action = input("Choisis une action (1: Attaquer, 2: Soigner): ")
    
    if action == "1":
        ton_pokemon.attaquer(pokemon_adversaire)
    elif action == "2":
        soin = random.randint(5, 15)
        ton_pokemon.points_de_vie += soin
        animation_texte(f"{ton_pokemon.nom} utilise une potion et récupère {soin} PV.")
        time.sleep(1)
    else:
        animation_texte("Action non reconnue! Le tour est perdu.")
        time.sleep(1)
    
    # Vérifie si l'adversaire est encore en vie
    if not pokemon_adversaire.est_vivant():
        animation_texte(f"{pokemon_adversaire.nom} est K.O.! Tu as gagné le combat!")
        break

    # Tour de l'adversaire
    animation_texte(f"\n{pokemon_adversaire.nom} prépare une attaque!")
    pokemon_adversaire.attaquer(ton_pokemon)
    
    # Vérifie si le joueur est encore en vie
    if not ton_pokemon.est_vivant():
        animation_texte(f"{ton_pokemon.nom} est K.O.! Tu as perdu le combat!")
        break
    
    # Affichage des PV restants
    animation_texte(f"\n{ton_pokemon.nom} (PV: {ton_pokemon.points_de_vie}) vs {pokemon_adversaire.nom} (PV: {pokemon_adversaire.points_de_vie})\n")

animation_texte("Le combat est terminé.")
