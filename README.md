# syllabus_tracker
nstallation
Just clone the repository to your system using your terminal, or download the repo as a zip. I tailored it to my own college experience but it can be used with the syllabus of any other college. See notes on how to add your own syllabus and other customization.

git clone https://github.com/Charakupa/syllabus_tracker.git
cd Syllabus-Tracker
Usage and Info
Run the downloaded Repo on a Web Server. (Like Python's Simple Server using the command : python -m http.server for Python 3) as the web app requires to run a XML HTTP Request to a syllabus JSON file.

The Syllabus files are present in the /syllabi directory are in the form of JSON.

The Web App utilises Local Storage to store User Data that has a max size of around 5-20 KB. Thus, there is no need for anyone to logout or remember sessions as the storage is in place and updated in real time. All the data regarding the user is stored on their own computers and hence makes the whole experience much faster.

To view the data stored in Local Storage, run the following command in the console.

JSON.parse(localStorage.getItem('syllabusTracker'))
Structure
The app utilizes :
Components present in /scripts/components.js
The core functionality is present in /scripts/scripts.js.
A minified pre-ES6 version of both has been transpiled to /scripts/scripts-min.js. Which is the recommended version to use as its half the length and cross - broswer compatible.
The styles are present in /styles directory.
Any Additional files that need to be added should be added to the /files directory.
The Syllabus files are present in /syllabi directory.
Customization
There are a no of customizations you can make to the web app.

Adding Your Own Syllabus
The Web App requires addition of syllabus files to it. By default, only the Syllabus of the Second Year Computer Science course of Fergusson College has been added to the project.

In order to add your own course syllabus, have a look at the structure of sybsccs.json file. That is the core structure expected for any JSON File consisting of a syllabus.

{
	"Year":"2022-23",
	"Course":"SY BSc CS",
	"Subject":"Computer Science",
	"Semester I":{
		"Units" : [
			{
				"Name":"Data Structures using C",
				"Lectures":48,
				"isPractical":false,
				"Credits":3,
				"Code":"CSC2301",
				"Sub-Units" : [
					{"Name":"Introduction to Data Structure and Algorithm Analysis"},
					{"Name":"Linear Data Structures"},
					{"Name":"Non-Linear Data Structures"}
				],
				"References" : [
					
				]
			}
		]
	}
}
The file consists of a master object that contains all the details. Year, Course and Subject fields are necessary to create a proper user header once the user logs in.

Note : The JSON when being read is case sensitive, so kindly pay close attention to the typed case of the keys above to avoid errors.

Beneath that is an Object for the Semester (The word Semester is compulsory otherwise it will not be read.) which houses details such as No of Lectures, Name, No Of Credits, whether the subject is a practical, the chapters included in it and also references to the study materials for the subject, in case you plan to help someone else with this web app too in your group.

The Lectures, Credits and Code properties are optional and will not be rendered to the UI of the app, however, you could always change that if you want to.

Create a JSON file in the above format for as many semesters you may want and as many units. The App should take care of rendering them.

Linking your syllabus file and course
After you are done creating your syllabus file. Its time to add it and its sources to the app. Open the file scripts.js in the scripts folder. At the top of it.

Change the line :

const options = Object.freeze(["SY BSc CS"]);
Add all the options for courses you want to. Object.freeze has been used to prevent the changing of the options once the app has been started.

Underneath that, change the code :

const courseFiles = Object.freeze({
	"SY BSc CS" : "./syllabi/sybsccs.json"
});
Set the course files that should be read using an XML HTTP Request once the user selects the course.

Note : Don't repeat the same unit name. Just Telling, otherwise the script starts crying baby tears.

Viewing References for a Subject + UI Details
The References you add will not appear when you log in to your dashboard, to view them, click on the subject name / unit name. That will generate a modal box containing all the links.

To mark a unit complete, just click the checkbox adjacent to it, this will re-render the progress bar at the top.

Practicals for now cannot be marked complete as many colleges do not allow the completion of practicals at home. You could change it however you want by changing the script.

Applying the changes
The index.html file is linked to the scripts-min.js file and hence your changes will not directly take effect.

Therefore, replace

<script type="text/javascript" src="scripts/scripts-min.js"></script>
with

<script type="text/javascript" src="scripts/components.js"></script>
<script type="text/javascript" src="scripts/scripts.js"></script>
Fire up your web server and if you did everything right, you will see the changes take effect.

PS : I know that is a lot to deal with for such a simple project. Sorry. 😛✌
