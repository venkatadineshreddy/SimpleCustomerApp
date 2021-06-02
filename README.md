
## SonarQube Integration with Jenkins

Integration SonarQube server with Jenkins is necessary to store your reports. Follow below steps to enable that.
### Follow this in **[YouTube](https://www.youtube.com/watch?v=k-3krTRuAFA)**

### Prerequisites
1. SonarQube Server **[Get Help here](https://www.youtube.com/watch?v=zRQrcAi9UdU)**
1. Jenkins Server  **[Get Help here](https://www.youtube.com/watch?v=M32O4Yv0ANc)**

### Implementation

Login to Jenkins server and install sonarqube scanner. 

- SonarQube scanner URL : https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner
- Package : https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.2.0.1227-linux.zip
- 
```sh 
# wget https://repo-maven-apache-org.azurefd.net/maven2/org/sonarsource/scanner/cli/sonar-scanner-cli/3.2.0.1227/
# unzip sonar-scanner-cli-3.2.0.1227-linux.zip
# mv sonar-scanner-3.2.0.1227-linux /var/jenkins_home/sonar_scanner 
```

Set SonarQube server details in sonar-scanner property file 

 - Sonar properties file: /var/jenkins_home/sonar_scanner/conf/sonar-scanner.properties
   - sonar.host.url=http://`<SONAR_SERVER_IP>`:9000

Login to Jenkins GUI console and install " SonarQube scanner" plugin

 - `Manage Jenkins` > `Manage Plugins` > `Avalable` > `SonarQube scanner` 

Configure SonarQube scanner home path

- `Manage Jenkins` > `Global Tool Configuration` > `SonarQube Scanner` 
   - Name  : `sonar_scanner`
   - SONAR_RUNNER_HOME : `/var/jenkins_home/sonar_scanner`

Configure SonarQube server name and authentication token 
- `Manage Jenkins` > `Configure Systems` > `SonarQube Servers`
    - Name : `SonarQube`
	- ServerURL : `http://<Sonarqube_server>:9000/`
	- Server `authentication token`
To Get Authentication code follow below steps.
	Login to SonarQube server as a admin  `My Account` > `Security` > `Generate Token`

Create a job to test SonarQube. Provide below sonar properties details in the job under build 
- Build:
  - `Execute SonarQube Scanner` > `Analysis properties`  (it is mandatary).  
     - sonar.projectKey=`Valaxy`
     - sonar.projectName=`ValaxyDemo`
     - sonar.projectVersion=`1.0`
     - sonar.sources=`/var/lib/jenkins/workspace/$JOB_NAME/SimpleCustomerApp/src`
     - sonar.java.binaries=**/build/classes

Execute job to get analysis report. 
