
import random
from game_data import data  # assuming your data is named game_data

def format_data(account):
    """Format the account data into a printable string."""
    account_name = account["name"]
    account_descr = account["description"]
    account_followers = account["followers"]
    return f"{account_name}, a {account_descr}, with {account_followers:,} followers"

def compare_followers(a, b, guess):
    """Return True if guess is correct, else False."""
    if a["followers"] > b["followers"]:
        return guess == 'a'
    else:
        return guess == 'b'

score = 0
game_should_continue = True

account_a = random.choice(data)
account_b = random.choice(data)
# Make sure A and B are not the same
while account_a == account_b:
    account_b = random.choice(data)

while game_should_continue:
    print(f"\nCompare A: {format_data(account_a)}.")
    print(f"Against B: {format_data(account_b)}.")

    guess = input("Who has more followers? Type 'A' or 'B': ").lower()

    is_correct = compare_followers(account_a, account_b, guess)

    if is_correct:
        score += 1
        print(f"✅ Correct! Current score: {score}")
        account_a = account_b
        account_b = random.choice(data)
        while account_a == account_b:
            account_b = random.choice(data)
    else:
        print(f"\n❌ Wrong! Final score: {score}")
        print(f"A had {account_a['followers']:,} followers.")
        print(f"B had {account_b['followers']:,} followers.")
        game_should_continue = False
        print(f"A has {account_a['followers']:,} followers.")
        print(f"B has {account_b['followers']:,} followers.")
