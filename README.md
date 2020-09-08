# ✨ Astra101Java

Minimal code sample to work ASTRA in Java

[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)

## Table of Contents

| Steps | Description and Links
|---|---|
| 0. Create your Astra instance | [Prerequisites](#1-create-your-astra-instance) |
| 1. Download the secure bundle | [Download secure bundle](#2-download-the-secure-bundle) |
| 2. Run the demo | [Connectivity](#3-run-the-application) |


## 1. Create your Astra instance

`ASTRA` service is available at url [https://astra.datastax.com](https://astra.datastax.com/)

**✅ Step 1a. Register (if needed) and Sign In to Astra** : You can use your `Github`, `Google` accounts or register with an `email`

- [Registration Page](https://astra.datastax.com/register)

![Registration Image](images/astra-create-register.png?raw=true)

- [Authentication Page](https://astra.datastax.com/)

![Login Image](images/astra-create-login.png?raw=true)


**✅ Step 1b. Fill the create new Database Form**

If you don't have have any Astra instances you will be routed to creation form. Here are some insights.

![Database Form](images/astra-create-2.png?raw=true)

- **Set the Compute Size**: Please use `Free tier`. You instance will be there forever, free of charge, no credit card what so ever.

- **Select the region**: This is the region where your database will reside physically (choose one close to you or your users). For people in EMEA please use `europe-west-1` idea here is to reduce latency.

- **Database name** - It should be alpha numeric without spaces we propose here `demo`

- **Keyspace name** - It should be alpha numeric without spaces we propose here `astra101`. You will be able to add keyspaces later.

- **Database User name** - Provide a username your will remember let's user `astra`

- **Password** - Provide a username your will remember let's user `astra2020`

- **Launch the database**. if all fields are filled click the Launch Database button.


![Launch Database](images/astra-create-3.png?raw=true)

**✅ Step 1c. View your Database and connect**

View your database. It may take 2-3 minutes for your database to spin up. You will receive an email at that point. But, go ahead and continue with the rest of the exercise now.

![View Database](images/astra-create-4.png?raw=true)

Once Database is ready you should see the following home page:

![Home Page](images/astra-create-5.png?raw=true)

Let’s review the database you have configured. In the box on the left side of the window, you can see the database and keyspace name metadata. The box on the right describes the size and location of your database along with your estimated cost. Once Astra initializes the database completely, the left box will have connection details.

[🏠 Back to Table of Content](#table-of-content)

## 2. Download the secure bundle

**✅ Step 2a. Download the secure connect bundle** : Go to the home page. Execute a _refresh_ of the page using (F5) (the download link will be valid for 5 minutes and we want to ensure NOT to reach the timeout). Locate link `Download secure connect bundle` and click. You should download a file named `secure-connect-<your_db_name>.zip`. Please remember the location of the file.

![TodoBackendClient](images/astra-create-7.png?raw=true)

Save the file in a path you will remember, again we will need it for the next exercises.

[🏠Back to HOME workshop](https://github.com/DataStax-Academy/cassandra-workshop-series)

## 3. Run the application

**✅ Step 3a. Edit the configuration files** : 

locate the file `application.conf` and edit #1, #2, #3 reflecting user,passwordmzip and keyspace.

```yaml
datastax-java-driver {
   basic {
    request {
    	timeout     = 10 seconds
        consistency = LOCAL_QUORUM
        page-size   = 5000
    }
    # 1. Enter keyspacec 
    session-keyspace = astra101
    cloud {
      #2. Where is the zip
      secure-connect-bundle = /Users/cedricklunven/Downloads/secure-connect-astra.zip
    }
  }
  advanced {
    auth-provider {
      class = PlainTextAuthProvider
      # 3. User and password
      username = astra 
      password = astra2020
    }
    connection {
      init-query-timeout = 10 seconds
      set-keyspace-timeout = 10 seconds
    }
    control-connection.timeout = 10 seconds
  }
}
```

**✅ Step 3b. Run the demo** : 

You can now run with 

```
mvn exec:java
```

If you are not using Maven all dependencies are in the folder `libs` at root of this repo

You should have the following output

```
Initializing connection to ASTRA
+ Connection Successfully established.
+ Table 'messages' has been created.
+ Messages '072a4170-f21b-11ea-b3b6-6ba79e21f4bd' has been created.
+ Messages '07c744c0-f21b-11ea-b3b6-6ba79e21f4bd' has been created.
+ Reading records from table:
[OK] - End of Demo
```


