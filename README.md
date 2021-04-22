# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. PDF Generator to produce the report of analysis
3. Notification service provider to send the notifications to respective medium
4. File directory access to store the PDF file generated
5. CSV validator to check the csv file is valid or not

### Mark the System Boundary

| Item                       | Included?     | Reasoning / Assumption
|----------------------------|---------------|---------------------------------------------------------------------------------------------------------|
|Battery Data-accuracy       | No            | We do not test the accuracy of data																	   |
|Computation of maximum      | Yes           | This is part of the software being developed															   |
|Off-the-shelf PDF converter | No 			 | PDF converter is a external service which is already developed									       |
|Counting the breaches       | Yes 			 | Counting the breaches is one of the requirements for the software									   |
|Detecting trends            | Yes			 | We need to check whether we are catching up the trend if its rising up for 30mins by mocking the output |
|Notification utility        | Yes			 | Need to check whether the information is passed properly to the notification service used               |

### List the Test Cases

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the number of times the data has passed threshold limit in the report
4. Record the trend when ever there is a increase of trend for 30 mins
5. Write the case to check whether notification message has been sent to the service
6. Case to check if the notification service is not available or invalid
7. Case to check the report generated successfully


### Recognize Fakes and Reality

| Functionality             | Input        		   | Output                      | Faked/mocked part
|---------------------------|----------------------|-----------------------------|--------------------------------|
|Read input from server     | csv file     		   | internal data-structure     | Fake the server store          |
|Validate input             | csv data     		   | valid / invalid             | None - it's a pure function    |
|Notify report availability | Notification message | message sent/unsent         | Mock                           |
|Report inaccessible server | Fake server url  	   | Server error                | Fake the server url            |
|Find minimum and maximum   | csv data 			   | minimum data/ max data      | None - it's a pure function    |
|Detect trend               | Mock input data 	   | Increase/decrease in trend  | Mock - Data stream for 30 mins |
|Write to PDF               | PDF Converter data   | Report               		 | Mock - PDF converter           |
