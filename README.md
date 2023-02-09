# clab-avd
Simple Arista AVD example to be run on a cEOS containerlabs topology.

The files in this repository are to be used with a simple leaf-spine [containerlabs](https://containerlab.dev) topology.
The topology consists of a two spine, four leaf fabric and a pair of hosts for connectivity testing (which are not configured through AVD).
The corresponding containerlab topology file `ceos-leaf-spine.yml` can be found [here](https://github.com/layer-zero/containerlab-topologies).

First, install the Python prerequisites using `pip3 install -r requirements.txt`. Then push a basic configuration with the required EOS user
to the switches using `ansible-playbook deploy-initial-config.yml`. Next you can use the following AVD playbooks.

To generate configurations and documentation run:
```
ansible-playbook playbooks/deploy-fabric.yml
```

To deploy the generated configurations to the switches use:
```
ansible-playbook playbooks/deploy-fabric.yml -t deploy
```

To validate that the fabric is running properly and generate test reports use:
```
ansible-playbook playbooks/validate-states.yml 
```

To take snapshots of arbitrary commands and generate reports of the output use:
```
ansible-playbook playbooks/collect-snapshots.yml
```

The inventory files make some assumptions about the environment, such as NTP and DNS servers,
predefined management IP addresses being set up in `/etc/hosts` by containerlab, etc,
so you may need to finetune these for your environment.
