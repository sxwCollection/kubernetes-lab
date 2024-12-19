# what

if you want to develop cloud applications,  
you will need some playground to test your ideas.  
Kind (Kubernetes in docker) is a good choice.  
With kind you can easyly create or delete kubernetes clusters.  
In this demo, 3 parts are shown.

1. install kind
2. install ingress (nginx)
3. config/deploy a demo app

# install kind

1. curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.26.0/kind-linux-amd64
1. sudo chmod +x ./kind
1. sudo mv ./kind /usr/local/bin/kind  
   see:  
   https://kind.sigs.k8s.io/docs/user/quick-start/#installation

