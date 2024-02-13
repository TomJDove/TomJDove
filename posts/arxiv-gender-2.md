---
layout: post
title: "What the ArXiv metadata says about gender equality in mathematics"
date: 2023-07-04
permalink: '/2023/07/04/Arxiv-Gender'
---

<p align='justify'>
In this project, I use Python/Pandas and Power BI to process a large dataset of scientific papers to gain insight into gender equality among mathematics researchers.
</p>

<p align='justify'>
I summarised the findings in a Power BI report.
I only have a free Power BI license, so I can't share the Power BI report directly. 
The following are screenshots of the report:
</p>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/report1.jpg"
  style="width:100%"
  >
  <figcaption>
    The first page of the report, which gives an overview of submissions.
  </figcaption>
</figure>
</center>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/report2.jpg"
  style="width:100%"
  >
  <figcaption>
  The second page, which has information on the gender proportion of the authors.
  </figcaption>
</figure>
</center>

To start, let me explain what the ArXiv is and the methods I used.

## What is ArXiv?

<p align='justify'>
Owned and operated by Cornell University, ArXiv is an open-access repository of scientific papers in fields ranging from mathematics and physics to quantitative biology and economics.
First established in 1991, it now holds over 2 million scholarly articles, and almost every mathematics paper that is written will be uploaded to ArXiv.
</p>

<p align='justify'>
To make ArXiv more accessible, Cornell has shared the metadata of its submissions on <a href='https://www.kaggle.com/datasets/Cornell-University/arxiv'> Kaggle </a>
Here, you can view information about each of the 1.7 million submissions, including the title, abstract, author names, and submission date.
You can also do some calculations; for example, there are currently almost 45,000 mathematics papers uploaded each year:
</p>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/journal-ref.png"
  style="width:100%"
  >
  <figcaption>
    More submissions, but fewer journal publications
  </figcaption>
</figure>
</center>

<p align='justify'>
There are other interesting observations to be made in this trove of data.
For example, of the 594,000ish total submissions, almost a quarter had journal references, which means they were likely published in a peer-reviewed journal.
Even more interestingly, the annual proportion of submissions with journal references has dramatically declined in the last two decades.
As we see in the above chart, it starts at around 40% and has plummeted to below 10%.
Does this indicate a rise in hobbyist mathematics posting papers to ArXiv?
</p>

<p align='justify'>
Another fun fact: since there are currently about 594,000 mathematics posts on ArXiv, a lucky mathematician will soon post the 600,000th mathematics paper to ArXiv (congratulations to this person).
</p>

<p align='justify'>
I want to get something more meaningful from the ArXiv data.
Could this dataset give us any information on the gender balance in mathematics?
An author does not submit their gender when uploading a paper, so it doesn't seem like we have much information to go on.
</p>

## Gender inequality in mathematics

<p align='justify'>
Gender inequality is a well-known issue in STEM, and it is especially serious in mathematics.
Despite girls performing as well if not better than boys in maths at school, the proportion of women studying and working in mathematical sciences is significantly lower than it ought to be.
</p>

If we look at the numbers for Australia, the problem is quite visible:
 - Women make up only 37% of undergraduate mathematical science degrees and 29% of postgraduate degrees, according to [STEM Women](https://www.stemwomen.com/women-in-stem-australia).
- [Government data](https://labourmarketinsights.gov.au/occupation-profile/mathematicians?occupationCode=224112) reveals that women make up only 23% of mathematicians.
- Only [9% of professors](https://www.sydney.edu.au/news-opinion/news/2016/03/30/australia_s-got-scientific-female-talent---heres-how-to-stop-was.html) in mathematical science are women.

<p align='justify'>
So, there is no shortage of evidence for the gender gap in mathematics, but I want to see whether it can be seen in the ArXiv data.
The problem is that authors do not share their gender when uploading papers.
We only have one piece of information that could indicate an author's gender: their first name.
</p>

## Getting on a first-name basis

<p align='justify'>
The idea is to use the first names of the authors to get a very (repeat *very*) crude idea of the gender disparity in ArXiv postings.
I figure that, for certain names, one could take a reasonable guess at which gender this person identifies as.
If an author's name is Thomas, for example, they will probably (if not necessarily) identify as a man.
</p>

<p align='justify'>
There are indeed commercially available tools to achieve this.
<a href = 'https://gender-guesser.com/'>Gender Guesser</a> claims to be the best on the market: 8 billion names processed in 22 alphabets, contributions to scientific research, and a slew of fancy academic and corporate users.
With thousands of names to process and a PhD student salary, I decided to use the freely available Python package <a href = 'https://github.com/lead-ratings/gender-guesser'>gender-guesser</a>, which is based on a comparatively tiny dataset of 40,000 names collected by a man named Jorg Michael.
</p>

<p align='justify'>
The Python package assigns a name to one of five categories: male, mostly male, unknown, mostly female, and female.
I simplified this to three categories: man, unknown, and woman, with the 'mostly' entries being put into the unknown category.
</p>

Now, this method has several flaws and limitations:
- It excludes those who don't identify as either a man or a woman.
- Some names are commonly used by people of all genders so even with the best possible methods we couldn't determine their gender.
- Many authors prefer to just give their first initial or submit their name in some non-standard way, which messes the data up.

<p align='justify'>
So, we certainly shouldn't be using this method to produce any hard quantitative conclusions.
Nonetheless, if there's a very clear gender disparity, we might be able to pick up on it.
</p>


## Data processing

<p align='justify'>
The first thing we need to do is process the <a href = 'https://www.kaggle.com/datasets/Cornell-University/arxiv'>ArXiv dataset</a> from Kaggle into tables more suitable for data analysis (e.g. to add to a database or open in Power BI).
</p>

<p align='justify'>
The data begins as a single table with the ArXiv ID, submitter, authors, title, comments, journal reference, doi, report-no, categories, license, abstract, versions, update date, and a list of the authors in a parsed format.
</p>

This data will be processed into five tables:
- Submission, to record the submissions themselves
- Category, to record the categories a submission can be labelled as
- Author, to record the authors of the papers
- Submission-Category, to capture the many-to-many relationship between a submission and its categories.
- Submission-Author, to capture the many-to-many relationship between Submission and Author.

![arxiv-db](https://tomjdove.github.io/TomJDove/assets/arxiv/arxiv-db.png){: style="display: block; margin: 0 auto"}

<p align='justify'>
The dataset is quite large, so some of the computations take some time (but not 'leave your computer on overnight' time).
All of the code can be viewed on <a href = 'https://github.com/TomJDove/ArXiv-Investigation'>Github</a>.
</p>

<p align='justify'>
The processing will be done in six steps; the first filters out only the mathematics papers from the ArXiv dataset and then each of the five tables is created one by one.
</p>

```python
# Import required packages
import pandas as pd
import csv
from datetime import datetime
from dateutil import parser
from collections import defaultdict
import gender_guesser.detector as gender
```

#### Step 1: Filtering out maths submissions

<p align='justify'>
The ArXiv dataset contains papers from several different fields, but we only need the mathematics ones.
</p>

```python
# Determine whether a paper is a maths paper
def isMathCategory(categories):
    cats = categories.split(" ")
    for cat in cats:
        if cat[:cat.find(".")] == "math":
            return True
    return False

# Load the relevant data from the ArXiv file with a given filter on the categories.
# There is also the option to only load a selection of columns.
def loadArxivData(file, catFilter = lambda x : True, cols=None):
    f = open(file)
    data = []
    for line in f:
        doc = json.loads(line)
        if cols:
            lst = [doc[col] for col in cols]
        else:
            lst = doc
        if catFilter(doc['categories']):
            data.append(lst)
    f.close()
    return pd.DataFrame(data=data, columns=cols)
```

```python
# Load all the maths ArXiv data
fileName = 'data/arxiv-metadata-oai-snapshot.json'
arxiv_math = loadArxivData(fileName, catFilter = isMathCategory)

# Save to csv so that we don't need to re-collect the data each time
arxiv_math.to_csv('data/arxiv-math.csv', index=False)
```

#### Step 2: Submissions table

```python
# Get date of first submisson
arxiv_math['versions'] = arxiv_math['versions'].apply(eval)
arxiv_math['submission_date'] = arxiv_math['versions'].apply(lambda x : datetime.date(parser.parse(x[0]['created'])))

# Create submissions dataframe
submission_cols = ['id', 'submission_date', 'title', 'abstract', 'journal-ref', 'comments']
submission = arxiv_math[submission_cols].copy()
submission.rename(columns={'id':'arxiv_id'})

submission.to_csv('data/submission.csv', index=False, quoting=csv.QUOTE_NONNUMERIC)
```

#### Step 3: Category table

```python
# Create the category table, starting with the category names and acronyms (to be used as a primary key)
category_dict = {'AC':'Commutative Algebra',
                'AG':'Algebraic Geometry',
                'AP':'Analysis of PDEs',
                'AT':'Algebraic Topology',
                'CA':'Classicial Analysis and ODES',
                'CO':'Combinatorics',
                'CT':'Category Theory',
                'CV':'Complex Variables',
                'DG':'Differential Geometry',
                'DS':'Dynamical Systems',
                'FA':'Functional Analysis',
                'GM':'General Mathematics',
                'GN':'General Topology',
                'GR':'Group Theory',
                'GT':'Geometric Topology',
                'HO':'History and Overview',
                'IT':'Information Theory', 
                'KT':'K-Theory and Homology',
                'LO':'Logic',
                'MG':'Metric Geometry',
                'MP':'Mathematical Physics',
                'NA':'Numerical Analysis',
                'NT':'Number Theory',
                'OA':'Operator Algebras',
                'OC':'Optimization and Control',
                'PR':'Probability',
                'QA':'Quantum Algebra',
                'RA':'Rings and Algebras',
                'RT':'Representation Theory',
                'SG':'Symplectic Geometry',
                'SP':'Spectral Theory',
                'ST':'Statistics Theory'}


category = pd.DataFrame(category_dict.items(), columns = ['category_id', 'category_name'])
category.to_csv('data/category.csv', index=False)
```

#### Step 4: Author table

<p align='justify'>
This is the step where I use the authors first names to guess their genders.
I started by parsing the authors first and last names:
</p>


```python
# Create author table
arxiv_math['authors_parsed'] = arxiv_math['authors_parsed'].apply(eval)

names_list = arxiv_math['authors_parsed'].explode().to_list()
unique_names = [name for name in set(tuple(x[:2]) for x in names_list)]

author = pd.DataFrame()
author['surname'] = pd.Series([name[0] for name in unique_names])
author['first_name'] = pd.Series([name[1] for name in unique_names])

# Make the index the author id
author['author_id'] = author.index
author = author[['author_id', 'surname', 'first_name']]
```
<p align='justify'>
Next, I got a list of unique first names and applied the gender detector ot each of them.
The result was stored in a dictionary, which was used to add the genders of each of the authors in the author table.
</p>

```python
# Add genders
names = [x.split(' ')[0] for x in author['first_name'].to_list()]
unique_names2 = list(set(names))

# Guess the genders of all the names and construct a dictionary
d = gender.Detector()
genders = [d.get_gender(name) for name in unique_names2]

gender_dict = defaultdict(lambda :"unknown")
for name, gender_ in zip(unique_names2, genders):
    gender_dict[name] = gender_

genders = [gender_dict[name] for name in names]

author['gender'] = pd.Series(genders)
author.loc[(author['gender'] != 'male') & (author['gender'] != 'female'),'gender'] = 'unknown'

author.to_csv('author.csv', index=False)
```

#### Step 5: Submission-author table

```python
# Create a dict to map author name to index
author_dict = dict(zip(unique_names, author['author_id'].to_list()))

for name in unique_names[:5]:
    print(name, author_dict[name])

# Create submission-author dataframe

submission_author = arxiv_math[['id', 'authors_parsed']].copy().explode('authors_parsed')
submission_author['author_id'] = submission_author['authors_parsed'].apply(lambda x : author_dict[tuple(x[:2])])
submission_author.drop('authors_parsed', axis=1, inplace=True)
submission_author.rename(columns={'id':'arxiv_id'}, inplace=True)

submission_author.to_csv('submission_author.csv', index=False)
```

#### Step 6: Submission-category table

```python
# Create submission-category table
submission_category = arxiv_math[['id']].copy()
submission_category['category_id'] = arxiv_math['categories'].apply(lambda x : x.split(' '))

submission_category = submission_category.explode('category_id')

# Only want math categories
submission_category = submission_category[submission_category['category_id'].str.startswith('math')]
submission_category['category_id'] = submission_category['category_id'].apply(lambda x : x[5:])

submission_category.rename(columns={'id':'arxiv_id'}, inplace=True)

submission_category.to_csv('submission_category.csv', index=False)
```

<p align='justify'>
We now have all of the data processed into nice tables. 
I next uploaded the tables into Power BI to analyse the data.
</p>

## Results


Let's first look at the gender division of all of the authors:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/total-gender-prop.png"
  style="width:75%" 
  >
  <figcaption>
  The gender proportion for mathematics ArXiv papers.
  </figcaption>
</figure>
</center>

<p align='justify'>
The first thing to notice is that 43% of the names couldn't reasonably be used to guess a gender.
Likely their name was androgynous, unknown, or entered as an initial.
</p>

<p align='justify'>
Otherwise, the difference is stark: 47% are men and 11% are women.
Of the authors whose gender we could reasonably guess, less than 1 in 4 are women.
It might be reasonable to assume the unknown authors have a similar gender split.
If we generously assumed that the unknown authors were half men and half women, women would still only make up a third of authors.
</p>

<p align='justify'>
If we consider the change in proportions over time, there is some room for optimism:
</p>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/gender-by-year.png"
  >
  <figcaption>Gender proportion over time</figcaption>
</figure>
</center>

<p align='justify'>
If we graph only the proportion of women then we see a steady increase:
</p>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/women-trend.png"
  >
  <figcaption>
  The number of female authors is increasing!
  </figcaption>
</figure>
</center>

<p align='justify'>
There is a clear upward trend in the proportion of women submitting mathematics papers.
</p>

<p align='justify'>
There is too much uncertainty (in all aspects of this analysis) to make any quantitative conclusions about the gender division in mathematics ArXiv submissions.
Nonetheless, this dive into the ArXiv dataset corroborates the well-known gender disparity among mathematicians.
</p>


