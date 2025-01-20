---
eleventyNavigation:
  key: Grouping data and descriptive statistics
  order: 7
Update: 2018-08-19
Version: VisiData 1.3.1
---



## How to set statistical aggregators for a single column

Aggregators provide summary statistics for grouped rows.

Command             Operation
--------            ----------
 `+` *aggregator*   adds *aggregator* to current column
`z+` *aggregator*   displays result of *aggregator* over values in selected rows for current column

The following statistical aggregators are available:

Aggregator      Description
-----------     ------------
`min`           smallest value in the group
`max`           largest value in the group
`avg`/`mean`    average value of the group
`mode`          most frequently appearing value in group
`median`        median value in the group
`q3/q4/q5/q10`  add quantile aggregators to group (e.g. q4 adds p25, p50, p75)
`sum`           total summation of all numbers in the group
`distinct`      number of distinct values in the group
`count`         number of values in the group
`keymax`        key of the row with the largest value in the group
`list`          gathers values in column into a list
`stdev`         standard deviation of values

The follow howtos will have examples of workflows involving grouping of data and statistical aggregation.

---
The following examples use the file [sample.tsv](https://raw.githubusercontent.com/saulpw/visidata/stable/sample_data/sample.tsv).

## How to group data (frequency table, pivot table, describe table,)

## How to make a pivot table frequency table, pivot table, describe table,)

<div class="asciicast">
    <asciinema-player id="player" poster="npt:0:10" rows=27 src="../casts/pivot.cast"></asciinema-player>
    <script type="text/javascript" src="/asciinema-player.js"></script>
</div>

1. Move to the column A with the independent variable, and press `!` to mark it as a key column to group by.
2. Move to a numeric column B, and press `+` to add an *aggregator* to that column, so that the aggregator will be applied to each group of values.
3. Make sure column B has a numeric type: int (`#`),  float (`%`),  currency (`$`), or date (`@`).
4. Move to the column C with the dependent categorical variable to be pivoted, and press `Shift+W` (`pivot`)  to pivot on that column.  The pivoted sheet then will have a column for each distinct value in the source column.

---

## [How to create a frequency chart](#frequency) {#frequency}


### How to make a histogram

**Question** How many of each **Item** were sold?

1. Move the cursor to the **Item** column.
2. Press `Shift+F` to open the **Frequency table**.

### How to use the Frequency table to view the results of statistical aggregation

**Question** What was the monthly revenue?

1. On the **OrderDate** column, type `;` followed by `(\d+-\d+)` to create a column with only the year and the month using regex capture groups.
2. Press `-` to hide the **OrderDate** column.
3. On the **OrderDate_re0** column, type `^` followed by `OrderDate` to rename it.
4. On the **Total** column, press `$` to set its type to currency.
5. Type `+` followed by `sum` to add a statistical aggregator to **Total**.
6. On the **OrderDate** column type `Shift+F` to open the **Frequency table**.
7. On the **OrderDate** column, press `[` to sort the table in chrononological order.
8. On the **sum_Total** column, type `^` followed by `Revenue` to rename the column.

---

### How to calculate some descriptive statistics

1. Press `Shift+I` to open the **Describe sheet**.

---

### How to filter for grouped rows

1. Press `Shift+F` to open the **Frequency table**.
2. Press `s` or `t` on the groups you are interested in to select those entries in the source sheet.
3. Press `q` or `Ctrl+^` to return to the source sheet.
4. Press `"` to open a duplicate sheet with selected rows.

**or**

1. Press `Shift+F` to open the **Frequency table**.
2. Press `Enter` on the grouping you are interested in to open a sheet of the source rows that are part of that group.

### How to filter for described rows

1. Press `Shift+I` to open the **Describe sheet**.
2. Use `zs` to select rows on source sheet which are being described in the cells of interest.
3. Press `q` or `Ctrl+^` to return to the source sheet.
4. Press `"` to open a duplicate sheet with selected rows.

**or**

1. Press `Shift+I` to open the **Describe sheet**.
2. Press `zEnter` open copy of source sheet with rows being described in the current cell of interest.

### How to filter for the rows aggregated in a pivot table

`Enter`/`zEnter` can both be used in the **Pivot table** to open a sheet of the source rows which are aggregated in the current pivot row/cell.

---

### How to combine cells in one for column for matching rows in another

This tutorial shows you how to go from this dataset:

field           value
------          -----
A               1
A               2
B               3
C               4
C               5

to

field           value
------          -----
A               1;2
B               3
C               4;5

in VisiData.

1. On the **value** column, type `+` followed by `list` to add to it a list aggregator.
2. Press `Shift+F` on the **field** column to open the **Frequency table**.
3. Type `=` followed by `';'.join(value_list)` to add an expression column with the joined values.
