---
layout: post
title: "A Dive in the ArXiv: Gender Equality"
date: 2023-07-04
categories: 
---

<!---
Other title ideas:
- An ArXiv of gender equality in mathematics
- ArXiv dive: gender equality
-->


## What is ArXiv?

Owned and operated by Cornell University, ArXiv is an open-access repository of scientific papers in fields ranging from mathematics and physics to quantitative biology and economics.
First established in 1991, it now holds over 2 million scholarly articles, and almost every mathematics paper that is written will be uploaded to ArXiv.

To make ArXiv more accessible, Cornell has shared the metadata of its submissions on [Kaggle](https://www.kaggle.com/datasets/Cornell-University/arxiv).
Here, you can view information about each of the 1.7 million submissions, including the title, abstract, author names, and submission date.
You can also do some calculations; for example, there are currently almost 45,000 mathematics papers uploaded each year:

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

There are other cool observations to be made in this trove of data.
For example, of the 594,000ish total submissions, almost a quarter had journal references, which means they were likely published in a peer-reviewed journal.
Even more interestingly, the annual proportion of submissions with journal references has dramatically declined in the last two decades.
As we see in the above chart, it starts at around 40% and has plummeted to below 10%.
Does this indicate a rise in hobbyist mathematics posting papers to ArXiv?

Another fun fact: since there are currently about 594,000 mathematics posts on ArXiv, a lucky mathematician will soon post the 600,000th mathematics paper to ArXiv (congratulations to this person).

Putting fun aside, I wanted to get something more meaningful from the ArXiv data.
Could this dataset give us any information on the gender balance in mathematics?
An author does not submit their gender when uploading a paper, so it doesn't seem like we have much information to go on.


## Gender inequality in mathematics

Gender inequality is a well-known issue in STEM, and it is especially serious in mathematics.
Despite girls performing as well if not better than boys in maths at school, the proportion of women studying and working in mathematical sciences is significantly lower than it ought to be.

If we look at the numbers for Australia, the problem is quite visible:
 - Women make up only 37% of undergraduate mathematical science degrees and 29% of postgraduate degrees, according to [STEM Women](https://www.stemwomen.com/women-in-stem-australia).
- [Government data](https://labourmarketinsights.gov.au/occupation-profile/mathematicians?occupationCode=224112) reveals that women make up only 23% of mathematicians.
- Only [9% of professors](https://www.sydney.edu.au/news-opinion/news/2016/03/30/australia_s-got-scientific-female-talent---heres-how-to-stop-was.html) in mathematical science are women.

So, there is no shortage of evidence for the gender gap in mathematics, but I want to see whether it can be seen in the ArXiv data.
The problem is that authors do not share their gender when uploading papers.
We only have one piece of information that could indicate an author's gender: their first name.

## Getting on a first-name basis

The idea is to use the first names of the authors to get a very (repeat *very*) crude idea of the gender disparity in ArXiv postings.
I figure that, for certain names, one could take a reasonable guess at which gender this person identifies as.
If an author's name is Thomas, for example, they will probably (if not necessarily) identify as a man.

There are indeed commercially available tools to achieve this.
[Gender Guesser](https://gender-guesser.com/) claims to be the best on the market: 8 billion names processed in 22 alphabets, contributions to scientific research, and a slew of fancy academic and corporate users.
With thousands of names to process and a PhD student salary, I decided to use the freely available Python package [gender-guesser](https://github.com/lead-ratings/gender-guesser), which is based on a comparatively tiny dataset of 40,000 names collected by a man named Jorg Michael.

The Python package assigns a name to one of five categories: male, mostly male, unknown, mostly female, and female.
I simplified this to three categories: man, unknown, and woman, with the 'mostly' entries being put into the unknown category.

Now, this method is riddled with flaws and limitations:
- It excludes those who don't identify as either a man or a woman.
- Some names are commonly used by people of all genders and so even with the best possible methods we couldn't determine their gender.
- Many authors prefer to just give their first initial or submit their name in some non-standard way, which messes the data up.

So, we certainly shouldn't be using this method to produce any hard quantitative conclusions.
Nonetheless, if there's a very clear gender disparity, we might be able to pick up on it.

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

The first thing to notice is that 43% of the names couldn't reasonably be used to guess a gender.
Likely their name was androgynous, unknown, or entered as an initial.

Otherwise, the difference is stark: 47% are men and 11% are women.
Of the authors whose gender we could reasonably guess, less than 1 in 4 are women.
It might be reasonable to assume the unknown authors have a similar gender split.
If we generously assumed that the unknown authors were half men and half women, women would still only make up a third of authors.

If we consider the change in proportions over time, there is some room for optimism:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/arxiv/gender-by-year.png"
  >
  <figcaption>Gender proportion over time</figcaption>
</figure>
</center>

If we graph only the proportion of women then we see a steady increase:

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

There is a clear upwards trend in the proportion of women submitting mathematics papers.

There is too much uncertainty (in all aspects of this analysis) to make any quantitative conclusions about the gender division in mathematics ArXiv submissions.
Nonetheless, this dive into the ArXiv dataset corroborates the well-known gender disparity among mathematicians.


## Technical details

Though it was an interesting project, the world hardly needs additional low-quality evidence of gender differences in STEM (actionable solutions would likely be preferable).
My main goal was to practise my data skills.
I will therefore describe the process:
1. Data was collected from Kaggle in the form of a .json file.
2. Python (Pandas) was used to filter out the mathematics submissions and process the data into tables.
This included parsing the author names, guessing their gender, and assigning author IDs to serve as the primary key.
![arxiv-db](https://tomjdove.github.io/TomJDove/assets/arxiv/arxiv-db.png){: style="display: block; margin: 0 auto"}
3. The tables were loaded into Power BI desktop, which was used to create the visuals.
The Power BI report can be found [here](https://app.powerbi.com/links/RDRqrHuPyW?ctid=149053c5-55e1-4229-a5b9-0efb72205d64&pbi_source=linkShare).

All of the code can be viewed on [Github](https://github.com/TomJDove/ArXiv-Investigation).

