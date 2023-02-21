Day 1 - Simple Logistic Regression
================

In this repository/directory you should see two items:

- `README.md` - this document.
- `activity06.Rmd` - the file you will complete in RStudio for this
  week.

## Task 1: Open the RMarkdown document

Read these directions first, then work through them.

- In the **Files** pane of RStudio, locate and click on the
  `activity06.Rmd` file to open it.
- This file is essentially a blank document with only a `title` and
  `output` option (to produce a GitHub friendly Markdown file). You will
  follow the tasks in this `README` file and do the work (coding,
  responding, etc.) in RStudio.

As you work through this activity, be descriptive in your response to
questions and even leave comments in your code to help you understand
what you are doing. These are your notes to yourself. How can you make
it easier for *future* your to remember what *current* you is
thinking/doing?

## Task 2: Load the necessary packages

Again, we will use two packages from Posit (formerly
[RStudio](https://posit.co/)): `{tidyverse}` and `{tidymodels}`.

- Once you have verified that both `{tidyverse}` and `{tidymodels}` are
  already installed (remember how to do this in the **Packages** pane?),
  load these packages in the R chunk titled `setup`. Press Enter/Return
  after line 7 to add more code lines, then type the following:

  ``` r
  library(tidyverse)
  library(tidymodels)
  ```

- Run the `setup` code chunk or **knit**
  <img src="../README-img/knit-icon.png" alt="knit" width = "20"/> icon
  your Rmd document to verify that no errors occur.

<!-- Since we will be looking at many relationships graphically, it will be nice to not have to code each of these individually.
`{GGally}` is an extension to `{ggplot2}` that reduces some of the complexities when combining multiple plots.
For example, [`GGally::ggpairs`](http://ggobi.github.io/ggally/articles/ggpairs.html) is very handy for pairwise comparisons of multiple variables.

- In the **Packages** pane of RStudio, check if `{GGally}` is already installed.
  Be sure to check both your **User Library** and **System Library**.
  **We used this last activity so it should already be there.**
- Once you have verified that `{GGally}` is installed, load it in the R chunk titled `setup`.
  Add another code line in this chunk, then type the following:
  
  
  ```r
  library(GGally)
  ```
  
- Run the `setup` code chunk or **knit** <img src="../README-img/knit-icon.png" alt="knit" width = "20"/> icon your Rmd document to verify that no errors occur.
-->

Remember to organize your RMarkdown document using your amazing Markdown
skills 😄

## Task 3: Load the data and

The data we are working with is again from the OpenIntro site. Read in
the following **CSV** file using the URL method:
`https://www.openintro.org/data/csv/resume.csv`

- Create a new R code chunk to read in the linked CSV file.
- Rather than downloading this file, uploading to RStudio, then reading
  it in, explore how to load this file directly from the provided URL
  with the appropriate `{readr}` function (remember that `{readr}` is
  part of `{tidyverse}` so you do not need to load/`library` it
  separately).
- Assign this data set into a data frame named `resume`.

### The data

From OpenIntro’s [description of the
data](https://www.openintro.org/data/index.php?data=resume):

> This experiment data comes from a study that sought to understand the
> influence of race and gender on job application callback rates. The
> study monitored job postings in Boston and Chicago for several months
> during 2001 and 2002 and used this to build up a set of test cases.
> Over this time period, the researchers randomly generating résumés to
> go out to a job posting, such as years of experience and education
> details, to create a realistic-looking résumé. They then randomly
> assigned a name to the résumé that would communicate the applicant’s
> gender and race. The first names chosen for the study were selected so
> that the names would predominantly be recognized as belonging to black
> or white individuals. For example, Lakisha was a name that their
> survey indicated would be interpreted as a black woman, while Greg was
> a name that would generally be interpreted to be associated with a
> white male.

Review the description page. If you still have questions, review the
**Source** at the bottom of the description page. Additionally, you can
use `dplyr::glimpse` to see some meta information about the R data
frame. After doing this, answer the following questions:

1.  Is this an observational study or an experiment? Explain.

2.  The variable of interest is `received_callback`. What type of
    variable is this? What do the values represent?

3.  For `received_callback`, create an appropriate data visualization
    using `{ggplot2}`. Be sure to provide more descriptive labels (both
    axes labels and value labels - there are many ways to do this) as
    well as an appropriate title.

4.  Below, I provide you with a numerical summary table that should
    reiterate (i.e., provides numerical values) your plot in (3). Write
    the code to produce this table.

| received_callback |    n | percent |
|:------------------|-----:|--------:|
| No                | 4478 |   91.95 |
| Yes               |  392 |    8.05 |

5.  Using the output from (4) and (5), what do you notice?

## Task 4: Probability and odds

Using your output from (4) and (5), answer the following questions:

6.  What is the probability that a randomly selected résumé/person will
    be called back?

7.  What are the **odds** that a randomly selected résumé/person will be
    called back?

## Task 5: Logistic regression

Logistic regression is one form of a *generalized linear model*. For
this type of model, the outcome/response variable takes one one of two
levels (sometimes called a binary variable or a two-level categorical
variable).

In our activity, $Y_i$ takes the value 1 if a résumé receives a callback
and 0 if it did not. Generally, we will let the probability of a
“success” (a 1) be $p_i$ and the probability of a “failure” (a 0) be
$1 - p_i$. Therefore, the odds of a “success” are:

$$
\frac{Pr(Y_i = 1)}{Pr(Y_i = 0)} = \frac{p_i}{1-p_i}
$$

From your reading, you saw that we use the *logit function* (or *log
odds*) to model binary outcome variables:

$$
\begin{equation*}
\log\left(\frac{p_i}{1-p_i}\right) = \beta_0 + \beta_1 X
\end{equation*}
$$

To keep things simpler, we will first explore a logistic regression
model with a two-level categorical explanatory variable: `race` - the
inferred race associated to the first name on the résumé. Below is a
two-way table (also known as a contingency table or crosstable), where
the rows are the response variable levels, the columns are the
explanatory variable levels, and the cells are the percent (and number
of in parentheses). Note that the values in each column add to 100%.

| received_callback | Black        | White        |
|:------------------|:-------------|:-------------|
| No                | 93.55 (2278) | 90.35 (2200) |
| Yes               | 6.45 (157)   | 9.65 (235)   |

Using the above table, answer the following question:

6.  What is the probability that a randomly selected résumé/person
    perceived as Black will be called back?

7.  What are the **odds** that a randomly selected résumé/person
    perceived as Black will be called back?

This process of calculating conditional (e.g., if a résumé/person
perceived as Black is called back) odds will be helpful as we fit our
logistic model. We will now begin to use the `{tidymodel}` method for
fitting models. A similar approach could be used for linear regression
models and you are encouraged to find out how to do this in your past
activities.

- Create a new R code chunk and type the following, then run your code
  chunk or knit your document.

  ``` r
  # The {tidymodels} method for logistic regression requires that the response be a factor variable
  resume <- resume %>% 
    mutate(received_callback = as.factor(received_callback))

  resume_mod <- logistic_reg() %>%
    set_engine("glm") %>%
    fit(received_callback ~ race, data = resume, family = "binomial")

  tidy(resume_mod) %>% 
    knitr::kable(digits = 3)
  ```

After doing this, respond to the following questions:

8.  Write the estimated regression equation. Round to 3 digits.

9.  Using your equation in (8), write the *simplified* estimated
    regression equation corresponding to résumés/persons perceived as
    Black. Round to 3 digits.

Based on your model, if a randomly selected résumé/person perceived as
Black,

10. What are the log-odds that they will be called back?

11. What are the odds that they will be called back? How does this
    related back to your answer from (7)? *Hint*: In (9) you obtained
    the log-odds (i.e., the natural log-odds). How can you
    back-transform this value to obtain the odds?

12. What is the probability that will be called back? How does this
    related back to your answer from (6)? *Hint* Use the odds to
    calculate this value.

## What is next?

We will fit more advanced logistic models and assess the fit of these
models.
