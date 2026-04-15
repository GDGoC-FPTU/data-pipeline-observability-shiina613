# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600197
**Name:** Nguyễn Quang Tùng
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Kết quả hợp lý, Laptop là sản phẩm electronics có giá cao nhất sau khi đã lọc dữ liệu sạch |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Kết quả sai hoàn toàn — outlier cực đoan ($999,999) không bị lọc, agent chọn sản phẩm vô nghĩa |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi chạy agent với `garbage_data.csv`, agent đã gợi ý "Nuclear Reactor at $999,999" — một kết quả hoàn toàn vô nghĩa trong thực tế. Nguyên nhân đến từ nhiều vấn đề chất lượng dữ liệu tồn tại trong file garbage:

**Outlier cực đoan:** Record "Nuclear Reactor" có giá $999,999 — một giá trị bất thường không được lọc. Vì logic của agent là tìm sản phẩm có giá cao nhất trong category "electronics", outlier này thắng tuyệt đối và được trả về như "best choice", dù không có ý nghĩa thực tế.

**Duplicate IDs:** File có 2 records với `id = 1` (Laptop và Banana). Điều này gây ra sự mơ hồ trong dữ liệu — không rõ record nào là hợp lệ, có thể dẫn đến kết quả không nhất quán nếu pipeline dựa vào ID để tra cứu.

**Sai kiểu dữ liệu:** Record "Broken Chair" có `price = "ten dollars"` (string thay vì số). Nếu pipeline không xử lý, phép so sánh giá sẽ bị lỗi hoặc cho kết quả sai.

**Null values:** Record "Ghost Item" có `id = None`, `category = None` và `price = 0`. Những giá trị này nếu không được lọc sẽ gây crash hoặc làm nhiễu kết quả tính toán.

Tóm lại, agent không có khả năng tự phán đoán dữ liệu đầu vào có hợp lý hay không — nó chỉ thực thi logic trên bất kỳ dữ liệu nào được cung cấp. Vì vậy, nếu dữ liệu bẩn, output của agent cũng bẩn theo (Garbage In, Garbage Out).

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý.

Dù agent có logic tốt và prompt rõ ràng, kết quả vẫn sai hoàn toàn khi dữ liệu đầu vào có vấn đề. Một ETL pipeline với bước validate và transform kỹ càng là nền tảng bắt buộc trước khi đưa dữ liệu vào bất kỳ hệ thống AI nào. Chất lượng dữ liệu quyết định chất lượng câu trả lời — không có prompt nào có thể bù đắp cho dữ liệu bẩn.
