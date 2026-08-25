# SC1003-Mini-Project

# Team Balancing Algorithm — SC1003 Group Project

Assigns 6,000 students into balanced teams of five within their tutorial
groups, optimising for gender balance, CGPA diversity, and school
affiliation diversity.

## Problem

Organise 6,000 students into teams of five, with each team drawn from a
single tutorial group. Teams are balanced across three factors, in order
of priority:

1. **Gender**
2. **Current CGPA**
3. **School affiliation**

## Targets

- 90% of teams have a gender composition of 3M/2F or 2M/3F
- 75% of teams have a mean CGPA within 1 standard deviation of the overall
  population mean
- 90% of teams have representation from at least 4 different schools

## Approach

1. **Parsing** — read and group all 6,000 student records (tutorial group,
   student ID, school, name, gender, CGPA) from `records.csv` into 120
   tutorial-group lists.
2. **Gender & CGPA diversity** — within each tutorial group, students are
   sorted by CGPA (bubble sort) and split by gender, then teams are formed
   by alternating gender and pairing low/high CGPA students together to
   balance both factors simultaneously.
3. **School diversity** — a second pass checks each formed team for
   over-represented schools and swaps students between teams (within the
   same tutorial group) to improve school spread, without breaking the
   gender/CGPA balance already achieved.
4. **Output generation** — final teams are written to a new CSV with
   columns for tutorial group, team number, and each student's details.

## Results

- Over 90% of teams draw from at least 4 different schools; more than 40%
  have every student from a different school.
- ~98% of teams achieve a healthy gender mix (mostly 3F/2M or 2F/3M), with
  a small number of 4F/1M anomalies.
- Team mean CGPAs cluster in a bimodal distribution around 4.05–4.12,
  with most teams falling within 1 standard deviation of the population
  mean (~4.09); a few outlier teams are pulled up by individual students
  with very high CGPAs.

Full breakdown and per-tutorial-group visualisations (gender, school, and
CGPA distributions, both across all teams and within a single tutorial
group) are in the notebook's "Analysis of the Groups" section.

## Challenges

- **Priority trade-offs** — the school diversity pass runs after gender/
  CGPA balancing and is constrained to preserve that balance, which limits
  how much school diversity can be improved without disturbing the
  higher-priority factors.
- **Computational efficiency** — bubble sort was used for CGPA ordering,
  which is simple but not efficient at scale.

## Setup & Running

1. Install dependencies: `pip install -r requirements.txt`
2. Place `records.csv` in the same folder as the notebook (see note below
   on data)
3. Run all cells top to bottom — parsing, diversity optimisation, and
   output generation are each in their own section, with a combined
   "Final Code" cell that runs the full pipeline end to end
4. Output is written to a new CSV containing the finalised team
   assignments

