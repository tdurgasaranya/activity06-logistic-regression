Activity 06 - Logistic Regression
================

This activity is intended to be completed in one week - outside of class
preparation work and three 75-minute class meetings. On our Blackboard
course site you were provided with items to read, watch, and do prior to
attempting this activity. Do not proceed in this activity until you have
minimally:

1.  (Day 1 portion) Read *ISL* [Sections 4.3.0 -
    4.3.4](https://hastie.su.domains/ISLR2/ISLRv2_website.pdf).
2.  (Week 8 portion) Read *ISL* [Sections 4.3.5](https://rdcu.be/c5fqV).

In this repository/directory, you should see five items:

- `README-img` - a folder containing images that I am embedding within
  this `README.md` file and other files. You do not need to do anything
  with this.
- `.gitignore` - a file that is used to specify what Git can ignore when
  pushing to GitHub. You do not need to do anything with this.
- `README.md` - the document you are currently reading.
- `day01-logistic` - a folder that contains items for you to complete
  during the first 75-minute class meeting.
- `day02-multinomial` - a folder that contains items for you to complete
  during Week 8.

We will explore most of these items over this week. Before doing that,
you will first make your own copy of this repository.

![check-in](README-img/noun-magnifying-glass.png) **Check in**

Do you want an interactive way to check your understanding outside of
class? Remember that these are a good way to check your foundation
understanding and were created by [Benjamin
Baumer](https://beanumber.github.io/www/) (associate professor at Smith
College), in collaboration with the OpenIntro team and others. The
following tutorials will provide you with an applied approach to our
topics (reorganized to better correspond with our readings):

Day 1:

- *ISL* 3.2 & 3.3 - [Logistic
  regression](https://openintro.shinyapps.io/ims-03-model-09/)

Week 8:

- There is no interactive tutorial that corresponds to multinomial
  logistic regression.

## Task 1: Forking & cloning

### Forking

Read these directions first, then work through them. In this GitHub repo
(i.e., my repo):

1.  Click on the ![fork](README-img/fork-icon.png) **Fork** icon near
    the upper-right-hand corner. You will be taken to a **Create a new
    fork** screen.
2.  Verify that your GitHub username is selected under **Owner** and
    that the **Repository name** is `activity06-logistic-regression`
    with a green check mark (this verifies that you do not already have
    a GitHub repository with this name).
3.  You may provide a **Description** if you would like. This is a way
    to provide some additional, more descriptive, meta information
    related to the things you did. I like to provide a brief description
    of what happened.
4.  Verify that **Copy the `main` branch only** is selected.
5.  Click on the green **Create fork** button at the bottom of this
    page.

You should be taken a copy of this repo that is in your GitHub account.
That is, your page title should be
`username/activity06-logistic-regression`, where `username` is replaced
with your GitHub username. Directly below this, you will see the
following message:

> forked from
> [gvsu-sta631/activity06-logistic-regression](https://github.com/gvsu-sta631/activity06-logistic-regression)

You will complete the rest of this activity in **your** forked copy of
the `activity06-logistic-regression` repo.

### Cloning

Read these directions first, then work through them. Note that you will
be switching between RStudio and your GitHub repo (that you previously
forked).

1.  In RStudio, click on the
    <img src="README-img/rproj-icon.png" alt="RStudio Project" width = "20"/>
    icon (the icon below the Edit drop-down menu).
2.  Click on **Version Control** on the *New Project Wizard* pop-up.
3.  Click on **Git** and you should be on a “Clone Git Repository” page.
4.  Back to **your** `activity06-logistic-regression` GitHub repo, click
    on the green **Code** button near the top of the page.
5.  Verify that **HTTPS** is underlined in orange/red on the drop-down
    menu, then copy the URL provided.
6.  Back in RStudio, paste the URL in the “Repository URL” text field.
7.  The “Project directory name” text field should have automatically
    populated with `activity06-logistic-regression`. If yours did not
    (this is usually an issue on Macs),
    - Click back into the “Repository URL” text field.
    - Highlight any bit of this text (it does not seem to matter what or
      how much).
    - Press Ctrl/Cmd and the “Project directory name” should now have
      automatically populated with `activity06-logistic-regression`.
8.  Browse to `STA 631/Activities` (assuming you followed my opinionated
    file structure from earlier in the semester), then click **Choose**.
9.  Click on **Create Project**.

Your screen should refresh and the **Files** pane should say that you
are currently in your `activity06-logistic-regression` folder that
currently has the same files and folders as your GitHub repo. If you are
asked for your GitHub credentials, provide your GitHub username and your
PAT (not your password).

![check-in](README-img/noun-magnifying-glass.png) **Check in**

Take a moment to reflect on what is possibly your second time doing this
forking process.

- How is this process going for you? Is it “muscle memory” yet?
- What is easier since last week?
- What do you still need help remembering?

We will use a dataset with information from résumés and job callbacks.

## Task 2: Odds and logistic regression

Read these directions first, then work through them.

1.  In your `activity06-logistic-regression` repo folder/directory,
    locate and click into the `day01-logistic` subfolder.
2.  In the `day01-logistic` subfolder, you will be greeted by a new
    `README.md` file. Do your best to complete the tasks/directions
    provide in this subfolder by **11:59 pm (EST) on Tue, Feb 21**.
3.  Ask questions in class as you are working. If you need to finish
    this up outside of our class meetings, remember that you can use our
    Teams workspace (linked on Blackboard), and post questions/issues in
    the **Muddy** channel. If someone else already posted what you
    though was muddy, add any clarification to their post and give them
    a “+ 1” 👍. Remember that this space is for conversations as well as
    posting questions. Read through your peers’ muddy posts and do your
    best to provide help.

The rest of this `README` document contains tasks/directions for the
second class meeting of this week.

## Task 3: Mulinomial logistic regression

You will work in `activity06-multinomial.Rmd` file for this portion of
the activity as we are working with a different dataset. Read these
directions first, then work through them.

1.  In your `activity06-logistic-regression` repo folder/directory,
    locate and click into the `day03-multinomial` subfolder.
2.  In the `day03-multinomial` subfolder, you will be greeted by a new
    `README.md` file. Do your best to complete the tasks/directions
    provide in this subfolder by **11:59 pm (EST) on Tue, Feb 28**.
3.  Ask questions in class as you are working. If you need to finish
    this up outside of our class meetings, remember that you can use our
    Teams workspace (linked on Blackboard), and post questions/issues in
    the **Muddy** channel. If someone else already posted what you
    though was muddy, add any clarification to their post and give them
    a “+ 1” 👍. Remember that this space is for conversations as well as
    posting questions. Read through your peers’ muddy posts and do your
    best to provide help.

## Attribution

This document is based on materials from
[OpenIntro](https://www.openintro.org/) and [Dr. Maria
Tackett](https://scholars.duke.edu/person/maria.tackett) (Duke
University).

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png"
style="border-width:0" alt="Creative Commons License" /></a><br />This
work is licensed under a
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative
Commons Attribution-ShareAlike 4.0 International License</a>.
