# Simple Web Application with Kubernetes

This project demonstrates a simple web application deployed with Kubernetes.

## Project Structure

The project is organized as follows:

- `base/`: Contains the base Kubernetes manifests, including a Deployment and a Service. These manifests define the core application components.
- `stages/`: Contains environment-specific configurations for different deployment stages such as production (`prod`), testing (`test`), and user acceptance testing (`uat`).
- `stages/<environment>/configmap.yaml`: Each environment directory within `stages/` includes a `configmap.yaml` file. This ConfigMap defines the HTML content (`index.html`) specific to that environment.

## How the Application Works

The application utilizes nginx to serve a static HTML page. The key aspects of its operation are:

- **nginx Web Server**: nginx is used as the web server to handle incoming HTTP requests and serve the static HTML content.
- **HTML Content via ConfigMap**: The actual HTML content for the web page is injected into the nginx container using a Kubernetes ConfigMap. This allows for easy customization of the content without rebuilding the container image.
- **Environment-Specific Content**: Each deployment environment (e.g., `prod`, `test`, `uat`) has its own unique `index.html` file. This content is defined in the `configmap.yaml` file located in the respective environment's directory under `stages/`.

## How to Deploy/View the Application

To deploy the application for a specific environment, you would typically use `kubectl` with Kustomize. For example, to deploy the production environment:

```bash
kubectl apply -k stages/prod
```

Similarly, for the test environment:

```bash
kubectl apply -k stages/test
```

And for the UAT environment:

```bash
kubectl apply -k stages/uat
```

Once deployed, the application's service is exposed via a NodePort on port **3000**. You would typically access it by finding the IP address of one of your Kubernetes nodes and opening `http://<node_ip>:3000` in a web browser.
