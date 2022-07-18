## Deploying the UPF

To deploy a UPF the following parameters are required on deployment:
* upf.lbIP="THE UPF IP WE WANT THE LB TO PROVIDE"
* upf.tun="THE TUN SUBNET NUMBER - 45 or 46"
* upf.dnn="internet or work"

To deploy with Helm use:
```bash
helm install -n open5gs-hack -f values.yaml upf1 ./ --set upf.lbIP="10.10.10.222",upf.tun="45",upf.dnn="internet"
```


