# mybom GitOps deployment

โฟลเดอร์นี้เป็น manifest สำหรับให้ Argo CD deploy แอป `mybom` จาก Git

## ก่อน push

แก้ค่าต่อไปนี้ให้ตรงกับโปรเจกต์จริง:

- `k8s/base/deployment.yaml`: เปลี่ยน `image` เป็น container image จริง
- `k8s/base/deployment.yaml`: เปลี่ยน `containerPort` และ health-check path หากแอปไม่ได้ฟังที่ port `8080` หรือไม่ได้ใช้ `/`
- `argocd/application.yaml`: ใช้ URL repository ระดับ root เช่น `https://github.com/bomzaza/mybom-cd.git` ห้ามใช้ URL หน้าเว็บแบบ `/tree/main/...`

## ตรวจสอบ manifest

```bash
kubectl kustomize k8s/base
```

## ติดตั้ง Argo CD Application

```bash
kubectl apply -f argocd/application.yaml
```

Argo CD จะ sync จาก branch `main` ไปยัง namespace `mybom` และสร้าง namespace ให้โดยอัตโนมัติ