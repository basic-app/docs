Installation
============

To get started with Basic App, you need to install the "basic-app/basic-app" package through Composer, or download it from GitHub directly. This is a basic application, it is downloaded once, and then you modify and customize it for your project.

## Step 1

Install the application via Composer with the following command:

`composer create-project --stability=dev --remove-vcs --prefer-dist basic-app/basic-app demoapp`

The command installs the application in a directory named "demoapp". You can choose a different directory name if you want.

## Step 2

Rename the file named "env" to ".env". Configure a base site url, timezone, and database connection settings in the ".env" file.

## Step 3

Apply migrations using the following command:

`php spark migrate:latest -all`
    
## Step 4

Installs the project dependencies:

`bower install`
    
## Step 5

Set the document root of your web server to "/public" directory.
   
## Step 6

Run the "install" hook:

`php spark install`

## Step 7

Run the "cron" command every 5 minutes using Cron:

`php spark cron`
    
## Access Backend

Access an application backend in your brower by opening "example.com/admin" url.
```
login: admin
password: admin
```

Please change the password to another using backend web interface.