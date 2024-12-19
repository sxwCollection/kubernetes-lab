# what

if you want to develop cloud applications,  
you will need some playground to test your ideas.  
Kind (Kubernetes in docker) is a good choice.  
With kind you can easyly create or delete kubernetes clusters.  
In this demo, 3 parts are shown.

1. install kind
2. install ingress (nginx)
3. config/deploy a demo app

# how
## install kind

1. curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.26.0/kind-linux-amd64
1. sudo chmod +x ./kind
1. sudo mv ./kind /usr/local/bin/kind  
   see:  
   https://kind.sigs.k8s.io/docs/user/quick-start/#installation


## install ingress
1. create cluster, with
kind create cluster --name cluster-ingress --config kind-config.yaml
2. install nginx ingress controller,  
kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/deploy-ingress-nginx.yaml
3. check ingress installation  
```
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
```
## install app
1. use ingress
kubectl -f gohttpbin.yaml apply
1. check ingress
curl localhost/httpbin

## config ingress
you can config ingress like this format   
```

spec:
  rules:
    - http:
        paths:
          - pathType: xxx
            path: /httpbin
            backend:
              service:
                name: httpbin
                port:
                  number: 8080
```
there are 3 types of pathType,  
1. Exact: will forward as definition, like /a will be forwarded to service  
2. Prefix: all requests with that match the Prefix will be forwarded, Prefix is forwarded as well   
3. ImplementationSpecific: you can use regex in this a implement some logics  
in this demo, I want to all requests with Prefix httpbin are forwarded to service, but Prefix "httpbin" should not be forwarded,
which means use ImplementationSpecific with regex  