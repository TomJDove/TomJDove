---
layout: post
title: "Drug Use in Victoria - Excel Dashboard"
date: 2023-10-12
categories: 
---
I created two dashboards in Excel to explore the data on ambulance drug attendances and hospital admissions compiled by [AODstats.org.au](AODstats).
I've uploaded the Excel workbook to my Google drive [here](https://drive.google.com/file/d/1YPFZAZQMgdFiQsO5bCOzTSJrrcVuKVxu/view?usp=sharing).
The first dashboard looks at the Victoria-wide statistics and the second looks at the statistics for individual drugs.

To get an idea of what the dahsboards look like, here are some pictures:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/drugs/db1.png"
  style="width:100%"
  >
  <figcaption>
    The first dashboard, on the Victoria-wide drug statistics for ambulance attendances and hospital admissions.
  </figcaption>
</figure>
</center>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/drugs/db2.png" style="width:100%" > 
  <figcaption>
  The second dashboard, looking at the statistics for individual drugs and drug categories.
  </figcaption>
</figure>
</center>

I created the dashboards in the following way:

1. I put each of the datasets (ambulance attendances, hospital admissions, and deaths) into a single Excel file and turned them into Excel **tables**.

2. **Power Query** was used to lightly process the data to fit my needs. This includes unpivoting the LGA data, renaming columns, changing the '< n' data entries to 0 so that the fields are all of the same type, and combining the ambulance, hospital, and deaths tables into one combined table.

3. Using Excel's **data model** features, I created a **relationship** between the table that contained Victoria-wide statistics and the table that contained the numbers for each Local Government Area (LGA). This is because I wanted to create pivot tables and slicers that used information from both tables.

4. I created **pivot tables** based on the charts I wanted to include in the dashboards, then created the relevant **pivot charts**. I created the slicers so that the dashboards would be interactive.

5. I styled everything and put all the charts together into a nice **dashboard**.
