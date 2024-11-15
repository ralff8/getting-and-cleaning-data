================================================================== Human
Activity Recognition Using Smartphones Dataset Mean & Standard Deviation
Version 1.0
================================================================== Abel
V. ==================================================================

The experiments have been carried out with a group of 30 volunteers
within an age bracket of 19-48 years. Each person performed six
activities (WALKING, WALKING\_UPSTAIRS, WALKING\_DOWNSTAIRS, SITTING,
STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the
waist. We extract the data of this experiment and create a new table
with the Mean and Standard Deviation of any variable.

# The dataset includes the following files:

-   ‘tidy\_data.txt’

# Steps for creating the dataset the following files:

1: Read the data files

Read feature names and activity labels

Read training data

Read test data

2: Merge the training and test sets to create one dataset

Combine subject, activity, and data for both train and test datasets

3: Extract only measurements on the mean and standard deviation

Ensure column names match features

Select columns with “mean” and “std” in their names

4: Use descriptive activity names to name the activities

Join with activity labels to get descriptive activity names

Remove activity\_id and reorder columns

5: Label the dataset with descriptive variable names

Replace column names to make them more descriptive

6: Create a second, independent tidy data set with the average of each
variable for each activity and each subject

Write the tidy data to a file

# License:

Abel V.
