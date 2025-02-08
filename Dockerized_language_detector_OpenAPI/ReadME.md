# **Language Detection API (FastAPI + Docker)**  

This project builds a **language detection API** using **FastAPI**. The trained **machine learning model** detects the language of a given text and is served via a RESTful API. The API is further **dockerized** for easy deployment on any server.  

## **1. Project Overview**  
- **Model Training:** A language detection model was trained and saved as a **pickle file (`.pkl`)**.  
- **API Development:** The trained model is served via a **FastAPI-based REST API**.  
- **Deployment:** The API is **dockerized** and can be deployed on any server.  

## **2. Model Training**  
The language detection model was trained using **Scikit-Learn** with the following steps:  
1. **Dataset Collection**: A multilingual dataset was used to train the model.  
2. **Text Preprocessing**: Tokenization, vectorization (e.g., TF-IDF), and feature extraction.  
3. **Model Training**: A classification model (e.g., `LogisticRegression`, `RandomForestClassifier`, or `Naïve Bayes`) was trained.  
4. **Model Saving**: The trained model was saved using `joblib.dump()` into a **pickle (`.pkl`) file**.  

## **3. API Development (FastAPI)**  
A **FastAPI server** was created to handle language detection requests:  
- **Endpoint:** `POST /predict`  
- **Input:** JSON containing text for language detection  
- **Output:** Predicted language  

### **API Workflow**  
1. **Initialize FastAPI** application (`app.py`).  
2. **Load the trained model** from the pickle file.  
3. **Define API endpoint** to receive text and return the predicted language.  
4. **Run API using Uvicorn** for asynchronous handling.
   
## **4. Dockerizing the API**  
The API is containerized using **Docker** for easy deployment.  

### **Dockerfile**  
```dockerfile
# Use official Python image
FROM python:3.8

# Set working directory
WORKDIR /app

# Copy project files
COPY requirements.txt ./
COPY app.py ./
COPY model.pkl ./

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose API port
EXPOSE 8000

# Run FastAPI server
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

### **Building & Running the Docker Container**  
1. **Build the Docker image:**  
   ```bash
   docker build -t language-detector-api .
   ```
2. **Run the container:**  
   ```bash
   docker run -p 8000:8000 language-detector-api
   ```
3. **Access the API at:**  
   ```plaintext
   http://localhost:8000/docs
   ```

## **5. API Usage**  

### **Send a Request to the API**  
To detect the language of a text, send a `POST` request:  

#### **Example Request (Using `curl`)**  
```bash
curl -X 'POST' 'http://localhost:8000/predict' \
     -H 'Content-Type: application/json' \
     -d '{"text": "Bonjour, comment ça va ?"}'
```

#### **Example Response**  
```json
{
  "language": "French"
}
```

---

## **6. Project Structure**  
```
📂 language-detector-api  
│── app.py                 # FastAPI application  
│── model.pkl              # Trained language detection model  
│── Dockerfile             # Docker configuration  
│── requirements.txt       # Python dependencies  
│── README.md              # Project documentation  
```

## **7. Deployment on a Server**  
Once the container is built, it can be deployed on a **cloud server** using:  
```bash
docker run -d -p 80:8000 --restart=always language-detector-api
```
This will run the API in the background and restart automatically if the server restarts.  

## **8. Future Improvements**  
- **Enhance Model Accuracy**: Use deep learning (e.g., LSTMs, transformers) for better language detection.  
- **Multi-Language Support**: Expand the dataset to include more languages.  
- **Rate Limiting & Security**: Implement authentication and request limits for production use.
  
