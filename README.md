# Tutorial: Installing SQL Server on Docker

In this tutorial, we'll guide you through the steps to install Microsoft SQL Server on Docker using the official SQL Server Docker image. Docker allows you to run applications in containers, providing an isolated and consistent environment across different platforms. SQL Server is a robust relational database management system developed by Microsoft, and running it in a Docker container offers flexibility and portability.

## Prerequisites:

- Docker installed on your machine. You can download and install Docker from [here](https://docs.docker.com/get-docker/).

## Step 1: Pull the SQL Server Docker Image

Open a terminal or command prompt and run the following command to download the SQL Server Docker image from the official Docker Hub repository:

```bash
docker pull mcr.microsoft.com/mssql/server
```

## Step 2: Run the SQL Server Container

Now, let's run the SQL Server container with the necessary configurations. Replace `YourStrongPassword` with a strong and secure password for the SQL Server `SA` (System Administrator) account.

```bash
docker run --name sqlserver -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=supersecret1' -p 1433:1433 -e 'MSSQL_PID=Express' --restart unless-stopped -d mcr.microsoft.com/mssql/server
```

Explanation of the command arguments:
- `docker run`: This is the basic command to run a Docker container.
- `--name sqlserver`: Specifies the name of the Docker container as "sqlserver." You can replace "sqlserver" with a different name if you prefer.
- `-e 'ACCEPT_EULA=Y'`: Sets the environment variable `ACCEPT_EULA` to "Y," indicating that you accept the End-User License Agreement (EULA) for SQL Server. This is a requirement when running the SQL Server Docker image.
- `-e 'SA_PASSWORD=YourStrongPassword'`: Sets the environment variable `SA_PASSWORD` to "YourStrongPassword." This is the password for the `SA` (System Administrator) account in SQL Server. You should replace "YourStrongPassword" with a strong and secure password of your choice.
- `-p 1433:1433`: Maps port 1433 of the container to port 1433 on the host machine. Port 1433 is the default port used by SQL Server for database connections. This mapping allows you to connect to SQL Server on the host machine using port 1433.
- `--restart unless-stopped`: Configures the container to automatically restart unless it is explicitly stopped by the user or during system reboot. This ensures that the SQL Server container continues running even after system reboots.
- `-d`: Runs the container in detached mode, which means it runs in the background, and the terminal is not attached to its console.
- `mcr.microsoft.com/mssql/server`: Specifies the Docker image to use for running the SQL Server container. This is the official Microsoft SQL Server Docker image available on Docker Hub.
- `-e 'MSSQL_PID=Express'`: Sets the `MSSQL_PID` environment variable to "Express," which configures SQL Server to use the Express edition. This edition allows both Windows and SQL Server authentication by default.

## Step 3: Verify SQL Server Installation

To verify that SQL Server is running inside the Docker container, use the following command to see the running containers:

```bash
docker ps
```

You should see an output similar to this, indicating that the SQL Server container is running:

```
CONTAINER ID   IMAGE                                COMMAND                  CREATED          STATUS          PORTS                    NAMES
xxxxxxxxxxxx   mcr.microsoft.com/mssql/server   "/opt/mssql/bin/sqls…"   x seconds ago   Up x seconds    0.0.0.0:1433->1433/tcp   sqlserver
```

## Step 4: Connect to SQL Server

To connect to the SQL Server database from your host machine or any other client, you can use your favorite SQL Server client and connect to `localhost` on port `1433`, using the `SA` username and the password you specified during the container setup.

For example, if you have SQL Server Management Studio (SSMS) installed, you can connect to the SQL Server container by specifying the server name as `localhost,1433` and using the `SA` username and your password.

## Step 5: Stopping and Restarting the SQL Server Container

To stop the SQL Server container, use the following command:

```bash
docker stop sqlserver
```

To start the stopped container, use:

```bash
docker start sqlserver
```

Remember, the container will not automatically restart when your system reboots, so you need to start it manually.

## Step 6: Removing the SQL Server Container

If you want to remove the SQL Server container entirely, run the following command:

```bash
docker rm -f sqlserver
```

## Step 7: Connect to SQL Server Using DBeaver

[DBeaver](https://dbeaver.io/) is a free and open-source universal database tool that supports various database management systems, including Microsoft SQL Server. Follow these steps to connect to your SQL Server container using DBeaver:

1. **Install DBeaver**: If you haven't already, download and install DBeaver from the [official website](https://dbeaver.io/download/).

2. **Launch DBeaver**: Open DBeaver after installation.

3. **Create a New Database Connection**:

   - Click on "Database" in the top menu.
   - Select "New Database Connection."
   - In the "Select Database Driver" dialog, choose "Microsoft SQL Server" and click "Next."

4. **Configure the Connection**:

   - In the "Database Connection" settings, provide the following details:

     - **Host**: `localhost`
     - **Port**: `1433`
     - **Database**: Leave this field blank.
     - **Username**: `SA`
     - **Password**: The password you set during the SQL Server container setup.

   - Click "Test Connection" to verify that DBeaver can connect to your SQL Server container successfully.

5. **Save the Connection**:

   - Click "Finish" to save the connection configuration.

6. **Connect to SQL Server**:

   - In the main DBeaver window, you should see your newly created connection listed under the "Database Navigator" on the left-hand side.
   - Double-click on the connection to connect to your SQL Server container.

7. **Explore and Manage Your SQL Server Database**:

   - You can now use DBeaver to explore, query, and manage your SQL Server database just like you would with any other SQL Server instance.

DBeaver provides a user-friendly interface for interacting with SQL Server, allowing you to run SQL queries, manage databases, and perform various database-related tasks.

With these steps, you can easily connect to your SQL Server Docker container using DBeaver and start working with your database.

## Conclusion

Congratulations! You have successfully installed Microsoft SQL Server on Docker using the official SQL Server Docker image. Docker containers allow you to easily deploy SQL Server and other applications, ensuring consistency and portability across different environments.

---

