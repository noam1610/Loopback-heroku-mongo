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

### Use a generator

First :

```
yo sublime
```

Then

```
yo sublime:gulps
```
You will see this :

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
    ⋅⋅* dependencies
    ⋅⋅* devDependencies
    ⋅⋅* optionalDependencies

Paste it in the initial package.json (located in the root directory).

Now copy the folder server in tempFolder and deplace it to the root directory.

You can now delete tempFolder.

To make sure all dependencies are added :
```
npm install
```


### Use a generator


















