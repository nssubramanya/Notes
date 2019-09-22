# Kubernetes on CentOs

## Install Docker
```
# Update System
sudo yum update -y

# Install Docker
sudo yum install docker -y

# Create Docker Group and add current user to that group
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker

# Start the docker process on startup
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker

# Run docker and Verify
docker images

```

## Install Kubeadm
Run as Super-user
```
sudo su
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF

# Set SELinux in permissive mode (effectively disabling it)
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

systemctl enable --now kubelet
```

## Run as Normal User
```
exit

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```






