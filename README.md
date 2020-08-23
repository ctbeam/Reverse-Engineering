# Reverse-Engineering
Overall User Story:
This app is to give the user a safe way to register and log in to various types of websites. The data that is registered is stored on a MySQL database. 

Reverse Engineering

Folder >Config
Files Contained: config.json, passport.js, isAuntheticated.js

Config.json- is the code that contains the database info within the package. It contains validation to access the database.

Passport.js- (“http://www.passportjs.org/”) This code Imports functions “Passport’ and “Local Strategy” prompting the user to “login” by entering their email(as opposed to username/user) and password. Then passport.js will pull the database(db) from the  “models” folder to see if what has been entered matches with the email/password stored in the database. If either are incorrect, then the user will be returned to the main(root) page via isAuthenticated.js which is the middleware.  The same middleware will be used to redirect users to the restricted route if both username and password are both correct.  The passport is then serialized/deserialized to keep the user authenticated throughout all the HTML’s when they are browsing through pages on the site so they will not have to log in each time.  The function “Passport” is then exported to be used in other files.


Folder- Models
Contains files: index.js and user.js

Index.js handles the starting, routing, and functions of this application.  It declares requirements for functionality 

Exports the functions “sequelize” and “DataTypes” to be used in other files. 

The user is to enter their email (DataTypes.STRING) which cannot be left blank (allowNull: false) the email must be unique.  Email addresses will be verified in the database to match possible emails.   

User then enters their own password (DataTypes.STRING).  Password cannot be left blank (allowNull: false) Password will then be created and hashed.

Folder- Public
Contains folders: “js” and “stylesheets” and files: “login.html” “members.html” and “signup.html”

Login.html-  The user logs in here. Using the script from login.js if login info is correct, user will be redirected to “members.html” which uses the members.js. If login is unsuccessful then user will be directed to “signup.html”

Folder > Public > stylesheets
style.css
Is the styling for the HTML.  

Folder > Public > JS
login.js, members.js, signup.js

Login.js creates the loginForm that prompts a submit event when a user puts in their email (emailInput) and password(passwordInput).  The form is then cleared and if login is correct, the user is redirected to members.html.  

Members.js does a GET request to figure out which users are logged in and keeps the HTML up-to-date.

Signup.js creates a signUpForm where the user enters email (emailInput) and password(passwordInput). Upon submit event, forms will be validated as not left blank, and the user will be taken to the member page.  Signup.js is the running script used in signup.html.

Folder > Routes
Contains files: “api-routes.js” “html-routes.js”

Api-routes.js imports db and passport that can be used for the four different routes.
The first route connects to a login/api that uses passport.authenticate middleware to validate the login credentials and if everything matches, will direct the user to members.html.  

The next route connects to signup/api where the user can enter a unique email and password to be used.  The password will be hashed by users.js and store securely in db. Once a user is signed up they will be redirected to members.html.  

The next route is simply a logout route.

The last route connects to user_data/api and is used clientside to get user data.

Html-routes.js imports the paths so the routes can be used for the HTML files.  

isAuthenticated keeps users logged in when browsing through pages.  If the user is not authenticated then the user will be redirected to a sign up page.

Server.js
Server.js causes the app the work to serve as a connecting hub is the first connecting hub. It imports all the packages and functions and declares the PORT. 

It also contains the boiler plate, and sets the valid routes.  

Package.json
Shows what is all installed in the app. 

travis.yml
Testing situation for the app.

eslintignore
Files to ignore for the purpose of linting.

File → gitignore
Tells github which files to ignore.

eslintignore.json
Lint- Json packages to ignore for the purpose of linting.
