# Synthetic Patient Data Generator

### Project Overview

This repository contains a Python script developed to generate realistic, synthetic patient data. The purpose of this project is to create a reliable and repeatable source of data for:

* **Personal Practice:** Developing and testing data analysis and machine learning skills.
* **Application Testing:** Providing a realistic dataset to test software and applications without using sensitive, real-world information.
* **Portfolio Demonstration:** Showcasing data generation and data cleaning skills.

### Repository Contents

* `generate_data.py`: The Python script for generating the data.
* `synthetic_patient_data.csv`: A small, sample dataset produced by the script.

### How to Use the Script

To use this script, you first need to have Python and the necessary libraries installed.

```bash
pip install pandas numpy faker

Once you have the script, you can run it from your terminal to generate a new dataset:

python generate_data.py

You can easily change the size of the dataset by modifying the num_records variable at the top of the script.

Understood. I will help you prepare the project for a private GitHub repository. A private project is perfect for personal use, for building a portfolio, or for a specific team.

The tone will be more like a personal notebook or a professional project for your own use.

### **Step 1: The Project Description (for your README.md file)**

This is the narrative that will describe your project's purpose. It's written as if you are documenting the project for yourself or a small, private audience.

**Instructions:** Copy and paste the entire text below into the `README.md` file when you create your new private repository.

````markdown
# Synthetic Patient Data Generator

### Project Overview

This repository contains a Python script developed to generate realistic, synthetic patient data. The purpose of this project is to create a reliable and repeatable source of data for:

* **Personal Practice:** Developing and testing data analysis and machine learning skills.
* **Application Testing:** Providing a realistic dataset to test software and applications without using sensitive, real-world information.
* **Portfolio Demonstration:** Showcasing data generation and data cleaning skills.

### Repository Contents

* `generate_data.py`: The Python script for generating the data.
* `synthetic_patient_data.csv`: A small, sample dataset produced by the script.

### How to Use the Script

To use this script, you first need to have Python and the necessary libraries installed.

```bash
pip install pandas numpy faker
````

Once you have the script, you can run it from your terminal to generate a new dataset:

```bash
python generate_data.py
```

You can easily change the size of the dataset by modifying the `num_records` variable at the top of the script.

````

---

### **Step 2: The Final Script (`generate_data.py`)**

This is the complete and final script we built. It is ready for you to copy and save to a file named `generate_data.py`.

**Instructions:** Copy and paste the entire code block below into a text editor and save it as **`generate_data.py`**.

```python
import pandas as pd
import numpy as np
import random
from faker import Faker

# Step 1: Initial Setup and Libraries
# Change the number of records here to generate a larger dataset
num_records = 10
fake = Faker()
data = {}

# Step 2: Generating Patient ID
print("Step 2: Generating Patient IDs...")
data['PatientID'] = [f'P{str(i).zfill(6)}' for i in range(1, num_records + 1)]

# Step 3: Generating Patient Age
print("Step 3: Generating Age...")
ages = np.random.normal(loc=45, scale=20, size=num_records).astype(int)
data['Age'] = np.clip(ages, 0, 95)

# Step 4: Generating Patient Gender and Insurance Provider
print("Step 4: Generating Gender and Insurance Provider...")
data['Gender'] = random.choices(['Male', 'Female', 'Non-binary'], weights=[0.49, 0.50, 0.01], k=num_records)
data['InsuranceProvider'] = random.choices(['Blue Cross Blue Shield', 'Cigna', 'Medicaid', 'Medicare', 'None'], weights=[0.3, 0.2, 0.2, 0.1, 0.2], k=num_records)

# Step 5: Generating Patient Weight
print("Step 5: Generating Weight...")
data['Weight_kg'] = np.round(np.random.normal(loc=75, scale=15, size=num_records), 2)

# Step 6: Generating Blood Pressure
print("Step 6: Generating Blood Pressure...")
systolic_bp = np.random.normal(loc=120, scale=15, size=num_records)
diastolic_bp = (systolic_bp * 0.5) + np.random.normal(loc=20, scale=8, size=num_records)
data['SystolicBP'] = np.round(systolic_bp, 0).astype(int)
data['DiastolicBP'] = np.round(diastolic_bp, 0).astype(int)

# Step 7: Generating Health Conditions
print("Step 7: Generating Health Conditions...")
data['SmokerStatus'] = random.choices(['Yes', 'No'], weights=[0.2, 0.8], k=num_records)
data['HasAllergies'] = random.choices(['Yes', 'No'], weights=[0.2, 0.8], k=num_records)
chief_complaints = ['Fever', 'Cough', 'Chest Pain', 'Headache', 'Abdominal Pain', 'Fatigue']
data['ChiefComplaint'] = random.choices(chief_complaints, k=num_records, weights=[0.2, 0.2, 0.15, 0.15, 0.1, 0.2])
diagnosis_map = {
    'Fever': 'Infection',
    'Cough': 'Bronchitis',
    'Chest Pain': 'Angina',
    'Headache': 'Migraine',
    'Abdominal Pain': 'Gastritis',
    'Fatigue': 'Anemia',
}
data['PrimaryDiagnosis'] = [diagnosis_map.get(complaint, 'Unspecified') for complaint in data['ChiefComplaint']]

# Step 8: Generating Medication
print("Step 8: Generating Medication...")
medication_map = {
    'Hypertension': 'Lisinopril',
    'Diabetes': 'Metformin',
    'Asthma': 'Albuterol',
    'Angina': 'Nitroglycerin',
    'Infection': 'Penicillin',
    'Bronchitis': 'Amoxicillin',
    'Migraine': 'Ibuprofen',
    'Gastritis': 'Antacid',
    'Anemia': 'Iron Supplement',
}
medication_list = []
for diagnosis in data['PrimaryDiagnosis']:
    medication = medication_map.get(diagnosis, 'None')
    medication_list.append(medication)
data['Medication'] = medication_list

# Step 9: Generating Encounter and Administrative Data
print("Step 9: Generating Encounter and Administrative Data...")
data['DateOfVisit'] = [fake.date_between(start_date='2024-01-01', end_date='2024-12-31') for _ in range(num_records)]
department_names = ['General Surgery', 'Pediatrics', 'Orthopaedic', 'Dermatology', 'Internal Medicine']
data['DepartmentName'] = random.choices(department_names, k=num_records)
doctor_map = {
    'General Surgery': ['Dr. Alex Smith', 'Dr. Maria Garcia'],
    'Pediatrics': ['Dr. John Doe', 'Dr. Jane Miller'],
    'Orthopaedic': ['Dr. Michael Chen', 'Dr. Sarah Lee'],
    'Dermatology': ['Dr. David Brown'],
    'Internal Medicine': ['Dr. Lisa Jones', 'Dr. Robert Davis'],
}
doctor_list = []
for department in data['DepartmentName']:
    doctors_in_dept = doctor_map.get(department, ['Unknown Doctor'])
    chosen_doctor = random.choice(doctors_in_dept)
    doctor_list.append(chosen_doctor)
data['DoctorName'] = doctor_list

# Step 10: Create DataFrame and Save
print("\nStep 10: Creating a table and saving the file...")
df = pd.DataFrame(data)
df.to_csv('synthetic_patient_data.csv', index=False)
print(f'\nProcess Complete: Successfully generated and saved {num_records} patient records to synthetic_patient_data.csv')
````
