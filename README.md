# Intro

Compilation of the process to install the tools to play with containers in windows.

# Instalation

-   Enable Hyper-v 
    
    Start Powershell as Administrator and execute the following command

    
    ```
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
    ```

-   Enable support for wsl:
    1. Check that you have Windows 10, version 1903 or higher or Windows 11.
    2. Enable WSL 2 feature on Windows. For detailed instructions, refer to the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
    3. Download and install the [Linux kernel update package](https://docs.microsoft.com/windows/wsl/wsl2-kernel).

-   Download and install docker
    https://www.docker.com/get-started/

-   Download and install [minikube](https://minikube.sigs.k8s.io/docs/start/)

-   Start Powershell as Administrator and run the following command

    ```
    minikube config set driver hyperv
    ```
    This command config minikube to use hyperv by default on windows

-   On Powershell as Administrator and run the following command

    ```
    minikube kubectl
    ```
    In my case it looked like it installed kubectl binary

-   Enable kubectl code completion
    
    *   [for macOS](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#enable-shell-autocompletion)
    *   [for linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#enable-shell-autocompletion)
    *   [for windows](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#enable-shell-autocompletion)

-   On Powershell as Administrator and run the following command

    ```
    minikube kubectl
    ```
    In my case it looked like it installed kubectl binary

-   Follow the [instructions](https://minikube.sigs.k8s.io/docs/handbook/pushing/#4-pushing-to-an-in-cluster-using-registry-addon) to be able to push images to the container private container registry

-   Download and install [helm](https://helm.sh/docs/intro/quickstart/)

    ***Make sure*** the command is in the system path and that you can execute it from the command line


# Minikube commands

    For the minikube commands you need to have be on Powershell as Administrator

-   Start the cluster
    
    No cluster instance is started by default and one needs to be created.
    This command takes some time to finish, so please be patient.

    After the execution running `minikube kubectl get nodes` should returns the list of running nodes

    ```
    minikube start -n 1 --memory='4gb' --cpus='2' --disk-size='20gb' --addons='ingress,dashboard,metallb,registry,metrics-server' --kubernetes-version='1.24.7'
    ```

    Command explanation:
    ```
    --n 1            : number of nodes to create. To play around 1 is more than enough;
    --memory='4gb'  : each node make use of 4gb of ram. I would recommend a minimum of 2gb and if you spin up more nodes take 
    into account that each one will be using this amount of memory. I recommend at max half of your system memory;
        --cpus='2' : number of cpu per node. Take into account the number of cores that your system has;
    --disk-size='20gb' : Size of each node hard disk. 
    --addons='ingress,dashboard,metallb,registry,metrics-server' : list of addons to enable by default
        -   ingress: ingress-nginx
        -   dashboard: kubernetes dashboard
        -   metallb: load balancer
        -   registry: container registry
        -   metrics-server: service to allow auto-scaling 
    --kubernetes-version='1.24.7' : we don't want to go with the latest for now
    ```

-   Delete the cluster

    ```
    minikube delete
    ```

-   Kubernetes dashboard

    ```
    minikube dashboard
    ```

# kubectl commands

-   Get list of nodes

    ```
    kubectl get nodes
    ```

    or

    ```
    minikube kubectl get nodes
    ```



# Helm commands TODO




# Documentation


*   [Kubernetes](https://kubernetes.io/docs/)
*   [Minikube](https://minikube.sigs.k8s.io/docs/)
*   [Helm](https://helm.sh/docs/)


