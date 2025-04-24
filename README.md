delivery-optimizer/
├── app.py                      # Backend Flask
├── optimisation.py             # Script d'optimisation
├── requirements.txt            # Dépendances Python
├── templates/
│   └── map.html               # Page web (frontend)
└── static/
    └── script.js              # JavaScript pour la carte
    from flask import Flask, render_template, jsonify, request
import os
from optimisation import optimize_delivery

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('map.html')

@app.route('/optimize', methods=['POST'])
def optimize():
    data = request.json
    route = optimize_delivery(data["locations"], data["demands"], data["vehicle_capacity"])
    return jsonify({"route": route})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=int(os.environ.get('PORT', 10000)))
