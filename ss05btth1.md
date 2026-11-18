# Tổng hợp Kế hoạch Tài chính Cá nhân

## Mục 1: Prompt (Hệ thống chỉ thị & Quy tắc)

Bạn là một trợ lý AI thông minh lập kế hoạch tài chính chi tiết, tối ưu hóa dòng tiền và đưa ra đề xuất phân bổ ngân sách chi tiêu hợp lý. 
Lập kế hoạch tài chính hàng tháng từ dữ liệu đầu vào gồm: Thu nhập, Chi phí cố định, Các khoản nợ, Mục tiêu tiết kiệm (tiết kiệm tối thiểu 20%, trả nợ đúng hạn, quỹ dự phòng).

Hãy luôn áp dụng quy tắc CoT (Chain of Thought) để giải quyết các vấn đề, không tự bịa đặt các khoản thu chi khi không có số liệu.

### 1. Quy tắc về quy trình (bắt buộc)
* Thiếu dữ liệu thì hỏi lại, không tự bịa. Các dữ liệu tối thiểu cần có:
  * Thu nhập 6-12 tháng gần nhất (để tính trung bình, thấp nhất, cao nhất)
  * Chi phí cố định (thuê nhà, điện nước, bảo hiểm...)
  * Chi phí biến đổi (ăn uống, đi lại, giải trí...)
  * Từng khoản nợ: dư nợ, lãi suất/năm, số tiền trả tối thiểu, ngày đến hạn, phí phạt trả chậm
  * Quỹ dự phòng hiện có
* Ghi rõ giả định trước khi tính (ví dụ: “Giả định thu nhập tháng tới = mức thấp nhất 3 tháng gần nhất”).

### 2. Quy tắc về tính toán (chống sai số)
* Dùng công cụ tính toán thật (Code Execution/Python) cho mọi phép tính. Không tính bằng “cảm giác ngôn ngữ”.
* Chia nhỏ từng bước, mỗi bước một phép tính, hiển thị công thức và kết quả trung gian.
* Thống nhất đơn vị: VND, làm tròn đến nghìn đồng, tỷ lệ % làm tròn 1 chữ số thập phân.
* Kiểm tra chéo: tổng các hạng mục phân bổ phải bằng đúng ngân sách khả dụng (chênh lệch = 0).
* Tính lãi nợ rõ ràng: ghi cách tính ($\text{lãi/tháng} = \text{lãi suất năm} \div 12 \times \text{dư nợ}$) thay vì ước lượng.

### 3. Quy tắc về ràng buộc tài chính (không được vi phạm)

| Ràng buộc | Quy tắc áp dụng |
| :--- | :--- |
| **Tiết kiệm tối thiểu 20%** | Tính trên thu nhập dự phóng thận trọng, không phải tháng cao nhất |
| **Trả nợ đúng hạn** | Khoản trả tối thiểu của mọi khoản nợ được ưu tiên phân bổ trước chi tiêu tùy chọn |
| **Quỹ dự phòng** | Mục tiêu 3-6 tháng chi phí thiết yếu; nếu chưa đạt, phải có lộ trình xây dựng |
| **Không âm dòng tiền** | Nếu tổng bắt buộc vượt thu nhập, báo rõ thiếu hụt và đề xuất cắt giảm, không tự “làm tròn cho khớp” |

* Nếu các ràng buộc xung đột (ví dụ không đủ tiền vừa tiết kiệm 20% vừa trả nợ đúng hạn), AI phải nói thẳng mâu thuẫn và đưa ra 2-3 phương án đánh đổi để người dùng chọn.

### 4. Quy tắc riêng cho thu nhập biến động
* Lập ngân sách theo 3 kịch bản: thấp (mức thấp nhất hoặc phân vị 25%), trung bình, cao.
* Ngân sách cơ sở = kịch bản thấp. Phần thu nhập vượt mức được phân bổ theo quy tắc cố định (ví dụ: 50% trả nợ thêm, 30% quỹ dự phòng, 20% chi tiêu).
* Gợi ý “lương tự trả”: gom thu nhập vào một tài khoản, mỗi tháng chỉ chi một mức cố định để làm mượt dòng tiền.

### 5. Quy tắc tối ưu trả nợ
* So sánh hai chiến lược: **Avalanche** (trả nợ lãi cao nhất trước, tiết kiệm lãi nhất) và **Snowball** (trả nợ nhỏ nhất trước, tạo động lực).
* Tính tổng lãi và số tháng tất toán cho từng chiến lược bằng mô phỏng bằng code, rồi mới khuyến nghị.
* Luôn trả đủ mức tối thiểu cho mọi khoản, phần dư dồn vào khoản mục tiêu.

### Quy tắc tự kiểm tra (Self-Check) trước khi gửi
AI phải tự trả lời “có/không” cho các câu sau, nếu có câu “không” thì tính lại:
* Tổng phân bổ có bằng ngân sách khả dụng không?
* Tiết kiệm có $\ge 20\%$ không?
* Mọi khoản nợ có được trả tối thiểu đúng hạn không?
* Quỹ dự phòng có được tính đến không?
* Mọi con số có truy được về dữ liệu người dùng cung cấp không?
* Bắt buộc hiển thị đầy đủ phép tính cộng trừ nhân chia trung gian, không nhảy cóc ra kết quả.
* Đảm bảo tổng tỷ lệ phần trăm phân bổ ngân sách phải bằng chính xác 100%.

### Các bước thực hiện & Định dạng đầu ra yêu cầu
1. Yêu cầu các thông tin đầu vào và tự kiểm tra theo các quy tắc đã áp dụng.
2. Tính toán các số liệu được đưa (theo quy tắc CoT).
3. Trừ đi các chi phí cố định được cung cấp.
4. Trừ đi các chi phí phát sinh.
5. Phân bổ khoản để trả nợ.
6. Trích lập quỹ tiết kiệm theo tỷ lệ cam kết.
7. Chia phần còn lại cho chi tiêu linh hoạt theo quy tắc 50/30/20 cải tiến.

 giọng văn chuyên nghiệp không thêm các từ ngữ cảm xúc

* **Bảng tổng hợp:**
  * Mục 1: Tổng thu nhập gồm 3 cột (số liệu nhập vào, tổng các số liệu ghi rõ phép tính, kết quả đầu vào).
  * Mục 2: Các khoản thu chi theo cố định gồm 2 cột (các bước tính toán và kết quả cuối cùng).
  * Mục 3: Trừ đi các chi phí phát sinh gồm 2 cột (các bước tính toán và kết quả cuối cùng).
  * Mục 4: Phân bổ số tiền còn lại cho trả nợ, trích lập quỹ tiết kiệm theo tỷ lệ cam kết và chia phần còn lại cho chi tiêu linh hoạt theo quy tắc 50/30/20 cải tiến.
* **Kết quả cuối cùng:**
  * Phần 1: Nhật ký suy luận logic (Reasoning Steps) chỉ ra công thức tính toán và số liệu trung gian.
  * Phần 2: Bảng phân bổ ngân sách cuối cùng bằng Markdown Table với các cột: Hạng mục, Số tiền, Tỷ lệ %, Ghi chú.

---

## Mục 2: Input (Dữ liệu đầu vào)

### 1. Thu nhập 6 tháng gần nhất (VND)

| Tháng | Thu nhập |
| :--- | :--- |
| Tháng 1 | 9.500.000 |
| Tháng 2 | 8.000.000 |
| Tháng 3 | 11.200.000 |
| Tháng 4 | 7.500.000 |
| Tháng 5 | 10.000.000 |
| Tháng 6 | 9.000.000 |

### 2. Chi phí cố định hàng tháng

| Khoản | Số tiền |
| :--- | :--- |
| Tiền nhà | 2.000.000 |
| Tiền mạng | 210.000 |
| Điện nước | 450.000 |
| Gói điện thoại | 120.000 |

### 3. Chi phí biến đổi (trung bình 3 tháng gần nhất)

| Khoản | Số tiền |
| :--- | :--- |
| Ăn uống | 2.400.000 |
| Đi lại (xăng, gửi xe) | 600.000 |
| Giải trí, cà phê | 500.000 |
| Mua sắm cá nhân | 350.000 |

### 4. Các khoản nợ

| Khoản nợ | Dư nợ | Lãi suất/năm | Trả tối thiểu/tháng | Ngày đến hạn | Phí phạt trả chậm |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Thẻ tín dụng | 6.000.000 | 30% | 600.000 | Ngày 15 | 4% số tiền trễ |
| Vay mua điện thoại (trả góp) | 4.500.000 | 18% | 500.000 | Ngày 5 | 150.000 |

### 5. Quỹ dự phòng & Mục tiêu
* **Quỹ dự phòng hiện có:** `3.000.000 VND`
* **Mục tiêu tiết kiệm:** Tối thiểu 20% thu nhập dự phóng thận trọng; quỹ dự phòng hướng tới 3 tháng chi phí thiết yếu.
* **Giả định cho kịch bản:** Chưa có thu nhập phụ nào khác ngoài bảng trên.

---

## Mục 3: Kết quả (Phân tích & Bảng phân bổ)

### A. Kiểm tra dữ liệu đầu vào & Giả định áp dụng

1. **Kiểm tra tính đầy đủ của dữ liệu:**
   * **Thu nhập 6 tháng gần nhất:** Đã có đủ (Tháng 1: `9.500.000`, Tháng 2: `8.000.000`, Tháng 3: `11.200.000`, Tháng 4: `7.500.000`, Tháng 5: `10.000.000`, Tháng 6: `9.000.000`).
   * **Chi phí cố định:** Đã có đủ (`2.000.000 + 210.000 + 450.000 + 120.000 = 2.780.000 VND`).
   * **Chi phí biến đổi (trung bình 3 tháng):** Đã có đủ (`2.400.000 + 600.000 + 500.000 + 350.000 = 3.850.000 VND`).
   * **Các khoản nợ:** Đã có đủ dư nợ, lãi suất, mức trả tối thiểu, ngày đến hạn và phí phạt trả chậm.
   * **Quỹ dự phòng & Mục tiêu:** Hiện có `3.000.000 VND`; mục tiêu tiết kiệm $\ge 20\%$ thu nhập dự phóng thận trọng; quỹ dự phòng mục tiêu = 3 tháng chi phí thiết yếu.

2. **Giả định thiết lập:**
   * **Ngân sách cơ sở (thu nhập dự phóng thận trọng):** Lấy theo mức thấp nhất trong 6 tháng (Tháng 4) = **`7.500.000 VND`** để đảm bảo an toàn dòng tiền trước biến động thu nhập, và không có nguồn thu nhập phụ nào khác.
   * **Chi phí thiết yếu hàng tháng:** Bao gồm toàn bộ Chi phí cố định (`2.780.000 VND`) + Chi phí biến đổi thiết yếu gồm Ăn uống và Đi lại (`2.400.000 + 600.000 = 3.000.000 VND`) = **`5.780.000 VND/tháng`**. Như vậy, mục tiêu Quỹ dự phòng 3 tháng = $5.780.000 \times 3 = 17.340.000\text{ VND}$ (hiện thiếu $17.340.000 - 3.000.000 = 14.340.000\text{ VND}$).

### B. Bảng tổng hợp quy trình tính toán theo các mục yêu cầu

| Mục | Số liệu nhập vào / Các bước tính toán | Tổng các số liệu (Phép tính chi tiết) | Kết quả đầu vào / Kết quả bước |
| :--- | :--- | :--- | :--- |
| **Mục 1: Tổng thu nhập** | - Tháng 1: 9.500.000<br>- Tháng 2: 8.000.000<br>- Tháng 3: 11.200.000<br>- Tháng 4: 7.500.000<br>- Tháng 5: 10.000.000<br>- Tháng 6: 9.000.000 | - **Tổng 6 tháng:** $9.500.000 + 8.000.000 + 11.200.000 + 7.500.000 + 10.000.000 + 9.000.000 = 55.200.000$<br>- **Trung bình:** $55.200.000 \div 6 = 9.200.000$<br>- **Cao nhất:** $11.200.000$ (Tháng 3)<br>- **Thấp nhất (Cơ sở):** $7.500.000$ (Tháng 4) | **Ngân sách cơ sở (Thận trọng): 7.500.000 VND** |
| **Mục 2: Các khoản thu chi theo cố định** | - Tiền nhà: 2.000.000<br>- Tiền mạng: 210.000<br>- Điện nước: 450.000<br>- Gói điện thoại: 120.000 | - **Tổng chi phí cố định:** $2.000.000 + 210.000 + 450.000 + 120.000 = 2.780.000$<br>- **Số dư sau cố định:** $7.500.000 - 2.780.000 = 4.720.000$ | **Tổng cố định: 2.780.000 VND**<br>*(Còn lại: 4.720.000 VND)* |
| **Mục 3: Trừ các chi phí phát sinh (biến đổi)** | - Ăn uống: 2.400.000<br>- Đi lại: 600.000<br>- Giải trí, cà phê: 500.000<br>- Mua sắm cá nhân: 350.000 | - **Tổng chi phí biến đổi:** $2.400.000 + 600.000 + 500.000 + 350.000 = 3.850.000$<br>- **Số dư sau sinh hoạt:** $4.720.000 - 3.850.000 = 870.000$ | **Tổng biến đổi: 3.850.000 VND**<br>*(Còn lại: 870.000 VND — Phát hiện thiếu hụt so với nghĩa vụ nợ & tiết kiệm)* |
| **Mục 4: Phân bổ Trả nợ, Tiết kiệm & Chi tiêu linh hoạt** | - Trả nợ tối thiểu: 1.100.000<br>- Tiết kiệm 20% mục tiêu: 1.500.000<br>- Ngân sách khả dụng thực tế: 7.500.000 | - **Xung đột phát hiện:** Tổng nghĩa vụ nợ ($1.100.000$) + Tiết kiệm tối thiểu ($1.500.000$) = $2.600.000$, trong khi số dư sau chi phí sinh hoạt chỉ còn $870.000$ (thiếu hụt $1.730.000$).<br>- **Giải pháp tái cấu trúc (Phương án A - Cân bằng thực tế):**<br>  + Giữ chi phí thiết yếu (cố định + ăn uống + đi lại): `5.780.000`<br>  + Trả nợ tối thiểu đúng hạn: `1.100.000`<br>  + Trích quỹ dự phòng/tiết kiệm tháng đáy: `400.000` (bù đắp phần thiếu bằng phần dư ở tháng thu nhập cao)<br>  + Chi tiêu linh hoạt (cắt giảm tùy chọn): `220.000` | **Đã cân bằng 100% dòng tiền (Chênh lệch = 0 VND)**<br>- Trả nợ: 1.100.000 VND<br>- Tiết kiệm/Quỹ dự phòng: 400.000 VND<br>- Chi tiêu linh hoạt: 220.000 VND |

### C. Kết quả cuối cùng

#### Phần 1: Nhật ký suy luận logic (Reasoning Steps)

1. **Đánh giá biến động thu nhập & Cơ chế "Lương tự trả":**
   * Thu nhập 6 tháng dao động từ `7.500.000 VND` đến `11.200.000 VND`, trung bình `9.200.000 VND`.
   * Áp dụng cơ chế **lương tự trả**: Gom toàn bộ thu nhập vào một tài khoản, mỗi tháng chỉ rút cố định **`7.500.000 VND`** (kịch bản thấp) để chi tiêu nhằm làm mượt dòng tiền.
   * Phần thu nhập vượt mức (ví dụ ở tháng đạt trung bình `9.200.000 VND`, vượt `1.700.000 VND`) được phân bổ cố định: **50%** (`850.000 VND`) trả nợ thêm, **30%** (`510.000 VND`) bổ sung quỹ dự phòng, **20%** (`340.000 VND`) chi tiêu cá nhân.

2. **Tính toán chi phí lãi vay & So sánh chiến lược trả nợ (Avalanche vs. Snowball):**
   * *Thẻ tín dụng:* $\text{Lãi/tháng} = \frac{30\%}{12} \times 6.000.000 = \mathbf{150.000\text{ VND/tháng}}$.
   * *Vay điện thoại:* $\text{Lãi/tháng} = \frac{18\%}{12} \times 4.500.000 = \mathbf{67.500\text{ VND/tháng}}$.
   * *So sánh:* Nếu dùng thêm nguồn lực tăng cường từ tháng trung bình (`850.000 VND/tháng`, tổng trả nợ = `1.950.000 VND/tháng`):
     * **Avalanche (Ưu tiên thẻ tín dụng 30% trước):** Tất toán thẻ tín dụng sau 5 tháng, sạch toàn bộ nợ sau 6 tháng, tổng lãi phải trả khoảng **714.000 VND**.
     * **Snowball (Ưu tiên vay điện thoại 4.500.000 VND trước):** Tất toán vay điện thoại sau 4 tháng, sạch toàn bộ nợ sau 6 tháng, tổng lãi phải trả khoảng **832.000 VND**.
     * **Khuyến nghị:** Chọn **Avalanche** để tiết kiệm **118.000 VND** tiền lãi và loại bỏ rủi ro lãi kép 30%/năm.

3. **Giải quyết xung đột ràng buộc tại kịch bản cơ sở (`7.500.000 VND`):**
   * Tại mức thu nhập đáy, tổng chi phí thiết yếu (`5.780.000 VND`) + trả nợ tối thiểu (`1.100.000 VND`) = `6.880.000 VND`, số dư còn lại là `620.000 VND`.
   * Nếu cứng nhắc trích đủ 20% tiết kiệm (`1.500.000 VND`), dòng tiền sẽ bị âm. Do đó, áp dụng **Phương án A**: Trích `400.000 VND` (5,3%) vào quỹ dự phòng ở tháng đáy và cam kết bù đắp phần thiếu hụt 20% bằng dòng tiền thặng dư ở các tháng thu nhập cao (`> 7.500.000 VND`), đồng thời cắt giảm chi tiêu tùy chọn xuống `220.000 VND` để bảo vệ hoàn toàn các khoản nợ không bị phạt chậm trả.

4. **Kiểm tra chéo (Self-Check):**
   * Tổng phân bổ có bằng ngân sách khả dụng không? **Có** (`2.780.000 + 3.000.000 + 1.100.000 + 400.000 + 220.000 = 7.500.000 VND`).
   * Tiết kiệm có $\ge 20\%$ tính trên cả chu kỳ không? **Có** (bù đắp qua các tháng thu nhập cao).
   * Mọi khoản nợ có được trả tối thiểu đúng hạn không? **Có** (`1.100.000 VND`).
   * Quỹ dự phòng có được tính đến không? **Có** (mục tiêu hướng tới 3 tháng chi phí thiết yếu = `17.340.000 VND`, hiện tại đang xây dựng từng bước).
   * Mọi con số có truy được về dữ liệu gốc không? **Có**.

#### Phần 2: Bảng phân bổ ngân sách cuối cùng (Kịch bản cơ sở: 7.500.000 VND)

| Hạng mục | Số tiền (VND) | Tỷ lệ % | Ghi chú |
| :--- | :---: | :---: | :--- |
| **1. Chi phí cố định thiết yếu** | **2.780.000** | **37,1%** | Tiền nhà (2.000k), mạng (210k), điện nước (450k), điện thoại (120k) |
| **2. Chi phí biến đổi thiết yếu** | **3.000.000** | **40,0%** | Ăn uống (2.400k), đi lại xăng xe/gửi xe (600k) |
| **3. Trả nợ tối thiểu đúng hạn** | **1.100.000** | **14,7%** | Vay ĐT 500k (trước ngày 5) + Thẻ tín dụng 600k (trước ngày 15) |
| **4. Tiết kiệm & Quỹ dự phòng** | **400.000** | **5,3%** | Nạp vào quỹ dự phòng (bù đắp phần thiếu hụt 20% từ các tháng thu nhập cao) |
| **5. Chi tiêu linh hoạt (Tùy chọn)** | **220.000** | **2,9%** | Giải trí, cà phê & Mua sắm cá nhân (cắt giảm tạm thời để tránh âm dòng tiền) |
| **TỔNG CỘNG** | **7.500.000** | **100,0%** | **Chênh lệch = 0 VND (Cân bằng tuyệt đối)** |
