~~ The Grand Truthers - 145 FINAL PROJECT ~~

Team Members: Omid Eghbali, Garvit Pugalia, Kanisha Shah, Hengda Shi, Prabhjot Singh


~~ Requirements ~~
Necessary: 
	Python version: >= 3.6 (Tested on 3.6.7)
	Matplotlib: For graphs 
	scikit-learn: For ML algorithms used
Optional: 
	yellowbrick : To see feature importances, uncomment the related lines


~~ How to run ~~

After extracting the directory, fill the /data file with the 5 data files provided by Yelp.
We used sample data files given to us from our Kaggle challenge, but feel free to use your own.  
These files are: business.csv, test_queries.csv, train_reviews.csv, users.csv, and validate_queries.csv.
Even though these files contain only a fraction of the data provided by Yelp, they're too large to push to Github.
Sample files can be downloaded from here: https://drive.google.com/drive/folders/1pJMsi2CMB5rFd-33vlc4LeCYEMvoEkYQ?usp=sharing
Then in the main directory run: (assuming default python3)
	python preprocess.py 
		This will take a few minutes based on how fast your computer is, and outputs new files in the
		/data folder, which are used by project.py
	python project.py
		Runs all the models we needed for this project. Log regression is commented out because it did
		not converge with our final feature set. KNN and Random forest are also commented out because
		they would take some extra time to run.


~~ Included Files and Description ~~

project.py:
	The main project file. Runs through our various models that we implemented and spent much time
	tuning. The models implemented are as follows:

	Complete Random Model: Just predicts a random value 1-5 to classify for y, used to see how bad 
			       RMSE can be.

	Random Probalistic Model: Another random classifier, but predicts a value 1-5 based on the 
				  distribution of labels in the training data set.

	Decision Tree: Used sklearns version of the DT. The current version of the project will run the DT
		       for the feature set chosen for the Gradient Boosting Regressor. We tuned the tree depth
		       to avoid overfitting, and found that you can do quite well (relative to the class competition)
		       with just this simple model.

	Linear Regression: Used sklearns version. Couldn't do better than a simple decision tree. Also tried 
			   using the polynomial version of the features and still couldn't do any better. 
	
	NN, KNN, Log Regression: Used sklearns version as well again for all, optimizing parameters for	
	KNN didnt help, NN optimizing made differences but couldn't do as well as the basic DT.

	Random Forest: Through sklearn, did a serach over the different hyperparameters, did very well as expected.
	
	Gradient Boost Regressor: The best model we used for our submission. 

	See report for more info on all of the models.

constants.py: 
	This file constants all the constant names that are used within the preprocessor and
	the project python file. It includes things like where to find the datapath and
	specific datafile names. The output file names, for when preprocessing is over, as well 
	as the submission file name is also specified within this file. There is also several
	self explanatory feature variables, which are just arrays of feature names we used to 		
	pick the features we wanted. Lastly min max scaling can be turned on or off in this file.

preprocess.py:
	Run to preprocess the data. Requires all 5 data files from kaggle be put in a \data folder.
	Simply calls methods in preprocessor.py

preprocessor.py: The class where we preprocess all the data. There are four main functions in the class. 
	preprocess_bus(): The function that preprocess the file business.csv. It extracts all the useful features
			  given in the constant.py and fills all missing data. It then export the preprocessed data 
			  into a file called bus_dict.csv

	preprocess_users(): The function that preprocess the file user.csv. It also extracts all the useful features 
			    given in the file constant.py and fills all the missing data. All the preprocessed data 
			    is then exported to a file called user_dict.csv.

	preprocess_reviews(): The function where we make our own training dataset. We first extract all the features 
     			    from bus_dict.csv and user_dict.csv and concatenate the feature corresponding to specific 
			    ids together, i.e. removing the user id and business id with corresponding features. 
			    After that, we will export the data into a file called cleaned_train_reviews.csv, and this 
	  		    is our training dataset.

	preprocess_queries(): The function where we preprocess validation_queries.csv and test_queries.csv to replace 
			      all user_id and bus_id with features. We will then export them into two files 
			      called cleaned_validation_queries.csv and cleaned_test_queries.csv
	
utils.py:
	Just a faster way to call a function to calculate RMSE and get the csv files loaded. 
	