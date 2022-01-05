# Phase4-NLP

This repo was created as part of a project for the Flatiron School Data Science course. Per the course website, the suggested task is to:

    "Build a model that can rate the sentiment of a Tweet based on its content."

Although we may refine this task as time allows.


# The Data

The data for this project was provided by data.world, and can be found here: https://data.world/crowdflower/brands-and-product-emotions

The data set contains 9093 tweets about tech products that human raters have flagged as either positive, negative, or neutral.

For the moment, our plan is to train a model to determine what sort of sentiment the the tweet expresses. Having such a model would allow PR teams to scan for tweets that might relate to their products and react to potencial swings in sentiment, especially around particular updates or events that might prompt changes to overall sentiment towards their products. 

# Preprocessing

Preprocessing text is a critical part of any NLP project. A few tweaks have been made to typical text preprocessing to account for the particular nature of this dataset.  Because the dataset we are working on is pulled from tweets, a few adjustments have been made. We are dropping all @'s, as who a person is talking too does not matter to emotional sentiment (a client may wish to whitelist their own handle or the handle of a product rival for later modelling purposes). Additionally, the dataset has several over represented hashtags, particularly SXSW. This is an artifact of data collection and has been hardcoded out of the model at the moment by adding SXSW and varients into the stopwords list. Further manual additions to the stop words may follow.

# The Model
