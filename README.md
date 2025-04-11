
### Project Directory Structure
BHP/
│
├── client/                        # (Optional) Could be ignored if not in use
│
├── model/                         # Jupyter and model training files
│   ├── Bengaluru_House_Data.csv   # Dataset used for training
│   ├── Bengaluru_House_Data_csv.ipynb  # Notebook for preprocessing and model building
│   ├── columns.json               # JSON containing the features used by model
│   └── banglore_home_prices_model.pickle  # Trained model file
│
├── server/
│   ├── server.py                  # Main Flask server file
│   ├── util.py                    # Utility functions: prediction logic, loading model
│   ├── artifacts/                 # Duplicate of model and columns.json (used by server)
│   │   ├── banglore_home_prices_model.pickle
│   │   └── columns.json
│   ├── static/                    # CSS & JS files
│   │   ├── style.css
│   │   └── script.js
│   ├── templates/                # HTML files
│   │   └── index.html
│   └── __pycache__/              # Auto-generated Python cache (can ignore)
│
└── README.txt.txt                # (Optional) Notes or instructions


### Ensure `server.py` in `BHP/server` is configured properly

```python
from flask import Flask, request, jsonify, render_template
import util

app = Flask(__name__, template_folder='../artifacts/templates')

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

### Verify the presence of `index.html`
Ensure that the `index.html` file exists in the `BHP/artifacts/templates` directory.

### Example content of `index.html`

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

### Running the Flask server
Ensure you're in the `server` directory and run the server using:

```sh
python server.py
```

With the correct structure and files in place, your Flask server should start without issues, and you should be able to access the `index.html` template by navigating to `http://127.0.0.1:5000` in your web browser.


```markdown
# Bengaluru House Price Prediction Project

## Project Structure

Here’s an overview of the project structure:

![Project Structure](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/project.bhp.structure.PNG)

## Running the Server

To run the server, use the following command:

```bash
python server.py
```

![Running Server Command](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/cmd_run_server_bhp_1.PNG)

## Server Running Confirmation

You should see an output similar to this:

![Server Running Output](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/cmd_run_server_bhp_1.PNG)

## User Interface

### Home Page

This is what the home page looks like:

![Home Page UI](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/Capture_webpage_ui.PNG)

### Blog UI

Here's the blog UI capture:

![Blog UI](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/Capture_webpage_blogui.PNG)

### About Page

This is the about page:

![About Page](https://github.com/SKABDULAHMED8/HOME_PRICE_PREDICTION_PROJECT/blob/main/cpture_about_ui.PNG)

## Data

The project uses data from Bengaluru. The dataset is available in `Bengaluru_House_Data.zip`.

## Usage

1. Unzip `Bengaluru_House_Data.zip`.
2. Run `server.py` to start the server.
3. Open your browser and navigate to `http://localhost:5000`.
```
