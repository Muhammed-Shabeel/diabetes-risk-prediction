Diabetes Risk Prediction

Predicts whether a patient is likely to have diabetes from basic health measurements, using logistic regression in Python.

Result: 75.3% accuracy on a held-out test set, against a 64.3% baseline for always guessing "no diabetes". The model catches 35 of 55 diabetic cases (64% recall).

Team project, done for a internship task at IHRD chelakkara, Calicut University. My part: developing the logic of the code and testing it's correctness

The problem

Diabetes is easier to manage when it's caught early. Can a simple model flag high-risk patients from a few routine measurements?

Data
Source:https://www.kaggle.com/datasets/mrsimple07/diabetes-prediction
Size: 768 patients, 8 input features, 1 label (Outcome: 1 = diabetic, 0 = not)
Balance: about 35% of patients are diabetic
Features: Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI, DiabetesPedigreeFunction, Age
Method
Explored the data with describe() and info(). No null values and no duplicate rows.
Found a data-quality problem: Glucose and BMI contain 0, which is not possible for a living patient. I replaced those zeros with the column median.
Chose 3 features: Glucose, BMI, Age, guided by a correlation heatmap.
Split the data 80/20 (614 train, 154 test), random_state=42.
Trained a LogisticRegression model with scikit-learn.
Evaluated on the test set with accuracy, a confusion matrix and a classification report.
Results
Metric	Value
Accuracy	75.3%
Baseline (always predict "no diabetes")	64.3%
Precision (diabetic)	0.66
Recall (diabetic)	0.64
F1 (diabetic)	0.65

Confusion matrix (154 test patients):

	Predicted: no	Predicted: yes
Actual: no	81	18
Actual: yes	20	35
Limitations
20 of 55 diabetic patients were missed. In a screening setting a missed case costs more than a false alarm, so recall matters more than accuracy here.
Only 3 of 8 features were used. Insulin, SkinThickness and BloodPressure also contain impossible zeros and were left out rather than cleaned.
One train/test split. With 154 test rows, the score could move noticeably on a different split.
No second model to compare against.
This is a learning project, not a medical tool.
Next steps
- Treat zeros in Insulin, BloodPressure and SkinThickness as missing values, then use all 8 features
- Add feature scaling
- Use 5-fold cross-validation
- Compare against Random Forest
- Report recall and ROC-AUC, and tune the decision threshold to catch more diabetic cases
Run it
bash
pip install pandas numpy matplotlib seaborn scikit-learn
Put diabetes.csv in the project folder.
Change the path in the pd.read_csv(...) cell. The notebook currently reads from /content/sample_data/diabetes.csv (Google Colab).
Run all cells in Diabetes_Prediction.ipynb.
Tech

Python · Pandas · NumPy · scikit-learn · Matplotlib · Seaborn

Team

Muhamed Salihe 

Muhammed Shabeel:www.linkedin.com/in/muhammed-shabeel-b34655327

Jinesh prakash

Abhishek Suresh


Contact

Muhammed Shabeel 

mshabeel46@gmail.com

www.linkedin.com/in/muhammed-shabeel-b34655327

