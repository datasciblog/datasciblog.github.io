---
layout: single
title:  "Kalapa's Credit Scoring Challenge - #13 Solution, 0.2729 Gini Score"
date:   2020-02-10
permalink: /2020/02/10/kalapa-credit-scoring-solution-13/
excerpt: ""
categories: 
- Competitions
tags:
- lightGBM
- competition
- credit scoring
classes: wide
# toc: true
# toc_label: "Table of Contents"
# toc_icon: "cog"
---
<div class="notice--info">

This was my second solution for the <a href="https://challenge.kalapa.vn/">Credit Scoring Challenge</a> hosted by <a href="https://kalapa.vn/en/home-en/">Kalapa</a> with the first prize is up to AUD$6000. After the first solution was <a href="https://datasciblog.github.io/2020/01/21/kalapa-credit-scoring-solution-17/">published</a> and get some credit, I kept improving my baseline and achieved a better result. 

The post was originally written in Vietnamese and published on <a href="https://forum.machinelearningcoban.com/t/kalapa-s-credit-scoring-challenge-13-solution-02-02-0-2729-gini-score/7139"> the largest machine learning forum in Vietnam</a>. The English version of this post will come soon!

</div>

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-10-kalapa-credit-scoring-solution-13/3.png?raw=true">
</figure>

# Giới thiệu

Dưới đây là lời giải phần 2 của mình cho cuộc thi [Kalapa’s Credit Scoring Challenge](https://challenge.kalapa.vn/) với nhiều thay đổi trong **Feature Engineering** và **Modelling** kể từ lời giải [phần 1](https://forum.machinelearningcoban.com/t/kalapas-credit-scoring-challenge-17-solution-21-01-0-22737-gini-score/7071). Lời giải này đã đưa mình lên vị trí thứ 13 vào ngày 02/02/2020 với Gini Score 0.2729.

# Data Preprocessing

- `province` Xử lý vấn đề "bất nhất" trong tên tỉnh thành

        df.replace('Tỉnh Hòa Bình', 'Tỉnh Hoà Bình', inplace=True)
        df.replace('Tỉnh Vĩnh phúc', 'Tỉnh Vĩnh Phúc', inplace=True)

- `maCv` Gom nhóm các mã công việc tương đồng. Ví dụ: toàn bộ các mã công việc *'Công nhân', 'công nhân', 'Công nhân mài ngồi', 'Công nhân kỹ thuật điện'* được đưa về cùng một nhóm **'Công nhân'**. Xử lý tương tự cho 'Nhân viên', 'Giáo viên', 'Lái xe', etc.
- `FIELD_9` Đây rõ ràng là một categorical feature chứa các giá trị là một cặp chữ cái như DN, GD, TN,... Vậy nên mình loại bỏ toàn bộ các giá trị nhiễu như 'na', 75, 80, 86, 79,... coi như missing values.
- `FIELD_12` Tương tự như FIELD_9, mình loại bỏ các giá trị nhiễu như GD, DK, XK,... coi như missing values
- `age_source1`, `age_source2` Mình tạo một feature mới tên `age`, chỉ giữ lại giá trị mà `age_souce1 == age_source2`. Còn lại coi như missing values.
- `FIELD_3` Do feature này chứa rất nhiều giá trị -1 nên mình đoán đây là missing values đã được BTC xử lý trước đó. Mình đưa các giá trị này ngược trở lại thành missing values.

# Feature Engineering

### 1. Categorical Features

    cat_features = ['province', 'district', 'maCv',
                    'FIELD_7', 'FIELD_8', 'FIELD_9',
                    'FIELD_10', 'FIELD_13', 'FIELD_17', 
                    'FIELD_24', 'FIELD_35', 'FIELD_39', 
                    'FIELD_41', 'FIELD_43', 'FIELD_44']

- `_isnull` Đối với mỗi feature, mình tạo thêm một boolean feature tương ứng để thể hiện các missing values.
- Tạo thêm một feature đếm tổng số missing values ở mỗi dòng
- Tạo thêm một feature đếm tổng số 'None' values ở mỗi dòng
- Mình fill toàn bộ missing values với giá trị 'Missing'
- Cuối cùng mình dùng kỹ thuật **count encoding** cho từng feature
- Đối với `FIELD_7`, mình tạo thêm một feature `FIELD_7_element_count` đếm số phần tử trong mỗi giá trị của feature này. Mình tạo thêm các boolean feature như `FIELD_7_AT`,  `FIELD_7_TL` để thể hiện việc AT, hay TL xuất hiện trong giá trị `FIELD_7`.
- Riêng với các features `['FIELD_8', 'FIELD_10', 'FIELD_17', 'FIELD_24', 'FIELD_35', 'FIELD_41', 'FIELD_43', 'FIELD_44']` mình dùng thêm kỹ thuật One-hot encoding để tạo các features mới
- Với ordinal features như `['FIELD_35', 'FIELD_41', 'FIELD_43', 'FIELD_44']` mình chuyển các giá trị như A, B, C, D hay I, II, III, IV về dạng số, Missing → -999, None → -1

## 2. Boolean Features

    bool_features = ['FIELD_1', 'FIELD_2', 'FIELD_12', 'FIELD_14', 
                     'FIELD_15', 'FIELD_18', 'FIELD_19', 'FIELD_20', 
                     'FIELD_23', 'FIELD_25', 'FIELD_26', 'FIELD_27', 
                     'FIELD_28', 'FIELD_29', 'FIELD_30', 'FIELD_31', 
                     'FIELD_32', 'FIELD_33', 'FIELD_34', 'FIELD_36', 
                     'FIELD_37', 'FIELD_38', 'FIELD_42', 'FIELD_46', 
                     'FIELD_47', 'FIELD_48', 'FIELD_49']

- Tương tự như trên, mình tạo các features `_isnull`, `_mising_count`, `_none_count`
- True, TRUE → 1
- False, FALSE → 0
- Missing values → -999
- None values → -1

## 3. Numeric Features

- Tương tự như trên, mình tạo các features `_isnull`, `_mising_count`, `_none_count`
- Mình impute missing values bằng cả 3 phương pháp: -999, median, mean

## 4. Mean Label Features

- Như đã nói ở phần 1, việc tạo thêm một feature với giá trị 'label mean' của K-nearest neighbors đã giúp mình cải tiến mô hình nhiều nhất. Sau đây là một số kinh nghiệm mình rút ra được khi tạo feature này.
    - Sau khi chạy LightGBM với bộ feature đang có, mình xác định 10 features quan trọng nhất dựa trên điểm số importance scores. Mình dùng 10 features này để tính toán K-nearest neighbors.
    - Điểm quan trọng nhất mà mình đã quên làm trong bài hướng dẫn lần trước là "**scaling**". Mình dùng MinMaxScaler với min=0 và max=1 cho 10 features trên trước khi tính toán KNNs.
    - Sau khi thử các giá trị K khác nhau từ 500 đến 5000, K=1000 cho mình feature tốt nhất.

# Feature Selection

- Một trong những việc mình chưa làm trong bài hướng dẫn trước là feature selection. Việc loại bỏ các features không quan trọng giúp tiết kiệm thời gian huấn luyện mô hình, tránh overfitting để cải thiện điểm số trên LB.
- Ở phần này, mình tìm các cặp features có correlation = 1, bỏ 1 giữ lại 1.
- Mình tiếp tục tính correlation của từng feature với label. Các features trả về giá trị `NaN` mình cũng loại bỏ đi.
- Số lượng features còn lại là 197, mình tạm dừng feature selection tại đây

# Modelling

- Thời điểm hiện tại, mình vẫn chỉ dùng LightGBM + Stratified 5-Fold CV để huấn luyện mô hình.
- Điểm quan trọng nhất mình quan sát được đó là điểm số trên LB phụ thuộc rất lớn vào giá trị `random_state` khi mình tạo StratifiedKFold.
    - Sau khi thử một vài giá trị, mình đánh giá một `random_state` tốt sẽ cho mình điểm số Gini Score trung bình cao (>0.26) với Standard Deviation thấp (<0.03).
    - Mình tìm ra được giá trị `random_state` tốt nhất bằng cách chạy LightGBM với `random_state` từ 1000 đến 25,000. Điều này đồng nghĩa với việc mình đã train 24,000 x 5 = 120,000 mô hình LightGBM. Mình sử dụng nguồn tài nguyên tính toán (10 CPUs) của Kaggle để làm việc này. Dưới đây là mô hình giúp mình đạt điểm số **0.2579**, đưa mình lên vị trí 21 trong ngày 01/02/2020.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-10-kalapa-credit-scoring-solution-13/1.png?raw=true">
</figure>

- Từ mô hình tốt nhất này, mình nhận ra validation score của fold 3 rất thấp (0.2425). Và vì kết quả cuối cùng mà mình có là giá trị probability trung bình của 5 mô hình được huấn luyện trên 5 folds, vậy nếu mô hình số 3 là một mô hình "tồi" thì kết quả trung bình kia sẽ bị ảnh hưởng nghiêm trọng. Do đó mình đã loại bỏ mô hình số 3, chỉ lấy probability trung bình của 4 mô hình còn lại. Gini Score trên LB của mình tăng lên **0.26559**.
- Mình tiếp tục thử nghiệm và loại bỏ lần lượt các mô hình còn lại, chỉ giữ lại mô hình số 4 với validation score cao nhất (0.3135). Điểm số trên LB của mình lúc này tăng lên **0.2729** đưa mình lên vị trí thứ 13 trên bảng xếp hạng.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-10-kalapa-credit-scoring-solution-13/2.png?raw=true">
</figure>

# What's next?

- Mình sẽ tiếp tục tìm hiểu các kỹ thuật để cải tiến mô hình hiện có thông qua khóa học này trên Coursera: [How to Win a Data Science Competition: Learn from Top Kagglers](https://www.coursera.org/learn/competitive-data-science).
- Tham khảo các mô hình chiến thắng trên Kaggle để tìm ra ý tưởng về Feature Engineering và Modelling.