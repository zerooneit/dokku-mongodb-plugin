[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/jeffutter/dokku-mongodb-plugin?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

MongoDB plugin for Dokku
---------------------------
Plugin to setup Mongodb accounts for containers deployed to Dokku


Installation
------------
```
git clone https://github.com/jeffutter/dokku-mongodb-plugin.git /var/lib/dokku/plugins/mongodb
dokku plugins-install
```


Commands
--------
```
$ dokku help
    mongodb:console                 		    Launch an admin mongodb console
    mongodb:create <app> <database> 		    Create a Mongo database and optional params for app
    mongodb:delete <app> <database> 		    Delete specified Mongo database
    mongodb:link <app> <database>	       	    Set ENV variables for app if database exists
    mongodb:list                    		    List all databases
    mongodb:logs                    		    Show logs from MongoDB program
    mongodb:start                   		    Start the MongoDB docker container if it isn't running
    mongodb:status                  		    Shows status of MongoDB
    mongodb:stop                    		    Stop the MongoDB docker container
```

Simple usage
------------
You need to have app running with the same name!

Create a new DB:
```
$ dokku mongodb:create foo            # Server side
$ ssh dokku@server mongodb:create foo # Client side

    {
        "_id" : ObjectId("524c90dc45addf0edad783a2"),
        "user" : "foo",
        "readOnly" : false,
        "pwd" : "825ec0deacccb3c6bb621d84153e5877"
    }

```

Now if you push your app again, you will have the following ENV variables:
```
MONGODB_DATABASE
MONGODB_HOST
MONGODB_PORT
MONGODB_USERNAME
MONGODB_PASSWORD
MONGO_URL
MONGO_URI
```

These can be found using:
```
dokku config appname
```

Persistence
-----------

The Mongo DB data is stored outside the container on the host at `$DOKKU_ROOT/.mongodb/data`. Inside the container, this location is bound to `/tmp/mongo` and will be there. 
Since the data is stored outside the container, it will persistent through container restarts, and also be available to future revisions of your container. 

