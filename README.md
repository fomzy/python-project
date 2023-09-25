# python-project
basic python project
import requests

# Define the URLs for each category
love_url = "https://api.quotable.io/quotes?tags=love%7Chappiness"
famous_url = "https://api.quotable.io/quotes?tags=technology,famous-quotes"

# Define the list of categories
inspire_me = ["Love", "Happiness", "Famous quotes", "Technology", "Wisdom"]

# Print the list of categories
for subjects in inspire_me:
    print(subjects)

# Ask user what they want to be inspired by today
input_inspiration = input("Hi! Please choose from the list what you want to be inspired by: ")

# Determine which URL to use based on user input
if input_inspiration in ["Love", "Happiness"]:
    request_url = love_url
else:
    request_url = famous_url

# Get data from web API and handle errors
try:
    response = requests.get(request_url)
    response.raise_for_status()
except requests.exceptions.RequestException as e:
    print(f"An error occurred: {e}")
    exit()

# Convert the JSON data object to a python friendly format
data = response.json()

# Go through each item in the data list and print content and author
for item in data['results']:
    print(item['content'])
    print(f"Author: {item['author']}")
    print("------")
