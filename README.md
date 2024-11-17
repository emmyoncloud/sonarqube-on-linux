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
- **Operating System**: A Linux distribution with a modern kernel version, preferably Ubuntu or CentOS.  

**Database Requirements**  
- **PostgreSQL**: Install and configure **PostgreSQL version 15 or newer**. PostgreSQL serves as the database backend for SonarQube, storing essential data for analysis and reporting.  

**Java Environment**
- **OpenJDK 21**: Ensure OpenJDK 21 is installed and set as the default Java runtime environment. SonarQube relies on a robust and compatible Java version for its core functionality.  

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
   aws --version
   ```

   ```sh
   aws --version
   ```

   ```sh
   aws --version
   ```









