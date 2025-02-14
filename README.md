# job-market-insights
This Python project analyzes job market trends using data from an csv database. It provides insights into top hiring industries, salary trends, interview success rates, and demand for specific skills

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load job applications data from CSV (assuming a local file)
df = pd.read_csv("job_applications.csv")

# Top Hiring Industries
industry_counts = df.groupby("industry")["application_id"].count().reset_index()
industry_counts = industry_counts.sort_values(by="application_id", ascending=False)

# Average Salary by Industry
salary_analysis = df.groupby("industry")["salary_offer"].mean().reset_index()
salary_analysis = salary_analysis.sort_values(by="salary_offer", ascending=False)

# Plot Job Applications per Industry
plt.figure(figsize=(10, 5))
sns.barplot(data=industry_counts, x="industry", y="application_id", palette="coolwarm")
plt.xticks(rotation=45)
plt.title("Top Hiring Industries")
plt.xlabel("Industry")
plt.ylabel("Number of Applications")
plt.show()

# Plot Salary Distribution by Industry
plt.figure(figsize=(10, 5))
sns.boxplot(data=df, x="industry", y="salary_offer", palette="viridis")
plt.xticks(rotation=45)
plt.title("Salary Distribution by Industry")
plt.xlabel("Industry")
plt.ylabel("Salary Offer")
plt.show()

# Save results to CSV
industry_counts.to_csv("industry_hiring_trends.csv", index=False)
salary_analysis.to_csv("salary_analysis.csv", index=False)

print("Analysis completed and CSV files saved.")

