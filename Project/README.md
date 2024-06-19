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

![Top Skills for each role](https://github.com/ehussain22/PythonDataAnalysis/blob/main/Project/images/skills_demand_distribution.png)

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
![SkillsTrendIntheUK](https://github.com/ehussain22/PythonDataAnalysis/blob/main/Project/images/skillstrend.png)

### Insights

 SQL consistently leads with a high demand, peaking above 50% in June and remaining around 40-50% throughout the year. Excel follows closely, maintaining a steady demand around 40-45%, with a slight decline towards December. Python shows a rising trend, starting at around 20% in January and peaking at 35% in July and September. Power BI and Tableau have lower and more variable demand, both fluctuating around 15-25%, with noticeable peaks for Power BI in September and for Tableau in December. Overall, SQL and Excel are the most consistently demanded skills, with Python gaining prominence mid-year, while Power BI and Tableau have more sporadic demand.

 ### Salary analysis between top data roles 

 ```Python

 sns.boxplot(data=df_UK_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')
sns.despine()
plt.title('Salary Distributions of Data Jobs in the UK')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000) 
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

## Visualisation

![Box plot for data job salaries](Project\images\salaryanalysisboxplot.png)

## Insights

The boxplot presents the salary distributions for various data job titles in the UK, expressed in yearly salary (USD). Senior Data Scientists have the highest salary range with a median around $200K and substantial variability, indicated by a wide interquartile range (IQR) and numerous outliers extending up to $500K. Senior Data Engineers also command high salaries with a median slightly above $150K, a smaller IQR than Senior Data Scientists, but still significant outliers reaching up to $250K. Senior Data Analysts have a median salary close to $120K and a moderate IQR, with outliers approaching $200K. Data Engineers show a median salary near $110K and a relatively tight IQR, indicating less variability in pay but notable outliers beyond $200K. Data Scientists have a median salary just under $100K, with a wider IQR than Data Engineers, suggesting more variability and outliers exceeding $200K. Data Analysts have the lowest median salary around $70K, with a narrow IQR and fewer outliers, the highest salaries reaching slightly above $100K. Overall, senior positions in data science and engineering command significantly higher salaries with more variability and higher potential outliers compared to non-senior roles. The median salaries decrease from senior to junior positions, highlighting a clear hierarchical structure in salary distributions within the data jobs market in the UK.

### Highest paid and most in demand skills in the UK for data analysts

``` Python 
fig, ax = plt.subplots(2, 1)  

# Top 10 Highest Paid Skills for Data Analysts in UK
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')
ax[0].legend().remove()
# original code:
# df_DA_top_pay[::-1].plot(kind='barh', y='median', ax=ax[0], legend=False) 
ax[0].set_title('Highest Paid Skills for Data Analysts in the UK')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))


# Top 10 Most In-Demand Skills for Data Analysts')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')
ax[1].legend().remove()
# original code:
# df_DA_skills[::-1].plot(kind='barh', y='median', ax=ax[1], legend=False)
ax[1].set_title('Most In-Demand Skills for Data Analysts in the UK')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_xlim(ax[0].get_xlim())  # Set the same x-axis limits as the first plot
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

sns.set_theme(style='ticks')
plt.tight_layout()
plt.show()
```

### Visualisation 

![boxplots for skills demand and pay](Project\images\skillspaydemandboxplot.png)


### Which skills are the most optimal for data analyst roles in the UK

```Python

sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology'
)

sns.despine()
sns.set_theme(style='ticks')

# Prepare texts for adjustText
texts = []
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], txt))

# Adjust text to avoid overlap
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

# Set axis labels, title, and legend
plt.xlabel('Percent of Data Analyst Jobs')
plt.ylabel('Median Yearly Salary')
plt.title('Most Optimal Skills for Data Analysts in the UK')
plt.legend(title='Technology')

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

# Adjust layout and display plot 
plt.tight_layout()
plt.show()
```

### Visualisation

![OptimalSkills](Project\images\optimalskills.png)

### Insights 

From analysing the graph above it is evident that the skills which have the highest demand are SQL, Excel and Python with Tableau being 4th. In terms of skills which provide the highest salary amongst data analysts in the UK we can observe that these would consist of SQL serer, Flow and Tableau. Although the data suggests that these skills on average pay more, the demand for these skills are significantly lower than SQL and Python meaning that for someone looking to get a role as a data analyst it would be more beneficial to learn skills that are higher in demand. 


