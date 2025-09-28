import pandas as pd
#load dataset
url = "https://www.dropbox.com/scl/fi/d5v08knbo3gha4xn2a44h/student_wellbeing_dataset.csv?rlkey=72iirijqpk6g2290myzng7pvi&st=kwwvfj6i&dl=1"
df = pd.read_csv(url)
print("✅ Dataset loaded successfully")
print("Columns in dataset:", df.columns.tolist())
print(df.head())
#column names
df.columns = df.columns.str.strip().str.replace(" ", "_").str.lower()
print("\n✅ Normalized column names:", df.columns.tolist())
#duplicates and missing values
df.drop_duplicates(inplace=True)
for col in df.columns:
    if df[col].dtype == "object":
        df[col].fillna(df[col].mode()[0], inplace=True)
    else:
        df[col].fillna(df[col].mean(), inplace=True)
#categories
df_encoded = df.copy()
for col in df_encoded.select_dtypes(include="object").columns:
    df_encoded[col] = df_encoded[col].astype("category").cat.codes
print("\n✅ Encoded dataset preview:")
print(df_encoded.head())
print("\n📊 Correlation with CGPA:")
print(df_encoded.corr()["cgpa"].sort_values(ascending=False))
#save 
df.to_csv("students_cleaned.csv", index=False)
print("\n✅ Cleaned dataset saved as 'students_cleaned.csv'")
