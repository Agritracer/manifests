# 🚀 Hướng Dẫn Cài Đặt Agritracer

## 🔰 Giới thiệu

Đây là hướng dẫn khởi tạo và triển khai hệ thống **Agritracer** – nền tảng hỗ trợ truy xuất nguồn gốc nông sản, ứng dụng công nghệ hiện đại để phục vụ công tác quản lý chuỗi cung ứng.

---

## 🖥 Yêu Cầu Tối Thiểu

```txt
CPU:    Intel x86_64, 2 nhân
RAM:    Tối thiểu 4GB
Ổ đĩa:  Tối thiểu 50GB
Hệ điều hành: Debian 64-bit (hoặc tương thích)
```

---

## ⚙️ Cài Đặt Môi Trường

### 1. Cấu hình GitHub cá nhân

```bash
git config --global user.name "username"
git config --global user.email "email@example.com"
```

### 2. Tạo thư mục làm việc

```bash
mkdir -p ~/Agritracer
cd ~/Agritracer
```

### 3. Cài đặt Repo và thiết lập PATH

```bash
mkdir -p ./bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ./bin/repo
chmod a+x ./bin/repo
export PATH=./bin:$PATH
# Hoặc thêm vào ~/.bashrc để dùng vĩnh viễn
```

---

## 🐳 Cài Đặt Docker & Docker Compose

```bash
sudo apt-get update -yq
sudo apt-get install ca-certificates curl gnupg lsb-release -yq

export DISTRO="debian"
curl -fsSL https://download.docker.com/linux/$DISTRO/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/$DISTRO \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update -yq
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -yq
sudo systemctl enable docker.service
```

---

## 🔄 Đồng Bộ Mã Nguồn
### Di chuyển vào folder chứa mã nguồn (Hiện tại đang trống hoặc chứa folder `bin`)
```bash
cd ~/Agritracer
```

### Nếu bạn muốn triển khai dưới môi trường Development
```bash
repo init -u https://github.com/Agritracer/manifests.git -b dev
```

### Nếu bạn muốn triển khai dưới môi trường Production
```bash
repo init -u https://github.com/Agritracer/manifests.git -b main
```

### Bắt đầu quá trình đồng bộ hoá
```bash
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

---

## 🚀 Triển Khai Hệ Thống
📌 Chỉnh sửa File trong thư mục [**Enviroment**](https://github.com/Agritracer/Enviroment.git) trước khi deploy

```bash
cd ~/Agritracer
docker compose up -d  # Thêm --build nếu muốn dựng lại toàn bộ image
```

---

✅ Sau khi hoàn tất, hệ thống **Agritracer** sẽ hoạt động tại máy chủ của bạn.

📌 Đảm bảo Docker daemon đang chạy trước khi thực hiện `docker compose`.
