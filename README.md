
# Installing and Configuring SonarQube on a Linux Server.

**Why SonarQube?** 

**SonarQube** is more than just a code quality tool; it's a partner in building better software. SonarQube helps build a sustainable, resilient codebase while elevating code review to a tool for creating exceptional software. It’s your key to excellence in static code analysis and future-ready development. Here are some features why SonarQube stands out as an essential addition to your development workflow:  
- Elevates Code Quality  
- Enhances Security 
- Supports Multiple Languages
- Seamless CI/CD Integration  
- Customizable and Scalable  
- Promotes Collaboration 
- Open-Source and Enterprise Options  
- Future-Proof Your Projects 


**Minimum System Requirements for Installing and Configuring SonarQube on a Linux Server** 

Setting up SonarQube on a Linux server requires meeting specific system requirements to ensure optimal performance and functionality. Below are the key prerequisites:  

**Server Requirements** 
- **Memory and CPU**: A server with at least **2GB of RAM** and **1 vCPU** is required for a smooth installation and operation.  
- **Operating System**: A Linux distribution with a modern kernel version, preferably CentOS.  

**Database Requirements**  
- **PostgreSQL**: Install and configure **PostgreSQL version 17 or newer**. PostgreSQL serves as the database backend for SonarQube, storing essential data for analysis and reporting.  

**Java Environment**
- **OpenJDK 23**: Ensure OpenJDK 23 is installed and set as the default Java runtime environment. SonarQube relies on a robust and compatible Java version for its core functionality.  

**User and Permissions** 
- **Sonar User**: All SonarQube processes must run under a dedicated non-root user account, typically named `sonar`. This enhances security by isolating SonarQube processes from the root user.  

**Additional Recommendations**  
1. Ensure the server has reliable network connectivity for downloading necessary dependencies and updates.  
2. Regularly update the operating system and installed software to maintain security and compatibility.  
3. Use a firewall or security group rules to restrict access to SonarQube ports, allowing connections only from authorized sources.  

**Step 1: Prepare the Server**

Update the system packages and install necessary utilities:

   ```sh
   sudo yum update -y
   ```

   ```sh
   sudo yum install java-21-openjdk -y
   ```

   ```sh
   sudo yum install wget unzip -y
   ```

Check system parameters:

   ```sh
   sysctl vm.max_map_count
   ```

   ```sh
   sysctl fs.file-max
   ```

   ```sh
   ulimit -n
   ```

   ```sh
   ulimit -u
   ```

**Step 2: Install and Setup PostgreSQL 17**
Install PostgreSQL 17:

   ```sh
    sudo dnf module install postgresql:17/server -y
   ```

Initialize the PostgreSQL database:

   ```sh
    sudo postgresql-setup --initdb
   ```

Start and enable PostgreSQL:

   ```sh
    sudo systemctl enable postgresql.service
   ```

   ```sh
    sudo systemctl start postgresql.service
   ```

Change the default password for the PostgreSQL user:

   ```sh
    sudo passwd postgres
   ```

Create a new database and user for SonarQube:

   ```sh
    sudo su - postgres
   ```

   ```sh
    createuser sonar
   ```

   ```sh
    psql
   ```

   ```sh
    ALTER USER sonar WITH ENCRYPTED password 'sonar';
   ```

   ```sh
    CREATE DATABASE sonarqube OWNER sonar;
   ```

   ```sh
    GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;
   ```

   ```sh
    \q
   ```

   ```sh
    exit
   ```


**Step 3: Download and Install SonarQube**

Download the latest SonarQube binary files:

   ```sh
    cd /opt 
   ```

   ```sh
    sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.7.96285.zip
   ```

Unzip the downloaded file:

   ```sh
    sudo unzip sonarqube-9.9.7.96285.zip
   ```

   ```sh
    sudo mv sonarqube-9.9.7.96285.zip sonarqube
   ```

**Step 4: Configure SonarQube**

Create a group and set ownership:

   ```sh
    sudo useradd sonar
   ```

   ```sh
    sudo chown -R sonar:sonar /opt/sonarqube
   ```

Edit the SonarQube configuration file:

   ```sh
    sudo vi /opt/sonarqube/conf/sonar.properties
   ```

Set the PostgreSQL database username and password:

   ```sh
    sonar.jdbc.username=sonar
   ```

   ```sh
    sonar.jdbc.password=sonar
   ```


**Step 5: Configure Systemd Service**

Create a systemd service file:

   ```sh
    sudo vi /etc/systemd/system/sonar.service
   ```

Add the following content:

   ```sh
    [Unit]

    Description=SonarQube service

    After=syslog.target network.target



    [Service]

    Type=forking

    ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start

    ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop

    User=sonar

    Group=sonar

    Restart=always



    [Install]

    WantedBy=multi-user.target
   ```

Reload systemd and start SonarQube service:

   ```sh
    sudo systemctl daemon-reload
   ```

   ```sh
    sudo systemctl enable --now sonar
   ```

Check service status:

   ```sh
    sudo systemctl status sonar
   ```

**Step 6: Access SonarQube**

Access SonarQube via the browser using the server IP followed by port 9000:

   ```sh
   http://your_server_IP:9000
   ```

Login with the default administrator credentials:

- Username: admin
  
- Password: admin
  
**You've now successfully installed and configured SonarQube on your Linux server!**


# Contributing

Feel free to fork this repository and submit pull requests. Contributions are welcome!

