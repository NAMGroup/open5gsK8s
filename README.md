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

## Deploying the core

### One UPF
To deploy the core with one UPF the following parameters are required on deployment:
* amf.lbIP="THE AMF IP"
* upf.upf1IP="THE UPF IP"

To deploy with Helm use:
```bash
helm install -n open5gs-hack -f values.yaml 5gcore ./ --set amf.lbIP="10.10.10.221",upf.upf1IP="10.10.10.222"
```
### Two UPFs
To deploy the core with two UPFs the following parameters are required on deployment:
* amf.lbIP="THE AMF IP"
* upf.upfs="2"
* upf.upf1IP="THE FIRST UPF IP"
* upf.upf2IP="THE SECOND UPF IP"

To deploy with Helm use:
```bash
helm install -n open5gs-hack -f values.yaml 5gcore ./ --set amf.lbIP="10.10.10.221",upf.upfs="2",upf.upf1IP="10.10.10.222",upf.upf2IP="172.16.100.161"
```

## Deploying the UPF

To deploy a UPF the following parameters are required on deployment:
* upf.config="1|2 (upf 1 or upf 2)"
* upf.lbIP="THE UPF IP WE WANT THE LB TO PROVIDE"
* upf.tun="THE TUN SUBNET NUMBER - 45 or 46"
* upf.dnn="internet or work"

To deploy with Helm use:
```bash
helm install -n open5gs-hack -f values.yaml upf1 ./ --set upf.config="",upf.lbIP="10.10.10.222",upf.tun="45",upf.dnn="internet"
```