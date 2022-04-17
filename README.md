# Fraud_transaction_detection

Important Aspects of the model

Task 1: Data cleaning including missing values, outliers and multi-collinearity:
In the given dataset, there were no missing values.
I was not able to show the outlier detection because of RAM issues. I tried to display outliers using the boxplots and Z-score value. The outliers could have been removed using Quantile based flooring and capping or Mean/Median imputation.
Heatmaps are used to display the corelations among features. Features with considerable correlation values are handeled by computing a different information from them as shown above.

Task 2: Describe your fraud detection model in elaboration.
-> After cleaning the data and performing exploratory data analysis on the it, the produced dataset is used in training of the machine learning model.

-> In this particular task, I have used XGBoost classification algorithm to develop the model.

XGBoost improves the gradient boosting method even further.

XGBoost (extreme gradient boosting) regularises data better than normal gradient boosted Trees.

It was developed by Tianqi Chen in C++ but now has interfaces for Python, R, Julia.

XGBoost's objective function is the sum of loss function evaluated over all the predictions and a regularisation function for all predictors ( 𝑗 trees). In the formula 𝑓𝑗 means a prediction coming from the 𝑗𝑡ℎ tree.

                                        𝑜𝑏𝑗(𝜃)=∑𝑖𝑛𝑙(𝑦𝑖−𝑦𝑖^)+∑𝑗=1𝑗Ω(𝑓𝑗)

Loss function depends on the task being performed (classification, regression, etc.) and a regularization term is described by the following equation:

                                        Ω(𝑓)=𝛾𝑇+12𝜆∑𝑗=1𝑇𝑤2𝑗

First part ( 𝛾𝑇 ) is responsible for controlling the overall number of created leaves, and the second term ( 12𝜆∑𝑇𝑗=1𝑤2𝑗 ) watches over the scores.

Mathematics Involved Unlike the other tree-building algorithms, XGBoost doesn’t use entropy or Gini indices. Instead, it utilises gradient (the error term) and hessian for creating the trees. Hessian for a Regression problem is the number of residuals and for a classification problem. Mathematically, Hessian is a second order derivative of the loss at the current estimate given as:

where L is the loss function.

Initialise the tree with only one leaf. compute the similarity using the formula 𝑆𝑖𝑚𝑖𝑙𝑎𝑟𝑖𝑡𝑦=𝐺𝑟𝑎𝑑𝑖𝑒𝑛𝑡2ℎ𝑒𝑠𝑠𝑖𝑎𝑛+𝜆 Where 𝜆 is the regularisation term. Now for splitting data into a tree form, calculate 𝐺𝑎𝑖𝑛=𝑙𝑒𝑓𝑡𝑠𝑖𝑚𝑖𝑙𝑎𝑟𝑖𝑡𝑦+𝑟𝑖𝑔ℎ𝑡𝑠𝑖𝑚𝑖𝑙𝑎𝑟𝑖𝑡𝑦−𝑠𝑖𝑚𝑖𝑙𝑎𝑟𝑖𝑡𝑦𝑓𝑜𝑟𝑟𝑜𝑜𝑡 For tree pruning, the parameter 𝛾 is used. The algorithm starts from the lowest level of the tree and then starts pruning based on the value of 𝛾. If 𝐺𝑎𝑖𝑛−𝛾<0, remove that branch. Else, keep the branch

Learning is done using the equation 𝑁𝑒𝑤𝑉𝑎𝑙𝑢𝑒=𝑜𝑙𝑑𝑉𝑎𝑙𝑢𝑒+𝜂∗𝑝𝑟𝑒𝑑𝑖𝑐𝑡𝑖𝑜𝑛 where 𝜂 is the learning rate.

Task 3: How did you select variables to be included in the model?

The list variables or features are - [step,type,amount,nameOrig,oldbalanceOrg,newbalanceOrig,nameDest,oldbalanceDest,newbalanceDest,isFraud,isFlaggedFraud].
Out of these features, 'step', 'nameOrig', and 'nameDest' are the features which have no role to play in prediction a trasaction being fraud or not. This is because these are just the unique string values, which can be ignored.
The main role for classifying a prediction as fraud or not are played by the difference between the original and new_balance amount in the accounts of sender and receiver, further depending upon the 'type of transaction'. Therefore, the features considered for classification tasks are oldbalanceOrg, newbalanceOrig, oldbalanceDest, newbalanceDest and type.
'isFraud' is considered as the column of labels in the supervised learning model.

Task 4: Demonstrate the performance of the model by using best set of tools
The perfomance metrice I have used over here is accuracy. accuracy is the measurement used to determine which model is best at identifying relationships and patterns between variables in a dataset based on the input, or training, data.
I preffered to use accuracy over other perfomance measuring metrices like precision, F1 Score etc. because accuracy tells the measure of correct classification, which is utmost necessary to know, so that a Fraud transaction can be detected effectively.
At any cost, the company can not entertain the mistake of a actual fraud transaction being classified as 'not fraud' and a 'not fraud' transaction being classified as 'fraud'. If any such mistake happens, it would adversely affect the reputation of the bank or company.


Task 5: What are the key factors that predict fraudulent customer?

Some of the important factors that play a majour role in predicting a fradulant customer are:

Customer's identity (email addresses, credit card numbers, etc.)
The past order details.
Their preferred payment methods,
The locations they have used for the transactions.
Their network (emails, phone numbers, and payment details entered with the online account).
Task 6: Do these factors make sense? If yes, How? If not, How not?
In my point of view, yes! definitly the above mentioned points make sense.

Customer's identity is necessary to identify him or her so that further necessary action can be taken.
The history of the orders help in knowing what kind of transaction does the customer makes usually, so that an unusual transaction can be detected.
The location of the customer where he/she makes most of the transactions should be stored to know if any other location which maybe far away from the usual location can be determined, as it could be a posible fraud transaction.
Customer's personal information like his emails, payment details etc can be possible source through which fraud could have been conducted.
Task 7: What kind of prevention should be adopted while company update its infrastructure?
While updating the infrastructure of the company, in general, following preventions should be considered:

Understand your work, understand your necessary requirements, then update the infrastructure.
The dependability of your candidate infrastructure must be accessed.
Think about legal and ethical issues.
Consider financial issues. Over bugeting must be avoided.
Wastage of reusable material should be avoided.
Prevent employees from overusing the company resources.
Task 8: Assuming these actions have been implemented, how would you determine if they work?
This task can be performed at 4 levels:

Physical Level: Infrastructure needs physical protection in the form of locked doors, fences, backup generators, security cameras and the like. Failover plans that locate backup equipment in another part of the world are also a part of a physical security strategy.
Network Level: At its core, network security protects data as it travels into, out of and across the network. This includes traffic encryption, whether it is on-premises or in the cloud, proper firewall management and the use of authentication and authorization systems.
Application Level: Security also needs to be considered at the application level. This includes protection of databases against attacks such as SQL injections as well as the hardening of other applications against unauthorized use or malicious exploits.
Data Level: At the lowest level of infrastructure security, data protection must be considered, no matter where or how it is stored. This includes data encryption, backups and anonymization tactics where they are appropriate.
 
