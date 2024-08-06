# Joke Finder

This is a simple Python script that retrieves and displays jokes based on a user-provided topic. It uses the `requests` library to interact with the [icanhazdadjoke API](https://icanhazdadjoke.com/) and the `pyfiglet` library to create a stylized header for the output.

## Features

- Install required packages
- Fetch jokes related to a user-specified topic
- Display the total number of jokes found and one random joke

## Installation

1. **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. **Install the required packages:**
    ```bash
    pip install requests pyfiglet termcolor
    ```

## Usage

1. **Run the script:**
    ```bash
    python joke_finder.py
    ```

2. **Enter a topic when prompted:**
    ```plaintext
    Let me tell you a joke : Give me a Topic
    ```

3. **View the joke:**
    - If jokes related to the topic are found, one will be displayed.
    - If no jokes are found, a message indicating so will be shown.

## Script Details

```python
import requests
import pyfiglet
from random import choice

header = pyfiglet.figlet_format("find a joke")
print(header)

term = input("Let me tell you a joke : Give me a Topic ")

response_json = requests.get("https://icanhazdadjoke.com/search", headers={"Accept": "application/json"}, params={"term":term}).json()

results = response_json["results"]
total_jokes = response_json["total_jokes"]

if total_jokes > 1:
    print(f"i've got {total_jokes} about {term} here is one of them", choice(results)["joke"])
elif total_jokes == 1:
    print(f"i've got one joke about {term}. here it is", results[0]["joke"])
else:
    print(f"sorry i don't have a joke about {term}")
