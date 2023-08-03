I (Ana Martinovici) use this repo to check what happens when I change data in Qualtrics.

# How to detect if Qualtrics data was altered

Both 1 and 2 need to be done:

1. export data twice, with and without selecting "exclude survey response edits"

By comparing these two data exports, we can figure out which fields, if any were manually changed in the browser. This is the equivalent of finding the grey triangle (notch), but much faster and without the risks involved by human-performed visual search.

2. add embedded data fields and check their values. Specifically: `Q_R`, `Q_R_DEL`, and `Q_URL`. 

If any if the responses were retaken, then those responses will have `Q_R_DEL=1`, a value for `Q_R` (the old `ResponseId`), and the `Q_URL` will indicate that the response was retaken (it is different from the other ones and includes embeded fields in the URL)

To be able to perform 1 and 2, we need access to the Qualtrics survey (add as collaborator with full rights to edit the survey and export data).


# Summary of steps

Specifically, I will:

- create a simple Qualtrics survey:
  - two conditions (A and B) with random assignment
  - within each condition, one question that is shown only to that group
  - a second question that is shown to all participants, no matter the group

After setting up the survey:

1. answer the survey. Enter text to each of the questions. 6 responses, hopefully this means 3 / condition
2. download the data using the default settings in qualtrics
3. change one response in the browser (Data & Analysis tab)
4. retake another response and make no change
5. retake another response and make one change
6. when retaking the responses, pay attention to which condition I am assigned to this time
7. export data without selecting "exclude survey response edits"
8. export data WITH "exclude survey response edits"
9. add embedded data fields
10. export data without selecting "exclude survey response edits"
11. export data WITH "exclude survey response edits"

You can use `data_checked.Rmd` to see which checks I've made. The file doesn't yet have detailed explanations, 
feel free to do a pull request.
