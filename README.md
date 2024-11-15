================================================================== Human
Activity Recognition Using Smartphones Dataset Mean and Standard
Deviation Version 1.0
================================================================== Abel
V. ==================================================================
Script to developt tidy\_data.txt dataset:

## 1: Read the data files

### Read feature names and activity labels

features &lt;-
read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/features.txt”, col.names = c(“index”, “feature”))
activity\_labels &lt;-
read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/activity\_labels.txt”, col.names = c(“activity\_id”,
“activity”))

### Read training data

train\_data &lt;-
read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/train/X\_train.txt”, col.names = features$feature) train\_labels
&lt;- read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/train/y\_train.txt”, col.names = “activity\_id”) train\_subjects
&lt;- read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/train/subject\_train.txt”, col.names = “subject”)

### Read test data

test\_data &lt;-
read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/test/X\_test.txt”, col.names = features$feature) test\_labels
&lt;- read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/test/y\_test.txt”, col.names = “activity\_id”) test\_subjects
&lt;- read.table(“~/testR/datasciencecoursera/cleandata/data1/UCI HAR
Dataset/test/subject\_test.txt”, col.names = “subject”)

## 2: Merge the training and test sets to create one dataset

### Combine subject, activity, and data for both train and test datasets

train &lt;- cbind(train\_subjects, train\_labels, train\_data) test
&lt;- cbind(test\_subjects, test\_labels, test\_data) combined\_data
&lt;- rbind(train, test)

## 3: Extract only measurements on the mean and standard deviation

### Ensure column names match features

colnames(combined\_data)\[3:ncol(combined\_data)\] &lt;-
features$feature

### Select columns with “mean” and “std” in their names

mean\_std\_columns &lt;- grep(“-(mean|std)\\\\”, features$feature, value
= TRUE) selected\_data &lt;- combined\_data %&gt;% select(subject,
activity\_id, all\_of(mean\_std\_columns))

## 4: Use descriptive activity names to name the activities

### Join with activity labels to get descriptive activity names

selected\_data &lt;- merge(selected\_data, activity\_labels, by.x =
“activity\_id”, by.y = “activity\_id”)

### Remove activity\_id and reorder columns

selected\_data &lt;- selected\_data %&gt;% select(subject, activity,
everything())

## 5: Label the dataset with descriptive variable names

### Replace column names to make them more descriptive

names(selected\_data) &lt;- gsub(“^t”, “Time”, names(selected\_data))
names(selected\_data) &lt;- gsub(“^f”, “Frequency”,
names(selected\_data)) names(selected\_data) &lt;- gsub(“Acc”,
“Accelerometer”, names(selected\_data)) names(selected\_data) &lt;-
gsub(“Gyro”, “Gyroscope”, names(selected\_data)) names(selected\_data)
&lt;- gsub(“Mag”, “Magnitude”, names(selected\_data))
names(selected\_data) &lt;- gsub(“BodyBody”, “Body”,
names(selected\_data)) names(selected\_data) &lt;- gsub(“-mean\\\\”,
“Mean”, names(selected\_data)) names(selected\_data) &lt;-
gsub(“-std\\\\”, “STD”, names(selected\_data))

## 6: Create a second, independent tidy data set with the average of each variable

## for each activity and each subject

tidy\_data &lt;- selected\_data %&gt;% group\_by(subject, activity)
%&gt;% summarize(across(everything(), mean), .groups = “drop”)

### Write the tidy data to a file

write.table(tidy\_data, “tidy\_data.txt”, row.names = FALSE)
