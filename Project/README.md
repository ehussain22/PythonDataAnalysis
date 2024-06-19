# Analysis

## What are the most in demand skills for the top 3 jobs in data

Firstly, I had to identify the top 3 roles which were Data Analyst, Data Engineer and Dats scientist and then used pandas and other python libraries to extract data to discover the top 5 most valuable skills to obtain for each role which can viewed here:
[Skill_Demand.ipynb](Project\Skills_Demand.ipynb)

### Visualise The Data


```
python 
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percentage[df_skills_percentage['job_title_short']== job_title].head(5)
    sns.barplot(data=df_plot, x ='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:g_r')
    ax[i].set_title(job_title)
    ax[i].invert_yaxis()
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].get_legend().remove()
    ax[i].legend().set_visible(False)

fig.suptitle('percentage of top skills used in vacancies', fontsize = 12)
fig.tight_layout(h_pad=0.5)
plt.show()
```

### Results

![Top Skills for each role](Project\images\skills_demand_distribution.png)

### Insights

The analysis reveals that SQL and Python are the most critical skills across Data Analyst, Data Engineer, and Data Scientist roles, with SQL being particularly dominant for Analysts and Engineers, and Python being essential for Engineers and Scientists. For Data Analysts, Excel and Power BI are also important, along with Tableau, though to a lesser extent. Data Engineers value cloud technologies like Azure and AWS, as well as Spark. Data Scientists, in addition to Python and SQL, require knowledge of R, with AWS and Azure being somewhat relevant. Overall, SQL and Python are the top skills, with specific tools and technologies varying by role.

### How are data skills trending in the UK?

### Data visualisation

[Skills_Trend.ipynb](Project\Skills_Trend.ipynb)

```
from matplotlib.ticker import PercentFormatter

df_plot = df_DE_UK_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')
sns.set_theme(style='ticks')
sns.despine() # remove top and right spines

plt.title('Trending Top Skills for Data Analysts in the UK')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

# annotate the plot with the top 5 skills using plt.text()
for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i], color='black')

plt.show()
```

### Visualisation 
![SkillsTrendIntheUK](Project\images\skillstrend.png)

### Insights

 SQL consistently leads with a high demand, peaking above 50% in June and remaining around 40-50% throughout the year. Excel follows closely, maintaining a steady demand around 40-45%, with a slight decline towards December. Python shows a rising trend, starting at around 20% in January and peaking at 35% in July and September. Power BI and Tableau have lower and more variable demand, both fluctuating around 15-25%, with noticeable peaks for Power BI in September and for Tableau in December. Overall, SQL and Excel are the most consistently demanded skills, with Python gaining prominence mid-year, while Power BI and Tableau have more sporadic demand.