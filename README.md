# Open5Gs on K8s

## Deploying the core

### One UPF
To deploy the core with one UPF the following parameters are required on deployment:
* amf.lbIP="THE AMF IP"
* upf.upf1IP="THE UPF IP"

### Two UPFs
To deploy the core with two UPFs the following parameters are required on deployment:
* amf.lbIP="THE AMF IP"
* upf.upfs="2"
* upf.upf1IP="THE FIRST UPF IP"
* upf.upf2IP="THE SECOND UPF IP"

## Deploying the UPF

To deploy a UPF the following parameters are required on deployment:
* upf.config="1|2 (upf 1 or upf 2)"
* upf.lbIP="the UPF IP we want from the LB"
* upf.tun="tun subnet number - 45, 46, ..."
* upf.dnn="dnn"

## Examples
### Example 1 UPF

#### Deploying using Helm
```bash
helm install -n open5gs-hack -f values.yaml 5gcore ./ --set amf.lbIP="10.10.10.221",upf.upf1IP="10.10.10.222"
helm install -n open5gs-hack -f values.yaml upf1 ./ --set upf.config="1",upf.lbIP="10.10.10.222",upf.tun="45",upf.dnn="internet"
```

#### Deploying using OSM (--config)
```JSON
{
	"additionalParamsForVnf": [{
		"member-vnf-index": "1",
		"additionalParamsForKdu": [{
			"kdu_name": "open5gs",
			"k8s-namespace": "open5gs-hack",
			"additionalParams": {
				"amf": {
					"lbIP": "10.10.10.221"
					},
				"upf": {
					"upf1IP": "10.10.10.222"
					}
			}
		}]
	}]
}
```

```JSON
{
	"additionalParamsForVnf": [{
		"member-vnf-index": "1",
		"additionalParamsForKdu": [{
			"kdu_name": "upf",
			"k8s-namespace": "open5gs-hack",
			"additionalParams": {
				"upf": {
				"config": "1",
				"lbIP": "10.10.10.222",
				"tun": "45",
				"dnn": "internet"
				}
			}
		}]
	}]
}
```

### Example 2 UPFs (one at the central DC and one at the edge)
#### Deploying using Helm
```bash
# On main cluster
helm install -n open5gs-hack -f values.yaml 5gcore ./ --set amf.lbIP="10.10.10.221",upf.upfs="2",upf.upf1IP="10.10.10.222",upf.upf2IP="172.16.100.161"
helm install -n open5gs-hack -f values.yaml upf1 ./ --set upf.config="1",upf.lbIP="10.10.10.222",upf.tun="45",upf.dnn="internet"

# On edge cluster
helm install -n open5gs-hack -f values.yaml upf2 ./ --set upf.config="2",upf.lbIP="172.16.100.161",upf.tun="46",upf.dnn="work"
```

#### Deploying using OSM (--config)

**Core (on main cluster)**
```JSON
{
	"additionalParamsForVnf": [{
		"member-vnf-index": "1",
		"additionalParamsForKdu": [{
			"kdu_name": "open5gs",
			"k8s-namespace": "open5gs-hack",
			"additionalParams": {
				"amf": {
					"lbIP": "10.10.10.221"
				},
				"upf": {
					"upf1IP": "10.10.10.222"
				}
			}
		}]
	}]
}
```
**UPF 1 (on main cluster)**
```JSON
{
	"additionalParamsForVnf": [{
		"member-vnf-index": "1",
		"additionalParamsForKdu": [{
			"kdu_name": "upf",
			"k8s-namespace": "open5gs-hack",
			"additionalParams": {
				"upf": {
					"config": "1",
					"lbIP": "10.10.10.222",
					"tun": "45",
					"dnn": "internet"
				}
			}
		}]
	}]
}
```

**UPF 2 (on edge cluster)**
```JSON
{
	"additionalParamsForVnf": [{
		"member-vnf-index": "1",
		"additionalParamsForKdu": [{
			"kdu_name": "upf",
			"k8s-namespace": "open5gs-hack",
			"additionalParams": {
				"upf": {
				"config": "2",
					"lbIP": "172.16.100.161",
					"tun": "46",
					"dnn": "work"
				}
			}
		}]
	}]
}
```
