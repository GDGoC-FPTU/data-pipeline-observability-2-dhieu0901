# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** duonghieuasylum@gmail.com
**Name:** Nguyen Duong Hieu

---

## Mo ta

Bài lab này tập trung vào việc xây dựng một hệ thống **ETL Pipeline tự động** (Extract, Validate, Transform, Load) hoàn chỉnh. Nhiệm vụ chính của hệ thống là trích xuất dữ liệu từ file JSON, áp dụng các bộ lọc để loại bỏ dữ liệu rác (giá trị âm, thiếu thông tin), chuẩn hóa text và xuất ra một tập dữ liệu sạch.

Mục tiêu lớn nhất của bài lab là chứng minh tầm quan trọng của **Data Quality** và **Data Observability** (Ghi log chi tiết lỗi) trước khi cung cấp dữ liệu nền tảng cho các AI Agent.

---

## Cach chay (How to Run)

### Prerequisites

Bạn cần cài đặt thư viện `pandas` để phục vụ cho quá trình Transform.

```bash
pip install pandas
```

### Chay ETL Pipeline

Chạy script chính để kích hoạt tiến trình ETL, dọn dẹp dữ liệu và sinh ra file `processed_data.csv` sạch.

```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)

Để kiểm chứng hậu quả của việc đưa dữ liệu rác vào AI Agent, chạy 2 lệnh sau:

1. Tạo file dữ liệu rác (Poisoned data):

```bash
python generate_garbage.py
```

2. Chạy mô phỏng Agent để xem sự khác biệt giữa Data Sạch và Data Rác:

```bash
python agent_simulation.py
```

---

## Cau truc thu muc

```text
├── agent_simulation.py      # Kich ban mo phong RAG Agent (So sanh Sạch - Rác)
├── generate_garbage.py      # Script tao data rac cho qua trinh thu nghiem
├── raw_data.json            # File data goc (chua ca du lieu hop le va loi)
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline (Data Sach)
├── garbage_data.csv         # Output cua script tao rác
├── experiment_report.md     # Bao cao thi nghiem (Agent bi ảo giác)
└── README.md                # File nay
```

---

## Ket qua

Hệ thống ETL đã chạy thành công qua tập `raw_data.json` gồm tổng cộng **5 bản ghi**:

- **Bị loại bỏ (Dropped):** 2 bản ghi. Trong đó, 1 bản ghi bị loại do giá âm (`price <= 0`) và 1 bản ghi bị loại do thiếu hạng mục (`Missing Category`).
- **Giữ lại (Kept) & Transform:** 3 bản ghi. Cả 3 đều được áp dụng logic kinh doanh (Discounted price giảm 10%, chuẩn hóa Title Case cho Category, và gắn Batch Timestamp).
- **Xuất file (Loaded):** Lưu thành công 3 bản ghi sạch này ra file `processed_data.csv`.
