# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600822
**Name:** Nguyen Duong Hieu
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario                            | Agent Response                                                          | Accuracy (1-10) | Notes                                                                                                         |
| ----------------------------------- | ----------------------------------------------------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------- |
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.            | 10              | Tư vấn cực kỳ chuẩn xác và hợp lý với nhu cầu thực tế của khách hàng.                         |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1               | Agent bị ảo giác, đưa ra tư vấn phi thực tế và cực kỳ nguy hiểm cho trải nghiệm người dùng. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai hoàn toàn khi dùng Garbage Data là vì dữ liệu đầu vào chứa quá nhiều các bản ghi bất thường, outlier hoặc rác, ví dụ như giá trị bị đẩy lên mức cao phi lý một cách cố ý ($999999).

Khi xây dựng ứng dụng AI (như hệ thống RAG), Agent chỉ làm nhiệm vụ trích xuất và suy luận dựa trên dữ liệu mà nó được cung cấp. Các vấn đề kinh điển như giá âm, category bị thiếu null values, hoặc giá trị ngoại lai outliers nếu không được bộ phận Data Engineering (Data Pipeline) chặn lại và làm sạch từ sớm, chúng sẽ trực tiếp xâm nhập vào Knowledge Base. Kết quả là Agent bị mù mờ, không phân biệt được đâu là dữ liệu thật và đâu là dữ liệu rác, dẫn đến việc lấy nhầm thông tin độc hại để trả lời cho người dùng.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Đồng ý hoàn toàn! (Quality Data > Quality Prompt)

Dù bạn có kỹ năng viết Prompt xuất sắc, áp dụng các kỹ thuật suy luận phức tạp (Chain-of-Thought, ReAct...) đến đâu đi chăng nữa, thì Agent vẫn phải hoạt động trên nền tảng dữ liệu (Context) được cung cấp. Nếu dữ liệu đầu vào là rác, Agent sẽ sử dụng logic hoàn hảo của nó để đưa ra một câu trả lời cực kỳ thuyết phục nhưng lại **SAI HOÀN TOÀN** về mặt thực tế (Garbage Out). Do đó, dữ liệu sạch luôn là cốt lõi của bất kỳ hệ thống AI đáng tin cậy nào.
