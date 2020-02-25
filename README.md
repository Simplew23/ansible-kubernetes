Kubernetes ansible deploy roles
------

For local cluster, start VM's (use Vagrantfile and vbox):

    vagrant up

Prepare ssh config file:

    ansible-playbook stage0/site.yml -i inventories/kube_cluster.yml

Set up common tasks and software:

    ansible-playbook stage1/site.yml -i inventories/kube_cluster.yml

Set up kubernetes cluster:

    ansible-playbook stage2/site.yml -i inventories/kube_cluster.yml

3rd stage contains specific software and uder development.

Kubernetes and flannel version must set up in variables at *stage2\group_vars\all*
