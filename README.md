# kindでk8sを試すサンプル  
kindでローカルにk8sの開発環境を構築し、  
Go言語のAPIをデプロイするサンプルです。  
  
## 機能一覧  
・テキスト表示１（GET /）  
・テキスト表示２（GET /k8s-go）  
  
## 使用技術  
Go "1.24"  
Echo "v4.13.3"  
Docker  
docker-compose  
kubectl  
kind  
k8s  
  
## コマンド  
・コンテナのビルド  
```
docker build --no-cache -f ./docker/prod/Dockerfile -t k8s-go-api:latest .
```
  
・kindでクラスターおよびノードの作成  
```
kind create cluster --config k8s/kind-cluster.yaml
```
  
・ノードの確認  
```
kubectl get nodes -o wide
```
  
・ローカル環境で事前にビルドしたDockerコンテナのイメージをkindにロード  
```
kind load docker-image k8s-go-api:latest
```
  
・ポッドのデプロイ  
```
kubectl create -f k8s/kind-deployment.yaml
```
  
・ポッドの確認  
```
kubectl get pods -o wide
```
  
・サービスの作成  
```
kubectl create -f k8s/kind-service.yaml
```
  
・サービスの確認  
```
kubectl get services -o wide
```
  
・コンテナの再ビルドとポッドの更新  
```
docker build --no-cache -f ./docker/prod/Dockerfile -t k8s-go-api:latest .
kind load docker-image k8s-go-api:latest
kubectl rollout restart deployment kind-go-deployment
```
  
・クラスターの削除
```
kind delete cluster
```
  
## 参考記事  
[・kindでKubernetes（k8s）のローカル開発環境を作ってGo言語（Golang）のAPIをデプロイする方法](https://golang.tomoyuki65.com/how-to-build-a-k8s-development-ev-with-kind)  
  