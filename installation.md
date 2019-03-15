Installation
============

## Step 1

Install the application via Composer with the following command:

`composer create-project --stability=dev --remove-vcs --prefer-dist basic-app/basic-app demoapp`

The command installs the application in a directory named "demoapp". You can choose a different directory name if you want.

## Step 2

Rename the file named "env" to ".env". Configure base site url, timezone, and database connection settings in the ".env" file.

## Step 3

Run migrations:

`php spark migrate:latest -all`
    
## Step 4

Install Bower libraries:

`bower install`
    
## Step 5

Set document root of your web server to "/public" directory.
   
## Step 6

Run the "install" hook:

`php spark install`

## Step 7

Run the "cron" command every 5 minutes using Cron:

`php spark cron`
    
## Backend

Access application backend in your brower by opening `http://example.com/admin` url.
```
login: admin
password: admin
```

Please change the password to another via backend web interface.