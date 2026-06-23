# End-to-End-Medallion-Data-Lakehouse-for-Financial-Loans

[![Databricks](https://img.shields.io/badge/Platform-Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)](https://www.databricks.com/)
[![Apache Spark](https://img.shields.io/badge/Engine-Apache_Spark-E25A1B?style=for-the-badge&logo=apachespark&logoColor=white)](https://spark.apache.org/)
[![NotebookLM](https://img.shields.io/badge/Tool-NotebookLM-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://notebooklm.google/)
[![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=for-the-badge&logo=Kaggle&logoColor=white)](https://www.kaggle.com/)
[![Python](https://img.shields.io/badge/Language-Python_3-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)

Dự án xây dựng kiến trúc Data Lakehouse từ đầu đến cuối theo mô hình Medallion (Bronze, Silver, Gold) để xử lý ELT và phân tích dữ liệu các khoản vay tài chính dựa trên bộ dữ liệu thực tế của tổ chức cho vay **Lending Club**.

<p align="center">
  <img width="1272" height="409" alt="Architecture Diagram" src="https://github.com/user-attachments/assets/cf0a962c-4bb7-41a6-ba4a-d81d7e015424" />
</p>

## Summary
### 1. System Overview
Hệ thống chịu trách nhiệm tự động hóa hoàn chỉnh luồng xử lý dữ liệu (**Data Pipeline**):
* Tự động trích xuất, biến đổi và tải dữ liệu qua các tầng lưu trữ Delta Lake.
* Làm sạch, chuẩn hóa dữ liệu thô và thực hiện làm giàu dữ liệu (**Data Enrichment**).
* Xử lý triệt để các giá trị thiếu (`Null values`), lọc bỏ các thuộc tính/cột không cần thiết nhằm tối ưu hiệu năng cho các thuật toán học máy (**Machine Learning**) và hệ thống báo cáo (**Reporting**).

### 2. Technologies Used
* **Data Platform:** Databricks
* **Data Processing & Storage:** Apache Spark (PySpark), Delta Lake
* **Programming Language:** Python
* **Development Tools:** Databricks Notebooks, NotebookLM
* **Data Visualization:** Databricks Dashboard

## Installation and Setup
> 📝 **Lưu ý:** Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị sẵn một tài khoản **Databricks** (phiên bản Free/Community Edition là đủ).
> 
> Sau khi hoàn thành các bước dưới đây bạn có thể thực hiện machine learning và reporting.
### Bước 1: Kết nối GitHub với Databricks
Để quản lý mã nguồn trực tiếp từ GitHub trên Databricks, bạn cần thiết lập Personal Access Token (PAT):
1. Trên **GitHub**: Vào `Settings`(settings ở profile) -> `Developer settings` -> `Personal access tokens` -> `Tokens (classic)`.
2. Bấm `Generate new token (classic)`, tích chọn quyền `repo` và copy dải mã Token được cấp.
3. Trên **Databricks**: Vào `User Settings` -> `Git Integration` (hoặc `Linked accounts`).
4. Chọn Add Git credential, Git provider là **GitHub**, điền Username và dán dải mã Token vừa tạo vào -> Bấm `Save`.
### Bước 2: Clone Dự án về Databricks Git Folders
1. Tại thanh menu bên trái Databricks, chọn **Workspace**.
2. Chuột phải vào thư mục tài khoản của bạn -> Chọn `Create` -> `Git Folder` (hoặc `Repo`).
3. Dán đường dẫn URL github của kho lưu trữ này 
4. Bấm **Create Git Folder**. 
### Bước 3: Thiết lập Pipeline Tự động hóa
1. Tại thanh menu bên trái Databricks, chọn **Jobs&Pipelines** -> Bấm nút **`Create Job`**.
2. Đặt tên cho Job ở góc trên bên trái: `Lending_Club_ELT_Orchestration`.
3. Tiến hành cấu hình chuỗi các tác vụ (**Tasks**) tuần tự như bảng dưới đây:

| Thứ tự | Tên Task (`Task name`) | Loại (`Type`) | Nguồn (`Source`) | Đường dẫn file (`Path`) | Phụ thuộc (`Depends on`) |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | `01_Ingest_to_Bronze` | `Notebook` | `Workspace` | Chọn file `Bronze` trong thư mục Git của bạn | *Không có* |
| **2** | `02_Cleanse_to_Silver` | `Notebook` | `Workspace` | Chọn file `Silver` trong thư mục Git của bạn | `01_Ingest_to_Bronze` |
| **3** | `03_Transform_to_Gold` | `Notebook` | `Workspace` | Chọn file `Gold` trong thư mục Git của bạn | `02_Cleanse_to_Silver` |

### Bước 4: Chạy Pipeline (nhấn run now)

## 🔗 Link dataset from Kaggle 
https://www.kaggle.com/datasets/adarshsng/lending-club-loan-data-csv
