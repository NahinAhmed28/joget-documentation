# Deployment of Joget in minikube alongside GovStack USCT-DIY

## Install minikube and tools

Please follow the official instructions on how to:

- Run [minikube](https://minikube.sigs.k8s.io/docs/start/)
- Install [kubectl](https://kubernetes.io/docs/reference/kubectl/)
- Install [helm](https://helm.sh/)
- Optionally install [k9s](https://k9scli.io/)

## Deployment of USCT DIY

To install USCT DIY you can follow [documentation](https://github.com/GovStackWorkingGroup/sandbox-usecase-usct-backend/blob/main/docs/diy.md)

## Deployment of Joget in k8s

Optionally you can choose which version of Joget to install (we are using DX8), but here we will present both DX7 & DX8 installations in k8s

1. DX7 [Source Documentation](https://dev.joget.org/community/display/DX7/Joget+on+Kubernetes#JogetonKubernetes-DeployMySQLonKubernetes)

   * Deploy MYSQL DB for Joget

        * create persistent volume (data will not be lost on restart)
        ```
        kubectl apply -f ./assets/src/joget/mysql-pv.yaml
        ```
        * deploy mysql
        ```
        kubectl apply -f ./assets/src/joget/mysql-deployment_5.6.yaml
        ```
        * inspect
        ```
        kubectl describe deployment mysql
        ```
        ```
		kubectl get pods -l app=mysql
        ```
        ```
		kubectl describe pvc mysql-pv-claim
        ```
    * Deploy Joget on Kubernetes

        * deploy joget
        ```
        kubectl apply -f ./assets/src/joget/joget-dx7-tomcat9-deployment.yaml
        ```
        * inspect
        ```
        kubectl describe deployment joget-dx7-tomcat9
		kubectl get pods -l app=joget-dx7-tomcat9
        ```
        * get url to access Joget
        ```
        minikube service joget-dx7-tomcat9 --url
        ```
        Then follow the url

        * Setup database configuration
            * Database Type: MySQL
		    * Database Host: the service name of the database e.g. mysql
		    * Database Port: 3306
		    * Database Name: jwdb
		    * Database User: root
		    * Database Password: the configured password e.g. password
        * Default credentials
            * u: admin
            * p: admin

2. DX8 [Source Documentation](https://dev.joget.org/community/display/DX8/Joget+on+Kubernetes)

   * Deploy MYSQL DB for Joget

        * create persistent volume (data will not be lost on restart)
        ```
        kubectl apply -f ./assets/src/joget/mysql-pv.yaml
        ```
        * deploy mysql
        ```
        kubectl apply -f ./assets/src/joget/mysql-deployment_5.7.yaml
        ```
        * inspect
        ```
        kubectl describe deployment mysql
        ```
        ```
		kubectl get pods -l app=mysql
        ```
        ```
		kubectl describe pvc mysql-pv-claim
        ```
    * Deploy Joget on Kubernetes

        * deploy joget
        ```
        kubectl apply -f ./assets/src/joget/joget-dx8-tomcat9-deployment.yaml
        ```
        * inspect
        ```
        kubectl describe deployment joget-dx8-tomcat9
		kubectl get pods -l app=joget-dx8-tomcat9
        ```
        * get url to access Joget
        ```
        minikube service joget-dx8-tomcat9 --url
        ```
        Then follow the url

        * Setup database configuration
            * Database Type: MySQL
		    * Database Host: the service name of the database e.g. mysql
		    * Database Port: 3306
		    * Database Name: jwdb
		    * Database User: root
		    * Database Password: the configured password e.g. password
        * Default credentials
            * u: admin
            * p: admin

 ## Install container registry in minikube to be able to deploy custom images like Building Block emulators, adapters and more ([Documentation](https://minikube.sigs.k8s.io/docs/handbook/registry/))

1. Start registry
```
minikube addons enable registry
```

2. For macOS: Redirect the push to the minikube registry (still localhost:5000) - terminal should stay open! (For other OS please follow the [Documentation](https://minikube.sigs.k8s.io/docs/handbook/registry/))
```
docker run --rm -it --network=host alpine ash -c "apk add socat && socat TCP-LISTEN:5000,reuseaddr,fork TCP:$(minikube ip):5000"
```

3. When you have installed registry you can deploy your own images in that registry.

    For example if you are following the strategy that GovStack use for emulators:

    3.1. Run the following command based on the Spring Boot project that implements BB spec:

    ```
    ./gradlew bootBuildImage
    ```

    3.2. Re - tag the image :

    ```
    docker image tag <image_name_from _local_docker_registry> localhost:5000/xxxx:version
    ``` 

    3.3. Push image

    ```
    docker push localhost:5000/xxxx:version
    ```

    3.4. After that in deployments or so you can reference that image as "localhost:5000/xxxx:version"

    * example deployment using the local registry image [simple deployment](./../assets/src/minikube/deployment.yaml)

    3.5. After that you can follow the "DIY" way of registering Building Block in Security Server and then to access it directly or through Information Mediator Security Server





