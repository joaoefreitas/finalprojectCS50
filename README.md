# MyMaps
#### Video Demo:  <URL HERE>
#### Description:
## Overview
My project starts when I realize the difficult to find game maps, all they in yours own wiki's, **MyMaps** is the solution to this problem, in it anyone can share a map, it can be a game map, to help players, or a real place, like a natural reserve or a water park, don't have limits! The functionalities include: After you create your account you can like and dislike other maps and create your own, with an image, a title and a description, people who don't have an account can see the community maps and search for one, making it possible for anyone to access all maps. To make my project possible I used `Python` with `Flask` to manage the web application, `Jinja` manipulating the `HTML` pages, `SqLite3` for store data and `Bootstrap` for design, along the development, the use of this technologies prove it was a right decision. Next let's discuss the `app.py`.
## app.py
### Libraries
#### Flask
- Flask
  - To configure the application, your routes, the upload folder, secret key and others.
- render_template
  - Display the HTML templates to the user and pass the variables to the front-end.
- request
  - Receives the form data and arguments from the user and the type of request, "GET" or "POST".
- redirect
  - Redirect the user with safety for another route.
- session
  - Take the information of the user and manage the login and logout.
- url_for
  - Ensures the redirect was led for the right place.
- send_from_diretory
  - Ensures the directory for the upload folder is correct.
#### Sqlite3
- sqlite3.connect()
  - Connect the application to the database file making possible the communication between python and the sqlite.
- cur.cursor()
  - Define the variable `cur` for a cursor, used to indicate data.
- cur.execute()
  - Use `cur` to indicate the result of a sqlite command, like *SELECT*, *UPDATE* and *INSERT*.
- cur.fetchall() and cur.fetchone()
  - Take the data indicated by `cur` for a python variable.
- cur.commit()
  - Save changes made by `cur.execute()`.
- con.close()
  - Ends the communication with the database.
#### Os
- os.path.abspath(os.path.dirname(\_\_file\_\_))
  - Create an absolute way for where the `app.py` is.
- os.path.join(app.config[\'UPLOAD_FOLDER\'], filename)
  - Save inside `UPLOAD_FOLDER` the user archive.
#### Hashlib
- hashlib.sha256()
  - Attribute a variable `m` to encrypt the information using sha256.
- `m`.update(`ìnfofile`.encode(\'uft-8\')
  - Encrypt `infofile` to bytes.
- `m`.hexdigital()
  - Convert encrypted bytes to hexdecimals (making it easier to implement).
#### Datetime
- datetime.now().date()
  - Gives the date of day in format Year/Month/Day.
- datetime.now().strftime("%d.%m.%Y.%H.%M.%S")
  - Gives the date and time in format Day/Month/Year/Hour/Minute/Second
#### Werkzeug.utils
- secure_filename(`filename`)
  - Check if the name `filename` is secure for use, if not, change it to a secure name.
#### Werkzeug.security
- generate_password_hash()
  - Encrypt the password to prevent database invasion.
- check_password_hash()
  - Compare the hash stored in the database with the try of login.
### Functions
Now you already know all libraries used and their uses. It's time to see the functions, the structure of the web application, and discuss about how their **work**.
#### login_check()
It's a fast way to check if the user is logged in with their account using `session.get(\'user_id\')`. If he is logged it returns `True`, else, `False`.
#### extensions_check()
Use any() with loops to ensure the file extension is allowed, checking if it is in `ALLOWED_EXTENSIONS`. If it is in, returns `True`, else, `False`.
#### serve_upload_file()
Created a secure route for access to the image which users want. It returns the exact location of the file.
#### home_page()
It searches the 8 most liked maps and gives information to the front-end, if the user searches, it receives a form and reloads the page with the search argument, after the reload the result will be passed together with 8 most liked maps.
#### register()
Register function take a form with email, username, name, birth, password to create a new account, it guarantees the username and email hasn't been used yet, to make each account unique, finally,
It encrypts the password using `generate_password_hash()` and adds the new user data in the database and redirects the user to the login page to enter in their new account.
#### login()
The login function gets the username and password to check if the values are valid, and then, compare with `check_password_hash()`, logging the user if they are equal.
#### account()
First of all use the `login_check()` to display this page only for people who are logged in, search in a data database using the id of the user and take your information, search all maps which have been created by the user and display them in the account page.
#### logout()
Simply every user who enters in the `/logout` route automatically logs out and redirects to the home page.
#### createmap()
Display the page with the form to create a new map.
#### upload()
Receives the inputs from `createmap.html` form check if the title name, description characters or the archive size limit was reached, and create a unique hash compound by the id of author + the date and time when the archive was uploaded + the original filename, it saves in upload folder and insert the new map in database.
#### viewer()
It takes the argument (the name of the file) passed and searches in the database from the map, displaying the image, the title, the description, the creation date. If the method is POST, it receives the value of user interaction (like or dislike) and adds in map information, then reloads the page to show the new value.
## layout.html
### Its importance
This HTML is the base structure of all pages, in it contains all links with Bootstrap and the CSS file, also has the navigation bar with all links and the footer of all pages, standardizing the pages making it easier to reuse features using Jinja.
### How its works?
Using Bootstrap I created a toolbar with the main pages, taking the logo from icons folder and using Jinja to change the account options if the user are logged or not, displaying \"Create an account\" and \"login\" or \"Accont Settings\" and \"logout\". After I created a block with text aligned in center and the block content, add a script to make the toolbar work, lastly, the footer bar with \"This is CS50\" message. 
## homepage.html
### How it works
Create a form to make the search bar, if the back-end returns results display then like cards with href's with view address, else display \"No results\" or if the search field is empty don't display anything, below this, display the 8 most liked maps. Remembering that the two, results and most liked maps, are being passed as dictionaries and displayed with a Jinja loop.
## account.html
### How it works
Takes the user's information as Username, Name, Birth, Email and displays then and receives all map information which was created by the user and shows as a Bootstrap card.
## createmap.html
### How it works
Displays the form to upload the map, the form will redirect with POST method for `/upload` route with the answers to do all the upload process.
## error.html
### Why I created it?
Creating an error page makes it easier to display the error and tell the user the reason, in a way more user friendly using a cute cat image and a link to try again.
### How it works
Jinja receives the reason for the error and the origin link, displaying the reason and creating a clickable text for the user to come back to the origin page.
## login.html
### How it works
Create a form with username and password fields with `/login` `POST` action, and below an clickable text to `/register` if the user doesn't have an account yet.
## register.html
### How it works
Create a form with E-mail, username, name, birth, password and their confirmation with `/register` `POST` action.
## view.html
### How it works
Uses the information passed by backend with name of map her description, up votes, down votes, author and creation date. For like or dislike a map the view.html use a form with a fild with two possible values, `like` or `dislike`, submitting for back-end to compute the vote, refreshing the page.
## style.css
### Why I created it?
Uses a base to style the page make the development more easier because don't make necessary the every element adjust and faster
### How it works
Make visited links without the underline and blue color, adjust the size and orientation of vote buttons, her places and the cursor behavior and the break line of texts which is so big.
## icons Folder
### Why I created it?
Is a folder where the logo of the site is stored as various formats and sizes, where all the application can easily access to use.
## images Folder
### Why I created it?
Is a folder where all images the site uses, standardizing a place to store this images and doing the directory of the project organized.
## uploads Folder
### Why I created it?
Is a folder where all base images of maps are stored, making a pattern where search for a map.
## database.db
### Why did I choose SqLite?
Because it is a simple and light database, organized in columns and rows and is easier to integrate with python.
### How it works
Have two tables one called users, with an unique id, username, name, password, birth and email fields, where stores all users informations and the other called maps, with an unique id, the author's id, the name, description, base (the name of image of map), elements (the type of map), up votes and down votes number, and the creation date.
## Conclusion
I think **MyMaps** serves its purpose and help me to understand more of development world, thanks so much CS50 for give this opportunity, the classes was very helpful, is unbelievable all the curse was totally free, I’m very grateful for all CS50 team for do this happen. And this was CS50x! 
