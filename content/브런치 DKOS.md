
deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: brunch-front
  name: brunch-front
spec:
  replicas: 1
  selector:
    matchLabels:
      app: brunch-front
  strategy:
    rollingUpdate:
      maxSurge: 100%
      maxUnavailable: 0
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: brunch-front
    spec:
      containers:
        - image: idock.daumkakao.io/blogdevteam/brunch-front:latest
          imagePullPolicy: Always
          name: brunch-front
          ports:
            - containerPort: 80
              protocol: TCP
```

ingress.yaml
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: brunch-front-ingress
spec:
  tls:
    - secretName: brunch-front-com
      hosts:
        - brunch-front.dev.onkakao.net
  rules:
    - host: brunch-front.dev.onkakao.net
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: brunch-front-service
                port:
                  number: 80
```

service.yaml
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: brunch-front-service
  name: brunch-front-service
spec:
  ports:
    - name: '80'
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: brunch-front
  type: ClusterIP

```