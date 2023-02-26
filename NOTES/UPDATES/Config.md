# Config

### kubecli conf
```sh
kubectl  config -h
```

###### view Current Config

```sh
kubectl  config view
```

###### Change Current Config

```sh
kubectl config use-context tester@local
```

### kubeConfig with cert

##### encode 

cat ca.crt | base64
##### decode 

echo "dhaksdal" | base64 --decode
