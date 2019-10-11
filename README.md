# How to run the example

* Start local Minikube installation.
* Grant extra permissions by invoking `oc policy add-role-to-user view system:serviceaccount:$(oc project -q):default -n $(oc project -q)`
* Rebuild this project `mvn clean install`.
* Publish artifacts to OpenShift `mvn fabric8:run`. Perhaps you will need to run `docker push` prior to this step.
* Verify logs `oc logs po/...`. There should be no exception in logs. The first Pod should become a coordinator.
* Scale the pods `oc scale dc jgroups-kube-ping --replicas=5`.
* Verify logs `oc logs po/...`. A new view should be installed.

# Debugging

* Use RHEL image with diagnosis tools: `oc run rheltest --image=registry.access.redhat.com/rhel7/rhel-tools --restart=Never --attach -i --tty`.
* Use `dig +search jgroups-dns-ping.myproject.svc.cluster.local` and make sure that proper IPs are returned.