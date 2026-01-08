# Gateway API (minor)

Some notes for myself.

Source: https://gateway-api.sigs.k8s.io/guides/#installing-a-gateway-controller
```bash
kubectl apply --server-side -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.4.0/experimental-install.yaml
```


Follow this guide until Deploy an application chapter: https://doc.traefik.io/traefik/getting-started/kubernetes/

Install Traefik:
```bash
helm install traefik traefik/traefik --values traefik-values.yaml --namespace traefik --create-namespace
```


https://community.traefik.io/t/getting-started-with-kubernetes-gateway-api-and-traefik/23601


Flow of the request
1. Dbeaver
2. 193.191.177.69:33060 (same as service)
3. Traefik Service (LoadBalancer) at port 33060, listening on external IP
2. Traefik Gateway, 69 address on the gateway is addressing the service. Because they are linked.
4. TCP route
5. DB pod.

In case of ingress how the the request flow? Is ingress also a load balancer service.

Manually ad the following code to the traefik service thorugh Lens or whatever you prefer:
```bash
spec:
  ports:
    # - name: web
    #   protocol: TCP
    #   port: 80
    #   targetPort: web
    #   nodePort: 32657
    # - name: websecure
    #   protocol: TCP
    #   port: 443
    #   targetPort: websecure
    #   nodePort: 31350
    - name: mysql
      protocol: TCP
      port: 33060
      targetPort: 33060
```



kubectl apply --server-side -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.4.0/experimental-install.yaml
kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v3.6/docs/content/reference/dynamic-configuration/kubernetes-gateway-rbac.yml