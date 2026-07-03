# ☸️ Kubernetes Learning Path (k8s-learning)

Chào mừng bạn đến với kho lưu trữ học tập và thực hành Kubernetes từ cơ bản đến nâng cao! Đây là nơi tổng hợp các tài liệu lý thuyết, script cấu hình tự động (Terraform, Shell scripts) cho các nhà cung cấp Cloud (Digital Ocean, AWS), mô hình On-Premise, cùng chuỗi bài thực hành (Labs) thực tế giúp bạn nhanh chóng làm chủ Kubernetes.

---

## 📂 Cấu trúc dự án (Project Structure)

Dự án được tổ chức khoa học với các thành phần chính nằm trong thư mục [`k8s_learning_example/`](./k8s_learning_example/):

```text
k8s-learning/
├── README.md                          # Tài liệu hướng dẫn chung (File này)
└── k8s_learning_example/              # Thư mục chứa toàn bộ bài học & tài nguyên
    ├── Doc/                           # Tài liệu lý thuyết chi tiết theo từng chủ đề
    │   ├── k8s-core/                  # Core K8s: Pod, Deployment, Service, ConfigMap, Secret, RBAC...
    │   ├── argoCD/                    # CD & GitOps với ArgoCD
    │   ├── containerd/ & podman/      # Container Runtimes thay thế Docker
    │   ├── helm/                      # Quản lý Package với Helm Chart
    │   ├── prometheus/ & elasticsearch/# Giám sát (Monitoring) & Ghi log (Logging)
    │   └── kubeadm/ & eksctl/         # Công cụ khởi tạo Cluster (On-premise / AWS EKS)
    ├── example/                       # Chuỗi bài tập Lab thực hành theo từng bài (Lesson L1 -> L15)
    │   ├── Pre/                       # Chuẩn bị môi trường trước khi học
    │   ├── L1/ đến L15/               # Script và File Manifest của từng bài lab
    │   └── final/                     # Bài tập/Dự án cuối khóa
    ├── dotest/                        # Script tự động khởi tạo Cluster trên Digital Ocean (DO)
    │   ├── droplet-u22/               # Bootstrap Script cho Ubuntu 22.10
    │   └── terraform/                 # Khởi tạo hạ tầng bằng Terraform
    ├── awstest/                       # Script thử nghiệm khởi tạo tài nguyên trên AWS (EKS/ECR)
    ├── onprem/                        # Hướng dẫn cài đặt K8s trên máy chủ vật lý / VM tự quản lý
    ├── terraform/                     # Các module Terraform tái sử dụng
    └── cheatsheet.md                  # Bảng tra cứu nhanh lệnh kubectl và các lệnh dự án thông dụng
```

---

## 📚 Các chủ đề lý thuyết chính (`Doc/`)

Thư mục [`Doc/`](./k8s_learning_example/Doc/) cung cấp tài liệu chi tiết giúp bạn hiểu sâu về cơ chế hoạt động của Kubernetes:

*   **Kubernetes Core**: Tìm hiểu các Resource cơ bản như [Pod](./k8s_learning_example/Doc/k8s-core/Pod.md), [Deployment](./k8s_learning_example/Doc/k8s-core/Deployment.md), [Service](./k8s_learning_example/Doc/k8s-core/Service.md), [ConfigMap](./k8s_learning_example/Doc/k8s-core/ConfigMap.md), [Secret](./k8s_learning_example/Doc/k8s-core/Secret.md), và phân quyền [RBAC](./k8s_learning_example/Doc/k8s-core/RBAC-ABAC/).
*   **Cluster Security**: Các tiêu chuẩn bảo mật [PodSecurityStandard](./k8s_learning_example/Doc/k8s-core/PodSecurityStandard.md), chính sách bảo mật với [Gatekeeper](./k8s_learning_example/Doc/k8s-core/Gatekeeper.md) và [CIS Benchmark](./k8s_learning_example/Doc/k8s-core/CIS%20Benchmark.md).
*   **GitOps & CI/CD**: Triển khai liên tục với [ArgoCD](./k8s_learning_example/Doc/argoCD/) và [Jenkins](./k8s_learning_example/Doc/jenkins/).
*   **Package Management**: Cách đóng gói ứng dụng bằng [Helm](./k8s_learning_example/Doc/helm/).
*   **Observability**: Giám sát hệ thống với [Prometheus](./k8s_learning_example/Doc/prometheus/) và quản lý log với [Elasticsearch](./k8s_learning_example/Doc/elasticsearch/).

---

## 🛠️ Hướng dẫn Lab thực hành (`example/`)

Mỗi thư mục từ `L1` đến `L15` tương ứng với một bài học thực tế chứa các file YAML Manifests và Scripts:

1.  **L1 - L2**: Khởi tạo Node, cấu hình Container Runtime (`containerd`/`docker`) và kết nối AWS ECR.
2.  **L3 - L8**: Thực hành quản lý vòng đời Pod, Deployments, Services, CNI, Volumes (PV/PVC).
3.  **L9 - L12**: Cấu hình nâng cao Ingress, ConfigMap, Secrets, Resource Quotas, Autoscaling (HPA).
4.  **L13 - L15**: Tích hợp CI/CD (Jenkins, ArgoCD), Helm Charts, Monitoring (Prometheus/Grafana).
5.  **Final**: Bài lab tổng hợp toàn bộ kiến thức để vận hành một hệ thống thực tế.

---

## 🚀 Bắt đầu nhanh (Quick Start)

### 1. Khởi tạo K8s Cluster thử nghiệm nhanh trên Digital Ocean
Thư mục [`dotest/`](./k8s_learning_example/dotest/) hỗ trợ bạn dựng nhanh Cluster với 1 Control-plane và các Worker Node bằng Terraform & Shell Script:

**Bước 1**: Cấu hình Access Token của Digital Ocean:
```bash
export DIGITALOCEAN_ACCESS_TOKEN=<your_do_token>
```

**Bước 2**: Khởi tạo hạ tầng bằng Terraform:
```bash
cd k8s_learning_example/dotest/terraform
terraform init
terraform apply
```

**Bước 3**: Cấu hình các node sau khi tạo (SSH vào Droplet và chạy script bootstrap tương ứng):
*   **Control Plane**: Run `control-plane.sh`
*   **Worker**: Run `worker.sh`

*(Chi tiết xem thêm tại [dotest/README.md](./k8s_learning_example/dotest/README.md))*

### 2. Tra cứu nhanh lệnh (Cheatsheet)
Sử dụng file [`cheatsheet.md`](./k8s_learning_example/cheatsheet.md) để tra cứu nhanh các lệnh `kubectl` thông dụng:
*   Xem trạng thái Pods: `kubectl get pod -n <namespace>`
*   Xem log của Pod: `kubectl logs pod/<pod-name> -n <namespace>`
*   Xem lịch sử Deployment: `kubectl rollout history deployment/<deployment-name>`
*   Tự động Rollback Deployment: `kubectl rollout undo deploy/<deployment-name>`

---

## 🤝 Đóng góp ý kiến (Contributing)
Mọi đóng góp nâng cao nội dung bài lab và tài liệu lý thuyết đều được hoan nghênh. Hãy tạo Pull Request hoặc Issues nếu bạn phát hiện lỗi hoặc muốn cải tiến dự án nhé!