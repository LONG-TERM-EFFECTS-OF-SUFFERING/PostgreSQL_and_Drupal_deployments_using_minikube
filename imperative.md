# Imperative deployment

1. PostgreSQL deployment creation.

    ```BASH
    kubectl create deployment postgresql --image=postgres:14
    ```

2. Setting environment variables of the PostgreSQL deployment.

    ```BASH
    kubectl set env deployment/postgresql POSTGRES_USER=user POSTGRES_PASSWORD=password POSTGRES_DB=drupaldb
    ```

3. PostgreSQL deployment service creation.

    ```BASH
    kubectl expose deployment postgresql --port=5432 --name=postgresql-service --type=ClusterIP
    ```

4. Drupal deployment creation.

    ```BASH
    kubectl create deployment drupal --image=drupal:9
    ```

5. Setting environment variables of the Drupal deployment.

    ```BASH
    kubectl set env deployment/drupal DB_HOST=postgresql-service DB_USER=user DB_PASSWORD=password DB_NAME=drupaldb
    ```

6. Drupal deployment service creation.

    ```BASH
    kubectl expose deployment drupal --port=80 --name=drupal-service --type=NodePort
    ```

7. Expose the machine service.

    ```BASH
    minikube service drupal-service
    ```
