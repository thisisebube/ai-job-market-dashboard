# 📊 AI & Data Science Job Market Dashboard (2020–2026)

An interactive Power BI report analyzing hiring patterns, salary trends, and job demand across the global AI and data science job market — built on a synthetic dataset of 10,345 records spanning 7 countries and 6 roles from 2020 to 2026.

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `AI_Job_Market_Trends_2026.csv` | Source dataset (10,345 records, 19 columns) |
| `AI_Job_Market_Dashboard.pbix` | Power BI report file |
| `powerbi-case-study.html` | Portfolio case study page |

---

## 🗂️ Dataset Overview

The dataset is synthetically generated to simulate real-world hiring patterns across the AI and data science industry.

| Property | Detail |
|----------|--------|
| **Rows** | 10,345 |
| **Columns** | 19 |
| **Period** | 2020 – 2026 |
| **Nulls** | None |

### Key Columns

- `job_title` — AI Engineer, ML Engineer, Data Scientist, Data Analyst, Data Engineer, Business Analyst
- `country` — USA, UK, Canada, Australia, Germany, Singapore, India
- `salary` — Annual salary in USD ($45K – $204K)
- `job_posting_year` / `job_posting_month` — Posting date
- `experience_level` — Entry, Mid, Senior
- `company_size` — Startup, Medium, MNC, Enterprise
- `company_industry` — Technology, Finance, Healthcare, Retail, E-commerce, Education
- `job_openings` — Number of open positions per posting
- `skills_python`, `skills_sql`, `skills_ml`, `skills_deep_learning`, `skills_cloud` — Binary skill flags (0/1)

---

## 📐 Data Preparation (Power Query)

Two additional columns were engineered before analysis:

**1. Posting Date**
```m
= Date.FromText(Text.From([job_posting_year]) & "-" & Text.From([job_posting_month]) & "-01")
```

**2. Total Skills Count**
```m
= [skills_python] + [skills_sql] + [skills_ml] + [skills_deep_learning] + [skills_cloud]
```

---

## 📐 DAX Measures

```dax
-- Total Job Openings
Total Openings = SUM('AI_Job_Market'[job_openings])

-- Average Salary
Avg Salary = AVERAGE('AI_Job_Market'[salary])

-- Year-over-Year Demand Growth
YoY Growth =
VAR CurrentYear =
    CALCULATE(
        [Total Openings],
        FILTER(
            ALL('AI_Job_Market'),
            'AI_Job_Market'[job_posting_year] = MAX('AI_Job_Market'[job_posting_year])
        )
    )
VAR PrevYear =
    CALCULATE(
        [Total Openings],
        FILTER(
            ALL('AI_Job_Market'),
            'AI_Job_Market'[job_posting_year] = MAX('AI_Job_Market'[job_posting_year]) - 1
        )
    )
RETURN DIVIDE(CurrentYear - PrevYear, PrevYear, 0)
```

---

## 📊 Dashboard Pages

### Page 1 — Job Demand
| Visual | Fields |
|--------|--------|
| Filled Map | Country → Total Openings |
| Clustered Bar Chart | Job Title → Total Openings |
| Line Chart | Posting Date → Total Openings |
| Stacked Bar Chart | Job Title + Experience Level → Openings |
| Slicers | Year, Country, Industry, Company Size |

### Page 2 — Salary Trends
| Visual | Fields |
|--------|--------|
| Line Chart | Posting Date → Avg Salary |
| Bar Chart | Job Title → Avg Salary |
| Matrix Table | Country × Job Title → Avg Salary |
| Scatter Plot | Years Experience → Salary (by Job Title) |
| Slicers | Experience Level, Remote Type, Company Size |

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — Report building and publishing
- **DAX** — Measure authoring and time intelligence
- **Power Query (M)** — Data transformation and column engineering
- **CSV** — Data source format

---

## 💡 Key Insights

- **Data Scientist** and **ML Engineer** roles consistently command the highest average salaries across all countries
- **USA** leads in total job openings, followed by **UK** and **Canada**
- Senior-level roles account for a disproportionately high share of postings in **Singapore** and **Germany**
- Job demand shows steady year-over-year growth from 2020, with an acceleration post-2022
- **Cloud** and **ML** skills appear most frequently as requirements across all job titles

---

## 👤 Author

**Ebubechukwu**
- GitHub: [@thisisebube](https://github.com/thisisebube)
- LinkedIn: [linkedin.com/in/thisisebubechukwu](https://linkedin.com/in/thisisebubechukwu)

---

## 📄 License

This project uses a synthetically generated dataset. Free to use for learning and portfolio purposes.
