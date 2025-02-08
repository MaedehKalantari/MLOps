### **California Housing Price Prediction API**  

This project builds a **FastAPI-based web application** that serves a trained **regression model** for predicting California house prices. The application allows users to submit house features via **URL parameters** and receive a predicted price displayed in a **popup window** on a webpage.  

## **Project Overview**  
- **Frontend:** A webpage (`popup_template.html`) that displays predictions in a **popup window**.  
- **Backend:** A **FastAPI-based API** (`app.py`) that loads the trained model and serves predictions.  
- **Model:** A regression model trained on the **California Housing Dataset** using **Scikit-Learn**.  
- **Deployment:** Uses **Uvicorn** for running FastAPI asynchronously.  

## **1. Dataset & Model**  
The **California Housing Dataset** is a well-known dataset in machine learning that contains **housing price data** from California districts. The dataset includes features like:  
- **MedInc** – Median income in the district  
- **HouseAge** – Median house age  
- **AveRooms** – Average number of rooms per household  
- **AveOccup** – Average number of occupants per household  
- **Latitude & Longitude** – Geographical location  

### **Model Training**  
The regression model was trained using **Scikit-Learn**. The workflow includes:  
1. **Data Preprocessing**: Handling missing values, feature scaling, and train-test split.  
2. **Model Selection**: A simple regression model (e.g., `RandomForestRegressor` or `LinearRegression`) was trained.  
3. **Model Saving**: The trained model and feature transformation pipeline were saved as `.pkl` files using `joblib.dump()`.  

## **2. Application Architecture**  

### **Frontend (popup_template.html)**  
- A webpage with **CSS and JavaScript** to trigger a **popup window** for showing predictions.  
- Uses **Jinja2** to dynamically update the webpage with model predictions.  

### **Backend (FastAPI - app.py)**  
1. **Initialize FastAPI** to handle API requests.  
2. **Load the trained model** and feature transformation pipeline.  
3. **Set up Jinja2** for rendering the webpage.  
4. **Define a GET API endpoint (`/predict`)** to receive user inputs and return predictions.  
5. **Run the API using Uvicorn** for fast asynchronous processing.  

---

## **3. Installation & Setup**  

### **Prerequisites**  
Ensure you have Python **3.8+** installed and install the required dependencies:  

```bash
pip install fastapi uvicorn joblib scikit-learn jinja2
```

### **Run the API**  
Start the FastAPI application with Uvicorn:  
```bash
uvicorn app:app --reload
```

### **Accessing the Web App**  
Once running, open your browser and navigate to:  
```plaintext
http://localhost:8000
```

### **Making Predictions via API**  
To make a prediction, send a GET request with house features as **URL parameters**:  
```plaintext
http://localhost:8000/predict?MedInc=8.0&HouseAge=30&AveRooms=5.0
```
The predicted price will be displayed in a popup window on the webpage.  

---

## **4. Project Structure**  
```
📂 project-folder  
│── app.py                  # FastAPI backend  
│── popup_template.html      # Frontend with popup  
│── model.pkl                # Trained regression model  
│── features.pkl             # Feature transformation pipeline  
│── README.md                # Project documentation  
```

---

## **5. Future Improvements**  
- **Improve Model Performance**: Use advanced regression techniques (e.g., XGBoost, LSTM for time-series housing data).  
- **Add User Input Form**: Allow manual input instead of only URL-based requests.  
- **Deploy to Cloud**: Host the API using **Docker + AWS/GCP** for real-world use.  
