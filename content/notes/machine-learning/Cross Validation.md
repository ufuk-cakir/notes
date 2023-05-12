How to find good parameter?
The Support Vector Machine has a hyper parameter: relative Weight of the data and regularization term.

- regularization Term: tries to maximize the margin in order to prevent overfitting
- data term: responsible for classifying the data term correctly

Questin: how do you find a good hyperparameter?

The standard approaches to hyperparameter selection:

The best is if you have 3 Datasets: Training, validation, test.

The idea is: 
- You pick a set of possible hyperparameters .ie $\beta  \in {10^{-3}, 10^{-1},1,10,100}$
- train with each $\beta$ on the training set 
-  measure the accuracy on the validation set
- keep best $\beta$ on validatoin set
- test again on test set

Why not get rid of validation test? If we select the hyperparamter on the test set, the test set secretly becomes part of the training set and hence is no test set anymore. This is why we need a second test set that is part of the training in order to preserve the test set for real testing.

## Fallback withoud validation set: cross-validation
idea: split the training set into k pieces ("folds")

It is really importatn that the Test set is randomly ordered.

- split up the test set into e.g 5 folds
- use each fold as validation set in term and train on the remaining k-1 folds
- in the second iteration use second set and train on the remaining folds etc
- Typical values for K: 2(only used if you cant afford more than 2 times), better is 5 or 10 Folds, (N-fold: "leave-one-out cross validation": leave one point out and train on all the data except that one). Often one can calculate the leave one out error analytically which is very nice!
- can also be applied hierarchically:
	- first take one fold out as a test set
	- take another one out as a validation set
	- train on the remaining folds
	- in the inner loop you would flip around the validation sets and in the outer loop you would flip around the test set
- K-Error Estimates after we trained: Report average error and variance: The best hyperparameter is the one with the lowest average error