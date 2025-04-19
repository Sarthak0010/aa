# aa
🎯 PROJECT GOAL
Create 3 Power BI Dashboards for the HR department using employee data, with a focus on:
1.	Demographics
2.	Grade Level & Hierarchy
3.	Tenure & Employee Lifecycle
________________________________________
✅ STEP 1: CLEAN THE DATA IN EXCEL
📂 Open your original Excel file and clean it like this:
🔹 KEEP ONLY IMPORTANT COLUMNS
(You can hide or delete the rest for now)
Column Name	Use It?	Notes
S.No	❌	Remove
Employee Code	✅	Keep
Name of Employee	✅	Keep
Department	✅	Keep
Designation	✅	Keep
Grade Code (Grade)	✅	Very Important
Date of Birth	✅	Will calculate age
Gender	✅	Keep
Marital Status	✅	Keep
City / Location Name	✅	Keep
State (Domicile State)	✅	Keep
Date of Joining	✅	Will calculate tenure
Employment Status / Type	✅	Keep
Business Unit / Legal Entity	✅	Optional, keep if useful
Manager / HOD	Optional	Only if needed
Date of Separation	❌	Remove (99% blank)
Last Transfer Date	❌	Remove (64% blank)
Others like Blood Group, Email	❌	Remove for now
________________________________________
✅ STEP 2: CREATE GRADE MAPPING TABLE IN EXCEL
1.	Open a new sheet in the same Excel file.
2.	Create the following table:
Grade	Designation	Level
CE	CEO	Business Head
DR	Director	Business Head
PR	President	Business Manager
JP	Joint President	Business Manager
SP	Senior Vice President	Function Manager
VP	Vice President	Function Manager
AP	Associate Vice President	Function Manager
GM	General Manager	Managing Managers
E4	Associate General Manager	Managing Managers
E3	Deputy General Manager	Managing Managers
E2	Senior Manager	Managing Managers
E1	Manager	Managing Others
O5	Associate Manager	Managing Others
O4	Deputy Manager	Managing Others
O3	Assistant Manager	Managing Self
O2	Executive / Senior Engineer / Officer	Managing Self
O1	Officer / Engineer / GET	Managing Self
S5	Associate Officer / Engineer	SS Level
S4	Junior Officer / Engineer	SS Level
S3	Supervisor	SS Level
S2	Senior Assistant / Technician	SS Level
Save your Excel file with both sheets.
Example:
•	Sheet1: Employee Data
•	Sheet2: Grade Mapping
________________________________________
✅ STEP 3: IMPORT DATA TO POWER BI
🔹 Open Power BI Desktop:
1.	Click "Get Data" → Excel
2.	Select your saved file
3.	Import both sheets: Employee Data and Grade Mapping
4.	Click "Load"
________________________________________
✅ STEP 4: CLEAN & CONNECT DATA IN POWER BI
🔹 Power Query (optional but useful)
•	Click on "Transform Data"
•	Make sure Date columns are in Date format:
o	Right-click on Date of Birth, Date of Joining → Change Type → Date
🔹 Add Calculated Columns
In Power BI (not in Excel), go to Modeling → New Column
1.	🧮 Age Column:
DAX
CopyEdit
Age = DATEDIFF(EmployeeData[Date of Birth], TODAY(), YEAR)
2.	🧮 Tenure (Years):
DAX
CopyEdit
Tenure (Years) = DATEDIFF(EmployeeData[Date of Joining], TODAY(), YEAR)
🔹 Create Relationship
•	Go to Model View
•	Drag Grade Code from Employee Data and connect it to Grade in the Grade Mapping Table
________________________________________
✅ STEP 5: BUILD DASHBOARDS


📊 DASHBOARD 1: DEMOGRAPHIC ANALYSIS
🎯 Goal:
To help HR understand the workforce’s age, gender, marital status, and geographic distribution.
________________________________________
✅ STEP-BY-STEP BEGINNER-FRIENDLY GUIDE
________________________________________
STEP 1: Open Power BI and Import Data
1.	Open Power BI Desktop.
2.	On the Home tab, click “Get Data” > Excel or CSV.
3.	Browse and select the file containing your employee data.
4.	Click “Load” (if the preview looks fine).
5.	Your data will now appear in the Fields pane on the right.
________________________________________
STEP 2: Clean the Data (Power Query Editor)
1.	Click Home > Transform Data (top ribbon).
2.	In Power Query Editor, do the following:
Clean Columns:
•	Right-click "Date of Separation", "Last Transfer Date", and others with 60–90% blanks → choose Remove.
•	Alternatively: Keep but ignore them in visuals.
Fix Column Types:
•	Ensure these are correctly typed:
o	Age → Number
o	Date of Birth → Date
o	Gender, Marital Status, Location, City, Department → Text
Add Age Band Column:
1.	Click Add Column > Custom Column.
2.	Name it: Age Band.
3.	Enter this formula:
m
CopyEdit
if [Age] <= 25 then "Below 25" 
else if [Age] <= 35 then "26-35"
else if [Age] <= 45 then "36-45"
else "46+"
4.	Click OK.
5.	Click Close & Apply on top left.
________________________________________
STEP 3: Create Basic Measures (Optional)
1.	Go to the Modeling tab → Click New Measure.
2.	Paste:
DAX
CopyEdit
Total Employees = COUNT(Employee[Employee Code])
3.	Repeat to create:
DAX
CopyEdit
Male Employees = CALCULATE(COUNT(Employee[Employee Code]), Employee[Gender] = "Male")

Female Employees = CALCULATE(COUNT(Employee[Employee Code]), Employee[Gender] = "Female")

Average Age = AVERAGE(Employee[Age])
________________________________________
STEP 4: Create the Visuals (One by One)
✅ 1. KPI Cards (Top Summary)
1.	Click Card visual (under Visualizations pane).
2.	Drag Total Employees measure to it.
3.	Format it:
o	Change Title to "Total Employees"
o	Increase font size
o	Add background color
4.	Repeat for:
o	Male Employees
o	Female Employees
o	Average Age
________________________________________
✅ 2. Gender Distribution (Donut or Pie Chart)
1.	Click Pie Chart icon.
2.	Drag Gender to Legend.
3.	Drag Employee Code to Values (will count automatically).
________________________________________
✅ 3. Marital Status Distribution
1.	Insert Donut chart.
2.	Drag Marital Status to Legend.
3.	Drag Employee Code to Values.
________________________________________
✅ 4. Age Band by Gender (Stacked Bar Chart)
1.	Click Stacked Column Chart.
2.	Drag:
o	Age Band to X-axis
o	Employee Code to Values
o	Gender to Legend
________________________________________
✅ 5. Employee Count by City/Location (Map)
1.	If your data has a City or Location column:
2.	Click Map visual.
3.	Drag Location to Location.
4.	Drag Employee Code to Size.
If asked to enable maps/geolocation: click Enable.
________________________________________
STEP 5: Add Filters / Slicers
1.	Click Slicer visual.
2.	Add these slicers:
o	Department
o	Gender
o	Age Band
o	Marital Status
o	Location
These let HR filter and compare specific segments easily.
________________________________________
STEP 6: Clean, Align, and Polish
1.	Arrange visuals in a clean layout:
o	Cards at the top
o	Pie/Donut charts in the middle
o	Bar and Map at the bottom
2.	Use consistent colors:
o	Blue = Male
o	Pink = Female
o	Orange = Married
o	Teal = Single
3.	Add Page Title:
o	Insert a Text box
o	Title: “Demographic Dashboard – HR Workforce Overview”
o	Center it and use large font
________________________________________
✔️ What This Dashboard Shows HR:
Insight	Helps HR To
Gender Ratio	Ensure diversity and inclusion
Age Bands	Plan training, succession
Marital Status	Tailor benefits and wellness
Location Map	Analyze regional hiring & retention
Slicers	Drill into any group instantly


📊 DASHBOARD 2: Grade & Designation Hierarchy
🎯 Goal:
To show how employees are distributed across different grades and management levels — and help HR analyze hierarchy, manpower gaps, and promotions.
________________________________________
✅ STEP-BY-STEP BEGINNER-FRIENDLY GUIDE
________________________________________
STEP 1: Prepare Grade Mapping Table (Using Your Uploaded Image)
From the mapping you uploaded, we’ll create a manual mapping table in Excel or directly in Power BI.
👇 Excel Table Format Example:
Grade Code	Level	Designation
CE	Business Head	CEO / Director
PR	Business Manager	President
JP	Business Manager	Joint President
SP	Function Managers	Senior Vice President
VP	Function Managers	Vice President
AV	Function Managers	Associate VP
GM	Senior Management	General Manager
SM	Senior Management	Senior Manager
M1	Mid Management	Manager
M2	Mid Management	Deputy Manager
AM	Mid Management	Assistant Manager
OE	Individual Contributor	Officer Executive
SE	Individual Contributor	Sr. Executive
EE	Individual Contributor	Executive
________________________________________
STEP 2: Import This Table into Power BI
Option A: Excel Method
1.	Save this table in Excel as GradeMapping.xlsx.
2.	In Power BI: Home > Get Data > Excel > Select file > Choose the table/sheet.
3.	Click Load.
Option B: Manual Table in Power BI
1.	Go to Modeling > New Table.
2.	Paste this DAX (example for 3 rows, expand for all):
DAX
CopyEdit
GradeMapping = 
DATATABLE(
    "Grade Code", STRING,
    "Level", STRING,
    "Designation", STRING,
    {
        {"CE", "Business Head", "CEO / Director"},
        {"PR", "Business Manager", "President"},
        {"JP", "Business Manager", "Joint President"}
        -- Add more rows here
    }
)
________________________________________
STEP 3: Create Relationships
1.	Go to Model View (left-side 3rd icon).
2.	Drag and link:
o	Grade Code in your Employee Table
o	to Grade Code in GradeMapping Table
✅ Now your employee data is linked to level and designation!
________________________________________
STEP 4: Create Dashboard Visuals (One by One)
✅ 1. Total Employees by Grade Level (Bar Chart)
1.	Insert a Stacked Column Chart.
2.	Axis: Level (from GradeMapping)
3.	Value: Employee Code (will count)
4.	Legend (optional): Gender for diversity insight
________________________________________
✅ 2. Designation Breakdown (Matrix Visual)
1.	Insert a Matrix Visual.
2.	Rows: Level → Grade Code → Designation
3.	Values: Count of Employee Code
🎯 HR can drill down by level → grade → title.
________________________________________
✅ 3. Tree Map (Visualize Headcount)
1.	Click Tree Map visual.
2.	Group: Designation
3.	Values: Count of Employee Code
Shows which roles have more/less employees — useful for staffing.
________________________________________
✅ 4. Donut Chart: Grade Code Distribution
1.	Click Donut Chart.
2.	Legend: Grade Code
3.	Values: Count of Employee Code
________________________________________
✅ 5. Table: Level vs Headcount
1.	Insert a Table visual.
2.	Add:
o	Level
o	Employee Code (change aggregation to "Count")
________________________________________
STEP 5: Add Filters / Slicers
Add Slicer visuals for:
•	Location
•	Department
•	Gender
•	Age Band (from Dashboard 1)
These make your dashboard interactive.
________________________________________
STEP 6: Polish & Final Touches
1.	Add Page Title: "Grade & Designation Hierarchy Dashboard"
2.	Align visuals neatly in grid layout:
o	Cards or bar charts on top
o	Matrix + tree map in middle
o	Filters on the left or right
3.	Use color themes:
o	Assign distinct colors per level (Business Head, Function Manager, etc.)
4.	Format charts:
o	Increase label size
o	Add data labels where helpful
o	Enable tooltips
________________________________________
✔️ What This Dashboard Shows HR:
Insight	HR Use
Grade Distribution	Track how workforce is spread across levels
Gender Mix in Grades	Ensure leadership diversity
Headcount by Designation	Spot staffing gaps
Drilldowns by Department	Plan internal movements and succession
