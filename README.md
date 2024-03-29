Server Room Swipe
==========

# Installation
### Prerequisites
- python 2.7
- python-pip `apt install python-pip`
- flask-admin      `pip install flask-admin`
- flask-httpauth   `pip install flask-httpauth`
- flask-login      `pip install flask-login`
- flask-migigrate  `pip install flask-migrate`
- flask-sqlalchemy `pip install flask-sqlalchemy`
- flask-wtforms    `pip install flask-wtf`
- evdev            `pip install evdev`
- pytz             `pip install pytz`
- requests         `pip install requests`

### Steps
- `git clone https://github.com/lime45/server_room_swipe.git`
- `cd` into the repo
- `echo <some_password> >new_user_pass` for a default new user password
- `echo <some_badge_id> >pioneer_badge` for a default pioneer badge
- `echo <pi_user_name> >pi_username` for the username the pi will have in the db
- `echo <pi_user_pass> >pi_user_pass` for the pi's password in the db
- `./reset_db.sh` to get a fresh db with just the pi's user account
- `flask db init` creates database, only needs to be done once
- `flask db migrate` migrates database if schema changes
- `flask db upgrade` commits changes from migrate
- `sudo ./run.sh |& tee server.log` to start the server
- The server is available at the IP of the raspberry pi on port 80
- `sudo ./quit.sh` to stop the server

# Web Interface
Navigate to the IP of host and you will be presented with a login page. Anyone
who will be an admin will need to initially login using the pi's account. See
above for where that info is stored. A user with admin rights is the only person
that can add users and change passwords.

# Pioneer badge
This is the badge you use to register new badges in the system. First scan
the pioneer badge, then scan the new persons badge. This scan doesn't count
as a real scan and won't get recorded in the Scans table until the next time
the badge is scanned. When the pioneer badge is used, a new user will be
created in the database as "new\_user\_XXXXXX" where XXXXXX is an assortment
of 6 random lowercase and uppercase letters. This user will have the password
from repo/.new\_user\_pass that you should have created.

# TODOs
- Use a real web server instead of the one that comes with Flask
- less ugly UI with CSS to make look and feel more consistent
- Make this a real python package with requirements.txt, setup.py etc
- Add option for users to reset their password.
