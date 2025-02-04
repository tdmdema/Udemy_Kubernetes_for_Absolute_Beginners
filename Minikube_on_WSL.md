# Minikube setup on Ubuntu WSL

## Ubuntu Preparation

1. Install docker desktop from here: <https://www.docker.com//et-started/>

2. Run series of commands to ensure you can interact with Docker without root
   * Third command here is a trick to reload your profile without actually logging out
   * Closing out Ubuntu shell and starting over instead of third command is an option

   ```shell
   sudo groupadd docker
   sudo usermod -aG docker ${USER}
   su -s ${USER}
   ```

3. Test the Docker configuration

   ```shell
   sudo service docker start
   docker run hello-world
   ```

## Minikube Preparation

1. Install Minikube

   ```shell
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
   sudo apt install ./minikube_latest_amd64.deb -y
   rm minikube_latest_amd64.deb
   ```

   This installation in WSL rise some error. Ignore them from the moment.

2. Start it

   ```shell
      minikube start
   ```

3. Get the dashboard going
   * The dashboard will continue to run and does not return back to a prompt here
   * You will need to kill the dashboard to continue in the guide

   ```shell
   minikube dashboard
   ```

4. Open the dashboard in your favorite browser (in Windows)
   * Port is dynamic, so can't document it well - you'll just have to be good at reading directions
   * The port will be in output of step 3 command
   * Should look something like this...

   ```shell
   http://127.0.0.1:[PORT GOES HERE]/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default
   ```

5. This process is going to block you from the finishing this guide, but to keep it running, do the following...
   * Perform "CTRL+Z" on the keyboard to send the process into paused state
   * Execute the following command to resume the paused process in the background

   ```shell
   bg
   ```

## Kubectl Preparation

1. Install Kubectl
   * Adds k8s key, adds k8s repo, installs the new hotness

   ```shell
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
   rm kubectl
   ```

2. Test it

   ```shell
   kubectl version --client
   ```

## Helm Preparation

1. Install Helm

   ```shell
   curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
   chmod 700 get_helm.sh
   ./get_helm.sh
   rm get_helm.sh
   ```

2. Use it

   ```shell
   helm version
   ```
