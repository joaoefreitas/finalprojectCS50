# MyMaps
#### Video Demo:  <URL HERE>
#### Description:
## Overview
My project starts when I realize the dificult to find game maps, all they in yours own wiki's, **MyMaps** is the solution to this problem, in it anyone can share a map, it can be a game map, to help players, or a real place, like a natural reserve or a water park, don't have limits! The funcionalits include: After you create your account you can like and deslike another maps and create you own, with an image, a title and a description, people who don't have an account can see the comunity maps and search for one, making possible anyone access all maps. To make my project possible I used `Python` with `Flask` to manage the web application, `Jinja` manipulating the `HTML` pages, `SqLite3` for store data and `Bootstrap` for design, along the development, the use of this technologies prove it was a right decision. Next let's discurs the `app.py`.
## app.py
### Libraries
#### Flask
- Flask
  - To configure the application, your routes, the upload folder, secret key and others.
- render_template
  - Display the HTML templates to user and pass the variables to front-end.
- request
  - Receives the form data and arguments from user and the type of request, "GET" or "POST".
- redirect
  - Redirect the user with safety for another route.
- session
  - Take the information of the user and manage the login and logout.
- url_for
  - Ensures the redirect was leaded for right place.
- send_from_diretory
  - Ensures the directory for upload folder is correct.
#### Sqlite3
- sqlite3.connect()
  - Connect the application to database file making possible the comunication between python and the sqlite.
- cur.cursor()
  - Define the variable `cur` for a cursor, using to indicate data.
- cur.execute()
  - Use `cur` to indicate the result of a sqlite comand, like *SELECT*, *UPDATE* and *INSERT*.
- cur.fetchall() and cur.fetchone()
  - Take the data indicated by `cur` for a python variable.
- cur.commit()
  - Saves changes made my `cur.execute()`.
- con.close()
  - Ends the comunicated with database.
#### Os
- os.path.abspath(os.path.dirname(\_\_file\_\_))
  - Create an absolut way for where the `app.py` is.
- os.path.join(app.config[\'UPLOAD_FOLDER\'], filename)
  - Save inside `UPLOAD_FOLDER` the user archive.
#### Hashlib
- hashlib.sha256()
  - Atribute a variable `m` to encrypt the informations using sha256.
- `m`.update(`ìnfofile`.encode(\'uft-8\')
  - Encrypt `infofile` to bytes.
- `m`.hexdigital()
  - Convert encrypted bytes to hexdecimals (making easier to implement).
#### Datetime
- datetime.now().date()
  - Gives the date of day in format Year/Month/Day.
- datetime.now().strftime("%d.%m.%Y.%H.%M.%S")
  - Gives the date and time in format Day/Month/Year/Hour/Minute/Second
#### Werkzeug.utils
- secure_filename(`filename`)
  - Check if the name `filename` is secure for use, if is not, change for a secure name.
#### Werkzeug.security
- generate_password_hash()
  - Encrypt the password to prevent in case of database invasion.
- check_password_hash()
  - Compare the hash stored in database with the try of login.
### Functions
Now you already know all libraries used and their uses. It's time to see the functions, the structure of the web aplication, and discurs about how their **work**.
#### login_check()
It's a fast way to check if the user are logged with their account using `session.get(\'user_id\')`. If he is logged it returns `True`, else, `False`.
#### extensions_check()
Use any() with loops to ensure the file extension are allowed, checking if is in `ALLOWED_EXTENSIONS`. If is in, returns `True`, else, `False`.
#### serve_upload_file()
Created a secure rote for access the image wich users want. It returns the exatly location of file.
#### home_page()
It search the 8 most liked maps and gives her informations to front-end, if the user search, It recives like a form and reload the page with the search argument, after the reload the result will be passed together with 8 most liked maps.
#### register()
Register function take a form with email, username, name, birth, password to create a new account, it guarantees the username and email was't been used yet, to make each account unique, finally,
it encrypt the password using `generate_password_hash()` and add the new user data in database and redirect the user to login page to enter in their new account.
#### login()
Login function gets the username and password check if the values are valid, and then, compare with `check_password_hash()`, logging the user if they are equal.
#### account()
First of all uses the `login_check()` to display this page only for people who are logged, search in data base using the id of user and takes yours informations search all maps wich have been created by the user and display in the accout page.
#### logout()
Simply every user who enter in `/logout` route automatically be logout and redirect for home page.
#### createmap()
Display the page with the form to create a new map.
#### upload()
Recieves the inputs from `createmap.html` form check if the title name, description caracthers or the archive size limit was reached, and create a unique hash compound by the id of author + the date and time when the archive was uploaded + the original filename, it saves in upload folder and insert the new map in database.
#### viewer()
It take the argument (the name of file) passed and search in database from the map, display the image, the title, the description, the creation date. If the method is POST, it recives the value of user interaction (like or deslike) and add in map information, then reload the page to show the new value.
## layout.html
### Its importance
This HTML is the base structure of all pages, in it contains all links with Bootstrap and the CSS file, also have the navegation bar with all links and the footer of all pages, standardizing the pages making more easier to reuse features using Jinja.
### How its works?
Using Bootstrap I created a toolbar with the main pages, taking the logo from icons folder and using Jinja to change the account options if the user are logged or not, displaying \"Create an account\" and \"login\" or \"Accont Settings\" and \"logout\". After I created a block with text align in center and the block content, add a script to make work the toolbar, lastly, the foother bar with \"This is CS50\" mensage. 
## homepage.html
### How its works?
Create a form to make the search bar, if the back-end returns results display then like cards with href's with view address, else display \"No results\" or if the search field is empty don't display anything, below this, display the 8 most liked maps. Remembering that the two, results and most liked maps, are being passed as dicionaries and displaying with a Jinja loop.
## account.html
### How its works?
Takes the user's informations as Username, Name, Birth, Email and display then and recives all maps informations with was criated by the user and shows as Bootstrap card.
## createmap.html
### How its works?
Displays the form to upload the map, the form will redirect with POST method for `/upload` route with the answers to do all the upload process.
## error.html
### Why I created it?
Create a error page make more easier to display the error and tell the user the reason, in a way more user friendly using a cute cat image and a link to try again.
### How its works?
Jinja recieves the reason of error and the origin link, displaying the reason and creating a clickable text to the user come back to origin page.
## login.html
### How its works?
Create a form with username and password fields with `/login` `POST` action, and below an clickable text to `/register` if the case the user don't have an account yet.
## register.html
### How its works?
Create a form with E-mail, username, name, birth, password and their confirmation with `/register` `POST` action.
## view.html
### How its works?
Uses the information passed by backend with name of map her description, up votes, down votes, author and creation date. For like or deslike a map the view.html use a form with a fild with two possible values, `like` or `deslike`, submitting for back-end to compute the vote, refreshing the page.
## style.css
### Why I created it?
Uses a base to style the page make the desevolviment more easier because don't make necessary the every element ajust and faster
### How its works?
Make visited links without the underline and blue color, adjust the size and orientation of vote bottons, her places and the cursor behavior and the break line of texts with is so big.
## icons Folder
### Why I created it?
Is a folder where the logo of site are stored as various formats and sizes, where all the aplication can easily access to use.
## images Folder
### Why I created it?
Is a folder where all images with the site uses, standardizing a place to store this images and doing the directory of project organized.
## uploads Folder
### Why I created it?
Is a folder where all base images of maps are stored, making a pattern where search for a map.
## database.db
### Why I chose SqLite?
Because is a simple and light database, organized in collums and rows and is easier to integrate with python.
### How its works
Have two tables one called users, with an unique id, username, name, password, birth and email fields, where stores all users informations and the other called maps, with an unique id, the author's id, the name, description, base (the name of image of map), elements (the type of map), up votes and down votes number, and the creation date.
## Conclusion
I think **MyMaps** serves its purpose and help me to undestand more of developement world, thanks so much CS50 for give this oportunity, the classes was very helpfull, is unbelievable all the curse was totally free, I’m very grateful for all CS50 team for do this happen. And this was CS50x! 
