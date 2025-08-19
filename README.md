# 📊 Planner Dashboard (Power BI)

An interactive Power BI dashboard that tracks **Productivity %** and **Goal %** for each facility (Toyota, Mazda, VW, GM) and flags whether the **Previous Day** was **Open/Closed**. Built to give operations a fast, visual pulse on performance with clear trends and targets.

<img width="1160" height="652" alt="image" src="https://github.com/user-attachments/assets/6624e762-1ddc-4b03-8ff4-151393da0922" />


---

## ✨ Features
- 🧭 **Per-Facility KPIs:** Card tiles for each facility, showing **Productivity %**, **Goal %**, and **Prev Day** status.
- 📈 **Trend Lines:** Monthly line charts for Productivity % and Goal % with dashed target/threshold guides.
- 📆 **Date Control:** A timeline slider to focus on any custom date range.
- 🧩 **Filter-Aware Titles:** Dynamic facility titles that respect page/visual filters.
- ✅ **Prev Day Logic:** Robust DAX handles multiple rows per day and returns a clear True/False status.
- 🧪 **Consistent Modeling:** Star schema with a marked Date table for reliable time intelligence.

---

## 🛠️ Tech & Tools
- **Power BI Desktop** for report design and modeling  
- **DAX** for KPI logic (Productivity %, Goal %, Prev Day Closed, Facility Title)  
- **Power Query** (optional) for data cleanup/normalization  
- **Date Dimension** marked as a Date table for `DATEADD`/time intelligence

---

## 📂 Dashboard Highlights
- **Top Row: Facility Cards**  
  Productivity %, Goal %, and **Prev Day Open/Closed** badges by facility.
- **Middle Row: Productivity % Trends**  
  Month-over-month lines with visual targets.
- **Bottom Row: Goal % Trends**  
  Goal attainment over time with the same date context.
- **Global Controls**  
  Date slider (and optional facility slicer) that all visuals respect.

---

## 🚀 How It Works
1. Data lands in a `Planner` fact (Date, Facility, Completed, ProductivityPct, GoalPct).  
2. A continuous `Dates` dimension drives time intelligence and relationships.  
3. DAX measures calculate:
   - **Productivity %** (average of `Planner[ProductivityPct]`)
   - **Goal %** (average of `Planner[GoalPct]`)
   - **Prev Day Closed** (boolean based on prior calendar day’s `Completed`)
   - **Facility Title** (filter-aware text for cards/titles)
4. Visuals render KPIs and trends, scoped by the selected date range and facility.

---

## 🧱 Data Model (Star Schema)
- **Fact:** `Planner`  
  `Date` | `Facility` | `Completed` (TRUE/FALSE) | `ProductivityPct` (0–1) | `GoalPct` (0–1)
- **Dimension:** `Dates` (marked as Date table)  
  Relationship: `Dates[Date]` → `Planner[Date]` (**1 → * , single direction**)

> Tip: Normalize facility names (e.g., `UPPER(TRIM(Planner[Facility]))`) to avoid hidden duplicates.

---

## 📊 Business Impact
- ⏱️ **Cuts reporting time** by centralizing KPIs with a single date control.
- 🔎 **Improves visibility** into facility performance and daily closures.
- 🧭 **Guides decisions** on staffing and process changes using clear trends vs. targets.

---

## 🔮 Future Enhancements
- Dynamic targets per facility (goal lines driven by a config table)
- Anomaly flags for sudden drops/spikes in productivity
- Drillthrough pages for day/facility deep dives
- Automated data refresh tied to your source system

---

## 👤 Author
**Joel Perez**  
- 🌐 [GitHub](https://github.com/JoelProjectHub)  

---

## 📄 License
MIT — see `LICENSE` for details.
