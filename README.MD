

### Build kubernetes
IF use minikube driver=docker  run command for windows:

`@FOR /f "tokens=*" %i IN ('minikube -p minikube docker-env') DO @%i`
##### build currency-cbr-adapter and create docker image
1) ./gradlew clean buildDependents
2) docker build . -t  anenahov/currency-cbr-adapter:1.0.0
##### build currency-api and create docker image
1) ./gradlew clean build
2) docker build . -t  anenahov/currency-api:1.0.0
##### Change configMaps and Secrets 
* in postgres and active mq folder
##### set env current-dir `set script_dir=%CD%`
##### Apply configs for kubernetes (Deployment and Services)
1) run kubernates/postgres/postgres.bat
2) run kubernates/active-mq/active-mq.bat
3) run kubernates/currency-cbr-adapter/app-deploy.bat
4) run kubernates/currency-api/app-deploy.bat
##### Create Ingres
* run kubernates/ingres/ingres.bat
##### if need local test minikube set host file:
1) get ip minikube node `minikube ip`
2) add to host file row : <minikube_ip> currency-api.com