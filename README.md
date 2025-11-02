# 🩺 Chronic Disease Risk Prediction System  

 🚀 Overview  
Chronic Disease Risk Prediction System is a cloud-based, AI-driven healthcare platform that predicts the likelihood of developing chronic diseases such as diabetes or heart disease based on user inputs like age, BMI, blood pressure, and lifestyle habits.  

This project leverages **AWS serverless architecture** for data ingestion, transformation, and machine learning — making the process scalable, secure, and fully automated.  

---

## 🧠 Key Objectives
- Collect and process user data through a simple web interface.  
- Apply ML models to identify potential chronic disease risks.  
- Generate personalized preventive recommendations.  
- Deliver an end-to-end automated pipeline using AWS services.  

---

 ⚙️ System Architecture  

The system is designed as a serverless data pipeline  on AWS:
User Input (S3 Website Form)
↓
API Gateway → Lambda (Data Validation)
↓
DynamoDB (Raw Data Storage)
↓
Lambda (Parquet Conversion using PyArrow)
↓
S3 (Data Lake)
↓
AWS Glue (ETL + Preprocessing with PySpark)
↓
Amazon SageMaker (Model Training & Prediction)
↓
Lambda (Prediction & Recommendations)
↓
DynamoDB (Results)
↓
API Gateway (GET Request)
↓
Dashboard (Risk Level + Suggestions)

---

## 🧩 AWS Services Used

| Service | Purpose |
|----------|----------|
| **Amazon S3** | Hosts the front-end website and stores data files (raw + processed). |
| **Amazon API Gateway** | Handles HTTP requests between the front-end and back-end. |
| **AWS Lambda** | Executes data validation, conversion, and prediction logic. |
| **Amazon DynamoDB** | NoSQL database for storing user data and prediction results. |
| **AWS Glue** | Performs ETL (Extract, Transform, Load) operations using PySpark. |
| **Amazon SageMaker** | Trains and deploys the Random Forest Regressor model. |

---

## 🧮 Machine Learning Model

The ML component is built using **Random Forest Regressor** due to its robustness and interpretability.

### **Input Features**
- **Demographic Data:** `age`, `gender`, `height_cm`, `weight_kg`, `bmi`, `region`
- **Lifestyle Factors:** `smoking_status`, `alcohol_consumption`, `physical_activity_level`, `diet_quality`, `sleep_hours_per_day`, `stress_level`
- **Health Metrics:** `family_history`, `existing_conditions`, `blood_pressure_sys`, `blood_pressure_dia`, `cholesterol_level`, `glucose_level`

### **Output**
- **Predicted Risk Score (0–100)**  
- **Risk Level:** Low 🟢 / Medium 🟡 / High 🔴  
- **Personalized Recommendation**

---

## 🧰 Tech Stack

| Category | Tools |
|-----------|-------|
| **Frontend** | HTML, CSS, JavaScript |
| **Backend** | AWS Lambda, Python (boto3, pyarrow) |
| **Database** | Amazon DynamoDB |
| **ETL** | AWS Glue + PySpark |
| **Machine Learning** | Amazon SageMaker (Random Forest Regressor) |
| **Hosting** | Amazon S3 (Static Website) |
| **Monitoring** | CloudWatch Logs + IAM Roles |

---

## 🔄 Data Flow Summary

1. User submits data through a web form hosted on **Amazon S3**.  
2. **API Gateway** sends this data to **Lambda** for validation.  
3. The validated data is stored in **DynamoDB**.  
4. Another Lambda function converts the DynamoDB data into a **Parquet file** using **PyArrow**.  
5. The Parquet file triggers an **AWS Glue** job for cleaning and preprocessing.  
6. Processed data is sent to **Amazon SageMaker**, where the model predicts the disease risk.  
7. **Lambda** writes the prediction results back into **DynamoDB**.  
8. The front-end fetches results via **API Gateway (GET request)** and displays them on the dashboard.

---

 🧪 Model Evaluation
| Metric | Value |
|--------|--------|
| **R² Score** | 0.88 |
| **RMSE** | 0.09 |
| **MAPE** | < 8% |
| **Model Type** | Random Forest Regressor |

The model achieved strong predictive performance with balanced accuracy and interpretability.

---

 📊 Dashboard Output

The final dashboard displays:
- User’s **risk score**
- **Risk category** (Low, Moderate, High)
- Personalized **health recommendations**

---

 🔐 Security & Monitoring
- **IAM roles** with least-privilege access for each service.  
- **CloudWatch** monitors Glue, Lambda, and SageMaker logs.  
- **S3 bucket policies** enforce encryption and access control.  

---

 🔮 Future Enhancements
- Integration of **IoT-based health sensors** (e.g., Fitbit, smartwatch).  
- Implementation of **automated model retraining pipelines** using AWS Step Functions.  
- Development of a **mobile application** for real-time monitoring.  
- Expansion to multi-disease prediction using advanced ensemble models.  

---

 🧑‍💻 How to Run the Project

 **1️⃣ Front-End Setup**
- Upload `index.html` and `form.html` to an S3 bucket.  
- Enable static website hosting under S3 bucket **Properties**.  
- Note the public URL.

 **2️⃣ Backend Setup**
- Create **API Gateway** endpoints for `POST /submitData` and `GET /getPrediction`.  
- Connect them to respective **Lambda functions**.  
- Configure IAM roles for Lambda access to DynamoDB and S3.

 **3️⃣ Database and ETL**
- Create **DynamoDB** table for raw data.  
- Create another table for prediction results.  
- Set up **AWS Glue** job with S3 input and output paths.

 **4️⃣ ML Model Deployment**
- Use **SageMaker Notebook** to train and deploy the Random Forest Regressor model.  
- Store model artifact in S3 and deploy it as an endpoint.

**5️⃣ Test**
- Visit your S3 website URL.  
- Enter test data and click submit.  
- Check DynamoDB → Glue → SageMaker pipeline for workflow completion.  
- View prediction results on dashboard.

---

## 📚 References
This project leverages:
- [AWS Glue Documentation](https://docs.aws.amazon.com/glue/latest/dg/)
- [Amazon SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/)
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/)
- [Random Forest Algorithm - scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html)

---

## 📄 License
This project is open-source and available under the [MIT License](LICENSE).

---

## 💬 Acknowledgements
Special thanks to AWS Educate resources and SRM University for providing the academic and technical support required for this project.


