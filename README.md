# Uninstall-Kubernetes

To completely uninstall Kubernetes from your system, you will need to remove the following components:

Kubernetes Packages and Dependencies

Kubernetes Configuration Files

Docker/Container Runtime (if applicable)

Here’s a step-by-step guide for a complete uninstallation:

1. Stop and Disable Kubernetes Services
If you're using kubeadm for managing the Kubernetes cluster, stop and disable all related services:


# Stop the kubelet and disable it

```
sudo systemctl stop kubelet
sudo systemctl disable kubelet
```

# Stop kube-proxy and disable it
```
sudo systemctl stop kube-proxy
sudo systemctl disable kube-proxy
```
2. Reset Kubernetes Cluster
If you used kubeadm to set up the cluster, reset it with the following command:

```
sudo kubeadm reset
```

This will remove most of the cluster configuration, but it may leave some residual files.

3. Remove Kubernetes Packages
Next, remove Kubernetes-related packages:

For Debian/Ubuntu systems:

```
sudo apt-get purge -y kubeadm kubectl kubelet kubernetes-cni kube* 
sudo apt-get autoremove -y
```

For CentOS/Red Hat systems:

```
sudo yum remove -y kubeadm kubectl kubelet kubernetes-cni kube*
```

4. Delete Configuration Files
Remove any leftover Kubernetes configuration files:

```

sudo rm -f $(which kubectl)
sudo rm -f $(which kubeadm)
sudo rm -f $(which kubelet)

sudo rm -rf $(which docker)
sudo rm -rf $(which containerd)

sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd


sudo rm -rf ~/.kube
sudo rm -rf /etc/kubernetes
sudo rm -rf /etc/systemd/system/kubelet.service.d
sudo rm -rf /etc/systemd/system/kube-proxy.service
```

5. Clean up CNI Network Files
Remove network-related configuration:

```
sudo rm -rf /etc/cni
sudo rm -rf /opt/cni
```

6. Remove Docker and Container Runtime (Optional)
If you no longer need Docker or the container runtime (e.g., containerd or cri-o), uninstall it as well:

For Docker:

```
# Uninstall Docker
sudo apt-get purge -y docker docker-engine docker.io containerd runc
sudo apt-get autoremove -y
sudo rm -rf /var/lib/docker
```

For containerd:

```
# Uninstall containerd
sudo apt-get purge -y containerd.io
sudo rm -rf /var/lib/containerd
```

7. Reboot the System
Finally, reboot your system to apply all changes:

```
sudo reboot
```

After rebooting, Kubernetes should be completely removed from your system.

8. Check for Leftovers
To ensure everything is cleaned up, check if any Kubernetes services are still running:

```
ps aux | grep kube
```
