
### Set password as local variable
```shell
PASSWORD=replaceme
```

### Generate YML
```shell
cat <<EOF >kustomization.yaml && kubectl kustomize | kubectl apply -f - && rm kustomization.yaml
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
