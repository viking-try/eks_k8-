After:

Download Postman client

    https://www.postman.com/downloads/

Import Project to Postman

    Import the postman project AWS-EKS.postman_collection.json present in folder.

Create Environment in postman

    Go to Settings -> Click on Add
    Environment Name: UMS-NodePort
        Variable: url
        Initial Value: http://WorkerNode-Public-IP:30881
        Current Value: http://WorkerNode-Public-IP:30881
        Click on Add

Test User Management Services

    Select the environment before calling any API
    Health Status API
        URL: {{url}}/usermgmt/health-status
    Create User Service
        URL: {{url}}/usermgmt/user
        url variable will replaced from environment we selected

    {
        "username": "admin1",
        "email": "dkalyanreddy@gmail.com",
        "role": "ROLE_ADMIN",
        "enabled": true,
        "firstname": "fname1",
        "lastname": "lname1",
        "password": "Pass@123"
    }

    List User Service
        URL: {{url}}/usermgmt/users

    Update User Service
        URL: {{url}}/usermgmt/user

    {
        "username": "admin1",
        "email": "dkalyanreddy@gmail.com",
        "role": "ROLE_ADMIN",
        "enabled": true,
        "firstname": "fname2",
        "lastname": "lname2",
        "password": "Pass@123"
    }

    Delete User Service
        URL: {{url}}/usermgmt/user/admin1

Step-05: Verify Users in MySQL Database

# Connect to MYSQL Database
kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h user-mgmt-mysql-back-service -ppasswd1234

# Verify usermgmt schema got created which we provided in ConfigMap
mysql> show schemas;
mysql> use usermgmt;
mysql> show tables;
mysql> select * from users;
