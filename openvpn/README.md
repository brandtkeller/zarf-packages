# Openvpn zarf package

## Source
The chart for this zarf component is derived from the deprecated helm/stable charts.

## Credit
https://levelup.gitconnected.com/setup-openvpn-access-server-on-kubernetes-bdc35ca6b6c5
https://github.com/jfelten/openvpn-docker/blob/master/Dockerfile

## Creating client certificates
```
#!/bin/bash
# newClientCert.sh
if [ $# -ne 3 ]
then
  echo "Usage: $0 <CLIENT_KEY_NAME> <NAMESPACE> <HELM_RELEASE>"
  exit
fi
KEY_NAME=$1
NAMESPACE=$2
HELM_RELEASE=$3
POD_NAME=$(kubectl get pods -n "$NAMESPACE" -l "app=openvpn,release=$HELM_RELEASE" -o jsonpath='{.items[0].metadata.name}')
SERVICE_NAME=$(kubectl get svc -n "$NAMESPACE" -l "app=openvpn,release=$HELM_RELEASE" -o jsonpath='{.items[0].metadata.name}')
SERVICE_IP=$(kubectl get svc -n "$NAMESPACE" "$SERVICE_NAME" -o go-template='{{range $k, $v := (index .status.loadBalancer.ingress 0)}}{{$v}}{{end}}')
kubectl -n "$NAMESPACE" exec -it "$POD_NAME" -- /etc/openvpn/setup/newClientCert.sh "$KEY_NAME" "$SERVICE_IP"
kubectl -n "$NAMESPACE" exec -it "$POD_NAME" -- cat "/etc/openvpn/certs/pki/$KEY_NAME.ovpn" > "$KEY_NAME.ovpn"
```

