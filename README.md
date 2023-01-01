# How to Use

## Build back-end:1.0 docker image

```
git clone https://github.com/AllisonHu64/restful-api-practice.git
cd restful-api-practice
docker build -t back-end:1.0 .
```

## Build front-end:1.0 docker image 

```
git clone https://github.com/AllisonHu64/react-practice.git
```

Create `.env.production` file in `/react-practice` directory.
Copy the following content in the `.env.production` file.

See https://kubernetes.io/zh-cn/docs/concepts/services-networking/dns-pod-service/#service for details about how Kubernetes assign DNS names to services.
```
REACT_APP_BACKEND_DOMAIN=back-end-service.default.svc.cluster.local
REACT_APP_BACKEND_PORT=5000
```

Go to `/react-practice` directory and run the following commands.
```
yarn deploy:prod -v 1.0
```

## Use Kubernetes to deploy pods

Change the `MONGO_DOMAIN` in `./back-end/back-end-deploy.yaml` according to your need.
See https://kubernetes.io/zh-cn/docs/concepts/services-networking/dns-pod-service/#service for details about how Kubernetes assign DNS names to services.

Please remember to create a docker volume `mongo-db-vol` with `docker volume create mongo-db-vol`.
```
kubectl apply -f ./database/mongo-deploy.yaml
kubectl apply -f ./database/mongo-service.yaml

kubectl apply -f ./back-end/back-end-deploy.yaml
kubectl apply -f ./back-end/back-end-service.yaml

kubectl apply -f ./ui/ui-deploy.yaml
kubectl apply -f ./ui/ui-service.yaml
```
