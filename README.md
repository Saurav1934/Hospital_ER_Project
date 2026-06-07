# 🏥 Hospital ER Healthcare Analytics Dashboard

![Dashboard Preview](https://img.shields.io/badge/Status-Live-brightgreen?style=for-the-badge)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![ChartJS](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)
![Netlify](https://img.shields.io/badge/Deployed%20on-Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white)

> An interactive, fully responsive Hospital Emergency Room analytics dashboard built as a single `index.html` file — no frameworks, no build tools, no server required.

**🔗 Live Dashboard → [https://fanciful-gumdrop-f9e24e.netlify.app/](https://fanciful-gumdrop-f9e24e.netlify.app/)**

---

## 📊 Project Overview

This project visualizes **9,216 real patient records** from a Hospital Emergency Room collected between **April 2019 and October 2020**. The goal is to help hospital administrators and data analysts quickly identify patterns in patient flow, satisfaction, wait times, and department referrals.

The dashboard was inspired by a Power BI Healthcare Analytics project and recreated as a standalone web dashboard using vanilla HTML, CSS, and JavaScript — making it accessible in any browser without any software installation.

---

## ✨ Features

- **KPI Cards** — Total Patients, Avg Satisfaction Score, Avg Wait Time, % No Rating
- **Gender & Schedule Breakdown** — Male / Female / Non-Conforming split + Administrative vs Non-Administrative
- **Monthly Trend Line Chart** — Patient visit trend with dynamic Peak and Minimum month highlighting
- **Race × Age Heatmap** — Conditional color-coded grid showing Avg Satisfaction or Avg Wait Time per race and age group (toggle between both)
- **Age Group Bar Chart** — Infant, Early Childhood, Middle Childhood, Teenager, Adult
- **Department Referral Bar Chart** — All 7 departments + Walk-in patients
- **Weekday vs Weekend Chart** — Visit distribution by day type
- **Interactive Filters** — Filter by Year (2019 / 2020 / All) and Time of Day (AM / PM / All)
- **Fully Responsive** — Works on desktop, tablet, and mobile

---

## 📁 Dataset

**File:** `Hospital_ER.csv`

| Column | Description |
|---|---|
| `date` | Date and time of ER visit |
| `patient_id` | Unique patient identifier |
| `patient_gender` | M / F / NC (Non-Conforming) |
| `patient_age` | Age in years (1–79) |
| `patient_sat_score` | Satisfaction score 0–10 (frequently blank) |
| `patient_first_inital` | First name initial |
| `patient_last_name` | Last name |
| `patient_race` | Racial category (7 categories) |
| `patient_admin_flag` | True = Administrative visit |
| `patient_waittime` | Wait time in minutes (10–60) |
| `department_referral` | Referred department (blank = walk-in) |

**Data Period:** April 2019 – October 2020  
**Total Records:** 9,216 patients  
**Years Covered:** 2019, 2020

---

## 🔢 Key Metrics & Calculations

| Metric | Value | Logic |
|---|---|---|
| Total Patients | 9,216 | Count of all rows |
| Avg Satisfaction Score | 4.99 / 10 | Average excluding blank scores |
| Avg Wait Time | 35.26 min | Average of all wait times |
| % No Rating | 72.7% | Patients with blank satisfaction score |
| % Administrative | 50.0% | Patients with admin flag = True |
| Male Patients | 51.1% | Gender breakdown |
| Female Patients | 48.7% | Gender breakdown |
| Peak Month | Aug 2020 (530) | Highest monthly count |
| Lowest Month | Feb 2020 (431) | Lowest monthly count |

---

## 🧹 Data Transformations Applied

The following transformations were applied (equivalent to Power Query steps in Power BI):

- **Full Name** — Combined `patient_first_inital` + `patient_last_name`
- **AM/PM** — Extracted from timestamp hour (before 12 = AM, else PM)
- **Age Bucket** — Grouped into 10-year ranges: 0–10, 10–20 ... 70–80
- **Age Group** — Infant (0–2), Early Childhood (3–6), Middle Childhood (7–12), Teenager (13–17), Adult (18+)
- **Week Type** — Monday–Friday = Weekday, Saturday–Sunday = Weekend

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| HTML5 | Page structure and layout |
| CSS3 | Dark theme styling, responsive grid, animations |
| Vanilla JavaScript | Filter logic, data calculations, DOM updates |
| Chart.js 4.4 | Line chart with gradient fill and custom tooltips |
| Python + pandas | Data pre-processing and aggregation from CSV |
| Netlify | Free deployment and hosting |
| GitHub | Version control and source code |

> **Note:** This dashboard replicates a Power BI project as a standalone web app. For the equivalent Power BI version, see the DAX measures and Power Query steps documented below.

---

## 📐 Power BI Equivalent (DAX Measures)

If you want to recreate this in Power BI Desktop using the same dataset:

```dax
-- Total Patients
Total Patients = COUNTROWS(Hospital_ER)

-- Average Satisfaction (excluding blanks)
Avg Satisfaction Score =
CALCULATE(
    AVERAGE(Hospital_ER[patient_sat_score]),
    NOT ISBLANK(Hospital_ER[patient_sat_score])
)

-- Average Wait Time
Avg Wait Time = AVERAGE(Hospital_ER[patient_waittime])

-- % No Rating
% No Rating =
DIVIDE(
    COUNTROWS(FILTER(Hospital_ER, ISBLANK(Hospital_ER[patient_sat_score]))),
    [Total Patients]
)

-- % Administrative
% Administrative =
DIVIDE(
    COUNTROWS(FILTER(Hospital_ER, Hospital_ER[patient_admin_flag] = TRUE())),
    [Total Patients]
)
```

---

## 🚀 How to Run Locally

No installation needed. Just:

```bash
# Clone the repository
git clone https://github.com/Saurav1934/Hospital_ER_Project.git

# Open in browser
cd Hospital_ER_Project
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

Or simply double-click `index.html` — it opens directly in any browser.

---

## 🌐 Deployment

This project is deployed on **Netlify** via drag-and-drop.

To deploy your own copy:
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag and drop `index.html`
3. Get an instant live URL

---

## 📌 Project Structure

```
Hospital_ER_Project/
│
├── index.html          # Complete dashboard (all HTML + CSS + JS in one file)
├── README.md           # Project documentation
└── .gitattributes      # Git configuration
```

---

## 💡 Key Insights From the Data

- **Adults dominate** ER visits at 78.6% — paediatric load is relatively low
- **72.7% of patients leave no satisfaction rating** — feedback collection is a major gap
- **General Practice** receives the most referrals (1,840) after walk-ins
- **August 2020** was the busiest month with 530 patients
- **Native American/Alaska Native patients aged 70–80** have the longest average wait (40.07 min)
- **Pacific Islander patients aged 20–30** have the shortest average wait (32.53 min)
- The **AM/PM split** is nearly equal, suggesting consistent demand across shifts

---

## 🙋 Author

**Saurav** — Data Analyst  
📍 India  
🔗 [GitHub Profile](https://github.com/Saurav1934)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

⭐ If you found this project useful, please consider giving it a star!
