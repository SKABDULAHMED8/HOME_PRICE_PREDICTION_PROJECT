```markdown
# 🏠 Bengaluru House Price Prediction Project

A machine learning web application that predicts house prices in Bengaluru based on location, BHK, square footage, and bathrooms using a trained model and Flask.

---

## 📁 Project Directory Structure

```
BHP/
│
├── client/                        # (Optional) Web UI if used separately
│
├── model/                         # Model training and dataset
│   ├── Bengaluru_House_Data.csv
│   ├── Bengaluru_House_Data_csv.ipynb
│   ├── columns.json
│   └── banglore_home_prices_model.pickle
│
├── server/
│   ├── server.py
│   ├── util.py
│   ├── artifacts/
│   │   ├── banglore_home_prices_model.pickle
│   │   └── columns.json
│   ├── static/
│   │   ├── style.css
│   │   └── script.js
│   ├── templates/
│   │   └── index.html
│   └── __pycache__/
│
└── README.txt.txt
```

📸 *Visual Structure:*

![Project Structure](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/project.bhp.structure.PNG)

---

## ⚙️ Server Configuration: `server.py`

Ensure your `server.py` (inside `BHP/server/`) is configured properly:

```python
from flask import Flask, request, jsonify, render_template
import util

app = Flask(__name__, template_folder='templates')

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/predict_home_price', methods=['POST'])
def predict_home_price():
    total_sqft = float(request.form['total_sqft'])
    location = request.form['location']
    bhk = int(request.form['bhk'])
    bath = int(request.form['bath'])

    response = jsonify({
        'estimated_price': util.get_estimated_price(location, total_sqft, bhk, bath)
    })
    response.headers.add('Access-Control-Allow-Origin', '*')
    return response

if __name__ == "__main__":
    print("Starting Flask Server For Home Price Prediction>>>>")
    util.load_saved_artifacts()
    app.run()
```

✅ Ensure the model and `columns.json` are correctly located under `server/artifacts`.

---

## 🧾 Sample `index.html`

Place this file under `server/templates/index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Bangalore Home Price Prediction</title>
</head>
<body>
    <h1>Welcome to Bangalore Home Price Prediction</h1>
    <form action="/predict_home_price" method="post">
        <label for="total_sqft">Total Square Feet:</label>
        <input type="text" id="total_sqft" name="total_sqft"><br><br>

        <label for="location">Location:</label>
        <input type="text" id="location" name="location"><br><br>

        <label for="bhk">BHK:</label>
        <input type="text" id="bhk" name="bhk"><br><br>

        <label for="bath">Bathrooms:</label>
        <input type="text" id="bath" name="bath"><br><br>

        <input type="submit" value="Predict">
    </form>
</body>
</html>
```

---

## 🚀 How to Run the Server

1. Go to the `server/` directory:
```bash
cd server
```

2. Run the server:
```bash
python server.py
```

💡 Output Example:
![Running Server Command](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/cmd_run_server_bhp_1.PNG)

---

## 🌐 Web UI

🔗 Visit: [http://127.0.0.1:5000](http://127.0.0.1:5000)

### 🏠 Home Page
![Home Page UI](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/Capture_webpage_ui.PNG)

### 📝 Blog Page
![Blog UI](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/Capture_webpage_blogui.PNG)

### 👤 About Page
![About Page](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/cpture_about_ui.PNG)

---

## 📊 Dataset

- 📄 Filename: `Bengaluru_House_Data.csv`
- 📦 Zip: `Bengaluru_House_Data.zip` *(Extract before training)*

---

## 💡 Usage Steps

1. Unzip the dataset.
2. Ensure all paths are set correctly.
3. Run the server (`python server.py`).
4. Open your browser and visit `http://localhost:5000`.

---

## 👨‍💻 Developer Info

- ✍️ Shaik Abdul Ahmed  
- 🌐 [GitHub](https://github.com/SKABDULAHMED8) | [LinkedIn](https://www.linkedin.com/in/abdul-ahmed-shaik-61447a257)

---

⭐ **Star the repository** if you found this helpful!
```
