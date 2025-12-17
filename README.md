# MyMaps
#### Video Demo:  <URL HERE>
#### Description:
## Overview
My project starts when I realize the dificult to find game maps, all they in yours own wiki's, **MyMaps** is the solution to this problem, in it anyone can share a map, it can be a game map, to help players, or a real place, like a natural reserve or a water park, don't have limits! The funcionalits include: After you create your account you can like and deslike another maps and create you own, with an image, a title and a description, people who don't have an account can see the comunity maps and search for one, making possible anyone access all maps. To make my project possible I used `Python` with `Flask` to manage the web application, `Jinja` manipulating the `HTML` pages, and `SqLite3` for store data, along the development, the use of this technologies prove it was a right decision. Next let's discurs the `app.py`.
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
- datetime.now().strftime("%d.%m.%Y.%H.%M.%S.%f")
  - Gives the date and time in format Day/Month/Year/Hour/Minute/Second/Milisecond
#### Werkzeug.utils
- secure_filename(`filename`)
  - Check if the name `filename` is secure for use, if is not, change for a secure name.
### Functions
Now you already know all libraries used and their uses. It's time to see the functions, the structure of the web aplication, and discurs about how their **work**.
#### login_check()
It's a fast way to check if the user are logged with their account using `session.get(\'user_id\')`. If he is logged it returns `True`, else, `False`.
#### extensions_check()
Use any() with loops to ensure the file extension are allowed, checking if is in `ALLOWED_EXTENSIONS`. If is in, returns `True`, else, `False`.
#### serve_upload_file()
Created a secure rote for access the image wich users want. It returns the exatly location of file.
#### home_page()
- For GET method
  - Fist she search in database for the 8 most liked maps by comunity and stores in `data` variable

