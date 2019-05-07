apiVersion: extensions/v1beta1
kind: Deployment
  selector:
    matchLabels:
      app: guestbook
      tier: frontend
    spec:
      containers:
      - env:
        - name: GET_HOSTS_FROM
          value: dns
        image: gcr.io/google-samples/gb-frontend:v4
        name: php-redis
        ports:
        - containerPort: 80
          protocol: TCP
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
