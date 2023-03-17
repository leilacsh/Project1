## Background
Deafness and blindness are two separate conditions that can affect individuals of all ages and backgrounds.

Deafness, also known as hearing loss, is a condition where a person has a partial or complete inability to hear sound in one or both ears. This can be caused by a variety of factors such as genetics, exposure to loud noises, infections, trauma, or simply aging. Deafness can be categorized as conductive, sensorineural, or mixed, depending on which part of the ear is affected.

Blindness, on the other hand, is a condition where a person has little to no ability to see. This can be caused by various factors such as genetics, eye infections, injuries, or diseases such as glaucoma or macular degeneration. Blindness can be categorized as partial or complete, and can occur at any age.

Both deafness and blindness can have a significant impact on an individual's quality of life, as they can affect communication, mobility, education, and employment opportunities. However, there are many resources and technologies available to help individuals with these conditions, such as sign language interpreters, braille devices, hearing aids, and guide dogs.

## Problem Statement
I am a researcher working for a community services center that aims to provide support to people with disabilities, including those who are deaf or blind. In order to better understand the experiences and needs of these communities, I plan to classify subreddits related to deafness and blindness and evaluate the feedback and sentiment of these posts. This will help to identify common themes, concerns, and needs that are specific to these communities, which can inform the development of targeted support groups and resources.

Using machine learning algorithms, I will classify subreddits related to deafness and blindness into separate categories, and then evaluate the sentiment of the posts in each category using natural language processing techniques. For the classification models, I will priotise generalization error between training and testing data. It is also essential to consider sensitivity and specificity in additional to the overall accuracy.

## Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|**subreddit**|*object*|blind, deaf|0 represent blind, 1 represent deaf.|
|**title_selftext**|*object*|title, selftext| Combination of words in title and selftext.|\

## Data Preprocessing: EDA
The most important words appeared to include 'deaf' and 'blind'. That is the reason they are excluded in tokenization because it will be meaningless for classification if the keywords are included.

It is cleared that 'nt' has no special meaning, they are just contraction like can't, don't, hasn't, haven't...They are separated by tokenization. 

It is also important to highlight that most of the tokens appeared to be a common word in communication/ opinion expression. For example, 'just', 'know', 'does', 'want'. This could contribute to model overfitting. Hence, other than count vectorizer, tf-idf vectorizer will be utilized to take into consideration the weightage of each token. tf-idf vectorizer weights more heavily for words that occur often in one document but don't occur in many documents.

## Modeling
Accuracy measures the number of correct predictions made by a model in relation to the total number of predictions made.

Precision measures the proportion of positively predicted labels that are actually correct. This has lesser interest in this project as compared to accuracy.

However, because accuracy could be affected by imbalance class in the subreddit posts, sensitivity/true positive and specificity/true negative rates are also considered.

#### 1. Baseline Accuracy
This is a simple baseline model that simply predict the accuracy rate for positive (deaf) and negative (blind). For the majority class (positive), it achieved an accuracy rate of 54% if all are predicted to be positive. Hence, if the predictive models are performing worse than the baseline model, it is considered to be performing poorly and required further tuning/feature engineering. The best model should have higher accuracy than baseline model, and have the optimal tradeoff between variance and sensitivity and specificity.

#### 2. Logistic Regression
Logistics regression models the relationship between input features and output labels using a logistic function, which maps input features to a predicted probability value between 0 and 1. The algorithm iteratively adjusts the parameters of the logistic function to minimize the difference between the predicted probabilities and the actual labels in the training data. It can be used to make predictions on new data by computing the predicted probability using the trained model.

Logistics reg assumes linear relationship. Also, in NLP that involves large vocabularies, it is vulnerable to overfitting as the models is too complex. These could be the reasons this model results in 6-8% of generalizaton error. Overfitting occurs in both cases using different transformers,and apparently count vectorizer has higher variance comparing to tfidf vectorizer. Although the scores achieve more than 90%, this is not considered an optimal model given the large variance.

#### 3. Naive Bayes
Naive Bayes estimates the probability of each feature given each class using Bayes' theorem. Then, when given a new input, it calculates the probability of each class given the input features using Bayes' theorem. The class with the highest probability is then chosen as the output. 

The "naive" part of Naive Bayes comes from the assumption that the input features are conditionally independent given the class label. This assumption allows the algorithm to be computationally efficient and well-suited for high-dimensional feature space. Therefore, it has lower generalization error of 3-4%, much lower as compared to logistic regression.

The performance is better in terms of lower variance and higher accuracy of above 87% by using count vector as compared to tfidf vector, although both models have overfitting issue. The slightly higher score in sensitivity and specificity of the model using tf-idf vector is traded off for lower variance.

Overall, Naive Bayes is considered an optimal model in this project as it provides much lower variance to give much steady prediction.

#### 4. KNN
k-Nearest Neighbors (k-NN) is a distance-based algorithm that uses the similarities between data points to make predictions. The input data is represented as a set of feature vectors, such as word frequencies or tf-idf values. When given a new input, the algorithm identifies the k nearest neighbors to that input in the feature space. The class of the new input is then assigned based on the majority class among the k nearest neighbors.

Hence, KNN is more effective in NLP tasks that involve finding similar documents or identifying patterns in the data, such as document clustering or recommendation systems. It can be computationally expensive and may not scale well to large datasets or high-dimensional feature spaces. As the number of dimensions or features increases, the distance between any two points becomes less meaningful and the points become more uniformly distributed. This can make it difficult to find meaningful nearest neighbors and can reduce the accuracy of the k-NN algorithm.

KNN using TF-IDF vector has lower variance than using count vector because it can effectively capture the underlying structure of the data and better handle the high-dimensional, sparse nature of the feature space, while count vector introduces bias and noise into the data because it included common words that has higher frequency in the documents. This is proved by the variance output, in which count vector gives 14.52% generalization error while tfidf vector gives 4.48% variance only. 

Although the scores in KNN is above 86%, given the lower error and higher accuracy in Naive Bayes, KNN is not an optimal model in this project.

#### 5. Decision Tree
In a decision tree, the input data is represented as a set of features, such as word frequencies or presence of certain keywords. The algorithm recursively splits the data into subsets based on the values of the input features, with the goal of maximizing the separation between the classes of interest. The splitting criterion is based on Gini impurity. Once the tree is constructed, new inputs are classified by traversing the tree based on their feature values until a leaf node is reached, which corresponds to a class label.

The reason decision tree has very low generalization error, but lower accuracy is likely because the depth is not deep enough to capture all the relevant features and their interactions. The gridsearch value to depth is given up to 10, and both vectors has best param at 10. Also, zero alpha in both cases supported the reason. In order to have higher accuracy, the value should be adjusted higher to capture more relationships between the input features and the class labels. Otherwise, random forest might address this depth issue and perform better.

The reason count vector gives lower error than tf-idf vector in this model could be because of the smaller selected max feature of 2k, compared to tf-idf which selected 3k features, which captures more noise.

Due to the very low sensitivity and specificity of around 77%-79%, Decision Tree is not considered optimal in this project unless the parameter is adjusted for further tuning.

#### 6. Bagging Classifier
Bagging Classifier is a type of ensemble model that uses 'bootstrap aggregating' to improve the accuracy of a classification task. It trains multiple classifiers on different subsets of the training data, and then combining their predictions to make a final prediction for each instance.

By training multiple classifiers on different subsets of the data, it learns to generalize better to new instances and reduce the impact of any noise or outliers in the data. That could be the reason this model gives the lowest generalization. Similar to Decision Tree, it has  lower error but also lower scores in sensitivity and specificity. Since the estimator of Bagging Classifier is Decision Tree, and the parameter for depth is set at maximum 10, this model might have better result if the depth is adjusted higher, and zero alpha is selected could explain this phenomena with lower error but lower accuracy.

Classifier using tf-idf vector underperforms count could be because of selection of 3k max feature and 0.95% max df in tfidf that takes in too many noise, causes it to have higher variance than count vector that selected 2k max features and 0.9% max df.

Therefore, Bagging Classifier does not qualified as optimal model in this project without fine tuning.

#### 7. Random Forest
A Random Forest model involves training a large number of decision trees on random subsets of the training data and (additional layer of randomness on Bagging Classifier) a random subset of the features. Each decision tree votes on the output for each input instance, and the final prediction is based on the majority vote of all the trees.

Random Forest is a robust model as it can handle a large number of features and can automatically select the most important ones for the classification task. Additionally, the randomness introduced in the model training process helps to reduce overfitting and improve generalization performance.

With same and limited depth of 10 layers, Random Forest outperforms decision tree and bagging classifier. As mentioned earlier, this model can auto select the most influential features for classification. Even if higher selected feature of 4k, it filtered out the noise and resulted in an optimal model in this project that provides only 1-2% generalization error, and much higher sensitivity and specificity at above 95%. Bravo!

Small notes:\
The only difference in this model by using either count or tf-idf vectors is the selection of 5 minimum sample leaf in count vector and 10 minimum sample leaf in tfidf vector. However, it can hardly be explained that 'with higher minimum sample leaf in tfidf vector, the model might not able to capture some underlying patterns in the data, causing lower accuracy/scores.' because there is already overfitting problem, and the lowest parameter given in the gridsearch is 5. The only GUESS i am able to provide is that while Random Forest can auto select the best feature, the frequency of words might give more information to this model, hence performed better. However, this requires proof and further experiments from different datasets. Otherwise, hyperparameter between 5-10 should be added to experiment if tf-idf could work better than count vector by taking the number in between 5-10.

#### 8. Extra Trees
Extra Trees is a variant of the random forest algorithm that introduces additional randomization in the tree construction process. Specifically, Extra Trees constructs multiple decision trees by randomly selecting a subset of features and selecting the split point at each node randomly. This randomization leads to a more diverse set of trees and can improve the performance of the algorithm, particularly in situations where the data is noisy or the feature space is high-dimensional. Generally, Random Forest tends to work better on structured datasets with low to medium dimensionality, while Extra Trees can work better on noisy or high-dimensional datasets.

In this project, Extra Trees (tf-idf vector) works the best by providing the lowest negligible error, 0.29% and highest scores in sensitivity and specificity at above 96%. Although the version using count vector provides close to 99% sensitivity and specificity, it comes with slightly larger error of 1.52%. In this project, the score is traded off for more consistent prediction power.

#### 9. AdaBoost
AdaBoost works by combining multiple weak classifiers to form a strong classifier that can make accurate predictions on a given dataset. It give greater weight to misclassified labels, so that subsequent weak classifiers focus more on these labels. The final prediction is made by aggregating the predictions of all the weak classifiers using a weighted majority voting scheme.

It is particularly useful in situations where the data is imbalanced or noisy, as it can focus on the most difficult examples to improve overall performance. However, Adaboost can be prone to overfitting when the number of weak learners in the ensemble is too high. It appears that AdaBoost has mediocre performance in this project, with higher error/ overfitting of 3-4% and lower scores at 84-85%.

Lower variance/error in count vector could be due to lower max features selected (2k) compared to 3k in count vector that is subjected to more noise. However, lower scores in accuracy, sensitivity and specificity in tf-idf version with lower variance should not be happened in this model that focuses on improve errors and scores. The reason for lower scores is likely caused by limited option of parameter 'number of estimator' at n=100. It could have changed if the threhold is adjusted upwards and allow for further improvement in both variance and scores.

## Sentiment Evaluation
Sentiment score is in between of -1 to 1, represent most negative to most positive. The result shows that both groups are positive. However, negative/blind group is slightly more positive comparing to positive/deaf group in reddit community.  

## Interpretation: Naive Bayes

**For negative/blind group:**

The most important word "visually impaired" is 155 times more likely to be in the document belongs to blind group compared to deaf group.

The ten words that have the strongest association with blind group are "visually impaired", "voiceover", "low vision", "visually", "screen reader", "guide dog", "cane", "jaws", "braille". Note that "rblind" is a community in reddit, so it should be eliminated from the list.


<font size=2>*cane*: A person with a completely white cane, this will usually mean they are blind, or visually impaired. Pedestrians with a red and white striped cane however, are deafblind (with both sight and hearing impairments).
    
<font size=2>*jaws*: Job Access With Speech. It is the world's most popular screen reader, developed for computer users whose vision loss prevents them from seeing screen content or navigating with a mouse. JAWS provides speech and Braille output for the most popular computer applications on your PC.
    
<font size=2>*braille*: It is a system of raised dots that can be read with the fingers by people who are blind or who have low vision.

**For positive/deaf group:**

The most important word "asl" means American Sign Language (ASL). It is a complete, natural language that has the same linguistic properties as spoken languages, with grammar that differs from English. ASL is expressed by movements of the hands and face. This word is 190 times more likely to be in the document belongs to deaf group compared to blind group.

The ten words that have the strongest association with deaf group are "asl", "interpreter", "hoh, "hearing aid", "audiologist", "ci",  "hearing loss". Note that "hearing aids" and "hearing aid" are just singular and plural forms. While "signing" and "sign language" are refering the same thing as "asl".

<font size=2>*hoh*: Hard of Hearing (HoH). It refers to someone who doesn't hear well.

<font size=2>*ci*: Cochlear Implant. It is a small, complex electronic device that can help to provide a sense of sound to a person who is profoundly deaf or severely hard-of-hearing. However, these devices do not restore normal hearing. They are tools that allow sound and speech to be processed and sent to the brain.

## Interpretation: Extra Trees
The most important words in the most robust model using tf-idf vector are hearing, vision, sign, aids, accessible, visually, loss, cane, asl, legally.

Whereas in model using count vector are vision, hearing, asl, hearing loss, impaired, braille, visually impaired, visually, legally, language.

## Conclusion
||Logistic Regression|Naive Bayes|KNN|Decision Tree|Bagging|Random Forest|Extra Trees|Ada Boost|
|---|---|---|---|---|---|---|---|---|
|**Total fits**|34560|1920|30720|38880|11520|19440|19440|4800|
|---|---|---|---|---|---|---|---|---|
|---|**Count, Tf-idf**|**Count, Tf-idf**|**Count, Tf-idf**|**Count, Tf-idf**|**Count, Tf-idf**|**Count, Tf-idf**|**Count, Tf-idf**|**Count, Tf-idf**|
|**Training score**|0.9856, 0.9786|0.9465, 0.9490|0.8668, 0.9050|0.8335, 0.8470|0.8536, 0.8594|0.9157, 0.9223|0.8376, 0.8631|0.9272, 0.9165|
|**Testing score**|0.9125, 0.9211|0.9063, 0.8977|0.7176, 0.8681|0.8668, 0.8668|0.8755, 0.8779|0.9014, 0.8989|0.8274, 0.8545|0.9174, 0.9014|
|**GS Cross Val score**|0.9083, 0.9190|0.9153, 0.9083|0.7216, 0.8602|0.8215, 0.8335|0.8487, 0.8512|0.9030, 0.9001|0.8224, 0.8602|0.8919, 0.8857|
|**Generalization Error**|7.73%, 5.96% |**3.12%**, 4.07%|14.52%, 4.48%|1.20%, 1.35% |0.49%, 0.82%|**1.27%**, 2.22%|1.52%, **0.29%**|3.53%, 3.08%|
|---|---|---|---|---|---|---|---|---|
|**Accuracy**|0.9125, 0.9211|**0.9063**, 0.8977|0.7176, 0.8681|0.8668, 0.8668|0.8755, 0.8779|**0.9014**, 0.8989|0.8274, **0.8545**|0.9174, 0.9014|
|**Precision**|0.9316, 0.9287|0.9329, 0.9078|0.7537, 0.8733|0.9741, 0.9634|0.9641, 0.9643|0.8680, 0.8706|0.7601, 0.7970|0.9625, 0.9589|
|**Sensitivity**|0.9039, 0.9245|**0.8902**, 0.9016|0.7071, 0.8833|0.7735, 0.7826|0.7986, 0.8032|**0.9634**, 0.9542|0.9931, **0.9794**|0.8810, 08535|
|**Specificity**|0.8915, 0.9122|**0.8782**, 0.8859|0.6808, 0.8618|0.7866, 0.7917|0.8040, 0.8076|**0.9509**, 0.9398|0.9875, **0.9672**|0.8735, 0.8483|

Baseline Model Accuracy = 0.5395

Top 3 models that stands out are Naive Bayes, Random Forest and Extra Trees. While Naive Bayes has slightly worse result than other two, its coefficient is good for interpretation. Random Forest has a good combination of low variance and high accuracy score, and Extra Trees has the lowest variance and highest sensitivity and specificity. 

Out of these 3 models, Extra Trees is selected because variance, sensitivity and specificity are the most important metrics in this project to help correctly identify different groups of community. In additional, Extra Trees is the most efficient model as it has lesser hyperparameters, and hence took only one third of time comparing to other models.

The results shows that Extra Trees has almost no overfitting issue, and in terms of specificity and sensitivity, the model has corrently identified 96.72% of all actual positive instance (deaf), and 97.94% of all negative instance (blind).

Sentiment analysis also indicates that negative/blind community on reddit is slightly more positive comparing to positive/deaf group in reddit community. The score for them are 0.41 and 0.38 respectively, with 1 being the most positive and -1 being the most negative.

The most popular themes in blind community includes visually impaired, voiceover, low vision, visually, screen reader, guide dog, cane, jaws and braille. This reveals that the community faces unique challenges related to access to information more than mobility. 

Whereas the most popular topics in deaf community includes asl, interpreter, hoh, hearing aid, audiologist, ci, hearing aids, signing, hearing loss. It concludes that the community faces more challenges related to communication. Popular words such as "audiologist" and "cochlear implant," may suggest that there is a high level of awareness and acceptance of this technology as a viable option for addressing hearing loss. Also, individuals in the community are seeking professional help with their hearing or balance issues, or that they are familiar with the role of an audiologist in helping them manage their condition.

## Recommendation/ Limitation
The recommendation is to evaluate the model on larger datasets to see if the results are consistent across a broader range of posts. This would help to determine if the model is truly robust and reliable. The limitation is the interpretability of the model, Extra Trees. It is difficult to interpret the results or explain the underlying decision-making process, which could limit its practical use in certain contexts.