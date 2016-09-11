# SonarQube and Jenkins integration

## 1. Configure SonarQube to not use SCM Sensor
- #### Log into SonarQUbe UI at http://sonar.kube.wiseweb.co:9000/ using default `admin:admin` credentials
- #### Go to "Administration" -> "Configuration" -> "General Settings", select `SCM` category and switch "Disable the SCM Sensor" to `True` and press `Save SCM Settings`:
![scm_sensor_off](imgs/scm_sensor_off.png)

##### NOTE: Otherwise Jenkins's jobs with SVN usage will fail with "Error when executing blame for file" caused by "SVNAuthenticationException: svn: E170001: Authentication required for ..."  

## 2. Configure Jenkins to use it's SonarQube plugin
- #### Log into Jenkins UI at http://jenkins.kube.wiseweb.co:38080/
- #### Go to "Manage Jenkins" -> "Configure System" and adjust SonarQube settings as below:
![jenkins_sq_server](imgs/jen_sq_server.png)
- #### Add SonarQube scanner installation:
![sq_scanner](imgs/jen_sq_scanner.png)

## 3. Configure job to use SonarQube scanner
- ##### Edit job settings - "Add Build Step" - "Execute SonarQube Scanner" according to:
![jenkins_sq_job](imgs/jen_job.png)
- ##### Save configuration and build the project, log outputs should contain something like:

```

INFO: SonarQube Scanner 2.6.1
INFO: Java 1.7.0_80 Oracle Corporation (64-bit)
INFO: Linux 4.2.0-36-generic amd64
INFO: Error stacktraces are turned on.
INFO: User cache: /home/jenkins/.sonar/cache
INFO: SonarQube server 4.5.7

...
INFO  - Store results in database
INFO  - ANALYSIS SUCCESSFUL, you can browse
...
INFO  - -> Clean BuildSVN [id=1]
INFO  - <- Clean snapshot 202
INFO: EXECUTION SUCCESS
...
Finished: SUCCESS
```
