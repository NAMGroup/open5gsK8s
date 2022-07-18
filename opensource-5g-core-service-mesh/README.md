## Opensource 5G Core: Open5GS

This repo contains the code templates that was used in the Opensource 5G core with service mesh blog post.

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
