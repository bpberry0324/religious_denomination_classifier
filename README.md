# On Catholicism, Orthodoxy, and Reddit.com

This survey evaluates the potential for predictively modeling the subreddits of two religious traditions (presently divided by schism but united by an older shared history) in comparison to one another, then examines the implications and further possibilities of these findings.

### Table of Contents:

- Part I: Summary of Findings
- Part II: File Directory
- Part III: Datasets Used
- Part IV: Conclusion

## Part I: Summary of Findings

The Eastern and Western Churches, sharing many of the same traditions, beliefs, and doctrines, are--as the result of a nine-century schism--currently not in communion with one another. Thus, with all that they have in common, a great deal of time has passed, and they have diverged from one another in noticeable ways, from their respective understandings of authority and dogma, to more workaday things like fasting practices and Eucharistic formalities. So just how much do they differ in their concerns and ways of communicating? (Or, how alike are they still?)

In its own way, this project seeks to explore this question by way of statistical modeling, and to determine what details the modeling process might unearth. Additionally then, it touches on deeper questions: If machine learning can detect measures of separation between two conjoined religious traditions, could it also detect shifts within a single tradition as they take place in realtime? Could such models pick up on the diverging of preoccupations of different subgroups and tell us something about their cause? Can we predict the formation of reactionary movements and their subsequent impact on the larger tradition?

At the beginning of this survey, upwards of 9,000 subreddit posts (and their corresponding titles and timestamps) were collected respectively from both r/Catholicism and r/OrthodoxChristianity. The cleaning process involved thoroughly parsing the data and compiling a dataframe consisting of the text body in a handful of different forms so as to facilitate a more nuanced modeling process. During this phase, many models were fit to the text data in its various forms, and all of them performed substantially better than the baseline. Ultimately the strongest model (at the time of the project deadline) is a logistic regression model fit to the words and potentially significant digits of the combined title and post body, stemmed and vectorized according to term frequency. The modeling of such a large dataset was of course time-intensive, and future fine-tuning might potentially make it stronger.

Coefficients of this final model confirm much of what the exploratory process adumbrated--that words signifying the subreddit's primary denomination of focus (i.e. 'catholic', 'orthodox', and their variants) served as major predictors in terms of class probability, as did words associated with particular doctrines, practices and/or figures of each respective tradition.

## Part II: File Directory

|File or Folder|Description|
|---|---|
|datasets/|folder including all datasets collected, revised, or used throughout the course of this project|
|modeling/|folder including Jupyter notebooks used to develop and evaluate the project's many classification models|
|main.ipynb|the project's primary Jupyter notebook, providing concise explanations of its approach and findings (with code and graphs)|
|preprocessing/|folder documenting initial data collection, cleaning and exploratory analysis|
|presentation.pdf|a PDF version of the slide presentation given in conjunction with the completion of this project|
|README.md|a summary of the project's aims, findings, data dictionary, and conclusions|
|visuals/|visuals used in the presentation and elsewhere|

## Part III: Datasets Used

- [`Catholicism.csv`](./datasets/Catholicism.csv): first batch of posts collected from the Catholicism subreddit (5000 entries)
- [`Catholicism2.csv`](./datasets/Catholicism2.csv): second batch of posts collected from the Catholicism subreddit (5000 entries)
- [`logreg.csv`](./datasets/logreg.csv): a dataset including the predictions of the final logistic regression model used alongside actual values
- [`main_final.csv`](./datasets/main_final.csv): the final dataset as written to the `datasets` folder after all preprocessing was completed; used for modeling
- [`main_revised.csv`](./datasets/main_revised.csv): the initial full dataset revised, with features engineered involving sentiment analysis
- [`main.csv`](./datasets/main.csv): the initial full dataset, combining all posts from both subreddits
- [`OrthodoxChristianity.csv`](./datasets/OrthodoxChristianity.csv): first batch of posts collected from the Orthodox Christianity subreddit (5000 entries)
- [`OrthodoxChristianity2.csv`](./datasets/OrthodoxChristianity2.csv): first batch of posts collected from the Orthodox Christianity subreddit (4500 entries)
- [`randomforest.csv`](./datasets/randomforest.csv): a dataset including the predictions of the final random forest model used alongside actual values

Below is a list of relevant features included in `main_final.csv`, the dataset upon which all classification models were fit:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|alltext|string|main_final.csv|text from each entry's title and post body, combined and parsed|
|author|string|main_final.csv|the author of each corresponding entry|
|comp_lem|string|main_final.csv|the full preprocessed text of an entry (words and potentially relevant digits), lemmatized|
|comp_stem|string|main_final.csv|the full preprocessed text of an entry (words and potentially relevant digits), stemmed|
|created_utc|int|main_final.csv|the Unix timestamp of each corresponding entry|
|lowtext|string|main_final.csv|combined and parsed text, made lowercase|
|selftext|string|main_final.csv|original post body of each corresponding entry|
|sent_inter|float|main_final.csv|the product of each coresponding entry's sentiment analysis label and respective probability|
|sent_label|int|main_final.csv|the label resulting from performing sentiment analysis on each corresponding entry, encoded (1 for 'POSITIVE' and -1 for 'NEGATIVE')|
|sent_score|float|main_final.csv|the probability assigned to each corresponding entry's sentiment analysis label|
|simp_lem|string|main_final.csv|the full preprocessed text of an entry (words), lemmatized|
|simp_stem|string|main_final.csv|the full preprocessed text of an entry (words), stemmed|
|status_length|int|main_final.csv|number of characters in each corresponding post body|
|status_word_count|int|main_final.csv|number of words in each corresponding post body|
|subreddit|int|main_final.csv|the subreddit for each corresponding entry, dummified (1 for Catholicism and 0 for Orthodox Christianity)|
|title|string|main_final.csv|the title of each corresponding entry|
|title_length|int|main_final.csv|number of characters in each corresponding title|
|title_word_count|int|main_final.csv|number of words in each corresponding title|
|unstopped|string|main_final.csv|combined and parsed text, made lowercase and with stopwords removed|

## Part IV: Conclusion

The central premise of the project--that classification of posts according to denomination (or at least according to subreddit) is to a high degree possible--has been confirmed by the final model. There may still be room for future revision to make this model even more accurate and to ease down some of the overfitting, but even at present, it performs well above the baseline. Further, it does so largely by picking up on themes and preoccupations on which these denominations diverge, shedding light for observers on the nature of these differences.

Such capacity could indeed be used in the future not merely to detect differences between two "similar" denominations, but between subgroups or subsects within a single denomination, and illustrate the ways that they might differ. In addition to being of interest to any adherents to such traditions, this might also allow for anticipating and understanding movements as they form, and the degree to which this or that subpopulation does or does not transform as a result.
