# Kubernetes-Cluster-Installation-Master-Node-only-untainted-
K8s Cluster Installation Steps Master only untainted

root@master:/etc/systemd/system# history 
    1  hostnamectl set-hostname master
    2  hostname -I
    3  echo "vm-IP master" >> /etc/hosts
    4  cat /etc/hosts
    5  ping master
    6  vim /etc/hosts
    7  ping master
    9  cat /etc/hosts
   10  apt update -y && apt upgrade -y
   11  sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
   12  swapoff -a
   13  apt-get update && apt-get install -y 
   14  apt install apt-transport-https curl
   15  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
   16  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee /etc/apt/sources.list.d/kubernetes.list
   17  deb https://apt.kubernetes.io/ kubernetes-xenial main
   18  apt update
   19  apt -y install vim git curl wget kubelet=1.18.20-00 kubeadm=1.18.20-00 kubectl=1.18.20-00
   20  sudo apt-mark hold kubelet kubeadm kubectl
   21  apt install containerd
   23  sudo modprobe overlay
   24  sudo modprobe br_netfilter
   25  cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF

   26  sudo sysctl --system
   27  sudo mkdir -p /etc/containerd
   28  containerd config default | sudo tee /etc/containerd/config.toml
   29  cd /etc/containerd/
   30  ls
   31  vim config.toml 
   32  sudo systemctl restart containerd
   33  sudo systemctl status containerd
   34  sudo systemctl status containerd
   35  kubectl version --client && kubeadm version
   36  systemctl enable --now kubelet
   37  systemctl status kubelet.service 
   38  systemctl disable --now kubelet.service 
   39  $ sudo mkdir -p  /etc/systemd/system/kubelet.service.d/
   
   40  $ cat << EOF | sudo tee  /etc/systemd/system/kubelet.service.d/0-containerd.conf
[Service]                                                 
Environment="KUBELET_EXTRA_ARGS=--container-runtime=remote --runtime-request-timeout=15m --container-runtime-endpoint=unix:///run/containerd/containerd.sock"
EOF

   43  sudo systemctl daemon-reload
   44  sudo systemctl daemon-reload
   45  sudo systemctl restart containerd
   46  sudo systemctl status containerd
   47  sudo systemctl restart containerd
   48  sudo systemctl status containerd
   49  systemctl enable --now kubelet.service 
   50  systemctl status kubelet.service 
   51  systemctl restart kubelet.service 
   52  systemctl status kubelet.service 
   53  journalctl -xe
   54  cd /etc/systemd/system/
   55  ls
   56  lsmod | grep br_netfilter
   57  systemctl enable kubelet
   58  systemctl start kubelet
   59  systemctl status kubelet.service 
   60  vim /etc/systemd/system/kubelet.service.d/0-containerd.conf
   61  sudo apt-get update
   62  sudo apt-get install libseccomp2
   63  systemctl daemon-reload
   64  systemctl restart kubelet.service 
   65  systemctl status kubelet.service 
   66  sudo kubeadm init --control-plane-endpoint <VM-IP>  --pod-network-cidr=10.244.0.0/16 --upload-certs
   67  mkdir -p $HOME/.kube
   68  kubectl get nodes
   69  systemctl status kubelet.service 
   70  kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
   71  kubectl get po -A
   72  kubectl get nodes
   73  kubectl get nodes -o wide
   74  kubectl taint nodes <NODE-NAME> node-role.kubernetes.io/master:NoSchedule-

	
