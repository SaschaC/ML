# Exercise Classification from Wearable Sensors

An R coursework analysis that uses accelerometer measurements to classify how participants performed a barbell exercise. The workflow combines data cleaning, nearest-neighbor imputation, principal component analysis, and a random forest classifier.

**Original recorded work:** August 2016 · **Author:** Sascha Coridun  
**Context:** Practical Machine Learning course assignment · **Stack:** R, caret, parallel, doParallel

This is a historical learning project. The original report and code remain unchanged; this README was prepared with AI assistance in November 2026.

## Analysis workflow

The [original report](pml_assignment.Rmd) documents the following steps:

1. Read the supplied training and testing CSV files.
2. Remove near-zero-variance predictors and selected identifier fields.
3. Impute missing values with a nearest-neighbor procedure.
4. Reduce the selected sensor predictors to 40 principal components.
5. Fit a random forest through `caret`, using ten-fold cross-validation and parallel processing.
6. Generate predictions for the assignment's test rows.

The task and dataset come from the course and the cited wearable-sensor research. My contribution is the analysis implementation and report, rather than collection of the sensor data or invention of the modeling algorithms.

## Results and evaluation limitations

The historical report records **99.95% cross-validation accuracy**. This is a reported coursework result, not an independently verified benchmark or a guarantee of performance on new participants.

The script fits imputation and PCA on the full training dataset before cross-validation. Validation folds therefore influence preprocessing. A stronger evaluation would fit every preprocessing step inside each training fold and assess performance on an untouched holdout set. For generalization to unseen people, participant-level splitting would also be important.

## Reproduction status

The report is available as [R Markdown source](pml_assignment.Rmd) and [rendered HTML](pml_assignment.html). Runtime reproduction was not performed during this refresh; R is not installed in the documentation environment.

The script expects `pml-training.csv` and `pml-testing.csv` in the working directory. They are not included in this repository. It uses `caret`, `parallel`, `doParallel`, and `nnet`; the selected random forest and imputation methods also require their supporting packages. No dependency lockfile is provided.

Two details need attention before rerunning:

- The optional cached-model branch loads `rfModel.Rda`, but the file is not bundled and its expected contents are not documented. The analysis later expects an object named `m`.
- Column selection includes numeric positions, which assume the original dataset layout.

Preserve the historical analysis when improving reproducibility. A corrected evaluation should be a clearly dated new experiment, with its own results.

## History and sources

- [Original source snapshot](https://github.com/SaschaC/ML/tree/96d2441daed6cc96db9c5baff24ea449abd785db)
- [Original development history](https://github.com/SaschaC/ML/commits/master/)
- [Dataset reference cited in the report](http://groupware.les.inf.puc-rio.br/har/)

Historical external links may have changed. This documentation refresh does not introduce a software or dataset license.
