# Ingress 

### Spec:

1. ingressClassName:

```sh
ingressClassName:
    - <value>
```
* supported value are 'nginx' , 'apache', 'route53'.

2. rules:
- host
- protocal_type

```sh
rules:
   host: 'domain_name.com'
   <type>: 
```
* supported value  for Type are 'http' , 'https', 'tcp'.

3. paths

```sh
   <type>:
    paths: 
      - path: /<endpoint>
        pathType: Prefix
        <srv_type>:
          service:
            name: <svc_name>
            port:
              number: <port_no>
```

example: 
```sh
      - path: /europe
        pathType: Prefix
        backend:
          service:
            name: europe
            port:
              number: 80
```

* supported value  for pathType are 'europe'
