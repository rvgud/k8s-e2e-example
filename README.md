# k8s-e2e-example


Assuption:- To install kubernetes on GCP instances and deploy service on top it there should be ingress and egress firewalls allowed for required ports.
## Install Kubernetes on GCP instances using kubespray
    1. cd kubespray

    2. # Install dependencies from ``requirements.txt`
        pip install -r requirements.txt

    3. Add internal and external IP address of GCP instances into inventory file at inventory/k8s-cluster1/hosts.ini

    4. Specify the master,worker,etcd nodes at:-  ./inventory/k8s-cluster1/hosts.ini

    5. # Deploy Kubespray with Ansible Playbook
        ansible-playbook -i inventory/k8s-cluster1/hosts.ini cluster.yml

## Get Kube config file into host machine

    To run kubectl command on the host machine you will need the kube context on system. Copy the config file at /root/.kube/.

## Install helm client and tiller server

    1. Run below shell script to install helm client:-
       /helm/install.sh
    2. Create service account tiller:-
       kubectl create -f /helm/serviceAccount.yaml
    3. Create tiller:-
       helm init --service-account=tiller

## Install FluentD using helm

    1. Specify hostname,port,username & password of elastic search cluster in /helm/fluentd/values.yaml
    
    2. Install fluentd:-
    helm install /helm-fluentd/ --name fluentd -f /helm-fluentd/values.yaml

## Install monitoring tools :- Prometheus , Grafana , Alertmanger using prometheus-operator

    1.Create Namespace
        kubectl create -f /monitoring/namespace/

    2.Create crd's
        kubectl create -f /monitoring/crds/

    3.Install Components
        kubectl create -f /monitoring/

## Install GuestBook application with canary version

    1. Deploy Artifects:-
       kubectl create -f /guestbook/all-in-one/guestbook-all-in-one.yaml

    2. Deploy Istio virtualservice and destinationrule:-
       kubectl create -f /guestbook/istio/
       
    3. Deploy Canary Artifects:-
       kubectl create -f /guestbook/canary/