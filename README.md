# Analyzing-Intoxication-Levels-through-Smartphone-Accelerometer-Data-and-TAC-Readings
This project aims to detect heavy drinking patterns by analyzing smartphone accelerometer data and transdermal alcohol content (TAC) measurements. By correlating movement data with TAC readings, it seeks to develop a predictive model for identifying intoxication.

PID's: phone ID's
BK7610
BU4707
CC6740
DC6359
DK3500
HV0618
JB3156
JR8022
MC7070
MJ8002
PC6771
SA0297
SF3079


1. Database Description:
    (a) Title
        Bar Crawl: Detecting Heavy Drinking
    (b) Abstract
        Accelerometer and transdermal alcohol content data from a college bar crawl. Used to predict heavy drinking episodes via mobile data.

2. Sources:
   (a) Owner of database
       Jackson A Killian (jkillian@g.harvard.edu, Harvard University); Danielle R Madden (University of Southern California); John Clapp (University of Southern California)
   (b) Donor of database
       Jackson A Killian (jkillian@g.harvard.edu, Harvard University); Danielle R Madden (University of Southern California); John Clapp (University of Southern California)
   (c) Date collected
       May 2017
   (d) Date submitted
       Jan 2020

3. Past Usage:
   (a) Complete reference of article where it was described/used: 
       Killian, J.A., Passino, K.M., Nandi, A., Madden, D.R. and Clapp, J., Learning to Detect Heavy Drinking Episodes Using Smartphone Accelerometer Data. In Proceedings of the 4th International Workshop on Knowledge Discovery in Healthcare Data co-located with the 28th International Joint Conference on Artificial Intelligence (IJCAI 2019) (pp. 35-42). http://ceur-ws.org/Vol-2429/paper6.pdf
   (b) Indication of what attribute(s) were being predicted
       Features: Three-axis time series accelerometer data
       Target: Time series transdermal alcohol content (TAC) data (real-time measure of intoxication)
   (c) Indication of study's results
       The study decomposed each time series into 10 second windows and performed binary classification to predict if windows corresponded to an intoxicated participant (TAC >= 0.08) or sober participant (TAC < 0.08). The study tested several models and achieved a test accuracy of 77.5% with a random forest.

4. Relevant Information:
    All data is fully anonymized.

    Data was originally collected from 19 participants, but the TAC readings of 6 participants were deemed unusable by SCRAM [1]. The data included is from the remaining 13 participants.
   
    Accelerometer data was collected from smartphones at a sampling rate of 40Hz (file: all_accelerometer_data_pids_13.csv). The file contains 5 columns: a timestamp, a participant ID, and a sample from each axis of the accelerometer. Data was collected from a mix of 11 iPhones and 2 Android phones as noted in phone_types.csv. TAC data was collected using SCRAM [2] ankle bracelets and was collected at 30 minute intervals. The raw TAC readings are in the raw_tac directory. TAC readings which are more readily usable for processing are in clean_tac directory and have two columns: a timestamp and TAC reading. The cleaned TAC readings: (1) were processed with a zero-phase low-pass filter to smooth noise without shifting phase; (2) were shifted backwards by 45 minutes so the labels more closely match the true intoxication of the participant (since alcohol takes about 45 minutes to exit through the skin.) Please see the above referenced study for more details on how the data was processed (http://ceur-ws.org/Vol-2429/paper6.pdf).

    1 - https://www.scramsystems.com/
    2 - J. Robert Zettl. The determination of blood alcohol concentration by transdermal measurement. https://www.scramsystems.com/images/uploads/general/research/the-determination-of-blood-alcohol-concentrationby-transdermal-measurement.pdf, 2002.

5. Number of Instances:
    Accelerometer readings: 14,057,567
    TAC readings: 715
    Participants: 13

6. Number of Attributes:
    - Time series: 3 axes of accelerometer data (columns x, y, z in all_accelerometer_data_pids_13.csv)
    - Static: 1 phone-type feature (in phone_types.csv)
    - Target: 1 time series of TAC for each of the 13 participants (in clean_tac directory).

7. For Each Attribute:
    (Main)
    all_accelerometer_data_pids_13.csv:
        time: integer, unix timestamp, milliseconds
        pid: symbolic, 13 categories listed in pids.txt 
        x: continuous, time-series
        y: continuous, time-series
        z: continuous, time-series
    clean_tac/*.csv:
        timestamp: integer, unix timestamp, seconds
        TAC_Reading: continuous, time-series
    phone_type.csv:
        pid: symbolic, 13 categories listed in pids.txt 
        phonetype: symbolic, 2 categories (iPhone, Android)
    
    (Other)
    raw/*.xlsx:
        TAC Level: continuous, time-series
        IR Voltage: continuous, time-series
        Temperature: continuous, time-series
        Time: datetime
        Date: datetime

8. Missing Attribute Values:
None

9. Target Distribution:
    TAC is measured in g/dl where 0.08 is the legal limit for intoxication while driving
    Mean TAC: 0.065 +/- 0.182
    Max TAC: 0.443
    TAC Inner Quartiles: 0.002, 0.029, 0.092
    Mean Time-to-last-drink: 16.1 +/- 6.9 hrs
