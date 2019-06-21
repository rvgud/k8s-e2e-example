1. This prometheus -Grafana - Alert Manager setup is customzied version of kube-prometheus Release:0.26.0..

2. kube-promotheus can be found at :- https://github.com/coreos/prometheus-operator/tree/master/contrib/kube-prometheus

2. Customizations:-


           1.Specify Reverse Proxy URl for Prometheus:-

                File Name:- prometheus-prometheus.yaml
                Description:- Specify externalUrl property.
     
           2.Specify Reverse Proxy URl for Grafana:-

                File Name:- grafana-deployment.yaml
                Description:- Expose Root URl using env variable.

           3.Specify pvc provisioning details:-

                File Name:- prometheus-prometheus.yaml
                Description:- provision volumeclaimtemplate for heketi storage class.

           4.Specify pvc provisioning details for grafana:-

                File Name:- grafana-deployment.yaml
                Description:- create a pvc and provision it.

           5.Specify pvc provisioning details for alertmanager:-

                File Name:- alertmanager-alertmanager.yaml
                Description:- provison volumeclaimtemplate for heketi storage class.
           
           6.Add new grafana dashboards in grafana-dashboardDefinitions.yaml and grafana-deployment.yaml

           7.Modify ClusterRole in prometheus-clusterRole.yaml

4. Installation

           1.Install Namespace
               kubectl create -f namespace/

           2.Install crd's
               kubectl create -f crds/

           3.Install Components
               kubectl create -f ./