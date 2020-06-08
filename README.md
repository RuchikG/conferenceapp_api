# conferenceapp_api
This is a Java and Spring based conference app that maintains data for a conference.

How to install the app:

1. Clone the repository to a location you like.
2. Install Docker Desktop, Postman, and PgAdmin for you device.
3. Once you have those things installed and ready to use, open terminal/cmd prompt and cd into the project directory.
4. In your terminal/cmd prompt run: docker run --name postgres-docker -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
   
   This will start a docker container called postgres-docker on internal port 5432 with a database called postgres.
   
   Once you have done that now let's test if your container and database is working.

5. In your terminal/cmd prompt run docker start postgres-docker
   
   This will start the docker and allow it to serve our database. In the docker desktop you should see your docker running.
   
   Now let's test to see if your database was created.

6. Open your PgAdmin and setup/login with your master password.
7. Right click on the Servers, go to create and then go to server...
8. Name the server whatever you would like to call it.
9. Now go the connections tab.
10. Under this tab the field:values should be:
   
   hostname/address: localhost
   
   Maintenance database: postgres
   
   Username: postgres
   
   Password: postgres

11. Now hit save and you should see a server under the servers test that you just created.

12. Click on the server and check to see if you can see your database that you just created.
   
   Now let's setup the tables and install the data.

13. Now go back to your terminal/cmd prompt and run the following commands:
   
   docker cp create_tables.sql postgres-demo:/create_tables.sql
   
   docker exec -it postgres-demo psql -d postgres -f create_tables.sql -U postgres
   
   These commands will create the necessary tables based on the schema I have provided. 
   
   Once these commands are completed you should be able to see table created.

14. Once you can see that run the following commands:
    
    docker cp insert_data.sql postgres-demo:/insert_data.sql
    
    docker exec -it postgres-demo psql -d conference_app -f insert_data.sql -U postgres
    
    These commands will insert the necessary data that I have provided.
    
    ------------------------------------ This should test the installation of the app -----------------------------
15. To test the app run the app on localhost:8080 in IntelliJ.
16. Make a GET request to https://localhost:8080/api/v1/speakers to see the data as a JSON object.
