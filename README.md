netchecker-agent
================

* Build and push container:

```bash
cd ./docker && cat README.md
```

* Label nodes for running netchecker agent:

```bash
kubectl get nodes | grep Ready | awk '{print $1}' | xargs -I {} kubectl label nodes {} netchecker=agent
```

* Set number of replicas equal to number of k8s minions:

```bash
NUMNODES=`kubectl get nodes | grep Ready | wc -l`
sed -e "s/replicas:.*/replicas: $NUMNODES/g" -i netchecker-agent_rc.yaml
```

* Run netchecker agents:

```bash
kubectl create -f netchecker-agent_rc.yaml
```
