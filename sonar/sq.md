# Run SonarQube in Kubernetes

## 1. Kubernetes ReplicationController and service for SonarQube

#### 1.1 Create Kubernetes ReplicationController for SonarQube container using [sq-rc.yaml](/kube/sq-rc.yaml):
```bash
kubectl create -f kube/sq-rc.yaml
```
#### 1.2 Create Kubernetes service for SonarQube using [sq-svc.yaml](/kube/sq-svc.yaml):

```bash
kubectl create -f kube/sq-svc.yaml
```
NOTE: Notice the first of the dynamically assigned ports - you'll be using it while connecting to the service.

##### 1.3 Check SonarQube status:
Get SonarQube pod name:
```bash
kubectl get pods
```
Check SonarQube status:
```bash
kubectl logs <sonar pod name>
```

### 2. Customize SonarQube settings
#### 2.1 Login to Jenkins UI
Open web browser and go to any node by port noticed at the stage 1.2.

http://san1.kube.wiseweb.co:\<dynamic_port\>

Using default user and password - `admin`

#### 2.2 Upgrade SonarQube Plugins (optional)

- Go to "Settings" -> "Plugin Manager" -> "Update Center" -> "Plugin Updates";
- Select plugins you want to update and complete updating;
- SonarQube needs to be restarted after plugin update, enter sonar pod:
```bash
kubectl exec -it <sonar pod name> bash
```
 - and execute:
```bash
service sonar restart
exit
```
NOTE: LDAP plugin cannot be updated at SonarQube 4.5.7 LTS

#### 2.3 Install SonarQube Plugins (optional)

- Go to "Settings" -> "Plugin Manager" -> "Update Center" -> "Available Plugins";
- Select desired plugins and install them;
- SonarQube needs to be restarted after plugin install as well.

NOTE: Restarting SonarQube in WEB UI doesn't re-read the sonar.properties file, so use `service sonar restart` if you need use fresh config.
