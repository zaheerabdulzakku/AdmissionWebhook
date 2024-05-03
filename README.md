# AdmissionWebhook

Step 1:

Go to the dev folder and run the command ./gen-certs.sh
Make sure you give execute permission.

Output: Cabundle will be shown in the terminal. copy it and store it.
secret manifest file will be automatically created in dev/manifests/webhook/webhook.tls.secret.yaml

Step 2:

Create a Docker image using a Docker file

use command *docker build -t <image tag> .*
and then push the docker image to the docker hub

Step 3:

Update the below files 
dev/manifests/cluster-config/mutating.config.yaml
dev/manifests/cluster-config/validating.config.yaml
with the latest CaBundle you copied

Step 4:

go to dev/manifests/webhook/webhook.deploy.yaml and update the image with the one you have in your docker hub

Step 5:

Go to dev/manifests/webhook 
and run *kubectl apply -f .*

then, go to dev/manifests/cluster-config
and run *kubectl apply -f .*

Now you can validate the pods and webhooks 
using commands
*kubectl get MutatingWebhookConfiguration*
*kubectl get ValidatingWebhookConfiguration*
*kubectl get all*

you should be seeing webhooks, pods, services and tls secrets.

Step 6:

Now, you can test the webhook using manifest files places in below folded 

dev/manifests/pods
bad-name.pod.yaml -> the pod will not be created due to validation webhook (Naming convention is not as expected)
lifespan-seven.pod.yaml -> Pod will get created with toleration with the help of  mutating webhook
lifespan-three.pod.yaml -> Pod will get created with toleration with the help of  mutating webhook
no-lifespan-label.deploy.yaml -> Pod will get created with toleration with the help of  mutating webhook
no-lifespan-label.pod.yaml -> Pod will get created with toleration with the help of  mutating webhook



![image](https://github.com/zaheerabdulzakku/AdmissionWebhook/assets/36044771/fb9ccb69-517f-404b-9116-b1aaa32ba1a6)


![image](https://github.com/zaheerabdulzakku/AdmissionWebhook/assets/36044771/d7dee4d3-6e8d-44a4-a165-ea65023be4da)


Happy Learning 
