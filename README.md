[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573932&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.tungnq@vinuni.edu.vn
**Name:** Nguyễn Quang Tùng - 2A202600197
**ID:** 2A202600197

---

## Mo ta

Bài lab xây dựng một ETL pipeline tự động bằng Python để xử lý dữ liệu sản phẩm từ file JSON. Pipeline thực hiện 4 bước: Extract (đọc dữ liệu), Validate (lọc dữ liệu lỗi), Transform (chuẩn hóa và tính giá giảm), Load (lưu ra CSV). Ngoài ra, bài lab còn thực hiện thí nghiệm so sánh hiệu quả của AI agent khi sử dụng dữ liệu sạch và dữ liệu "bẩn" để minh họa tầm quan trọng của Data Observability.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Tao garbage data
python generate_garbage.py

# Buoc 2: Chay agent voi ca 2 bo du lieu (clean vs garbage)
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── raw_data.json            # Du lieu dau vao
├── processed_data.csv       # Output cua pipeline (sau khi chay solution.py)
├── garbage_data.csv         # Du lieu "ban" de stress test (sau khi chay generate_garbage.py)
├── generate_garbage.py      # Script tao garbage data
├── agent_simulation.py      # Mo phong AI agent
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

Pipeline xu ly 5 records tu `raw_data.json`:
- 3 records hop le duoc giu lai va luu vao `processed_data.csv`
- 2 records bi loai: 1 record co price am (-10), 1 record co category rong
- Moi record duoc them cot `discounted_price` (giam 10%) va `processed_at` (timestamp)
