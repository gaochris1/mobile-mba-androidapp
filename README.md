### mobile-mba-androidapp - Carrier Build v1.241
===========================================

### 2013 Measuring Broadband America Program Mobile Measurement Android Application

The FCC Measuring Broadband America (MBA) Program's Mobile Measurement Effort developed in cooperation with SamKnows Ltd. and diverse stakeholders employs an client-server based anonymized data collection approach to gather broadband performance data in an open and transparent manner with the highest commitment to protecting participants privacy.  All data collected is thoroughly analyzed and processed prior to public release to ensure that subscribers’ privacy interests are protected.

Data related to the radio characteristics of the handset, information about the handset type and operating system (OS) version, the GPS coordinates available from the handset at the time each test is run, the date and time of the observation, and the results of active test results are recorded on the handset in JSON(JavaScript Object Notation) nested data elements within flat files.  These JSON files are then transmitted to storage servers at periodic intervals after the completion of active test measurements.

This Android application source code is made available under the GNU GPL2 for testing purposes only and intended for participants in the SamKnows/FCC Measuring Broadband American program.  It is not intended for general release and this repository may be disabled at any time.

--------------------------------------------

### Build Description

A build was developed for engineering and diagnostic use by carriers engineering staff and denoted the "cb" (carrier build). The carrier build enables a user of the Application to define a self-identifier via the menu setting that is included in the otherwise anonymous test results uploaded to the cloud storage. The self-identifier string is included in recorded results and facilitates the selection of specific data uploaded to the cloud storage. The ability to identify specific data for phones used in FEMA testing will be critical to differentiate collected results with self-identifier fields from the diverse results from various handsets contributing data in the beta trial.

This cb-1.241 build includes a significant difference from the cb-1.24 version. This build implements a continuous testing feature that can be enabled in the settings of the application. Under continuous testing mode, the user can specify a test that the application should repeat continuously. The time interval between tests can also be set by the user. This feature allows the collection of test results on a schedule defined by the Application user and the collection of the specific result from the cloud storage infrastructure storing beta trial data.

Minimum Operating System: Android 2.2 (Froyo) [API Level 8] Ideal Operating System: Android 4.2 (Jelly Bean) [API Level 17]

--------------------------------------------

### Continuous Testing Feature

* To activate continuous testing:

    1. Go to the menu and then settings.
    2. Scroll to the category titled "Continuous Test Controls".
    3. Select "Enable Continuous Testing".
       - Upon returning to the main screen, you should then see a toast that declares "Continuous is enabled".

* To begin the continuous tests:

    1. Tap the down arrow on the dark gray bar with the phrase "Run now". (Do not tap "Run now" as it will not begin continuous testing, but rather it wil begin a single run of a full suite of tests.)
    2. Tap "Continuous [Latency / Loss]". (The text in the bracket will change to whichever test you specify in the settings.)

* To stop the continuous tests:

    * During a test:
        1. Tap the back button.
        2. A dialog box will ask, "Do you want to cancel running test?" Select "Yes".

    * In between tests:   (This is usually only necessary if your testing interval is extremely long.)
        1. Go to the menu.
        2. Select "Cancel All Continuous".

--------------------------------------------

### Build Explanations:

    gb  General Build: This build is the baseline application.
    cb  Carrier Build: This build includes an option to add a self-identifier for debugging and testing purposes.
    mt  Manual Test: This build turns off automatic testing by default. Users of this build can turn the automatic testing on themselves.
