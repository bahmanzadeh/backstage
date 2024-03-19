helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add backstage https://backstage.github.io/charts


#make sure to have the app-config-extra.yaml available with the key values like this : key=value.... and then run below command to create a config map
kubectl create namespace backstage
kubectl create configmap my-app-config --from-file=app-config.extra.yaml=app-config.extra.yaml
#and then make sure to reference the config map like this to your pods from the 
backstage:
+   extraAppConfig:
+     - filename: app-config.extra.yaml
+       configMapRef: my-app-config
The chart will mount the content of the ConfigMap as a new app-config.extra.yaml file and automatically pass the extra configuration to your instance.



helm install backstage backstage/backstage -f ./my-bs-values.yaml --namespace backstage --create-namespace