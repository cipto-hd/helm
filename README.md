# Declaratively Manage Kubernetes manifests using `helmfile`

Kubernetes cluster is from minikube.

The docker image is pulled from minikube local image and minikube builtin-registry.

Important notes on using builtin minikube registry:

- initially I pushed image to the builtin minikube registry using image format `$(minikube ip):5000/microbot:v1` and then pull it using the same image format via deployment manifest. When deployment was applied, I got `ImagePullBackOff`/`ErrImagePull` error.
- after some googling, I used kubectl port-forward to map my local workstation to the minikube vm:
  ```terminal
  kubectl port-forward --namespace kube-system service/registry 5000:80
  ```
  and then I change the image format into `localhost:5000/microbot:v1`, finally deployment successfuly applied.

Actually I can pull image from docker hub, but I would like to save my internet quota by using docker local image.
