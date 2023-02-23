# CukeBoard
This repository contains a web application to use with a Cucumber.  This application has functionality to view,run and create Cucumber tests via Drag and Drop.


Introduction: CukeBoard™ is an interactive application created to increase velocity of any QA Automation team.  CukeBoard provides an efficient way  to view Coverage, Run Tests, View Test Results, Screen Shots, and enter Triage Notes on why tests fail. The test run functionality ability to re-run a single test to get regression “back to green”. CukeBoard is also a convenient place to easily create and schedule tests leveraging the QA machines on the team and eliminating the need for Jenkins and all the associated restrictions and infrastructure and labor costs.  You can even run the tests in up to 8 test sets each on X number of machines that report as a single test result. This app just works once setup  The Gherkin is parsed by a Rake task (needs to be made into a separate gem ) within the given repository to send to the database using cucumber_analytics Ruby Gem as well as the mysql2 gem. If the sync finds any Test Scenarios that no longer exist they will be marked as deprecated.  The data for the dashboard is stored in a MySQL database currently using the following details:
:adapter: mysql2
:host: YOURSQLSERVER
:port: 3306
:username: autouser
:password: Aut0mat10n
:database: automation
Basics:
![image](https://user-images.githubusercontent.com/5246775/220803727-8ed23210-9288-455e-bc3f-16dc29ebcefb.png)
Header: 
 
•	The header is how you navigate to the screens of the dashboard.
•	Hovering over any element will give a description as to it’s use.
•	The general search bar can be used to filter the data on any page using the visible columns.
•	The settings button (the Gear) can be used to change the columns or clickable filters on each view.
![image](https://user-images.githubusercontent.com/5246775/220803864-f19371e5-94df-4083-9168-8ef95ad6a2f3.png)

 
•	The Eye icon ![image](https://user-images.githubusercontent.com/5246775/220803880-8bd98438-7e68-4aa0-8216-21a83d3cebb5.png) can be used on any view with selectable rows to view details at the next level into the given view.  
•	The run button ![image](https://user-images.githubusercontent.com/5246775/220803923-3f78ca67-f0bf-4cc5-b1a9-02a1f8d176f6.png)will show up on any view that allows a test or tests to be re-ran when the rows are selected. 

1.	The run Screen is the place to launch a new test or schedule a test to run on a pattern.  
![image](https://user-images.githubusercontent.com/5246775/220803965-1ae14c6a-6549-45b4-9d2e-b8dfb9223ab5.png)
•	A test that is not assigned a time in the future will run now.
•	Tests scheduled in the future are stored in the database and can be viewed in the Schedule View.  
•	Changing the Frequency option to “Every ” will reveal the options for setting the recurrence pattern:    
![image](https://user-images.githubusercontent.com/5246775/220805508-015d8636-02b3-42d1-b001-e4c0b4b97619.png)


2.	Schedule View: The scheduler is where you will see the test sets that are scheduled.  
![image](https://user-images.githubusercontent.com/5246775/220804047-7abc3e77-491c-4deb-9d5e-f0f544e7e737.png)
•	The squares on this screen represent active (Green) or inactive tests (Red).  You can highlight a test and cancel it using the X in the upper right area of the header or activate a test with the checkmark.  Schedule configurations can be deleted with the trashcan.  
•	If a test is activated with a run date in the past it will launch immediately and then follow it’s recurrence pattern.
•	The machine assigned on which the test will run can be re-assigned by clicking that area and the same for the next run date.  

3.	The link to the test will show up once launched. That link will take you to the result set for the test you launched as shown below.  
![image](https://user-images.githubusercontent.com/5246775/220804106-0a272b89-9643-4efb-bc4e-b408197ff81c.png)
•	For convenience the Dashboard allows users to click the Passed or Failed words or use the filter provided.  The dashboard tries to be very flexible and give users options to filter data the way they choose. 
•	The Squares that have a camera on them will take you to the screen shot of the last passed assertion or the point the test failed.
•	The squares which represent status can be changed by right clicking as long as there are triage notes entered. Below is a basic explanation of the square/status colors.
o	Green = Passed but you can also enter a triage note such as “passed manually” if the test was the issue but the feature works properly and you need to report results to the development team or management.
o	Red = Failed 
o	Yellow = Warning – Warnings are most commonly assigned when the feature is not testable in the given environment.  It is a good way to communicate risk for untested features.

4.	The Result Set view also allows you to re-run a test by clicking that row(s) or the select all then clicking the run button. 
** note the log will stream live as the test runs.

![image](https://user-images.githubusercontent.com/5246775/220804186-2cf9ad41-0a8c-473a-bfeb-ae5806c65336.png)


5.	Results View – High level view of each test set that has ran and the pass/failure rates: 
![image](https://user-images.githubusercontent.com/5246775/220804303-d4b42eef-0e42-40a4-9b13-918a02a354a0.png)

This view shows any tests that were ran with a supplied environment variable called OFFICIAL_RUN_TYPE.  This variable is always assigned from a test initiated from the dashboard.  A test that is re-ran will inherit the variable.  The purpose of this distinction is to allow a view that is displayable with real test results not failures that occur during test development.  You can also double click or single a click and use the view icon (the eye) to go from this view to the detailed Result Set view shown earlier.  These sets may be comprised of runs from multiple machines or test runs.  This allows easy breakdown of tests into sets for speed but a single reported set of results.

6.	Status AKA Activity View – Similar to Result View except the Status view shows any test launched form any machine including results that may be from tests under construction.  This view also allows the capture of test artifacts such as the log and screen shots  This data can be purged via a rake task if it gets too large.:  
![image](https://user-images.githubusercontent.com/5246775/220804358-37460e37-4364-4be1-aa01-46c2808e4711.png)

7.	Scenario View: - This is a view that does not have a header option as you get to this view from any other view that shows Scenario level results.  The Scenario History View is accessed by double clicking the scenario result row or single clicking to select the row and using the view details button which is the eye icon:
 
![image](https://user-images.githubusercontent.com/5246775/220804405-31da6c6b-338a-4fbd-8da9-245a4158c0aa.png)

8.	Coverage view: - This view shows the available tests and is organized with a clickable filters for tags that also show the count of tests that have the given tag:

![image](https://user-images.githubusercontent.com/5246775/220804440-0db3905f-5798-4103-b617-c6d3390e41ab.png)

Unintended benefit of this view is that if you write manual tests in Gherkin for documentation and have the tests tagged @manual it is easy for manual testers to find them which ensures manual tests are not missed each release (I find this easier than JIRA and will make a screen to log a manual test run as well should be easy using existing framework).


9.	Performance view: - This view shows the performance results for any block automation code using a block method in the test stack called “performance_wait” that will then report the results of that action to the automation database table called “performance_metrics”.  This still a work in progress. 
![image](https://user-images.githubusercontent.com/5246775/220804512-0288ebfa-bbcd-4826-8332-c13bce0b7410.png)

•	The times recorded are based on UI timing that would be experienced by the user It is great at measuring relative change and can even work by release version if have a way to capture that from either the UI or an environment variable.


10.	Documentation View – This view shows the results from a specialized set of tests used to test and document the requirements of the APIs. The documentation of the api happens automatically when the test runs but this screen does need an icon to add the api.  
![image](https://user-images.githubusercontent.com/5246775/220804562-d69992df-97ec-41fe-93e2-72692bf070b8.png)


a.	First level API list: by clicking the icon you are taken into the list of tested APIs for that Application.:  
![image](https://user-images.githubusercontent.com/5246775/220804619-4f87f5da-e10c-416b-8f84-3f32bc581bec.png)

b.	Individual API result level: This level shows the result of the endpoint test and an actual working example of the headers, payload and expected response from the endpoint. Here are a few examples below:
 
![image](https://user-images.githubusercontent.com/5246775/220804666-d9cbf938-9c4e-4846-8701-8cea28975621.png)

Additional Example of API result and documentation: (coming soon with payloads and more headers)

Drag and Drop Gherkin Builder:
  The Drag and Drop Gherkin (The test language of Cucumber) builder is a feature of the Automation Dashboard created by the Jeremy Davis that allows Non-Developer QA staff to easily create fully functional automated tests from the list of defined reusuable Cucumber/Gherkin steps.  This makes the steps like legos that stacked on top of each other to build new tests.  This eliminates the typical concerns an Automation team will have allowing non-developers in the test stack.  This is for two main reasons.  One is because the builder ensures no syntax errors can be introduced that typically break the Cucumber tag parsing thus breaking the test stack until the syntax error is fixed.  The other is that they do mot have access to play with or adjust any automation code.  It also eliminates the need to buy licenses for an ide (Rubymine) for the QA staff that only write Gherkin only the ruby developers would need the ide licenses.  You can also use existing tests as templates that load in the builder as a starting point to save time if only the last few steps need to be different. 
  
![image](https://user-images.githubusercontent.com/5246775/220804735-33e2b849-12f6-483e-8023-c0dca4242146.png)

Step Details: The steps on the right are sent via json from a sinatra API for cucumber.  They can be dragged into the grey canvas area.  Cucumber AST tables are  formatted to avoid syntax errors.  The QA person can build test cases from created steps.
The steps also have instructions if the Automation Engineer placed comments in the step def as to how to use them when you hover over the step:

 ![image](https://user-images.githubusercontent.com/5246775/220804827-8d8ccaa1-3b70-4b7a-b158-4cd7930458d3.png)

Preview Built Gherkin:  You can preview your work as you go using the preview icon in the upper right:
![image](https://user-images.githubusercontent.com/5246775/220804874-5cb2f02f-a346-4f63-b774-3cf256902192.png)


3) Select a Test machine to save or run on as well as the environment and the feature file will be saved or saved and ran into a sub directory of the features directory.  (The location of the features directory will become a setting later in development to handle multiple test stacks).
 ![image](https://user-images.githubusercontent.com/5246775/220804948-01f83b32-03c3-45ea-8a3d-de2aeac84909.png)

4) You can also select a common browser or known mobile device for emulation:

![image](https://user-images.githubusercontent.com/5246775/220804967-39468807-125d-4b3a-bdad-9b1d121104ca.png)

Jira API Integration Enabled: If you are creating a drag and drop test and find you do not have the step you need you can request a step that needs to be created and it will create a task in Jira for the automation team.  You will be prompted for your JIRA user name and password and then you will see the JIRA chore created.
 
![image](https://user-images.githubusercontent.com/5246775/220805004-d27ee3eb-c412-432b-b1cb-8d3086419360.png)

6) The automation team sees the chore in jira under the step request filter in JIRA:
THIS CUSTOM PER ENVIRONMENT THIS WOULD BE A SCREENSHOT OF THE JIRA MADE THAT IS TBD WITHIN A GIVEN QA TEAM WHO/WHERE The jira task is created
Once the step code is made by the Automation Engineer and they run the rake task to sync with the database.

