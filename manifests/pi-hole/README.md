
### Set password as local variable
```shell
PASSWORD=replaceme
```

### Generate YML
```shell
cat <<EOF | kubectl kustomize | kubectl apply -f -
resources:
  - https://github.com/garretpremo/kubernets/manifests/pi-hole

patches:
  - target:
      kind: Secret
    patch: |-
      - op: replace
        path: /data/WEBPASSWORD
        value: $(echo "$PASSWORD" | base64)
EOF
```
