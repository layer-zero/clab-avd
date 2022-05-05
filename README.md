# clab-avd
Simple Arista AVD example to be run on a cEOS containerlabs topology.

The files in this repository are to be used with a [containerlabs](https://containerlab.dev) topology based on the Arista ACE L3 course.
The topology consists of a three spine, four leaf fabric and a pair of hosts for connectivity testing (which are not configured through AVD).
The topology also contains two borderleafs, which the example is not using.
The corresponding containerlab topology file can be found [here](https://github.com/layer-zero/containerlab-topologies).

(Note that the Arista ACE L3 course itself has a different lab environment, but I essentially recreated the base topology of that course using containerlabs).

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

The inventory files make some assumptions about the environment, such as AWS NTP and DNS servers,
predefined management IP addresses being set up in `/etc/hosts` by containerlab, etc,
so you may need to finetune these for your environment.
