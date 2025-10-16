```
 1472  kind create cluster --name cka-cluster-1
 1473  kubectl cluster-info --context kind-cka-cluster-1
 1474  kubectl get nodes
 1475  kind create cluster --name cka-cluster-2 --config
 1476  ls
 1477  vi kind-cluster.yml
 1478  kind create cluster --name cka-cluster-2 --config kind-cluster.yml
 1479  kubectl get nodes
 1480  kubectl cluster-info --context kind-cka-cluster-2
 1481  kubectl cluster-info --context kind-cka-cluster-1
 1482  kubectl get nodes
 1483  kubectl config use-context kind-cka-cluster-1
 1484  kubectl get nodes
 1485  kubectl config get contexts
 1486  kubectl config get-contexts
 1487  kubectl config get-contexts kind-cka-cluster-1
 1488  kubectl config get-contexts kind-cka-cluster-2
 1489  kubectl config --help
 1490  kubectl config get-context
 1491  kubectl config get-contexts
 1492  kubectl config --help
 1493  kubectl config set-context kind-cka-cluster-2
 1494  kubectl config use-context kind-cka-cluster-2
 1495  kubectl config get-contexts
 1496  kubectl get nodes
 1497  kubectl --help
 1498  kubectl config --help
 1499  kubectl config get-contexts
 1500  kubectl config current-contexts
 1501  kubectl config current-context
 1502  kubectl cluster-info --help
 1503  kubectl cluster-info kind-cka-cluster-2
 1504  kind get cluster
 1505  kind get clusters
 1506  kind
 1507  kubectl
 1508  kubectl config --help
 1509  kubectl config get-clusters
 1510  kubectl config get-contexts
 1511  kubectl config get-contexts --help
 1512  history
 1513  kubectl
 1514  kubectl cluster-info --help
 1515  kubectl cluster-info
 1516  kubectl get-clusters
 1517  kubectl config get-clusters
 1518  kubectl config --help
 1519  kubectl config get-contexts
 1520  kubectl config current-contexts
 1521  kubectl config current-context
 1522  kubectl config use-context kind-cka-cluster-1
 1523  kubectl cluster-info
 1524  kubectl config get-contexts
 1525  kubectl get nodes
 1526  kubectl config get-context
 1527  kubectl config get-contexts
 1528  kubectl config use-context kind-cka-cluster-2
 1529  kubectl get nodes
 1530  kubectl get pods
 1531  kubectl cluster-info --context kind-cka-cluster-2
 1532  kubectl cluster-info --context kind-cka-cluster-1
 1533  kubectl get nodes
 1534  kubectl run nginx --image=nginx
 1535  kubectl get pods
 1536  kubectl explin pod
 1537  kubectl explin pod nginx
 1538  kubectl explain pod
 1539  kubectl config view
 1540  kubectl config get-contexts
 1541  kubectl config use-context kind-cka-cluster-1
 1542  kubectl get nodes
 1543  kubectl config use-context kind-cka-cluster-2
 1544  kubectl get pods
 1545  ls
 1546  ls -la
 1547  cd .kube/
 1548  ls
 1549  nano config
 1550  cd
 1551  pwd
 1552  cd .kube/
 1553  pwd
 1554  ls
 1555  ls -la
 1556  cd
 1557  kubectl get pods
 1558  kind get clusters
 1559  kubectl config get-clusters

 1565  exit
 1566  kubectl get nodes
 1567  kubectl get pods
 1568  kubectl delete pod nginx
 1569  ls
 1570  vi pod.yml
 1571  kubectl create pod pod.yml
 1572  kubectl create pod -f pod.yml
 1573  kubectl create -f pod.yml
 1574  kubectl get pods

 1576  kubectl get pods
 1577*
 1578  kubectl get pods -o wide
 1579  kubectl delete pod nginx
 1580  nano pod.yml
 1581  kubectl apply -f pod.yml
 1582  kubectl get pods -o wide
 1583  kube get pods
 1584  kubectl get pods
 1585  kubectl describe pod nginx
 1586  kubectl edit pod nginx
 1587  kubectl apply -f pod.yml
 1588  kube get pods
 1589  kubectl get pods
 1590  kubectl edit pod nginx
 1591  kubectl apply -f pod.yml
 1592  kubectl get pods -o wide
 1593  kubectl get pods
 1594  kubectl get pods -o wide
 1595  kubectl edit pod nginx
 1596  kubectl get pods
 1597  kubectl get pods -o wide
 1598  kubectl exec -it nginx

 1600  kubectl exec -it nginx -- sh
 1601  kubectl run nginx --image=nginx --dry-run=client
 1602  kubectl run nginx --image=nginx --dry-run=client -o yaml
 1603  kubectl run nginx --image=nginx --dry-run=client -o yaml > my-pod.yml
 1604  ls
 1605  nano my-pod.yml
 1606  kubectl run nginx --image=nginx --dry-run=client -o json > my-pod.json
 1607  ls
 1608  nano my-pod.json
 1609  history
mir@DESKTOP-JASRD4A:~$ history >
```
