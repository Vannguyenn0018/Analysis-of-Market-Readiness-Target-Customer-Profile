#  Phân Tích Tệp Khách Hàng Tiềm Năng & Mô Hình Phân Cụm Ma Trận Capability - Readiness

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Data Analytics](https://img.shields.io/badge/Analytics-Wealth%20Management-green.svg)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)](#)

Báo cáo phân tích chuyên sâu về **Mức độ sẵn sàng cho Sản phẩm Tài chính Mới** trên tệp khảo sát 392 cán bộ nhân viên / khách hàng tiềm năng. Dự án thiết lập mô hình phân loại hai chiều độc lập (**Capability - Readiness Matrix**) để tối ưu hóa chiến lược chuyển đổi tài sản nhàn rỗi thành tài sản quản lý (AUM) và doanh thu phí dịch vụ.

---

## Mục Lục
- [1. Tổng Quan Dự Án & Bối Cảnh Kinh Doanh](#1-tổng-quan-dự-án--bối-cảnh-kinh-doanh)
- [2. Quy Trình Làm Bài & Phương Pháp Luận](#2-quy-trình-làm-bài--phương-pháp-luận)
- [3. Khung Khái Niệm Ma Trận Capability – Readiness](#3-khung-khái-niệm-ma-trận-capability--readiness)
- [4. Hồ Sơ Chi Tiết Các Phân Khách Hàng](#4-hồ-sơ-chi-tiết-các-phân-khúc-khách-hàng)
- [5. Phát Hiện Cốt Lõi & Insight Chi Tiết](#5-phát-hiện-cốt-lõi--insight-chi-tiết)
  - [5.1. Nghịch lý AUM vs Doanh thu phí](#51-nghịch-lý-aum-vs-doanh-thu-phí)
  - [5.2. Hành vi tự quản lý & Tâm lý bảo toàn vốn](#52-hành-vi-tự-quản-lý--tâm-lý-bảo-toàn-vốn)
  - [5.3. Mô hình phí & Mức phí chấp nhận](#53-mô-hình-phí--mức-phí-chấp-nhận)
  - [5.4. Phân hóa theo độ tuổi](#54-phân-hóa-theo-độ-tuổi)
- [6. Rào Cản Chuyển Đổi & Chiến Lược Đề Xuất](#6-rào-cản-chuyển-đổi--chiến-lược-đề-xuất)
- [7. Cấu Trúc Mã Nguồn & Hướng Dẫn Chạy](#7-cấu-trúc-mã-nguồn--hướng-dẫn-chạy)

---

## 1. Tổng Quan Dự Án & Bối Cảnh Kinh Doanh

Dữ liệu khảo sát từ **392 khách hàng/nhân viên** ghi nhận quy mô sức chứa thị trường rất lớn:
*  **Tổng tài sản nhàn rỗi (AUM tiềm năng):** `198.47 tỷ VNĐ`
*  **Tổng vốn ban đầu sẵn sàng đầu tư:** `22.02 tỷ VNĐ`
*  **Tỷ lệ vốn sẵn sàng/AUM:** Chỉ đạt **`10.87%`**

> **Thách thức kinh doanh cốt lõi:** Thị trường không thiếu nguồn lực tài chính, nhưng tồn tại một khoảng cách lớn giữa *tài sản nhàn rỗi* và *hành động đầu tư thực tế*. Bài toán chiến lược không chỉ là tìm kiếm khách hàng mới mà là **xây dựng giải pháp niềm tin để giải phóng dòng tiền nhàn rỗi**.

---

## 2. Quy Trình Làm Bài & Phương Pháp Luận

### Bước 1: Giả lập chỉ số tài chính & Dòng tiền
Sử dụng phương pháp kỳ vọng để tính toán: Chi phí phụ thuộc, Dòng tiền khả dụng, Vốn khả dụng, và Doanh thu tiềm năng (`Doanh thu tiềm năng.ipynb`).

### Bước 2: Chuẩn hóa 6 chỉ số đánh giá cơ bản $[1, 5]$
| Ký hiệu | Tên chỉ số (Scale 1-5) | Mô tả ngắn | Khoảng giá trị khảo sát |
| :---: | :--- | :--- | :---: |
| **FHS** | Financial Health Score | Sức khỏe tài chính & khả năng tích lũy vốn | $[1.76, 4.53]$ |
| **ICS** | Investment Knowledge Score | Trình độ hiểu biết & kiến thức đầu tư | $[2.00, 4.40]$ |
| **RAS** | Risk Appetite Score | Khẩu vị & mức độ chấp nhận rủi ro | $[1.70, 4.30]$ |
| **PDS** | Product Demand Score | Nhu cầu cụ thể đối với sản phẩm | $[2.25, 4.10]$ |
| **ANS** | Advisory Need Score | Mức độ cấp thiết của nhu cầu tư vấn (Pain Point) | $[1.00, 5.00]$ |
| **CRS** | Commercial Readiness Score | Mức độ sẵn sàng trả phí & cam kết sử dụng | $[1.65, 4.75]$ |

### Lý do từ bỏ điểm số đơn nhất (Single Composite Score)
Việc cộng gộp trực tiếp điểm Rủi ro (RAS) hay Nhu cầu vào chung với Sức khỏe tài chính (FHS) dẫn đến rủi ro đánh đồng: **Một khách hàng tài sản rất lớn nhưng thận trọng đầu tư sẽ bị đánh giá thấp** chỉ vì RAS thấp. 

Do đó, dự án chuyển sang mô hình hóa hai chiều độc lập: **Capability (Khả năng)** vs **Readiness (Sẵn sàng)**.

---

## 3. Khung Khái Niệm Ma Trận Capability – Readiness

Không gian khách hàng được phân tách thành ma trận 2D với ngưỡng phân loại **Threshold = 3.5 / 5.0**:

```
           Y (Capability)
             ▲
         4.0 │  [Khách hàng Tự chủ]    │  [Khách hàng Ưu tiên]
             │  High Wealth / Low Read │  High Wealth / High Read
         3.5 ├─────────────────────────┼─────────────────────────
             │  [KH Không đủ năng lực] │  [KH Chưa nhiều vốn]
             │  & [KH Nuôi dưỡng]      │  Low Wealth / High Read
         1.0 └─────────────────────────┴─────────────────────────► X (Readiness)
             1.0                      3.5                      5.0
```

### Công thức xác định tọa độ:

#### 1. Trục Y – Financial & Investment Capability (Năng lực tài chính & Đầu tư)
Trả lời câu hỏi: *"Khách hàng có đủ nguồn lực để trở thành nguồn AUM giá trị hay không?"*
$$	ext{Y (Capability)} = (	ext{FHS} 	imes 0.6) + (	ext{ICS} 	imes 0.4)$$
* *Trọng số FHS (0.6):* Ưu tiên quy mô và sự ổn định của nguồn vốn.
* *Trọng số ICS (0.4):* Định vị mức độ am hiểu để thiết kế độ phức tạp của sản phẩm.

#### 2. Trục X – Conversion Readiness (Mức độ sẵn sàng chuyển đổi)
Trả lời câu hỏi: *"Khách hàng có sẵn sàng chi trả/cam kết để giải quyết bài toán tài chính hiện tại?"*
$$	ext{X (Readiness)} = (	ext{CRS} 	imes 0.6) + (	ext{ANS} 	imes 0.4)$$
* *Trọng số CRS (0.6):* Đóng vai trò **Conversion Gate** (Cổng chuyển đổi) đảm bảo tính cam kết thương mại.
* *Trọng số ANS (0.4):* Đại diện cho mức độ cấp bách của "Pain Point".

---

## 4. Hồ Sơ Chi Tiết Các Phân Khúc Khách Hàng

| Phân khúc | Điều kiện phân loại | Đặc điểm tài chính & Hành vi | Định hướng hành động |
| :--- | :--- | :--- | :--- |
| **Khách hàng Ưu tiên** *(Priority Leads)* | $Y \ge 3.5$ & $X \ge 3.5$ | • **High Wallet - High Readiness**<br>• Tài sản: ~15B \| Phí hiện tại: 22M<br>• Rõ nhu cầu, sẵn sàng ra quyết định ngắn hạn | Chăm sóc VIP 1-1, tư vấn giải pháp quản lý tài sản toàn diện. |
| **Khách hàng Tự chủ đầu tư** *(Strategic/Self-directed)* | $Y \ge 3.5$ & $X < 3.5$ | • **High Wallet - Low Readiness**<br>• Tài sản: **>100B** \| Phí hiện tại: **23M**<br>• Tự quản lý, áp lực nợ ~0, ngại chuyển giao quyền kiểm soát | Chứng minh giá trị gia tăng (Alpha), tư vấn cảnh báo rủi ro, giữ nguyên quyền tự chủ cho KH. |
| **Khách hàng Chưa nhiều vốn** *(High Intent Leads)* | $Y < 3.5$ & $X \ge 3.5$ | • **Low Wallet - High Readiness**<br>• Tài sản: ~20B \| Phí hiện tại: **44M** (Cao nhất)<br>• Động lực đầu tư cực cao, chấp nhận trả phí dịch vụ | Cung cấp sản phẩm chi phí biên thấp, tự động hóa, gói tư vấn linh hoạt. |
| **Khách hàng Nuôi dưỡng** *(Incubation Leads)* | $Y < 3.5$ & $X < 3.5$<br>*(Thỏa $ICS \ge 3.0$ hoặc Tuổi $\le 35$)* | • **Growth Potential**<br>• Tài sản: ~45B \| Phí hiện tại: **43M**<br>• Khách hàng trẻ/mới đầu tư, có kiến thức tốt nhưng chưa tích lũy đủ | Giáo dục thị trường, sản phẩm tích lũy vốn nhỏ, đồng hành dài hạn. |
| **Khách hàng Không đủ năng lực** *(Low Capacity)* | $Y < 3.5$ & $X < 3.5$<br>*(Không thỏa Incubation)* | • **Low Wallet - Low Readiness**<br>• Tài sản: ~15B \| Phí hiện tại: 1M<br>• Ít quan tâm, chất lượng dữ liệu/sự phù hợp thấp | Hạn chế đầu tư nguồn lực bán hàng trực tiếp. |

---

## 5. Phát Hiện Cốt Lõi & Insight Chi Tiết

### 5.1. Nghịch lý AUM vs Doanh thu phí
* **Nhóm Tự chủ đầu tư (Chiến lược):** Cầm hơn **100 tỷ VNĐ tài sản nhàn rỗi** nhưng chỉ đóng góp **23 triệu VNĐ phí**. Họ có chi tiêu thấp (~0.4B), nghĩa vụ nợ gần như bằng 0. Do không bị áp lực tài chính ngắn hạn, họ không có động lực cấp bách để đổi mới phương thức quản lý tài sản.
* **Nhóm Chưa nhiều vốn & Nuôi dưỡng:** Dù tài sản nhỏ hơn nhiều (20B - 45B) nhưng đóng góp doanh thu phí lớn nhất (**44 triệu** và **43 triệu VNĐ**). Áp lực tài chính và nhu cầu tối ưu hóa dòng tiền khiến họ sẵn sàng trả phí cho các giải pháp tư vấn chuyên sâu.

### 5.2. Hành vi tự quản lý & Tâm lý bảo toàn vốn
* **Thích tự chủ:** `261/392` người chọn *Tự nghiên cứu / cảm tính cá nhân*, so với `54/392` chọn chuyên viên ngân hàng/chứng khoán.
* **Ủy thác cực kỳ thấp:** Hơn **90%** chọn hình thức tự thực hiện (hoặc tự thực hiện có tham khảo khuyến nghị). Chỉ có số ít chọn ủy thác hoàn toàn.
* **Loss Aversion (Tâm lý e ngại thua lỗ):** Khi thị trường giảm 15%, `104` người chọn "Tạm dừng, theo dõi" và `74` người chọn "Bán bớt để bảo toàn", thay vì vội vã tháo chạy. Đây là sự *kiên nhẫn có điều kiện* nếu được giải thích nguyên nhân rõ ràng.

### 5.3. Mô hình phí & Mức phí chấp nhận
* **Ưu tiên phí gắn liền với hiệu quả:** 
  * `101 người` chọn **Phí theo % hiệu quả đầu tư**
  * `96 người` chọn **Miễn phí cơ bản + Trả phí tư vấn nâng cao (Freemium)**
  * Chỉ `22 người` chọn Phí cố định hàng tháng hay Phí % trên tổng tài sản (AUM Fee).
* **Độ nhạy cảm phí theo quy mô vốn:**
  * Khoản đầu tư `< 10 triệu VNĐ`: 64% chỉ chấp nhận phí `< 0.5%/năm`.
  * Khoản đầu tư `> 200 triệu VNĐ`: Gần **70%** sẵn sàng trả mức phí từ `0.5%` đến `> 2%/năm`.

### 5.4. Phân hóa theo độ tuổi
```
  [ < 25 Tuổi ]    ──────► Tỷ lệ "Không đủ năng lực" cao (40%). Khao khát kiến thức. 
                           Cần: Micro-investing, tư vấn tự động.

  [ 26 - 55 Tuổi ] ──────► Giai đoạn Tích lũy & Tự chủ. Chi tiêu & Nợ cao hơn.
                           Cần: Tối ưu dòng tiền, Danh mục Tăng trưởng, Phí theo hiệu quả.

  [ > 55 Tuổi ]    ──────► 44.3% chuyển thành Khách hàng Ưu tiên. Bảo toàn tài sản.
                           Cần: Quản trị rủi ro chuyên sâu, dịch vụ chuyên gia 1-1.
```

---

## 6. Rào Cản Chuyển Đổi & Chiến Lược Đề Xuất

### 3 Rào cản hàng đầu khiến khách hàng chưa xuống tiền:
1.  **Thiếu định hướng phân bổ tài sản:** 97 người không biết chia tiền ra sao cho hợp lý.
2.  **Thiếu kế hoạch tài chính rõ ràng:** 90 người gặp khó khăn trong việc lập mục tiêu dài hạn.
3.  **Quá tải thông tin:** 89 người hoang mang, không biết nên tin vào nguồn thông tin nào.

### Điều kiện tiên quyết để chuyển đổi (Prerequisites):
*  **277 người** yêu cầu *Minh bạch pháp lý, điều khoản và chi phí*.
*  **150 người** yêu cầu *Minh bạch rủi ro danh mục*.
*  **137 người** yêu cầu *Khả năng rút tiền linh hoạt (Liquidity)*.

###  Đề xuất chiến lược hành động:
> **Thấu hiểu cốt lõi:** Khách hàng không tìm kiếm dịch vụ "làm thay hoàn toàn", họ cần một **"Công cụ hỗ trợ ra quyết định"** giúp nâng cao hiệu quả đầu tư mà vẫn giữ trọn quyền kiểm soát.

1. **Khách hàng Chiến lược / Tự chủ:** Bán giải pháp phân tích cảnh báo rủi ro, công cụ đề xuất tự động. Áp dụng mô hình phí theo hiệu quả (Performance-based Fee) để giảm rào cản ban đầu.
2. **Khách hàng Chưa nhiều vốn & Nuôi dưỡng:** Đẩy mạnh các gói sản phẩm tích lũy an toàn, danh mục tăng trưởng đa dạng hóa, bắt đầu từ số vốn nhỏ, kết hợp đào tạo quản lý tài chính.
3. **Khách hàng Ưu tiên (Lớn tuổi):** Cung cấp dịch vụ ủy thác an toàn, bảo toàn vốn, quản trị rủi ro chuyên sâu đi kèm với tư vấn 1-1 từ chuyên gia.

---

## 7. Cấu Trúc Mã Nguồn & Hướng Dẫn Chạy

###  Cấu trúc thư mục:
```bash
.
├── data/
│   └── survey_data_392.csv          # Dữ liệu khảo sát mức độ sẵn sàng sản phẩm
├── notebooks/
│   ├── 1_Doanh_thu_tiem_nang.ipynb  # Tính toán chỉ số tài chính, kỳ vọng doanh thu
│   └── 2_Xu_ly_Phan_khuc_KH.ipynb   # Chuẩn hóa chỉ số, chạy ma trận Capability-Readiness
├── reports/
│   └── BÁO CÁO PHÂN TÍCH TỆP KHÁCH HÀNG TIỀM NĂNG.pdf
└── README.md                        # Tài liệu hướng dẫn dự án
```

###  Hướng dẫn thực thi:
1. **Cài đặt môi trường:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
2. **Chạy các Notebook phân tích:**
   * Mở Jupyter Notebook và thực thi theo thứ tự:
     1. `notebooks/1_Doanh_thu_tiem_nang.ipynb`
     2. `notebooks/2_Xu_ly_Phan_khuc_KH.ipynb`

---

*Dự án Phân tích Dữ liệu Khảo sát Mức độ Sẵn sàng Sản phẩm Mới.*
