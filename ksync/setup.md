1. Start the cluster via. minikube

`minikube start`{{execute}}

1. Install ksync. This will fetch the binary and put it at `/usr/local/bin`.

    ```bash
    curl https://vapor-ware.github.io/gimme-that/gimme.sh | bash
    ```

1. Initialize ksync and install the server component on your cluster. The server component is a DaemonSet that provides access to each node's filesystem. This will also go through a set of pre and postflight checks to verify that everything is working correctly. You can run these yourself by using `ksync doctor`.

    ```bash
    ksync init
    ```

1. Startup the local client. It watches your local config to start new jobs and the kubernetes API to react when things change. This will just put it into the background. Feel free to run in a separate terminal or add as a service to your host.

    ```bash
    ksync watch --daemon
    ```

1. Add the [demo app][demo-app] to your cluster. This is a simple python app made with flask. Because ksync moves files around, it would work for any kind of data you'd like to move between your local system and the cluster.

    ```bash
    kubectl apply -f https://vapor-ware.github.io/ksync/example/app/app.yaml
    ```

1. Make sure that the app is ready and running.

    ```bash
    kubectl get po --selector=app=app
    ```
