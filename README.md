# Adela-Pecena-Engeto-Projekt_Textovy-Analyzator
projekt_1.py: první projekt do Engeto Online Python Akademie autor: Adéla Pečená email: adela.pecena@email.cz discord: Adéla Pečená#5431

"""
projekt_1.py: první projekt do Engeto Online Python Akademie
autor: Adéla Pečená
email: adela.pecena@email.cz
discord: Adéla Pečená#5431
"""


# Registrovaní uživatelé a jejich hesla
registered_users = {
    "bob": "123",
    "ann": "pass123",
    "mike": "password123",
    "liz": "pass123"
}

# Texty k analýze
TEXTS = ['''
Situated about 10 miles west of Kemmerer,
Fossil Butte is a ruggedly impressive
topographic feature that rises sharply
some 1000 feet above Twin Creek Valley
to an elevation of more than 7500 feet
above sea level. The butte is located just
north of US 30N and the Union Pacific Railroad,
which traverse the valley. ''',
'''At the base of Fossil Butte are the bright
red, purple, yellow and gray beds of the Wasatch
Formation. Eroded portions of these horizontal
beds slope gradually upward from the valley floor
and steepen abruptly. Overlying them and extending
to the top of the butte are the much steeper
buff-to-white beds of the Green River Formation,
which are about 300 feet thick.''',
'''The monument contains 8198 acres and protects
a portion of the largest deposit of freshwater fish
fossils in the world. The richest fossil fish deposits
are found in multiple limestone layers, which lie some
100 feet below the top of the butte. The fossils
represent several varieties of perch, as well as
other freshwater genera and herring similar to those
in modern oceans. Other fish such as paddlefish,
garpike and stingray are also present.'''
]

# Funkce pro analýzu textu
def analyze_text(text):
    words = text.split()
    word_lengths = [len(word.strip(".,!?")) for word in words]

    word_count = len(words)
    titlecase_count = sum(1 for word in words if word.istitle())
    uppercase_count = sum(1 for word in words if word.isupper())
    lowercase_count = sum(1 for word in words if word.islower())

    numeric_count = 0
    numeric_sum = 0
    for word in words:
        if word.isnumeric():
            numeric_count += 1
            numeric_sum += int(word)

    word_length_counts = {}
    for length in word_lengths:
        if length not in word_length_counts:
            word_length_counts[length] = 0
        word_length_counts[length] += 1

    return word_count, titlecase_count, uppercase_count, lowercase_count, numeric_count, numeric_sum, word_length_counts

# Hlavní část programu
username = input("username: ")
password = input("password: ")

if username in registered_users and registered_users[username] == password:
    print("----------------------------------------")
    print(f"Welcome to the app, {username}")
    print(f"We have {len(TEXTS)} text{'s' if len(TEXTS) > 1 else ''} to be analyzed.")
    print("----------------------------------------")

    try:
        selected_text = int(input("Enter a number btw. 1 and 3 to select: "))
        if selected_text < 1 or selected_text > len(TEXTS):
            print("Invalid input. Program will terminate.")
        else:
            selected_text -= 1
            text_to_analyze = TEXTS[selected_text]
            word_count, titlecase_count, uppercase_count, lowercase_count, numeric_count, numeric_sum, word_length_counts = analyze_text(text_to_analyze)

            print("----------------------------------------")
            print(f"There are {word_count} words in the selected text.")
            print(f"There are {titlecase_count} titlecase words.")
            print(f"There are {uppercase_count} uppercase words.")
            print(f"There are {lowercase_count} lowercase words.")
            print(f"There are {numeric_count} numeric strings.")
            print(f"The sum of all the numbers {numeric_sum}")
            print("----------------------------------------")

            print("LEN|  OCCURRENCES  |NR.")
            for length, count in sorted(word_length_counts.items()):
                print(f"{length:2}|{'*' * count}|{count}")

    except ValueError:
        print("Invalid input. Program will terminate.")

else:
    print("Unregistered user, terminating the program..")

