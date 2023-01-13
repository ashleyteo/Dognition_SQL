# Dognition_SQL

## Table of Tasks
* [Data Cleaning and Relational Schema](#Data_Cleaning_and_Relational_Schema)
* [Identifying Potential Data Issues](#Identifying_Potential_Data_Issues )
* [Retention Challenges Investigation](#Retention_Challenges_Investigation)

## Data Cleaning and Relational Schema

* For complete_tests table:
The duplicated records were dropped and verified the primary key.

* For dogs table:
The duplicated records were dropped and verified the primary key.

* For exam_answers table:
* The duplicated records and were dropped and records with NULL vlaues in the dog_guid & end_time were dropped.

* For reviews table:
The duplicated records were dropped and verified the primary key.

* For site_activities table:
The duplicated records were dropped and verified the primary key.

* For users table:
We can see that there're 13 records that have multiple values for one user_guid. We find from the "uid_cnt" and "utc_correction" columns that the duplicate records are due to the records having N/A in the "utc_correction" column. We dropped these records.


## Identifying Potential Data Issues

* For complete_tests table:
We found it strange that there were so many records where the unique record ID for a human user is NULL. It does not make sense for there not to be a human ID.

* For dogs table:
We noticed that birthday was a character data type as such we converted it into an integer. Here, we further decided to only account for birthdays which were greater than 1995 because we assumed that in general most dogs do not live beyond 20 years old. Also, we decided to only include weight which was greater than 0 and less than 200 because no dog should weigh 0 pounds and there was only one dog which weighed greater than 200. Moreover it was the Shih Tzu breed which typically shouldn't weigh this much.

* For exam_answers table:
We noticed that there were some records which had start time greater than or equal to end time which doesn't make logical sense. We would expect the timestamp when a user receives a question to be less than the timestamp when they submitted their answer.

* For reviews table:
We noticed that there were three records where the user_guid was equal to the dog_guid. This does not make sense because we cannot have a unique ID for a human user be the same as a unique user for a dog.

* For site_activities table:
We decided to investigate if there were huge discrepancies in the way users interacted with Dognition's website and discovered that the data_viz category had the largest interaction. Although we're unsure what this category means, we're assuming it might represent charts or other visualizations on Dognition's website.

* For users table:
We noticed that there were some records where the timestamp of the user's last activity in their account was greater than the timestamp the record was created which did not make sense. Additionally, while it's possible for people to have more than 6 dogs, we assumed that it could be an overstatement as such we only analyzed records where max_dogs were less than 6.

* Irregularities:
In October 2014, there was a huge jump from July (only 95 user sign-ups) to October (3633 user sign-ups). Based on our Google search, we found that on 5 October 2014, they were featured on 60 Minutes. This was the likely for the spike in user sign-ups.
Since Dognition was founded in 2012, it could be likely that the sign-ups in December 2012 (1) and January 2013 (2) were "test" cases by the internal team.


## Retention Challenges Investigation
It is evident that there are more users that complete less than 10 tests than more than 10 tests for all membership types which may indicate that users don't complete all 20 tests possibly because the tests are too complicated and tedious. When looking at memebership type 1, the number of users that have completed less than 10 tests are signifciantly greater than the number of users that have completed more than 10 tests. There seems to be good evidence that people leave after 6-7 completed tests, indicating inpatience. It is expected that the number of users will peak at 20 completed tests as that is the minimum number of tests to obtain an assessment.


Additionally, we see that Mixed, Labrador Retriever, Border Collie, Golden Retriever and German Shepherd breeds have the highest sign ups. This seems to show that mid-large size dogs are the popular breed for this test. These breeds are also known to be intelligent dogs.
We grouped our results by script_detail_id and see that there is a huge number of users on script_detail_id 107, 132 and 158. We can possibly infer that these pages are the "problematic" pages that are causing users to be frustrated or confused. Here, we are assuming that the script_detail_id is the last web page users are on before logging off and exiting. However, we have to note that since we don't have access to further details on the script_detail_id, we cannot perform further investigation on which specific web pages people are having issues with (e.g. whether it's the homepage or terms and conditions page etc.)


Lastly, an interesting point we could have further analyzed was the "types" of owners that particiapted in these assessments. We could look at the country and/or city of the user which may indicate that most users come from a ceratin geographic location which will be helpful when the company is looking at retention measures.
