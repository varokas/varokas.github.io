---
layout:	post
title:	"สร้าง Kubernetes Cluster บน Google Cloud Platform"
date:	2019-01-04
---

  ![](/img/1*1GPJInCBvnUXVJWuMz_GGA.jpeg)Photo by [Joseph Barrientos](https://unsplash.com/photos/eUMEWE-7Ewg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/sea-navigation?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)เนื่องจากเป็นโปรแกรมเมอร์งบจำกัด เพิ่งมีคนใจดีให้เครดิตมาลองเล่น GCP ก็เลยสร้าง Kubernetes Cluster ซะเลย ง่ายสุดก็เข้าไปกดคลิ๊กๆ แต่วันนี้จะมาลองทำบน command line ดู

จริงๆ ก็ทำตามขั้นตอนที่ลิงก์แหละ แต่สรุปมาให้

[**Creating a Cluster | Kubernetes Engine | Google Cloud**  
*Google Cloud delivers secure, open, intelligent, and transformative tools to help enterprises modernize for today's…*cloud.google.com](https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-cluster "https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-cluster")[](https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-cluster)1. ลง Command Line Tool ของ Google Cloud ชื่อว่า gcloud
brew cask install google-cloud-sdk2. login ใช้ gcloud มันจะเปิดหน้า browser ขึ้นมาให้เราใส่ user/pass เข้าไป

gcloud auth loginเลือก Project ที่เราจะใช้ ดูรายชื่อ project ที่เรามีได้ที่นี่ <https://console.cloud.google.com/cloud-resource-manager>

gcloud config set project PROJECT\_ID3. สร้าง cluster

* machine type เลือก[ตามนี้](https://cloud.google.com/compute/pricing#standard_machine_types) (ยากจนก็ใช้ g1-small, $14 ต่อเดือน)
* num\_nodes ตามต้องการ แต่ default คือ 3
เลือกได้ว่าจะสร้างไว้ที่ zone เดียวหรือทั้ง region เลย ดูชื่อได้ [ที่นี่](https://cloud.google.com/compute/docs/regions-zones/#available)

* zone ที่เราจะสร้าง REGION\_NAME-ZONE\_NAME
* region ที่เราจะสร้าง แต่ถ้าใส่ num\_nodes ไปเท่าไหร่มันจะ x3
gcloud container clusters create CLUSTER\_NAME --machine-type=g1-small --num-nodes=1 --zone=us-west1-aสร้างอยู่นานเหมือนกัน (ประมาณสองสามนาที)

4. สร้าง config สำหรับ kubectl

จากนั้นเราก็สามารถสั่งให้มันไปสร้าง config ให้กับ

> brew install kubectl> gcloud container clusters get-credentials CLUSTER\_NAME --zone=us-west1-aFetching cluster endpoint and auth data.  
kubeconfig entry generated for k8s.5. kubectl

เสร็จหมดแล้ว ใช้ kubectl ได้เลย

kubectl get pods --all-namespaces | awk '{ print $2,$3 }'NAME READY  
event-exporter-v0.2.3-54f94754f4-j5m8s 2/2  
fluentd-gcp-scaler-6d7bbc67c5-lrnz7 1/1  
fluentd-gcp-v3.1.0-kxttm 2/2  
heapster-v1.5.3-7bd845b96c-r5f8n 3/3  
kube-dns-788979dc8f-8tpxm 4/4  
kube-dns-autoscaler-79b4b844b9-v7v5f 1/1  
kube-proxy-gke-k8s-default-pool-0c3f25d3-cpmt 1/1  
l7-default-backend-5d5b9874d5-qsnwk 1/1  
metrics-server-v0.2.1-7486f5bd67-xkrbb 2/2สำหรับขา UI เข้าไปดูผ่าน UI ได้ที่นี่ <https://console.cloud.google.com/kubernetes/list>

![](/img/1*i9ZVwQOc02o6GDR2EmHHqQ.png)  