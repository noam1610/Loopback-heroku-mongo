# Loopback-heroku-mongo

In this tutorial we are going to create a server :
    --> cloud : Heroku
    --> database : Mongodb (mongolab)
    --> server : Loopback

## Loopback and its files

### Create a new repo

On git, create manually a new repository 

Then, on your laptop create a folder :

```
mkdir my-new-folder
```
Now go into your folder :
```
cd my-new-folder
```

Once it's done, associate the repo and the folder :
Use the command lines given in Github 
```
    git init
    git commit -m "first commit"
    git remote add origin https://github.com/noam1610/LoopbackTEST.git
    git push -u origin master
```

Don't forget the :
```
npm init
```

This will create you a package.json
It's a very important file. Keep it !

### Create the data of the server

First :

```
yo sublime
```

Then

```
yo sublime:gulps
```
You will see this :

![alt text](https://github.com/noam1610/Loopback-heroku-mongo/blob/master/images/sublime.png "Logo Title Text 1")


Only choose **lint** **test** **changelog** and **release**


Make sure you have slc installed.

```
npm install -g strongloop
```

Now we can use the slc loopback generator to create a folder. 
Some of its files are needed.

```
slc loopback tempFolder
```

In temfolder, open the package.json

Copy the 3 sections : 
  * dependencies
  * devDependencies
  * optionalDependencies

Paste it in the initial package.json (located in the root directory).

Now copy the folder server in tempFolder and deplace it to the root directory.

You can now delete tempFolder.

To make sure all dependencies are added :
```
npm install
```


### Use a generator

Let's create an object which will be stored in the database : subsider

```
slc loopback:model
```
Now let's answer the questions :

![alt text](https://github.com/noam1610/Loopback-heroku-mongo/blob/master/images/loopback-model.png "Logo Title Text 1")

![alt text](https://github.com/noam1610/Loopback-heroku-mongo/blob/master/images/loopback-model-object.png "Logo Title Text 1")


Next Step:
```
slc loopback:datasource
```
Answer the questions
![alt text](https://github.com/noam1610/Loopback-heroku-mongo/blob/master/images/datasource.png "Logo Title Text 1")


Modify the code :

Go to common/models 
You have two files : subsider.js and subsider.json

In the first one add this :

```Javascript
module.exports = function(Subsider) {
    Subsider.sharedClass.find('create', true).shared = true;
    Subsider.sharedClass.find('update', true).shared = false;
    Subsider.sharedClass.find('upsert', true).shared = false; 
    Subsider.sharedClass.find('updateAttributes', false).shared = false;
    Subsider.sharedClass.find('deleteById', true).shared = false;
    Subsider.sharedClass.find('find', true).shared = false; 
    Subsider.sharedClass.find('findById', true).shared = false; 
    Subsider.sharedClass.find('count', true).shared = false; 
    Subsider.sharedClass.find('exists', true).shared = false; 
    Subsider.sharedClass.find('findOne', true).shared = false;
};
```


## Integrating Heroku

First, you have to go to [Heroku!](https://www.heroku.com) and create an account.
Then you have to install the [Heroku toolbelt](https://toolbelt.heroku.com).

Now you can login and create a new app :

```
$ heroku login
Enter your Heroku credentials.
Email: adam@example.com
Password (typing will be hidden):
Authentication successful.
```

```
$ heroku create
```

In your server folder, you have to create a new file called datasources.heroku.js :

```Javascript
'use strict';

module.exports = {
    mongo: {
        url: process.env.MONGO_URL
    }
};
```

Then, in the root directory create a file **Procfile** with no extension :

```
web: node server/server.js
```
## Mongo

The last file to change is datasources.js
It should looks like this :
```JSON
{
  "db": {
    "name": "db",
    "connector": "memory"
  },
  "mongo": {
    "name": "mongo",
    "connector": "mongodb"
  }
}
```

But before running to have to create manually a database in [Mongolab](https://mongolab.com)

You have to create a user for this database: with dbuser and dbpassword

Copy the uri given.
It should look like :

```
mongodb://<dbuser>:<dbpassword>@ds061148.mongolab.com:61148/tuto-server
```
Don't forget to change dbuser and dbpassword without <> 

Then in the terminal write :
```
heroku config:set NODE_ENV=heroku
heroku config:set MONGO_URL=mongodb://myuser:mypassword@ds061148.mongolab.com:61148/tuto-server
```

Now we can commit and push:
```
git cm "feat(app):yo!!"
git push
git push heroku
```

Now let's hope it works:
```
open heroku
```

REM = Don't forget to check in model-config that your object is linked with your datasource :
```JSON
"subsider": {
        "dataSource": "mongo",
        "public": true
    }
```

