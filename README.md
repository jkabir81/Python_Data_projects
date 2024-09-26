# The Analysis

## 1. What are the most in-demand skills for the top 3 most popular data related roles in the US?

To find the most demanded skills for the top 3 most popular data roles. i filtered out the the most popular roles and then got the top skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skill you should pay attention to depending on the role you are targeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](project\2_Skill_Demand.ipynb)


### Visualize Data
```python
fig, ax = plt.subplots(len(job_titles),1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc["job_title_short"] == job_title].head(5)
    sns.barplot(data=df_plot, x="skill_percent", y="job_skills", ax=ax[i], hue="skill_count", palette="dark:b_r")

plt.show()
```
### Results

![Visualization of Top Skills for Data Jobs in the US](project/Images/skill_demand%20_for_top_data_roles.png)

### Insights
Key Findings:

Data Analyst: SQL and Excel are the most in-demand skills, followed by Tableau, Python, and SAS.

Data Engineer: SQL and Python are the most requested skills, with AWS, Azure, and Spark also being significant.

Data Scientist: Python is the most sought-after skill, followed by SQL, R, SAS, and Tableau.

Overall SQL and Python are essential for all three roles, but the specific emphasis on each skill varies depending on the job's requirements.

## 2. How are in-demand skills trending for Data Scientists?

### Visualize Data

```python
df_plot = df_DS_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette="tab10")
for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])

plt.tight_layout()
plt.show()
```

### Results
![Trend of Top Skills for Data Scientists in the US](project\Images\Trend_of_Top_Skills_for_Data_Scientists.png)

### Insights

The data reveals a clear trend towards programming languages (Python and R) and data manipulation tools (SQL) as the core skills for data scientists. While the demand for data visualization tools like Tableau has remained relatively stable, there's a growing appreciation for R's capabilities in statistical analysis. This suggests that data scientists are increasingly expected to not only extract insights from data but also communicate them effectively and perform advanced statistical modeling.


## 3. How well do the top Data Roles pay?

### visualize Data

```python
job_order = df_US_top6.groupby("job_title_short")["salary_year_avg"].median().sort_values(ascending=False).index

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
### Results
![Salary Distribution Of Top Data Jobs in the US](project\Images\Salary_Analysis_of_Top_Data_jobs.png)


### Insights
Key Findings:

Senior Roles Command Higher Salaries: As expected, senior roles generally have higher median salaries and wider ranges, reflecting the increased experience, expertise, and responsibilities associated with these positions.

Data Scientists and Engineers Have Similar Salary Ranges: While the median salaries may differ slightly, the overall salary ranges for data scientists and engineers are comparable, suggesting that both roles are valued similarly in the market.

Data Analysts Have Lower Salaries: Data analysts typically have lower salaries compared to scientists and engineers, reflecting the more entry-level nature of the role and the narrower range of responsibilities.

