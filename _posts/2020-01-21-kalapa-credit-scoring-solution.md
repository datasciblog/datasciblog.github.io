---
layout: single
title:  "Kalapa Credit Scoring - #17 Solution, 0.22737 Gini Score"
date:   2020-01-21
permalink: /2020/01/21/kalapa-credit-scoring-solution/
excerpt: ""
categories: 
- Projects
tags:
- lightGBM
- competition
classes: wide
# toc: true
# toc_label: "Table of Contents"
# toc_icon: "cog"
---

# Giới thiệu
Dưới đây là lời giải của mình cho cuộc thi [Kalapa's Credit Scoring Challenge](https://challenge.kalapa.vn/regulations.html). Lời giải này đã đưa mình lên vị trí thứ 17 vào ngày 21/01/2020. Đây cũng là lần đầu tiên mình tham gia một cuộc thi về dữ liệu như thế này nên mọi thứ mình làm đều là các bước tiếp cận cơ bản, phù hợp với các bạn mới, muốn xây dựng một baseline model.

# EDA
Mình có một số quan sát thú vị đối với bộ dữ liệu như sau:
- Một số numerical features có chứa các giá trị -1, nên mình dự đoán dữ liệu này đã được BTC impute missing values trước đó. Rồi thêm một bước loại bỏ để tạo missing values mới. 
- Nhiều features có số lượng missing values giống hệt nhau như FIELD_3,4,5,6 hay FIELD16,21,22,50,51,52,53,54,55,56,57. 
- Các features FIELD_50,51,52,53 có giá trị trung bình giống nhau.
- FIELD_50,52,53 là 3 features có các bộ giá trị min, 25th percentile, 50th percentile và 75th percentile bằng nhau.

# Feature Engineering

Mình xác định có 3 dạng features cần xử lý theo các cách thức khác nhau.

1. Categorical và Boolean

    cat_features = ['province', 'district', 'maCv',
                    'FIELD_7', 'FIELD_8', 'FIELD_9',
                    'FIELD_10', 'FIELD_13', 'FIELD_17', 
                    'FIELD_24', 'FIELD_35', 'FIELD_39', 
                    'FIELD_41', 'FIELD_42', 'FIELD_43', 
                    'FIELD_44']
    
    bool_features = ['FIELD_2', 'FIELD_18', 'FIELD_19', 
                     'FIELD_20', 'FIELD_23', 'FIELD_25', 
                     'FIELD_26', 'FIELD_27', 'FIELD_28', 
                     'FIELD_29', 'FIELD_30', 'FIELD_31', 
                     'FIELD_36', 'FIELD_37', 'FIELD_38', 
                     'FIELD_47', 'FIELD_48', 'FIELD_49'

2. Numerical

    num_features = [col for col in all_data.columns if col not in cat_features+bool_features]

## Categorical & Boolean Features

### Missing and None values

- **NaN/na** values: Đối categorical features, mình tạo một feature đếm tổng số giá trị NaN/na trên từng dòng.
- **None** values: Tương tự như NaN/na ****values, mình tạo một feature tính tổng số giá trị None trên từng dòng.

### Categorical features với nhiều hơn 10 unique values

- Mình dùng kỹ thuật **Count Encoding** cho mỗi feature.

### Categorical features với ít hơn 10 unique values + Boolean features

- Mình sử dụng kỹ thuật **Count Encoding** và **One-hot Encoding** cho mỗi feature.

### Ordinal categorical features

- Có 5 categorical features với giá trị là text nhưng mang ý nghĩa thứ tự (ví dụ: Zero, One, Two, Three, A,B, C, D...) nên mình chuyển sang dạng số cho từng feature.

Kết quả là mình đã có 191 features mới sau khi thực hiện hết các kỹ thuật trên.

## Numerical Features

- **age_mean**: Mình tạo thêm một feature mới là **age_mean**, so sánh giá trị của **age_source1, age_source2** với nhau, giống nhau thì giữ nguyên, khác nhau thì lấy giá trị trung bình. Loại bỏ các giá trị tuổi với nhỏ hơn 18, coi như là missing values.
- Toàn bộ giá trị **None** mình mã hóa thành -2
- Một số numerical features chứa giá trị nhiễu như 'HT' 'GD', '02 05 08 11',... mình mã hóa thành -1
- Với mỗi numerical features chứa missing values, mình tạo một boolean feature tương ứng để biểu thị việc thiếu thông tin này.
- Cuối cùng, với mỗi feature mình impute missing values bằng cả 3 phương pháp: constant value (-1), median và mean.

Kết quả của các bước trên, mình có thêm 88 features mới.

## Label Mean Features

- Mình dùng thư viện scikit-learn để tạo các features mới là giá trị label trung bình của 500 đến 5000 nearest neighbors cho mỗi dòng.
- Đây là những features quan trọng nhất giúp model của mình tăng đến 0.2 Gini score.

# Modelling

- Mình dùng LightGBM + 5-fold CV với bộ features, mô hinh bị overfitting nhẹ. Validation score của mình rất cao, từ 0.25-0.4 nhưng điểm số đạt được tối đa trên LB là **0.21642**.
- Đưa bộ features trên lên AutoML, mình đạt được điểm số **0.22449**.
- Sau khi chạy nhiều lần LightGBM với các bộ hyperparameters khác nhau, mình lựa chọn một số file kết quả có điểm Gini > 0.21, cộng thêm file kết quả từ AutoML. Tính giá trị trung bình từ các file này, Gini score của mình tăng thêm một chút, đạt **0.22737**.
- 0.22737 hiện tại là kết quả tốt nhất của mình.