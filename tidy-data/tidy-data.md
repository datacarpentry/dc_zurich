---
title: "Better spreadsheets"
output:
  html_document:
    toc: true
    theme: united
---

# The problem

- most of the time (80%) of the data analysis process is spent on cleaning up
  data --> should instead be spending time on analysis (the interesting part)
- data needs to be clean because it's either dirty or needs to be rearranged to
  facilitate statistical analysis or plotting
- often no data format standard, so spending a lot of time converting data from
  one format to another

- Spreadsheet programs are very useful graphical interfaces for designing
  data tables and handling very basic data quality control functions.

- Spreadsheets are very flexible (and feature rich) but don't do anything very
  well in the context of scientific analysis. Spredsheets are used to:
    - enter data
    - create data tables for publications
	- generate summary statistics
	- make figures

- Entering data:
  - easy to erase or change data without realizing it
  - can insert typos

- Create data tables or figures for publications:
  - not reproducible: rely of manual steps, copy and paste
  - hard/impossible to track origin of data: breaks dependency on original data
  - creates formatting that makes data not readable for computers (merging
    cells, coloring, creating borders, making it pretty).

- differentiate data structure for:
  - data entry
  - data storage
  - data analysis

- your data vs. someone else data
  - preparation of the canonical dataset, ok that you use spreadsheets
  - someone else's data, need a way to trace your modifications and origin of
    the data -- importance of scripting


# Organizing your data for analysis

**Data organization is the foundation of your research project.** It can make it
easier or harder to work with your data throughout your analysis, so it's worth
thinking about when you're doing your data entry or setting up your
experiment. You can set things up in a different way in spreadsheets, but it
limits your ability to work with the data in other programs or have the
you-of-6-months-from-now or your collaborator work with the data.

## Defining tidy data

- each dataset can be messy in its own way, but a clean dataset should provide a
  standardized way to link structure with its meaning. How can we do this?
  Better data structure.

### Data structure

- [show examples]
- both dataset represent the same data; but the layout is different. It shows
  that simply using the row/column vocabulary isn't enough to describe the data
  in the table.
- We need to extend our vocabulary to capture the data semantics

### Data semantics

- dataset is a collection of values (quantitative, numbers; or qualitative,
  strings) organized in two ways
  - observation: all values measured in the same unit (an individual, a day, a strain)
  - variable: measure the same underlying attribute (height, temperature,
    duration)

> Challenge: What are the observations and variables in our dataset?

- What constitute a variable can be difficult to define:
  - if weight and height, pretty clear; but height and width could have been
    thought as values of a dimension variable
  - home phone and work phone could be treated as two variables, but if we are
    trying to detect duplicates (e.g., fraud detection) we may want phone number
    and phone type as variables
  - Rule of thumb: easier to describe functional relationships between variables
    than between rows; and easier to make comparison between groups of
    observations than between groups of columns
  - in a given analysis, there may be multiple levels of observations. Later we
    will work with species capture data. We may want to record data about the
    individuals that were captured each day (size, species, sex), data about the
    species (genus, species, group of animal), data about the day of the capture
    (weather conditions), and data about where the animals were trapped.


### Tidy data

- each variable forms a column
- each observation forms a row
- each type of observational unit forms a table

with tidy data, it's easier for **a computer** to extract relevant data
consistently across variables; but it might not be the easiest format for a
human to enter or have a quick glance at the data.

ordering of variables and observations doesn't affect analysis but makes
scanning easier. One way of organizing is trying to answer the question:

- are values fixed by design of data collection (known in advance) or measured
  during the course of the experiment?
  - Fixed variables should come first, followed by measured
    variables. Observations should be ordered so related variables are
    contiguous. Rows can be ordered by first variable, breaking ties with the
    second and subsequent fixed variables.

> ## Challenge
>
> We're going to take a messy version of the survey data and clean it up.
>
> - Download the data by clicking on [http://datacarpentry.github.io/dc_zurich/data/survey_data_tabs.xls](http://datacarpentry.github.io/dc_zurich/data/survey_data_tabs.xls)
>
> - Open up the data in a spreadsheet program
>
> - You can see that there are two tabs. Two field assistants conducted the surveys, one
> in 2013 and one in 2014, and they both kept track of the data in their own way. Now
> you're the person in charge of this project and you want to be able to start doing
> statistics with the data.
>
> - With the person next to you, work on the messy data so that a computer will
> be able to understand it. Clean up the 2013 and 2014 tabs, and put them all together
> in one spreadsheet.

> After you go through this exercise, we'll discuss as a group what you think was wrong
> with this data and how you fixed it.


## Tidying messy datasets

### Common problems with messy datasets

1. columns headers are values, not variable names
1. multiple variables are stored in one column
1. variables are stored in both rows and columns
1. multiple types of observational units are stored in the same table
1. a single observational unity is stored in multiple tables
   --> importance of scripting

# Entering data

## Multiple tables per sheet

- you break the rules of 1 row per observation
- duplicate variable names

## Using sheets

- This is bad practice for two reasons:
  1. you are more likely to accidentally add inconsistencies to your data if
  each time you take a measurement, you start recording data in a new tab

  2. even if you manage to prevent all inconsistencies from creeping in, you
  will add an extra step for yourself before you analyze the data because you
  will have to combine these data into a single datatable. You will have to
  explicitly tell the computer how to combine tabs- and if the tabs are
  inconsistently formatted, you might even have to do it by hand!

The next time you’re entering data, and you go to create another tab or table, I
want you to ask yourself “Self, could I avoid adding this tab by adding another
column to my original spreadsheet?”

Your data sheet might get very long over the course of experiment. This makes it
harder to enter data if you can’t see your headers at the top of the
spreadsheet. But do NOT repeat headers. These can easily get mixed into the
data, leading to problems down the road.

> Challenge: Demonstrate the use of the freezing

### Missing data

- missing data:
  - keep it if value represent observations that should have been made but
    wasn't
  - drop it if it's a structural missing data (measurement that can't be made:
    e.g., count of pregnant males)
- how to code it?

# Formating data -- Use at your own risk (but you are also putting others at risk)

## Using formatting to convey information

Example: highlighting cells, rows or columns that should be excluded from an
analysis, leaving blank rows to indicate separations in data

Solution: create a new field to encode which data should be excluded

## Using formatting to make the data sheet look pretty

Example: merging cells If you’re not careful, formatting a worksheet to be more
aesthetically pleasing can compromise your computer’s ability to see
associations in the data. Merged cells are an absolute formatting NO-NO if you
want to make your data readable by statistics software.

Consider restructuring your data in such a way that you will not need to merge
cells to organize your data

## Placing comments or units in cells

Example: your data was collected, in part, by a summer student you later found
out was mis-identifying some of your species, some of the time. You want a way
to note these data are suspect.

Solution: most statistical programs can’t see Excel’s comments, and would be
confused by comments placed within your data cells. Create another field if you
need to add notes to cells. Similarly, don't include units- ideally, all the
measurements you place in one column should be in the same unit, but if for some
reason they aren’t, create another field and specify the units the cell is in.

Document the intricacies of your dataset using a README file

> A word about dates

# Checking your values

## Pivot tables

## Conditional formatting

## Sorting

## Filtering
