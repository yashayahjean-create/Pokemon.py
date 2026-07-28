# =====================================================
#   ECCU GAP Camp 2026 · WEEK 1 · INTERACTIVE BOT ENGINE
# =====================================================

bot_name = "Zigzagon"

# import pokebase as pb
# bulbasaur = pb.pokemon("bulbasaur")
# print(bulbasaur.types[0].type.name)

import pandas as pd

# Load the Pokémon data from the CSV file
df = pd.read_csv("pokebase.csv")
print(df.head())

# FIX: pokemon_db must be defined before chatbot() tries to use it.
# This builds a lookup dictionary from the pokebase.csv DataFrame.
pokemon_db = {pokebase: {"type": "Unknown", "ability": "Unknown", "description": "Unknown"} for pokebase in df["name"].str.strip().str.lower()}

for _, row in df.iterrows():
    name = str(row["name"]).strip().lower()

    primary_type = row.get("primary_type", "Unknown")
    secondary_type = row.get("secondary_type", "")

    if pd.notna(secondary_type) and str(secondary_type).strip() != "":
        pokemon_type = f"{primary_type}/{secondary_type}"
    else:
        pokemon_type = str(primary_type)

    description = row.get("Description", "No description available.")
    if pd.isna(description) or str(description).strip() == "":
        description = "No description available."

    pokemon_db[name] = {
        "type": pokemon_type,
        "image": row.get("image", "No image available."),
        
        "description": description
    }
img = df["image"]
print(img)

def chatbot():
    print("⚡ Welcome to the Pokémon Chatbot!")
    print("Ask about any Pokémon in the database, like Pikachu, Charizard, Bulbasaur, Squirtle and more.")
    print("Type 'exit' to quit.\n")

    while True:
        user_input = input("You: ").strip().lower()

        print("User:", user_input)

        if user_input == "exit":
            print("Bot: Goodbye! Catch you later, User!")
            break

        if user_input in pokemon_db:
            pokemon = pokemon_db[user_input]
            print(f"\nBot: Here's what I know about {user_input.title()}:")
            print(f"Type: {pokemon['type']}")
        
            print(f"Description: {pokemon['description']}\n")
            print(f"Image: {pokemon['image']}\n")
        else:
            print("Bot: I don't know that Pokémon yet. Try Pikachu, Charizard, Bulbasaur, or Squirtle.\n")


if __name__ == "__main__":
    chatbot()
