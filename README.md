# End-to-End-Medallion-Data-Lakehouse-for-Financial-Loans
Dự án xây dựng kiến trúc Data Lakehouse từ đầu đến cuối theo mô hình Medallion (Bronze, Silver, Gold) để xử lý ELT và phân tích dữ liệu các khoản vay tài chính dựa trên bộ dữ liệu thực tế của tổ chức cho vay **Lending Club**.
<img width="1272" height="409" alt="{A3C2718C-ACCF-4870-A4C4-DF6FF15E80B7}" src="https://github.com/user-attachments/assets/cf0a962c-4bb7-41a6-ba4a-d81d7e015424" />
## Summary
### 1. System Overview
Hệ thống chịu trách nhiệm tự động hóa luồng xử lý dữ liệu (Data Pipeline). 

Làm sạch và làm giàu data, loại bỏ các cột không cần thiết cho ml và report, xử lý các giá trị null,...
### 2. Technologies Used
Data Platform: Databricks

Data Processing & Storage: Apache Spark (PySpark), Delta Lake

Programming Language: Python

Development Tools: Databricks Notebooks, NotebookLM

Data Visualization: Dashboard
## Installation and Setup
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị 1 tài khoản **Databricks** (bản free là đủ)

Sau khi hoàn thành các bước dưới đây bạn có thể thưc hiện machine_learning và reporting 
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
3. **Cấu hình Task 1 (Bronze Layer):**
   * **Task name:** `01_Ingest_to_Bronze`
   * **Type:** `Notebook`
   * **Source:** `Workspace`
   * **Path** Chọn file `Bronze` trong thư mục Git của bạn.
4. **Cấu hình Task 2 (Silver Layer):**
   * Bấm nút **`+ Add task`** (nằm ngay dưới Task 1).
   * **Task name:** `02_Cleanse_to_Silver`
   * **Depends on:** Chọn `01_Ingest_to_Bronze` 
   * **Path:** Chọn file `Silver`.
5. **Cấu hình Task 3 (Gold Layer):**
   * Bấm nút **`+ Add task`** (nằm dưới Task 2).
   * **Task name:** `03_Transform_to_Gold`
   * **Depends on:** Chọn `02_Cleanse_to_Silver`.
   * **Path:** Chọn file `03_Gold_ETL`.
### Bước 4: Chạy Pipeline (nhấn run now)

## Link Databricks
https://www.databricks.com/
## Link dataset from Kaggle 
https://www.kaggle.com/datasets/adarshsng/lending-club-loan-data-csv
