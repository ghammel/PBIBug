# PBIBug
Sample Power BI dataset illustrating a problem/conflict between a calculated column, a measure using the ALL() function, and filter context

The files here relate to an ongoing issue I have encountered in Power BI with using a calculated column [Fiscal Year] in combination with all of the following conditions: 

1. A measure that uses the ALL() function - both [Company share] and [Denominator] do this.
2. A filter on the [Fiscal Year] column that filters out one or more values. (I filtered out values 2018-19 and 2019-20 for illustration.)
3. A filter on another column - I used [Region] - that selects more than one, but not all values. (I selected values 111 and 113 for illustration.)

The problem appears to be that the [Region] filter is interacting in an odd way with the measures. For each value of [Company], it is only calculating a grand total denominator only on the basis of the [Region] values that are present for that particular [Company] in that particular [Fiscal Year]. For example, in the 2020-21 Fiscal Year, companies C, F, and I have values for Region 113 but do not have values from Region 111. When both Regions are selected in the filter, the grand total calculation for these companies - [Denominator] - is only drawing from the rows with Region 113, which results in incorrect percentage [Company share] calculations. 

Despite these obvious errors, there seems to be no problem with the [Denominator] and [Company share] measures themselves. In fact, when I use an alternate Fiscal Year column created in Power Query rather than DAX (entitled [FiscalYrQuery]), the measures act as expected and calculate the grand total denominator properly. 

If anyone else has encountered this issue, I would appreciate hearing about it. Also, if anyone knows how to contact the Product Development or Quality Review teams, that would be helpful. I have spent weeks back-and-forth with Power BI Customer Support with nothing to show for it.  

(PLEASE NOTE: I am aware that there are other ways to fix this issue for this particular instance - not using a DAX calculated column, for example. My concern here is more general - that this is a core functionality that should work properly in Power BI but does not appear to do so.)
