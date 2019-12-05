---
layout: single
title:  "What Was Happening in Data Science?"
date:   2019-12-05
permalink: /2019/12/05/what-was-happening-in-data-science/
categories: 
- Data Visualisation
tags:
- Kaggle
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# 1. Introduction

What's happening in Data Science? Hundreds of students in Monash who are working hard with their Master Degree in the field may ask. Whether all the subjects they are taking and skills they are developing will be sufficient? Will 100K salary for a graduated data scientist be realistic? Are there any difficulties for women in the field? And especially, how active the community in Australia is? It is probably hard to answer all these kinds of questions without data, quality data.

Fortunately, in the two year 2017 and 2018, Kaggle - the most well known data science platform - made an annual large scale survey in order to collect a comprehensive dataset on "the state of ML and data science" from thousands of data analysts, data scientists, machine learning practitioners, etc. around the world. By diving deeply into the data, questions will be answered, insights will be revealed and stories will be narrated.

## 1.1. Survey Methodology

To understand the nature of data, let's have a look at the survey methodology of the recent year (Kaggle, 2018):

- The survey received 23,859 usable respondents from 147 countries and territories. Countries or territories received less than 50 respondents were grouped into a group named "Other" for anonymity.

- Respondents who were flagged by the survey system as "Spam" were excluded from the data. Most of respondents were found primarily through Kaggle channels, like email list, discussion forums and social media channels.

- The survey was live from October 22nd to October 29th. Respondents were allowed to complete the survey at any time during that window. The median response time for those who participated in the survey was 15-20 minutes.

- Not every question was shown to every respondent. Details about the different segments used are in the schema.csv file.

- To protect the respondents' identity, the answers to multiple choice questions have been separated into a separate data file from the open-ended responses. The key to match up the two files is not provided. Further, the free form responses have been randomized column-wise such that the responses that appear on the same row did not necessarily come from the same survey-taker.

## 1.2. Questions and Motivation

The primary goal of this report is to produce a comparison between the state of Data Science in 2017 and the following year 2018 and to see how things have changed during one year in a fast growing field.

During the exploration, these are main interests from which questions will be derived:

- Gender
- Age
- Country
- Degree
- Tool/Library
- Salary

There will be a specific question that the author is particularly interested in, which is *"How students' performance in mathematics in a country correlates with the development of its data science community?"*.

## 1.3. Data Sources

- [Kaggle Machine Learning & Data Science Survey 2017](https://www.kaggle.com/kaggle/kaggle-survey-2017)
- [2018 Kaggle ML & DS Survey]( https://www.kaggle.com/kaggle/kaggle-survey-2018) 
- [Mathematics performance (PISA)]( https://data.oecd.org/pisa/mathematics-performance-pisa.htm)
- [World population](https://data.worldbank.org/indicator/SP.POP.TOTL)


## 1.4. Tools and Libraries

Since the convenience of R programming language in multiple purposes such as data wrangling, checking, visualizing and writing documents, all the tasks in the report are accomplished using R and its built-in and third-party libraries as well.

Libraries used include:

- readr: Data structure
- dplyr: Data manipulation
- stringr: Data manipulation
- forcats: Data manipulation
- tibble: Data wrangling
- tidyr: Data wrangling
- ggplot2: Visualisation
- highcharter: Visualisation
- countrycode: Visualisation
- scales: Visualisation

# 2. Data Wrangling

The main purpose of this report is to produce the comparison based on the Kaggle datasets of two years, therefore, several columns in the year 2018's data are adjusted in terms of its name and domains in order to match with the corresponding columns of 2017's data.

We now have a number of mutual columns with the same domains (sets of values) in both datasets and also some columns in the 2018's dataset only:

- GenderSelect: Male, Female, Other, Prefer not to say
- Country: United States, United Kingdom, Australia, China, India, Vietnam, ect.
- Age: 18-21, 22-24, 25-29,... , 70-79, 80+
- FormalEducation: PhD, Master, Bachelor, Professional, etc.
- MajorSelect: Computer Science, Engineering, Mathematics/Statistics, etc.
- MostLanguageSelect / MostVizLibrarySelect / MostMLFrameworkSelect (2018 only)
- CompensationAmount (2018 only)

# 3. Data Checking

There are 228 columns with 16,716 instances in the 2017 Kaggle dataset. 396 columns and 23,859 instances are found in the other data. Derived from systematic surveys and be processed beforehand, the two datasets are relatively clean and already to be explored. Though, most of columns have many NAs, we may simply ignore or make some visualisation of them.

The Mathematics performance and World population data are totally clean.

# 4. Data Exploration

## 4.1. Overall

<figure class="third">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/1.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/2.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/3.png?raw=true">
</figure>

Data Science is one of the fastest-growing jobs of 2018, as CNBC reported.

According to the 2018 reviewing, there were a sigificant increase of 1.1 million people who get involved in the new field during only one year. Kaggle ended the year with around 2.5 million members, up from 1.4 million in 2017. There were 1.55 million registered users visit Kaggle in 2018, almost double from 895 thousand in 2017.

The number of survey-takers, as a result, also extended from around 17,000 of people to almost 24,000. However, the increase is only 42.7% which is relatively lower than a 78.6% increase in the total number of Kaggle users.

## 4.2. Gender and Age

### 4.2.1. Gender

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/4.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/5.png?raw=true">
</figure>

After one year, there were still hundereds of people do not want to declare their gender. While the number of male and female participants was up, people with other gender were less willing to take the survey.

The survey showed that the proportion of female respondents slightly increased from 16.62% to 16.81% over one year and the proportion of male was almost stable. In general, the gender distribution did not change much. There was still a great gender imbalance in this field.

### 4.2.2. Age

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/6.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/7.png?raw=true">
</figure>

The age distributions showed that respondents of the 2018 survey seemed to be a lot younger than the previous year. The 18-21 and 22-24 age group saw substantial rises from 7.48% to 12.73% and 14.54% to 21.55%, respectively.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/8.png?raw=true">
</figure>

Most of working-age group saw an increase in the number of survey-takers. The figures for two youngest age groups were more than double after one year, with rises of 142.96% and 111.48%. 

There were slight decreases in the numbers of people aged from 55 to 79 years old. While Data Science seemed to be dominated by young people, surprisingly, the number of respondents aged over 80 was also almost double, from 21 up to 39 with an increase of 85.71%.


### 4.2.3. Age by Gender

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/9.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/10.png?raw=true">
</figure>

Female respondents were relatively younger than male in the year 2017, however, the age distributions for both gender looked more similar when it came to the year 2018.

### 4.2.4. Gender by Age

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/11.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/12.png?raw=true">
</figure>

While the percentages of female in age groups from 18 to 29 decreased, there were higher proportions of female in other age groups. In 2017, there were no female aged over 80 but we could see some in one year later.

## 4.3. Country

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/13.png?raw=true">
</figure>

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/14.png?raw=true">
</figure>

Look at the country distribution of respondents, we could see the domination of United States over two years. However, this may not last long since the communities of India and China are growing very fast.

Most of countries in Africa - the world's second largest and second most-populous continent have not appeared in the Data Science map yet. The three representatives of this continent are South Africa, Nigeria and Kenya.

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/15.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/16.png?raw=true">
</figure>

The list of top 10 countries with most respondents changed slightly ater one year:

- United States and India kept dominating. 
- China replaced Russia to become the third. 
- United Kindom dropped down from 4th to 7th. 
- Australia was out of the list, replaced by Japan.

Although, this is just a part of the big picture. Let's have a look at the speed of growth in different countries.

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/17.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/18.png?raw=true">
</figure>

What happened to Australia? The data science community in this country seemed not to be as strong as their economy in the year 2018 when the number of participants significantly decreased. Philippines followed Australia with a decline of 13.1%.

Meanwhile, top 5 countries with greatest growth are three from Asia and one from Africa. China had more than triple number of respondents after one year.

### 4.3.1. Age by Country

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/19.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/20.png?raw=true">
</figure>

India and China respondents looked a lot younger than those from the US. However, it may be a greate advantage for the US since older usually comes with wiser.

### 4.3.2. Gender by Country

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/21.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/22.png?raw=true">
</figure>

It seemed that United States was doing the best job in terms of gender equality while Japan had the lowest proportion of female participants.

## 4.4. Education

### 4.4.1. Formal Degree

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/23.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/24.png?raw=true">
</figure>

Most of new respondents of the survey had at least Barchelor degree. Especially, the numbers of respondents who obtained a Master degree were highest in both years. In the year 2018, the proportion of people who have a Master degree was up to 45.5% from 37.53% in 2017. Meanwhile, the proportions of people who have PhD or Barchelor remained the same.

### 4.4.2. Major of Degree

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/25.png?raw=true">
</figure>

Computer Science, Mathematics/Statistics, Engineering were the three main majors of participants. In 2018, there were a large amount of new respondents from Business disciplines. Hundered people with environment disciplines also took part in. Computer Science dominated in both years.

### 4.4.3. Degree by Major

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/26.png?raw=true">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/27.png?raw=true">
</figure>

For the top 6 majors of respondents, Physics/Astronomy was the only one in which the number of PhD was higher than the number of Master and Barchelor degree, in both two years.

## 4.5. Tools and Libraries

### 4.5.1. Programming Languages

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/28.png?raw=true">
</figure>

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/29.png?raw=true">
</figure>

In 2017, Python and R were the two programing languages that were recommended most for beginners. Python was voted by 63.11% of respondents, R came in the second with only 24.03% and much lower for other languages.

This was relatively reasonable since Python was picked as the most used language in 2018 by 53.74% of participants followed by R with 13.44% and SQL with 7.96%.

### 4.5.2. Visualisation Libraries

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/30.png?raw=true">
</figure>

The most used libraries used for visualisation in 2018 were Matplotlib for Python with 55.05% and ggplot2 for R with 23.61%. 

### 4.5.3. Machine Learning Frameworks

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/31.png?raw=true">
</figure>

For those who may be interested in working with Machine Learning algorithms, Scikit-Learn took the lead with 46.49%, followed by TensorFlow and Keras.

We could see a pattern here, for all kinds of tools and libraries, the most used ones usually were taken by around 50% of people and totally dominated others.

## 4.6. Salary

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/32.png?raw=true">
</figure>

Just like in many industries, gender inequality also occurred in Data Science. The gender pay gap in this filed was $6,560 last year 2018. The problem was even more extreme in some countries. Let's have a look at the average salaries by gender in Australia, China, India, Russia, United Kingdom and United States.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/33.png?raw=true">
</figure>

There were some points that remarkable here:

- United States was the country paying the highest salaries for both sexes with a gender pay gap of $25,248, followed by Australia and United Kingdom. 

- The amount of money people working in India, China and Russia were paid was relatively small in comparison with the three other coutries.

- The gender pay gap in Australia was $46,171, which was extremely high. Male workers here were paid more than double the amount female were paid.

- Russia and India were doing the best in this problem.

- In India, female were paid even higher than male.

## 4.7. Correlation

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-04-01-what-was-happening-in-data-science-2017-2018/34.png?raw=true">
</figure>

Look at the graph, we can see a positive correlation between mathematics performance Score of students in one country and the activeness of the data science comunity in that country. In particular, the correlation between them was around 64%.

These are some main points:

- Singapore was definitely an outlier for which both mathematics score and the number of respondents per 100K population were remarkably high.

- Greece, United States and Israel were three countries that had low math scores but high activeness.

- Meanwhile, Hong Kong, South Korea and Japan, the three countries from Asia had relatively high mathematics score but low activeness.

# 5. Conclusion

The exploration has answered many questions which were raised at the beginning of the report. These are some main points drawn from it:

- The workforce in Data Science is increasing with a high rate, from 78% each year.

- A half of data workers is under 29 years old. More and more young people are getting involved in the field. 

- There is still a gender gap in this field, 81% is male and 17% is female. Though, female are slightly younger than male.

- There is still a huge gender pay gap in many countries. The problem in Australia is extremely worse than others.

- United States, India and China are the three countries dominating in Data Science in terms of the number of data workers. People in India and China are much younger than people from the United States.

- In order to enter this field, one should have at least Barchelor degree. Most of people working with data have a Master degree.

- Computer Science, Engineering, Mathematics and Business are the main majors of data workers. However, there are many people from other disciplines such as Arts, Humanities, Environmental Science, etc.

- Python and R, Matplotlib and ggplot2, Scikit-Learn are fundamental tools and libraries who want to work with data in the future need to acquire.

- Mathematics performance is a good indicator for the activeness of data science community in a country.

# 6. Reflection

There are so many insights we can draw from the Kaggle datasets in order to understand what is happening inside "the sexiest job of the 21st century". Since a constraint of the length for the report, only several aspects were considered such as gender, age, country, tool, library and salary. As a student who is pursuing a master degree in this field, the author believe that data is the most important asset in businesses today, and by managing and using it in a right and ethical way, significant values will be added.

# 7. References

Kaggle. (2017). Kaggle Machine Learning & Data Science Survey 2017. Retrieved from https<!-- -->://www.kaggle.com/kaggle/kaggle-survey-2017

Kaggle. (2018). 2018 Kaggle ML & DS Survey. Retrieved from    https<!-- -->://www.kaggle.com/kaggle/kaggle-survey-2018

Kaggle. (2019). Reviewing 2018 and Previewing 2019. Retrieved from    http<!-- -->://blog.kaggle.com/2019/01/18/reviewing-2018-and-previewing-2019/

Organisation for Economic Co-operation and Development (OEDC). 2018. Mathematics performance (PISA). Retrieved from https<!-- -->://data.oecd.org/pisa/mathematics-performance-pisa.htm

The World Bank Group. 2017. Population, total. Retrieved from https<!-- -->://data.worldbank.org/indicator/SP.POP.TOTL