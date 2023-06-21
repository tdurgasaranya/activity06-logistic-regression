Day 1 - Logistic Regression
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
**Source** (also linked to shortly) at the bottom of the description
page. On an initial reading, there are some concerns with how this study
is designed. In [the
article](https://www.nber.org/system/files/working_papers/w9873/w9873.pdf),
the authors do point out these concerns (in Sections 3.5 and 5.1).

Recall that you can use `dplyr::glimpse` to see some meta information
about the R data frame. After doing this and your review of the data’s
description page, answer the following questions:

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

7.  What are the [**odds**](https://en.wikipedia.org/wiki/Odds) that a
    randomly selected résumé/person will be called back?

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

## Challenge: Extending to Mulitple Logistic Regression

We will explore the following question: Is there a difference in call
back rates in Chicago jobs, after adjusting for the an applicant’s years
of experience, years of college, race, and sex? Specifically, we will
fit the following model, where $\hat{p}$ is the estimated probability of
receiving a callback for a job in Chicago.

$$
\begin{equation*}
\log\left(\frac{\hat{p}}{1-\hat{p}}\right) = \hat\beta_0 + \hat\beta_1 \times (\texttt{years\\_experience}) + \hat\beta_2 \times (\texttt{race:White}) + \hat\beta_3 \times (\texttt{sex:male})
\end{equation*}
$$

Note that the researchers have the variable labeled `gender`, but this
is likely meant to be `sex`. [Curious as to what the difference
is](https://www.merriam-webster.com/words-at-play/sex-vs-gender-how-they2019re-different)?

- Create a new R code chunk and type the following, then run your code
  chunk or knit your document.

  ``` r
  resume_select <- resume %>% 
    rename(sex = gender) %>% 
    filter(job_city == "Chicago") %>% 
    mutate(race = case_when(
           race == "white" ~ "White",
           TRUE ~ "Black"
         ),
         sex = case_when(
           sex == "f" ~ "female",
           TRUE ~ "male"
         )) %>% 
    select(received_callback, years_experience, race, sex)
  ```

After doing this, answer the following question:

1.  Explain what six things the above code does in the context of this
    problem.

## Relationship Exploration

There are many variables in this model. Let’s explore each explanatory
variable’s relationship with the response variable. Note that I tried to
explore this using `GGally::ggbivariate`, but kept running into an error
that I did not have time to explore.

- Create a new R code chunk and create an appropriate data visualization
  to explore the relationship between `resume_select` and each of the
  explanatory variables, then run your code chunk or knit your document.

After doing this, answer the following question:

2.  Describe any patterns. What do you notice?

## Fitting the model

Aside: I kept running into an issue using `{tidymodels}` to fit this
model so I defaulted back to a method that I know works using `glm`. I
will keep exploring why I was experiencing issues and update you all
with a more modern method later this semester.

- Create a new R code chunk and type the following, then run your code
  chunk or knit your document.

  ``` r
  mult_log_mod <- glm(received_callback ~ years_experience + race + sex, data = resume_select, family = "binomial")

  tidy(mult_log_mod)
  ```

Focusing on the estimated coefficient for `years_experience`, we would
say:

> For each additional year of experience for an applicant in Chicago, we
> expect the *log odds* of an applicant receiving a call back to
> increase by 0.045 units. Assuming applicants have similar time in
> spent in college, similar inferred races, and similar inferred sex.

This interpretation is somewhat confusing because we are describing this
in *log odds*. Fortunately, we can convert these back to odds using the
following transformation:

$$
\text{odds} = e^{\log(\text{odds})}
$$

- Create a new R code chunk and type the following, then run your code
  chunk or knit your document.

  ``` r
  tidy(mult_log_mod, exponentiate = TRUE) %>% 
    knitr::kable(digits = 3)
  ```

After doing this, answer the following question:

2.  Interpret the estimated coefficient for `years_experience`.

## Assessing model fit

Now we want to check the residuals of this model to check the model’s
fit. As we saw for multiple linear regression, there are various kinds
of residuals that try to adjust for various features of the data. Two
new residuals to explore are *Pearson residuals* and *Deviance
residuals*.

**Pearson residuals**

The Pearson residual corrects for the unequal variance in the raw
residuals by dividing by the standard deviation.

$$
\text{Pearson}_i = \frac{y_i - \hat{p}_i}{\sqrt{\hat{p}_i(1 - \hat{p}_i)}}
$$

**Deviance residuals**

Deviance residuals are popular because the sum of squares of these
residuals is the deviance statistic. We will talk more about this later
in the semester.

$$
d_i = \text{sign}(y_i - \hat{p}_i)\sqrt{2\Big[y_i\log\Big(\frac{y_i}{\hat{p}_i}\Big) + (1 - y_i)\log\Big(\frac{1 - y_i}{1 - \hat{p}_i}\Big)\Big]}
$$

Since Pearson residuals are similar to residuals that we have already
explored, we will instead focus on the deviance residuals.

- Create a new R code chunk and type the following, then run your code
  chunk or knit your document.

  ``` r
  # To store residuals and create row number variable
  mult_log_aug <- augment(mult_log_mod, type.predict = "response", 
                        type.residuals = "deviance") %>% 
                        mutate(id = row_number())

  # Plot residuals vs fitted values
  ggplot(data = mult_log_aug, aes(x = .fitted, y = .resid)) + 
  geom_point() + 
  geom_hline(yintercept = 0, color = "red") + 
  labs(x = "Fitted values", 
       y = "Deviance residuals", 
       title = "Deviance residuals vs. fitted")

  # Plot residuals vs row number
  ggplot(data = mult_log_aug, aes(x = id, y = .resid)) + 
  geom_point() + 
  geom_hline(yintercept = 0, color = "red") + 
  labs(x = "id", 
       y = "Deviance residuals", 
       title = "Deviance residuals vs. id")
  ```

Here we produced two residual plots: the deviance residuals against the
fitted values and the deviance variables against the index id (an index
plot). The index plot allows us to easily see some of the more extreme
observations - there are a lot ($|d_i| > 2$ is quiet alarming). The
residual plot may look odd (why are there two distinct lines?!?), but
this is a pretty typical shape when working with a binary response
variable (the original data is really either a 0 or a 1). In general
because there are so many extreme values in the index plot, this model
leaves room for improvement.

## What is next?

We will continue exploring classification models with *multinomial
regression*. This is an extension of logistic regression when our
response variable has more than two levels (i.e., from a multinomial
distribution instead of a binomial distribution).
