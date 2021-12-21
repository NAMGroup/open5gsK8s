# open5gsK8s

```
cd open5gsK8s/upf-helm/ && helm -n open5gs install -f values.yaml upf ./
```
```
cd open5gsK8s/upf-helm/ &&  helm -n open5gs install --set upf.config=2,upf.lbIP="10.10.10.233",upf.tun="46",upf.device="ogstun2",upf.dnn=ims -f values.yaml upf2 ./
```
```
cd open5gsK8s/cd opensource-5g-core-service-mesh/helm-chart/ && helm -n open5gs install -f values.yaml 5gcore ./
```
