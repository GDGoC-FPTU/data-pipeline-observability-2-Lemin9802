[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112972&assignment_repo_type=AssignmentRepo)

# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** yennhi09082002@gmail.com
**Name:** Thái Thị Yến Nhi

---

## Mô tả

Bài lab này xây dựng một quy trình ETL Pipeline đơn giản để xử lý dữ liệu sản phẩm. Trong bài lab, em đã thực hiện các bước extract dữ liệu từ file `raw_data.json`, validate để loại bỏ các record không hợp lệ, transform dữ liệu bằng cách thêm giá sau giảm và thời gian xử lý, sau đó load dữ liệu sạch ra file `processed_data.csv`.

Ngoài ra, em cũng chạy mô phỏng Agent Simulation để so sánh kết quả của AI Agent khi sử dụng dữ liệu sạch và dữ liệu rác. Qua thí nghiệm này, em thấy rằng chất lượng dữ liệu có ảnh hưởng trực tiếp đến độ chính xác của câu trả lời từ AI Agent.

---

## Cách chạy

### Prerequisites

Cài đặt thư viện cần thiết:

```bash
pip install pandas pytest
```

### Chạy ETL Pipeline

Chạy lệnh sau để xử lý dữ liệu từ `raw_data.json` và tạo file `processed_data.csv`:

```bash
python solution.py
```

Kết quả sau khi chạy:

```text
Validation summary: 3 kept, 2 dropped.
Errors found: [{'id': 3, 'reason': 'Price <= 0'}, {'id': 4, 'reason': 'Missing Category'}]
Successfully loaded 3 records to processed_data.csv
```

### Tạo dữ liệu rác

Chạy lệnh sau để tạo file `garbage_data.csv`:

```bash
python generate_garbage.py
```

### Chạy Agent Simulation

Chạy lệnh sau để thực hiện stress test với dữ liệu sạch và dữ liệu rác:

```bash
python agent_simulation.py
```

Kết quả:

```text
Testing with CLEAN data:
Agent: Based on my data, the best choice is Laptop at $1200.

Testing with GARBAGE data:
Agent: Based on my data, the best choice is Nuclear Reactor at $999999.
```

---

## Cấu trúc thư mục

```text
├── .github/workflows        # Cấu hình GitHub Classroom Autograder
├── tests                    # Thư mục chứa test của bài lab
├── agent_simulation.py      # File mô phỏng AI Agent
├── experiment_report.md     # Báo cáo thí nghiệm
├── generate_garbage.py      # File tạo dữ liệu rác
├── raw_data.json            # Dữ liệu gốc
├── processed_data.csv       # Dữ liệu sạch sau khi chạy ETL Pipeline
├── garbage_data.csv         # Dữ liệu rác dùng để stress test
├── solution.py              # File cài đặt ETL Pipeline
└── README.md                # File mô tả bài lab
```

---

## Kết quả

Sau khi chạy ETL Pipeline, hệ thống đã xử lý dữ liệu thành công:

* 3 records hợp lệ được giữ lại.
* 2 records không hợp lệ bị loại bỏ.
* Record có `id = 3` bị loại vì `price <= 0`.
* Record có `id = 4` bị loại vì thiếu `category`.
* File `processed_data.csv` được tạo thành công.

Khi chạy Agent Simulation với dữ liệu sạch, agent trả lời hợp lý:

```text
Agent: Based on my data, the best choice is Laptop at $1200.
```

Khi chạy với dữ liệu rác, agent trả lời sai và không hợp lý:

```text
Agent: Based on my data, the best choice is Nuclear Reactor at $999999.
```

Điều này cho thấy dữ liệu rác có thể làm AI Agent đưa ra kết quả sai, ngay cả khi logic của agent vẫn chạy bình thường.

---

## Kết luận

Qua bài lab này, em hiểu rằng chất lượng dữ liệu là yếu tố rất quan trọng trong hệ thống AI. Nếu dữ liệu đầu vào bị lỗi, thiếu thông tin, có outlier hoặc bị poisoned, agent có thể đưa ra câu trả lời sai. Vì vậy, ETL Pipeline, data validation và data observability là các bước cần thiết để giúp hệ thống AI hoạt động ổn định và đáng tin cậy hơn.
