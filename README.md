#aa
That’s a smart move—and I love your approach! If we start from scratch, step-by-step, we’ll make sure every element in your Power BI dashboard is bulletproof, insightful, and competitive.

✅ PHASE 1: DATA IMPORT & PREP
🔹 Step 1: Open Power BI Desktop
If not already installed, download Power BI Desktop.

🔹 Step 2: Import Your HR Dataset
Open Power BI

Click on Home > Get Data > Excel (or CSV) depending on your file

Browse and select your dataset

Click Load

✅ You’ll now see the data in the Fields pane on the right.

🔹 Step 3: Go to Power Query Editor
We’ll clean and prepare the data here.

Click Home > Transform Data

This opens Power Query Editor

✅ PHASE 2: DATA CLEANING & TRANSFORMING
🔸 Step 4: Remove Unnecessary Columns
In Power Query Editor:

Select columns you want to remove (like Blood Group, Merger & Acquisition, etc.)

Right-click > Remove Columns

🔸 Step 5: Handle Missing Data
For columns with missing or blank values:

If a column has >90% missing, remove it.

For others, use:

Replace Values (e.g., replace null Gender with "Unknown")

Remove Rows (optional: only if it's safe)

🔸 Step 6: Correct Data Types
Ensure these fields have correct types:


Column	Type
Date of Birth, Joining Date	Date
Age, Total Years of Exp	Whole Number
Gender, Department	Text
GRADE1	Text
Adani/Previous Experience	Decimal or Whole Number
✔️ To change: Click column header → Transform → Data Type

🔸 Step 7: Rename Columns (Optional but cleaner)
Example:

Name of Employee → Employee Name

GRADE1 → Grade

WorkLevel → Level

✅ After cleaning: Click Close & Apply

✅ PHASE 3: CREATE CALCULATED COLUMNS
Go to Data View (table icon on the left sidebar)

🔸 Step 8: Create Age Group Column
Click Modeling > New Column, then paste:

DAX
Copy
Edit
Age Group = 
SWITCH(TRUE(),
    'TableName'[Age] <= 25, "≤25",
    'TableName'[Age] <= 35, "26–35",
    'TableName'[Age] <= 45, "36–45",
    'TableName'[Age] <= 55, "46–55",
    "56+"
)
(Replace TableName with your actual table name)

🔸 Step 9: Create Tenure (Years with Company)
DAX
Copy
Edit
Tenure (Years) = 
DATEDIFF('TableName'[Joining Date], TODAY(), YEAR)
🔸 Step 10: Create Tenure Bands
DAX
Copy
Edit
Tenure Band = 
SWITCH(TRUE(),
    'TableName'[Tenure (Years)] < 1, "<1 Year",
    'TableName'[Tenure (Years)] <= 3, "1–3 Years",
    'TableName'[Tenure (Years)] <= 5, "3–5 Years",
    "5+ Years"
)
✅ PHASE 4: CREATE MEASURES (for % insights)
Go to Modeling > New Measure

🔸 Step 11: Total Employee Count
DAX
Copy
Edit
Total Employees = COUNT('TableName'[Employee Code])
🔸 Step 12: Gender % (Example: Female %)
DAX
Copy
Edit
Female Count = 
CALCULATE(COUNT('TableName'[Employee Code]), 'TableName'[Gender] = "Female")

Female % = 
DIVIDE([Female Count], [Total Employees]) * 100
Create similar ones for Male %, Other %, etc.

🔸 Step 13: Grade-wise Employee Count
DAX
Copy
Edit
Employee by Grade = 
COUNTROWS('TableName')
(Use in visuals filtered by Grade)

🔸 Step 14: Average Experience
DAX
Copy
Edit
Avg Exp = AVERAGE('TableName'[Total Years of Exp])

🔹 2. Is Experienced (Yes/No)
For employees with 10+ years of total experience (Adani + Previous):

DAX
Copy
Edit
Is Experienced = 
IF(
    'TableName'[Adani Experience] + 'TableName'[Previous Experience] >= 10,
    "Yes",
    "No"
)
🔹 3. Manager Type (Based on Work Level)
You can categorize the type of manager using WorkLevel (or Grade):

DAX
Copy
Edit
Manager Category = 
SWITCH(TRUE(),
    'TableName'[Level] = "Managing Managers", "Senior Manager",
    'TableName'[Level] = "Managing Others", "Mid-Level Manager",
    'TableName'[Level] = "Managing Self", "Individual Contributor",
    'TableName'[Level] = "SS", "Support Staff",
    "Executive"
)
✅ POWERFUL DAX MEASURES FOR INSIGHTS & CARDS
(Go to Modeling > New Measure)

🔸 1. % of Women in Workforce
DAX
Copy
Edit
% Female = 
DIVIDE(
    CALCULATE(COUNT('TableName'[Employee Code]), 'TableName'[Gender] = "Female"),
    [Total Employees]
) * 100
🔸 2. Average Age
DAX
Copy
Edit
Average Age = AVERAGE('TableName'[Age])
🔸 3. Average Tenure (Years)
DAX
Copy
Edit
Average Tenure = AVERAGE('TableName'[Tenure (Years)])
🔸 4. % of Workforce Nearing Retirement
DAX
Copy
Edit
% Nearing Retirement = 
DIVIDE(
    CALCULATE(COUNT('TableName'[Employee Code]), 'TableName'[Retirement Risk] = "Yes"),
    [Total Employees]
) * 100
🔸 5. % Experienced Employees (10+ Years)
DAX
Copy
Edit
% Experienced = 
DIVIDE(
    CALCULATE(COUNT('TableName'[Employee Code]), 'TableName'[Is Experienced] = "Yes"),
    [Total Employees]
) * 100
🔸 6. Department with Highest Headcount
(For use in cards or tables)

DAX
Copy
Edit
Top Department = 
TOPN(
    1,
    SUMMARIZE('TableName', 'TableName'[Department], "DeptCount", COUNT('TableName'[Employee Code])),
    [DeptCount], DESC
)
Then use Top Department in a Table visual or display card.

🔸 7. Employees Count by Category
You can use these dynamically in visuals or just create measures like:

DAX
Copy
Edit
Count - Managing Self = 
CALCULATE(
    COUNT('TableName'[Employee Code]),
    'TableName'[Level] = "Managing Self"
)



Absolutely! Let’s go super detailed and beginner-friendly, step-by-step, for Dashboard 1: Demographic Analysis in Power BI.

🧭 OVERVIEW OF STEPS
We will cover:

Importing data

Creating necessary calculated columns and measures

Designing each visual one-by-one

Arranging visuals in a clean layout

Adding slicers for interactivity

Final polish and tips

✅ STEP 1: OPEN & IMPORT DATA
Open Power BI Desktop

Click Home > Get Data > Excel (or CSV)

Browse to your file and click Load

Wait for data to show on the Fields pane (right side)

✅ STEP 2: PREPARE DATA
Click Home > Transform Data (opens Power Query)

Remove columns not needed (like Marital Status, Blood Group)

Replace missing values with defaults (like “Unknown”)

Ensure correct data types:

Date of Birth → Date

Gender, Department → Text

Age, Experience → Whole Number

Rename confusing columns (optional)

Click Close & Apply

✅ STEP 3: CREATE CALCULATED COLUMNS
Click on Data View (table icon) → Modeling > New Column

🔹 Age Group:
DAX
Copy
Edit
Age Group = 
SWITCH(TRUE(),
    'Table'[Age] <= 25, "≤25",
    'Table'[Age] <= 35, "26–35",
    'Table'[Age] <= 45, "36–45",
    'Table'[Age] <= 55, "46–55",
    "56+"
)
🔹 Tenure in Years:
DAX
Copy
Edit
Tenure (Years) = 
DATEDIFF('Table'[Joining Date], TODAY(), YEAR)
🔹 Tenure Band:
DAX
Copy
Edit
Tenure Band = 
SWITCH(TRUE(),
    'Table'[Tenure (Years)] < 1, "<1 Year",
    'Table'[Tenure (Years)] <= 3, "1–3 Years",
    'Table'[Tenure (Years)] <= 5, "3–5 Years",
    "5+ Years"
)
✅ STEP 4: CREATE MEASURES (KPIs)
Click Modeling > New Measure

🔹 Total Employees:
DAX
Copy
Edit
Total Employees = COUNT('Table'[Employee Code])
🔹 % Female:
DAX
Copy
Edit
Female Count = 
CALCULATE(COUNT('Table'[Employee Code]), 'Table'[Gender] = "Female")

% Female = 
DIVIDE([Female Count], [Total Employees]) * 100
🔹 Average Age:
DAX
Copy
Edit
Average Age = AVERAGE('Table'[Age])
🔹 Average Tenure:
DAX
Copy
Edit
Average Tenure = AVERAGE('Table'[Tenure (Years)])
🔹 % Nearing Retirement:
DAX
Copy
Edit
% Nearing Retirement = 
DIVIDE(
    CALCULATE(COUNT('Table'[Employee Code]), 'Table'[Age] >= 58),
    [Total Employees]
) * 100
✅ STEP 5: BUILD VISUALS
🟪 1. KPI CARDS
Click Insert > Card

Create these cards one by one:

Total Employees → use [Total Employees]

% Female → use [% Female]

Avg Age → [Average Age]

Avg Tenure → [Average Tenure]

% Nearing Retirement → [% Nearing Retirement]

🔧 Format each card:

Title ON: "Total Employees" etc.

Data Label: BIG font

Use consistent color (e.g. blue/black)

🟩 2. Gender Distribution (Donut Chart)
Click on Donut Chart

Drag Gender to Legend

Drag Employee Code to Values (Count)

Turn ON:

Data Labels → Show Percent and Category

Title: "Gender Distribution"

🟧 3. Age Group Distribution (Column Chart)
Click Stacked Column Chart

Axis: Age Group

Values: Count of Employee Code

Format:

Data labels ON

Title: “Age-wise Employee Distribution”

🟨 4. Department-wise Gender Split (Stacked Bar)
Click Stacked Bar Chart

Axis: Department

Legend: Gender

Values: Employee Code (Count)

Title: “Department-wise Gender Split”

🟦 5. Location-wise Employee Count (Tree Map)
Click Tree Map

Group: Location or Domicile State

Values: Employee Code (Count)

Title: “Employee Distribution by Location”

🟫 6. Employee Type or WorkLevel (Bar or Donut)
You can do either:

Donut for WorkLevel

Bar Chart for Employee Type

Same pattern:

Legend: WorkLevel

Value: Count of Employee Code

Show % and value in data labels

✅ STEP 6: ADD SLICERS
Click Slicer

Add fields like:

Gender

Department

Location

WorkLevel

Grade

📌 Use these on the left/right side as filters.

✅ STEP 7: FINAL LAYOUT & POLISH
Align visuals neatly (use View > Snap to Grid)

Add titles above each visual

Optional: Use color themes (View > Themes)

Add a Text Box on top as dashboard title:
📝 “Dashboard 1: Demographic Analysis”

DASBOARD 2
Updated saved memory
Great! Here's an even more detailed, step-by-step guide to create Dashboard 2: Grade-Level & WorkLevel Analysis in Power BI. This version assumes you're working from scratch and want a clean, professional HR dashboard with full mapping of both GRADE1 and WORKLEVEL values.

🎯 Goal
Create a comprehensive Power BI dashboard analyzing employees based on:

Grade (mapped from codes like CE, DR, etc. to full titles)

Designation/Work Level

Hierarchical grouping

% Distribution visuals

Clear, presentation-ready layout

🧩 STEP 1: Load & Inspect Data
Open Power BI Desktop.

Click on “Get Data” > Excel/CSV → Load your employee dataset.

Inspect columns:

GRADE1 → coded values like CE, DR, etc.

WORKLEVEL → descriptive designations like Chief Executive, Director, etc.

🏷 STEP 2: Map GRADE1 Codes to Full Titles
Create a calculated column in Power BI to map GRADE1 codes to full titles:

Go to: Modeling → New Column

DAX
Copy
Edit
Grade_Title = 
SWITCH(
    TRUE(),
    'YourTableName'[GRADE1] = "CE", "Chief Executive",
    'YourTableName'[GRADE1] = "DR", "Director",
    'YourTableName'[GRADE1] = "Partner",
    'YourTableName'[GRADE1] = "PR", "Partner",
    'YourTableName'[GRADE1] = "JP", "Junior Partner",
    'YourTableName'[GRADE1] = "SP", "Senior Partner",
    'YourTableName'[GRADE1] = "VP", "Vice President",
    'YourTableName'[GRADE1] = "AP", "Assistant Vice President",
    'YourTableName'[GRADE1] = "GM", "General Manager",
    'YourTableName'[GRADE1] = "E4", "Executive Level 4",
    'YourTableName'[GRADE1] = "E3", "Executive Level 3",
    "Unknown"
)
🧠 STEP 3: Create Hierarchical Grouping (Optional)
To group employees into categories like Leadership, Mid-Level, etc.:

DAX
Copy
Edit
Grade_Group = 
SWITCH(
    TRUE(),
    'YourTableName'[GRADE1] IN {"CE", "DR"}, "Executive Leadership",
    'YourTableName'[GRADE1] IN {"PR", "JP", "SP"}, "Partners",
    'YourTableName'[GRADE1] IN {"VP", "AP"}, "Senior Management",
    'YourTableName'[GRADE1] IN {"GM"}, "Middle Management",
    'YourTableName'[GRADE1] IN {"E4", "E3"}, "Junior/Exec Level",
    "Other"
)
🧱 STEP 4: Create DAX Measures for Counts & Percentages
Total Employees:

DAX
Copy
Edit
TotalEmployees = COUNTROWS('YourTableName')
Employees by Grade Group:

DAX
Copy
Edit
Employees by Grade Group = 
CALCULATE([TotalEmployees], ALLEXCEPT('YourTableName', 'YourTableName'[Grade_Group]))
% by Grade Group:

DAX
Copy
Edit
% by Grade Group = 
DIVIDE([Employees by Grade Group], [TotalEmployees], 0)
% by Work Level:

DAX
Copy
Edit
Employees by WorkLevel = COUNT('YourTableName'[WORKLEVEL])

% by WorkLevel = 
DIVIDE([Employees by WorkLevel], [TotalEmployees], 0)
📊 STEP 5: Create Visuals
Go to the Report view and create the following visuals:

A. Bar Chart – Count of Employees by Grade_Title
Axis: Grade_Title

Values: TotalEmployees

B. Pie or Donut Chart – % of Employees by Grade Group
Legend: Grade_Group

Values: % by Grade Group

Show % Labels

C. Column Chart – Employees by WorkLevel
Axis: WORKLEVEL

Values: Employees by WorkLevel

Sort descending by value

D. Pie Chart – % by WorkLevel
Legend: WORKLEVEL

Values: % by WorkLevel

🎨 STEP 6: Design Tips
Use corporate fonts/colors (like Segoe UI, blue/gray tones)

Add a title card: “Grade-Level & WorkLevel HR Analysis”

Add slicers for filtering:

Gender

Department

Location

Use Data Labels and Tooltips for interactivity

Arrange visuals in 2-column or grid layout for clean design

🧹 STEP 7: Final Touches
Use Format Panel to:

Set label size (9–12pt)

Enable legends and data labels

Align text centrally

Add a text box footer:

“Dashboard powered by Power BI | HR Analytics – [Your Name]”

hould we move to Dashboard 3: Experience and Employment Type Analysis next
