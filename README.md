# 🔍 Web App Dự Báo Gian Lận Báo Cáo Tài Chính (Beneish M-Score & Logistic Regression)

Ứng dụng web tương tác hỗ trợ phân tích, đánh giá và dự báo nguy cơ **Gian lận Báo cáo Tài chính (BCTC)** của các doanh nghiệp dựa trên **8 chỉ số Beneish M-Score** và mô hình học máy **Logistic Regression**. 

Ứng dụng được xây dựng trên nền tảng **Streamlit** (Python), cho phép phân tích trực quan dữ liệu, đánh giá độ chính xác của mô hình và đưa ra dự báo rủi ro cho từng công ty đơn lẻ hoặc danh mục nhiều doanh nghiệp hàng loạt.

---

## 🌟 Tính Năng Nổi Bật

1. **📊 Khám phá & Trực quan hóa Dữ liệu (EDA)**:
   - Thống kê mô tả chi tiết 8 chỉ số Beneish (`DSRI`, `GMI`, `AQI`, `SGI`, `DEPI`, `SGAI`, `TATA`, `LVGI`).
   - Ma trận tương quan (Correlation Matrix) giữa các chỉ số và trạng thái gian lận (`FRAUD_FLAG`).
   - Biểu đồ Boxplot so sánh phân bố chỉ số giữa nhóm doanh nghiệp gian lận (1) và không gian lận (0).

2. **🤖 Huấn luyện & Đánh giá Mô hình Logistic Regression**:
   - Cho phép điều chỉnh tỷ lệ chia tập Train/Test (ví dụ: 80/20) và ngưỡng quyết định (Decision Threshold).
   - Tự động chuẩn hóa dữ liệu với `StandardScaler` trong Pipeline để đảm bảo độ chính xác.
   - Đánh giá toàn diện mô hình qua các chỉ số: **Accuracy, Precision, Recall / Sensitivity, Specificity, F1-Score, FPR, FNR**.
   - Trực quan hóa **Ma trận nhầm lẫn (Confusion Matrix)** và biểu đồ hệ số $\beta$ (Odds Ratio).
   - **Xuất báo cáo kết quả ra file Excel (`Logistic_Regression_MScore_Results.xlsx`)**.

3. **🏢 Dự báo Nguy cơ Gian lận cho 1 Công ty Cụ thể**:
   - Nhập nhanh 8 chỉ số tài chính tính toán từ BCTC.
   - Tính toán xác suất gian lận (%) bằng mô hình Logistic Regression.
   - Đánh giá song song với **Công thức Beneish M-Score gốc** ($M > -1.78$).
   - Đưa ra cảnh báo chi tiết từng chỉ số có sự biến động bất thường.

4. **📁 Dự báo Hàng loạt (Batch Prediction)**:
   - Tải lên file CSV chứa dữ liệu của nhiều doanh nghiệp.
   - Tự động tính toán xác suất gian lận, điểm M-Score và xuất danh sách phân loại rủi ro.
   - Tải xuống kết quả phân tích dưới dạng file CSV.

---

## 📁 Cấu Trúc Thư Mục Dự Án

```text
.
├── app.py                              # File ứng dụng chính (Streamlit Web App)
├── MScore_data.csv                     # Tập dữ liệu mẫu (8 biến Beneish + FRAUD_FLAG)
├── requirements.txt                    # Danh sách các thư viện Python cần cài đặt
├── README.md                           # File hướng dẫn chi tiết dự án
└── logistic_regression_mscore_colab.py  # Mã nguồn gốc chạy trên Google Colab
```

---

## 📐 8 Biến Beneish M-Score Được Sử Dụng

| Tên biến | Chỉ số | Mô tả chi tiết & Ý nghĩa kế toán |
| :--- | :--- | :--- |
| **DSRI** | Days Sales in Receivables Index | Tỷ lệ số ngày thu tiền khách hàng. DSRI > 1 phản ánh khoản phải thu tăng nhanh hơn doanh thu (dấu hiệu ghi nhận doanh thu sớm hoặc doanh thu ảo). |
| **GMI** | Gross Margin Index | Tỷ lệ lãi gộp năm trước so với năm nay. GMI > 1 cho thấy tỷ lệ lãi gộp suy giảm, làm tăng áp lực thao túng lợi nhuận. |
| **AQI** | Asset Quality Index | Chỉ số chất lượng tài sản (tỷ lệ tài sản phi tiền tệ & phi TSCĐ hữu hình). AQI > 1 thể hiện việc tăng vốn hóa chi phí vào tài sản. |
| **SGI** | Sales Growth Index | Tỷ lệ tăng trưởng doanh thu. SGI > 1 phản ánh tăng trưởng cao; doanh nghiệp tăng trưởng nóng dễ chịu áp lực duy trì kết quả kinh doanh. |
| **DEPI** | Depreciation Index | Chỉ số khấu hao. DEPI > 1 phản ánh tỷ lệ khấu hao giảm (kéo dài thời gian khấu hao để làm tăng lợi nhuận báo cáo). |
| **SGAI** | Sales, General & Admin Expenses Index | Chỉ số chi phí bán hàng và QLDN trên doanh thu. SGAI > 1 cho thấy hiệu quả quản lý chi phí giảm. |
| **TATA** | Total Accruals to Total Assets | Chỉ số dồn tích trên tổng tài sản. TATA cao phản ánh lợi nhuận báo cáo đến từ dồn tích kế toán thay vì dòng tiền thực tế. |
| **LVGI** | Leverage Index | Chỉ số đòn bẩy tài chính (Tổng nợ / Tổng tài sản). LVGI > 1 cho thấy rủi ro tài chính và nghĩa vụ nợ tăng cao. |

---

## 🚀 Hướng Dẫn Cài Đặt & Chạy Cục Bộ (Local)

### 1. Yêu cầu hệ thống
- Python 3.9 trở lên.

### 2. Cài đặt các thư viện phụ thuộc
Mở Terminal hoặc Command Prompt tại thư mục dự án và chạy lệnh:

```bash
pip install -r requirements.txt
```

### 3. Chạy ứng dụng Streamlit
Chạy lệnh sau để khởi chạy ứng dụng web:

```bash
streamlit run app.py
```

Sau khi chạy lệnh, trình duyệt của bạn sẽ tự động mở địa chỉ: `http://localhost:8501`.

---

## 🌐 Hướng Dẫn Đẩy Lên GitHub & Deploy Lên Streamlit Cloud

Để đưa ứng dụng này lên mạng cho mọi người truy cập miễn phí thông qua **Streamlit Community Cloud**, bạn thực hiện các bước sau:

### Bước 1: Khởi tạo và Đẩy code lên GitHub
1. Tạo một Repository mới trên GitHub (ví dụ đặt tên: `financial-fraud-detection-app`).
2. Mở Terminal tại thư mục dự án và chạy các lệnh:
   ```bash
   git init
   git add app.py requirements.txt MScore_data.csv README.md
   git commit -m "Initial commit for Financial Fraud Detection Streamlit App"
   git branch -M main
   git remote add origin https://github.com/TÊN_GITHUB_CỦA_BẠN/financial-fraud-detection-app.git
   git push -u origin main
   ```

### Bước 2: Deploy lên Streamlit Cloud
1. Truy cập vào trang [Streamlit Community Cloud](https://share.streamlit.io/) và đăng nhập bằng tài khoản GitHub của bạn.
2. Bấm vào nút **"New app"**.
3. Điền các thông tin:
   - **Repository**: Chọn `TÊN_GITHUB_CỦA_BẠN/financial-fraud-detection-app`
   - **Branch**: `main`
   - **Main file path**: `app.py`
4. Nhấn nút **"Deploy!"**.
5. Đợi 1-2 phút để Streamlit Cloud tự động cài đặt thư viện từ `requirements.txt` và khởi chạy web app của bạn.

---

## 📝 Tác Giả & Bản Quyền

- Dự án được phát triển dựa trên lý thuyết 8 biến **Beneish M-Score** (Messod Beneish, 1999) và mô hình phân loại **Logistic Regression**.
- Đơn vị sử dụng: Nghiên cứu phân tích tài chính & Kiểm toán.
