# iris_classifier

This project trains a machine learning model on the **Iris dataset**, converts it into a **pickle file**, and deploys a **Flask web application** that allows users to input data and get predictions. The app consists of two webpages:  
1. **index.html** – User enters input features.  
2. **result.html** – Displays prediction results.

---

## 🚀 Project Workflow  
1. **Train a model** on the Iris dataset.  
2. **Convert the model** into a pickle file (`iris_classifier.pkl`).  
3. **Create a Flask API** (`app.py`) to serve predictions.  
4. **Develop HTML templates** (`index.html`, `result.html`) inside the `templates/` folder.  
5. **Deploy to GitHub** (`iris_classifier` repository).  
6. **Deploy on Heroku** (connect GitHub and Heroku for live hosting).  

---

## 🛠️ Installation & Setup  
### **1️⃣ Clone the Repository**  
```bash
git clone https://github.com/YOUR_USERNAME/iris_classifier.git
cd iris_classifier
```

### **2️⃣ Install Dependencies**  
Make sure you have Python installed, then run:  
```bash
pip install flask scikit-learn pandas numpy gunicorn
```

### **3️⃣ Train and Save the Model**  
Run the following script to train the model and create `iris_classifier.pkl`:  
```python
import pickle
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris

# Load dataset
iris = load_iris()
X, y = iris.data, iris.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

# Save model
with open("iris_classifier.pkl", "wb") as file:
    pickle.dump(model, file)

print("Model saved as iris_classifier.pkl")
```

### **4️⃣ Run the Flask Web App**  
```bash
python app.py
```
Then, open your browser and go to:  
```
http://127.0.0.1:5000
```

---

## 📁 Project Structure  
```
iris_classifier/
│── templates/
│   ├── index.html       # User input page
│   ├── result.html      # Prediction result page
│── app.py               # Flask API
│── iris_classifier.pkl  # Trained model
│── requirements.txt     # Dependencies
│── README.md            # Project Documentation
```

---

## 🌐 Deployment (GitHub & Heroku)  
### **1️⃣ Push Project to GitHub**
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/iris_classifier.git
git push -u origin main
```

### **2️⃣ Deploy to Heroku**
1. Create a **Heroku account** at [https://www.heroku.com](https://www.heroku.com).  
2. Install Heroku CLI:  
   ```bash
   curl https://cli-assets.heroku.com/install.sh | sh
   ```
3. Login to Heroku:  
   ```bash
   heroku login
   ```
4. Create a Heroku app:  
   ```bash
   heroku create iris-classifier-app
   ```
5. Add a **Procfile** for deployment:  
   ```
   web: gunicorn app:app
   ```
6. Deploy to Heroku:  
   ```bash
   git push heroku main
   ```

---

## 🎯 Usage  
1. Open the **Flask app** in your browser.  
2. Enter feature values for the Iris dataset.  
3. Click **Submit**, and the prediction result will be displayed on `result.html`.  

---

## 📌 Technologies Used  
- **Python** (Flask, Scikit-learn, Pandas, NumPy)  
- **Flask** (for web API)  
- **Pickle** (for saving the model)  
- **HTML/CSS** (for web pages)  
- **Heroku** (for deployment)  
