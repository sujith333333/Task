# Step 1: Create an RDS Aurora MySQL 5.7 Instance
1. Log in to AWS Management Console:
    * Navigate to the RDS service.
    * Click on "Create database".
    * Select "Amazon Aurora" as the engine type.
    * Choose "MySQL 5.7" as the version.
    * Configure your instance settings (instance size, storage, etc.).
    ![preview](./Screenshot%202024-07-04%20104814.png)
    ![preview](./Screenshot%202024-07-04%20104924.png)
    ![preview](./Screenshot%202024-07-04%20105017.png)
    ![preview](./Screenshot%202024-07-04%20105138.png)
    ![preview](./Screenshot%202024-07-04%20105353.png)
    ![preview](./Screenshot%202024-07-04%20105353.png)
    ![preview](./Screenshot%202024-07-04%20105515.png)
    ![preview](./Screenshot%202024-07-04%20105544.png)
    ![preview](./Screenshot%202024-07-04%20105706.png)
2. Connect to RDS using MySQL Workbench:
    *  Open MySQL Workbench.
    *  Create a new connection with the endpoint provided by AWS.
    *  Enter your username and password.
    *  Test the connection to ensure it works
    ![preview](./Screenshot%202024-07-04%20105731.png)

## Step 2: Apply Dummy Data to MySQL 8.0.35

* Connect to the Database:
* Use the MySQL Workbench connection created earlier.
* Create Dummy Data:
* Use the following SQL script to create a dummy table and insert data
 
 ```
 CREATE DATABASE testdb;
USE testdb;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

INSERT INTO users (name, email) VALUES ('John Doe', 'john.doe@example.com'), ('Jane Smith', 'jane.smith@example.com');

 ```
 ![preview](./Screenshot%202024-07-04%20105832.png)

 ## Step 3: Take a Snapshot of the Database
 1.Create Snapshot:
* In the RDS console, select your Aurora MySQL 5.7 cluster.
* Click on "Actions" and select "Take snapshot".
* Give your snapshot a name and confirm the creation.
![preview](./Screenshot%202024-07-04%20105920.png)

## Step 4: Create Cluster and DB Parameter Groups for Aurora MySQL 8.0.35

1.Create Parameter Groups:
* Go to the RDS console and select "Parameter groups".
* Click on "Create parameter group".
* For the parameter group family, select "aurora-mysql8.0".
* Create both a cluster parameter group and a DB parameter group.
![preview](./Screenshot%202024-07-04%20105938.png)
![preview](./Screenshot%202024-07-04%20110002.png)

## Step 5: Restore the Database with MySQL 8.0.35

1.Restore Snapshot:

* Go to the "Snapshots" section in the RDS console.
* Select the snapshot you created earlier.
* Click on "Actions" and select "Restore snapshot".
* Choose "Amazon Aurora MySQL-Compatible Edition" and select version "8.0.32".
* When configuring the restore settings, select the newly created cluster parameter group and DB parameter group.

2. Monitor the Restore Process:
    * Wait for the restoration process to complete.
    * Check the status in the RDS console.
![preview](./Screenshot%202024-07-04%20110031.png)

## Step 6: Check the Status and Troubleshoot

1.Check Version:
* After the restoration is complete, connect to the new instance using MySQL Workbench.
* Run the following command to check the version
```
SELECT version();
```
![preview](./Screenshot%202024-07-04%20110051.png)
![preview](./Screenshot%202024-07-04%20110110.png)

# task completed


