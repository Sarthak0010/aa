#aa


📌 STEP 4: Create Alert Breakdown Bar Chart
📍 Insert → Stacked Bar Chart

Axis: Department

Legend: Alert Type (LateIn, UnderWorked, MissingPunch, NeedsRegularization)

Values: Use “Count of Rows” for each alert filter

💡 Use Tooltips to add Employee Name and Date.

📌 STEP 5: Alerts by Date
📍 Insert → Clustered Column Chart

Axis: Date

Legend: LateIn, UnderWorked, etc.

Values: Count of “Yes” for each

📌 STEP 6: Matrix Table (Detailed View)
📍 Insert → Matrix Visual

Rows: Employee Name

Columns: Date

Values: Confirmed In Punch, Confirmed Total Hours, LateIn, UnderWorked, NeedsRegularization

💡 Add Conditional Formatting:
Background color red if LateIn = "Yes" or UnderWorked = "Yes"

📌 STEP 7: 2-Hour Grouping Chart
📍 Insert → Bar Chart

Axis: HourGroup

Values: Count of employees

This is excellent for showing working time distribution.

📌 STEP 8: Pie/Donut Charts (Optional)
Absence Category Distribution

Time Type Split

Regularization Status Breakdown

📌 STEP 9: Add Filters / Slicers
📍 Insert → Slicer

Add slicers for:

Date

Department

Grade Code

Any alert column (LateIn, UnderWorked…)

📌 STEP 10: Make it Interactive
Enable Drillthrough: Right-click on a person → see their daily data

Add a Bookmark Button to toggle views (like “View by Employee” / “View by Dept”)
