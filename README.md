# Import necessary modules
from flask import Flask, render_template, request

# Initialize Flask app
app = Flask(__name__)

# Define word categories
categories = {
    "movies": ["avatar", "titanic", "inception"],
    "animals": ["elephant", "tiger", "giraffe"],
    "countries": ["usa", "canada", "japan"]
}

# Function to select a word from the chosen category
def select_word(category):
    return random.choice(categories[category])

# Routes
@app.route('/')
def index():
    return render_template('index.html', categories=categories.keys())

@app.route('/play', methods=['POST'])
def play():
    category = request.form.get('category')
    word = select_word(category)
    # Initialize game state
    # Render game template with initial state
    return render_template('game.html', word=word, category=category, max_attempts=6)

# Other routes for handling game logic, such as submitting guesses

if __name__ == '__main__':
    app.run(debug=True)
