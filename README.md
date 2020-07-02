# mycn
cloud native
#

#安装kubectl
#由于openYurt目前支持kube1.14.1，1.15.1，很快就会支持1.16.1，所以这里下载1.15.3
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.3/bin/linux/amd64/kubectl \
  && chmod +x kubectl


#下载minikube
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube


#注意用aliyun的镜像，否则很慢
minikube start --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers --driver=none --kubernetes-version v1.15.3

#第一次安装minikube的版本是默认的最新的：v1.18.3
#为了兼容本地私有云，minikube可以指定版本：v1.15.3
#报错conntrack
apt-get install conntrack -y

#说明--driver默认是用kvm2，其次是docker，也可以设置为none，则直接stand-alone binary部署安装。

#卸载kubernetes
minikube stop
minikube delete

#增加dashboard
minikube dashboard

#通过proxy对外提供访问dashboard默认8001
kubectl proxy --address='0.0.0.0' --accept-hosts='^*$' --port=8001

http://192.168.40.207:8001

#访问dashboard界面url
http://192.168.40.207:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/cronjob?namespace=default
