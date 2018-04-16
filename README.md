TEAM MEMBERS: Aishwarya Srivastava, Riddhi Kadam, Connor Patsel

## Important Documentation

* mpirun is built from mpich and as such does not use the modules and is instead freely available to run through /software
  * Because of this, when running mpirun make sure to specify the path to the file to run otherwise it will not find it. eg:
    ``mpirun -np 16 --hostfile hostfile ./hello.py``
 * At the moment, deploying from this script will produce instance VMs that are not as up to date as the currently deployed cluster.
 * Some functionalities are not automated at startup yet. NFS mounts correctly through fstab, but the headnode and storage nodes will need to enable networking by running ``dhclient`` if it has been rebooted. All the nodes will need to run ``service firewalld stop`` if they are rebooted.
* OrangeFS is setup and running on the deployed cluster but if the storage nodes are rebooted it will need to start the server again using ``/opt/orangefs/sbin/pvfs2-server -a {storage001/storage002} /opt/orangefs/etc/orangefs-server.conf``
    * If they are rebooted, the compute and head nodes will need to run ``insmod`` on the pvfs2.ko file found at the end of the orangefs/lib/modules/4.1... folder, in addition to starting the client again.
    * In short, reboot at your own risk.
 

This is an Openstack profile that is based on CloudLab's [default OpenStack profile](https://gitlab.flux.utah.edu/johnsond/openstack-build-ubuntu)

- These are a collection of scripts that install and configuration
Openstack Juno on Ubuntu 14 and onwards, within an Emulab/Apt/Cloudlab
testbed experiment.

- Modifications will be added to setup-controller.sh to further customize the cloud environment
