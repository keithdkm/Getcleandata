Please note that this work was completed in December 2014 and I am now re-submitting as part of the Signature Track
Characterize the data 

Description of raw dataset 
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. 

The original data was inspected and the following was noted: 
	The data files are fairly large consisting of a total of around 10000 rows of data between the training and test sets
	They are in text format in space delimited columns and could be inspected using a text editor
	All the data are numeric except the features.txt and the activity_labels.txt.  The latter two are character data 
	The data are static i.e.its structure and content are not changing
	The data are organized into space delimited columns int text files with no column headings 
	There are 561 columns in each of two files, "X_Test" (26Mb,2947 measurements) and "X_Train" (64.5Mb,7352 measurements).  
	Combining these sets together, we would expect our output file to have 2947 + 7352 = 10299 measurements
	For each, there is a corresponding "subject_test"(8kb,2947 subjects) and "subject_train"(20kb,7352 subjects). 
	For each X_file there is corresponding "Y_test" (6kb,2947activity codes) and "Y_train" (15kb, 7352 activity codes) that 
	contains the Activity being performed that measurement
	These latter files contain the data that lists the subject of each row of the X_ files 
	All the data in these 6 files is numeric 
	The "features.txt" document lists all the 561 column names
	The "activity_labels.txt" document is a mapping of activity codes onto meaningful labels.  This data was used to provide an replace activity codes in the data with meaningful activity names


Tidy the Data	
	
Requirements 1 and 2: Merge the training and test data sets and extract only the mean and standard deviation variables for each measurement

The data was combined together in the following way:

The X_test dataset was merged columnwise with subject_test and Y_test files so that each record in the file now has its corresponding Subject_ID and Activity_ID.  The same was done to the corresponding training files. Those two files were then be combined row-wise to create a complete dataset. 

Of the 561 columns of data, only those that correspond to the mean and standard deviation of below listed features were required.  Only these columns (numbering 66) were read in for processing using colClasses attribute of read.table to omit the unnecessary columns and identify the data as numeric .  This reduces that memory requirements of the script enormously and improves its performance 

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag
Note:  Any feature that has XYZ in its name is actually 3 features, one for each axis
The last 7 variables in the X_train and X_test files were used only in the angle variables and were therefore omitted as they were not part of the features list that had mean and standard deviation data 
  
All of this was done using line 50 of the run_analysis script.


Requirement 4 :  Appropriately label the data set with descriptive variable names
Using the feature names listed in "features.txt", the columns of the combined data were named.  Two additional names were added for the first two columns, Subject_ID and Activity_Label.  
Lines 64-68 of the script perform this step


Requirement 3: Use descriptive activity names to name the activities in the dataset
Using the Activity Labels from "activity_labels.txt", the Activity_IDs were replaced with meaningful labels.  The replacement mapping is as follows
1 WALKING
2 WALKING_UPSTAIRS
3 WALKING_DOWNSTAIRS
4 SITTING
5 STANDING
6 LAYING

Lines 75-76 perform the replacement

Requirement 5 : From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject
The mean of each variable grouped by Activity and subject is calculated.  
The output is a 180 row by 68 column table with one row for each Activity/Subject combination and one column for each mean value

Line 81 performs this step


The final output is a text file called "output.txt" placed in the working directory.
Line 87 performs this step
