# My data analysis practice
## Dataset used: https://huggingface.co/datasets/lukebarousse/data_jobs
## Project 1. Most demanded skills for most in-demand job roles in the US

I tried discovering the most demanded skills for the top 3 most demanded software engineering roles in the United States. These insights could help users understand what skills they should focus on for maximum chances of getting hired.

View the associated notebook here:  
[top_demanded_skills_p1.ipynb](Project\top_demanded_skills_p1.ipynb)

### Code snippet:

```python
fig,ax = plt.subplots(3,1)
for i, job in enumerate(top_3_jobs):
    df_subset = df_US_true_final[df_US_true_final['job_title_short'] == job]
    sns.barplot(data=df_subset, 
        x='percentage_of_jobs_with_skill', 
        y='job_skills', 
        ax=ax[i], 
        hue='skill_count',
        legend=False
    )
    ax[i].set_title(job)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].set_xlim(0,80)
    for n, v in enumerate(df_subset['percentage_of_jobs_with_skill']):
        ax[i].text(v+1, n, v, va='center')
    if(i != len(top_3_jobs)-1):
        ax[i].set_xticks([])

plt.tight_layout()
plt.show()
```
### Results
![Visualization of top skills for top AIML roles](Project\project1\output.png)

### Insights

#### 1. Universal Skills
- **SQL**: High demand across all roles (50.8%–68.3%).
- **Python**: Essential for Data Scientist (72%) & Data Engineer (64.9%), moderate for Analyst (27.1%).

#### 2. Role-Specific Trends
- **Data Analyst**: Strong need for **Excel** (40.6%) and **Tableau** (28.5%) — reporting & BI focus.
- **Data Scientist**: Heavy emphasis on **Python**, **R** (44.2%), and statistical tools (**SAS**).
- **Data Engineer**: Strong cloud/tool skills — **AWS** (42.8%), **Azure** (32.3%), **Spark** (32%).

#### 3. Specialization vs Overlap
- Analysts lean on **BI & reporting tools**; less programming-intensive.
- Scientists focus on **programming + statistical analysis**.
- Engineers focus on **data pipelines, cloud, and big data tech**.

#### 4. Strategic Skill Growth
- Learning **SQL + Python** provides strong cross-role opportunities.
- Role-specific boosts:
  - Analyst → Tableau, Excel
  - Scientist → R, SAS
  - Engineer → AWS, Spark, Azure

### Libraries Used

```python
from datasets import load_dataset
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import ast
```

