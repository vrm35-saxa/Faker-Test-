import streamlit as st
import pandas as pd
from faker import Faker
import random

fake = Faker()
Faker.seed(42)
random.seed(42)

@st.cache_data
def generate_patient_data(n=20):
    data = []
    for i in range(n):
        data.append({
            'Patient_ID': f'P{i+1:03d}',
            'Name': fake.name(),
            'Age': random.randint(18, 85),
            'Gender': random.choice(['Male', 'Female']),
            'Blood_Type': random.choice(['A+', 'A-', 'B+', 'B-', 'AB+', 'AB-', 'O+', 'O-']),
            'Diagnosis': random.choice(['Hypertension', 'Diabetes', 'Asthma', 'Arthritis', 'Migraine']),
            'Admission_Date': fake.date_between(start_date='-1y', end_date='today'),
            'Phone': fake.phone_number(),
            'City': fake.city()
        })
    return pd.DataFrame(data)

st.title('Healthcare Patient Dataset')
st.write('Sample dataset of 20 patients generated with Faker')

df = generate_patient_data(20)

st.dataframe(df, use_container_width=True)

st.subheader('Dataset Statistics')
col1, col2, col3 = st.columns(3)
col1.metric('Total Patients', len(df))
col2.metric('Avg Age', f"{df['Age'].mean():.1f}")
col3.metric('Gender Split', f"{(df['Gender']=='Male').sum()}M / {(df['Gender']=='Female').sum()}F")

st.subheader('Download Data')
csv = df.to_csv(index=False)
st.download_button('Download CSV', csv, 'patients.csv', 'text/csv')
