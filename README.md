# Phase4-NLP

This repo was created as part of a project for the Flatiron School Data Science course. Per the course website, the suggested task is to:

    "Build a model that can rate the sentiment of a Tweet based on its content."

We may refine this task as time allows.

For the moment, our plan is to train a model to determine what sort of sentiment the the tweet expresses. Having such a model would allow PR teams to scan for tweets that might relate to their products and react to potencial swings in sentiment, especially around particular updates or events that might prompt changes to overall sentiment towards their products. 

# The Data

The data for this project was provided by data.world, and can be found [here](https://data.world/crowdflower/brands-and-product-emotions).

The data set contains 9093 tweets about tech products that human raters have flagged as either positive, negative, or neutral. The tweets were largely directed at various products, mostly Apple or Google tech products and apps. They were collected in a fairly narrow timeframe, apparently around the South by Southwest confrence, for some reason. Because these tweets include a lot of commentary about tech products, they make a reasonably good starting place for a generic tech company looking to assess the sentiments displayed for their own products.

# Preprocessing

Preprocessing text is a critical part of any NLP project. A few tweaks have been made to typical text preprocessing to account for the particular nature of this dataset.  For the most part, we are leaning on the default tokenizing pattern within the sklearn vectorizers. As for specific tweaks, the dataset has several over represented hashtags, particularly SXSW. This is an artifact of the initial data collection. We have hardcoded SXSW into out of the model at the moment by adding SXSW into the stopwords list, along with @mention, which is overrepresented due to its common use on Twitter. Further manual additions to the stop words may follow.

# The Model

Our baseline model expects an accuracy rating of approximately 61%.

We prepared and tested numerous models, using GridSearch to sort through hyperparameter options. Although the RandomForestClassifier scored almost as well as the Multinomial Naive Bayes model, the Multinomial Naive Bayes model worked considerably faster. Given that, we opted for the naive Bayes model for our final model, as that model works better for a client attempting to repeatedly process large batches of tweets. 

Currently, our best model scores at approx 69% accuracy on cross-validation.

# Analysis and Results

Our model does fairly well, but due to class imbalances in the final dataset it has a hard time with negative sentiment specifically. We can see this in a low F1 score, and the recall. We could push the model thresholds to tag more negative tweets, but this would then require a human to sort through to compensate for the increase in false positives of negative sentiment.

| Neutral     |             | Positive   |             | Negative   |             |
| ----------- | ----------- |----------- | ----------- |----------- | ----------- |
| Precision   | .70         | Precision  | .60         | Precision  | .78         |
| Recall      | .84         | Recall     | .48         | Recall     | .14         |
| F1-score    | .76         | F1-score   | .53         | F1-score   | .24         |

# Recommendation

If we were to recommend action on the part of the client, we would recommend that they focus on the aggregate proportion of negative tweets to positive tweets, rather than focusing on attempting to flag particular instances or negative tweets. A time series model based on rolling snapshots of twitter would be helpful in this case. Additionally, further resouces could be put into creating a model that automates discovery of the client's product, creating a training dataset specific to the client's products, or finding more negative sentiment tweets to aid model training. 

# Navigating this Repository

The data for the project has been stored in the data folder. There is a folderr with notebooks consisting of early EDA, data preprocessing, and model experimentation. Important steps were taken from there and used to prepare data for the main notebook, which includes the iterative model building process. There are several grid search models in the main notebook which have been commented out, because they take a long time to run, but the best results from each grid have been preserved. The main notebook also contains the final model, various scoring and analysing techniques, and the creation of visuals for the presentation to the stakeholders.

## For More Information
Please review our full analysis in our [Jupyter Notebook](./main_notebook.ipynb) or [presentation deck](./presentation.pdf).

For additional questions, please contact [Vu](mailto:avbrown313@gmail.com) or [Julian](mailto:wardjulianm@gmail.com).

# Repository Structure
```
├── README.md                           <- The top-level README for viewers of this repository
├── main_notebook.ipynb                 <- Narrative documentation of analysis performed in Jupyter Notebook
├── presentation.pdf                    <- PDF version of presentation to stakeholders
├── data                                <- Sourced externally from data.world
└── supplementary_notebooks             <- Notebooks used for model experimentation and development of the main notebook.
```
