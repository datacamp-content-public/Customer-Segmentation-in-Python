# **Customer Segmentation in Python**<br/>by **Karolis Urbonas**

Specs deadline: YYYY-MM-DD

*Please read the [course design process description](http://authoring.datacamp.com/courses/design/)
and complete these steps in the `README.md` file in your course repository.
If you need assistance,
please speak with your Curriculum Lead.*

## Course development resources

* Course admin page: https://www.datacamp.com/teach/
* Authoring documentation: https://authoring.datacamp.com/

## Step 1: Brainstorming

### 1. What problem(s) will students learn how to solve?

- How to break down trends and group customers into comparable cohorts
- How to discover interesting relationships between product purchases
- How to group customers into recency, frequency and monetary value segments
- How to prepare data for clustering
- How to cluster customers into interpretable behavioral segments

### 2. What techniques or concepts will students learn?

*Concepts:*
- Time-based cohorts
- Size-based cohorts
- Behavior-based cohorts
- Association rules mining
- Market basket analysis
- RFM (Recency, Frequency, Monetary value) segmentation
- Clustering
- Kmeans segmentation
- Data normalization and standardization

*Skills/Techniques:*
- Disseminating "vanity" metrics / general trends into more granular cohort view
- Understanding changes in customer behavior over time
- Identifying actionable rules between customer product purchases
- Calculating behavioral customer metrics such as recency, frequency and monetary value
- Correcting for abnormalities in the data to prepare for effective segmentation
- Building meaningful and interpretable customer segments

*Things to leave out:*
- In the beginning I thought of expanding the chapter 4 and including additional models like NMF, GMM, and teaching how to pre-process data with PCA before clustering, but it seems that this in-depth customer segmentation topic would deserve a separate course.
- Some of the Cohort analysis elements might be reduced e.g. behavior-based cohorts to make sure the students spend enough time learning the key concepts of cohort analysis rather than spreading too thin exploring multiple ways of doing it. 

### 3. What technologies, packages, or functions will students use?

Python: pandas, numpy, datetime, matplotlib, seaborn, mlxtend, sklearn.

pandas:
- groupby
- aggregate
- transform
- pivot
- qcut
- sort_values
- sort_index
- assign
- apply

sklearn:
- KMeans
  - fit
  - labels_
  - inertia_
- StandardScaler
- silhouette_score

### 4. What terms or jargon will you define?

cohorts, segmentation, pivoting, rfm, recency, frequency, monetary value, normalization, standardization, kmeans, silhouette score, elbow method, percentile, index, heatmap, retention, cohort index, month offset, acquisition, association rules, support, confidence, lift, basket, market basket analysis, bundle.

### 5. What analogies or heuristics will you use?

Cohort analysis comes from demographics where the population's qualities such as income, education and others are studied based on the date of birth. 

Association rules lets discover "interesting" rules on which products are bought together - we are trying to find more "pairs" of products that are frequently purchased in the same basket which we should promote as a bundle.

Clustering is trying to find customers that are similar to each other within the cluster, and different from others outside of their cluster. It's like trying to identify your hobby and then looking for people with similar activities to bond with. In this case we are trying to group customers by their behaviors to customize service and product offers.

K-means clustering works well with normally-distributed and standardized data, so we will do some simple data preparation to get a meaningful clustering solution.

### 6. What mistakes or misconceptions do you expect?

Understanding which metrics should be used for identifying "interesting" association rules - support, confidence, or lift. Students might be lured to use confidence vs. lift as it is easier to interpret.

How optimal number of clusters cannot be fully identified by mathematical methods - these just give a indication of ranges, but the main decision has to be based on the interpretability of the segments and actionability for the business.

### 7. What datasets will you use?

Original dataset is http://archive.ics.uci.edu/ml/datasets/online+retail but I have pre-processed it to make it smaller, see my git repo - https://github.com/karolisurbonas/cleaning-online-retail-dataset. The pre-processed dataset is still roughly 16 MB - should I try to reduce its size even more? A risk is that I might remove meaningful data.

## Step 2: Who Is This Course for?

Link to [learner personas](https://authoring.datacamp.com/courses/design/personas.html)

* **Mathematical Marta** understands the underpinnings of the association rule mining algorithm, and can easily breakdown the different algorithms and distance methods used for k-means clustering, but now she wants to understand how these methods - together with the more descriptive techniques - can be applied to mine actionable insights into customer behavior.

* **Advanced Alex** has done business analytics and understands the high level concepts. This course will give him edge over his peers by adding a list of actionable and practical techniques to his toolbox, and understanding his business better and being able to make better data-driven decisions. He wants to understand different techniques from a practical business application stand-point and then read more about additional techniques in blogs, and other websites.

* **Starting Sindhu** wants to learn the ways to analyze data better from multiple angles and with different techniques, but she prefers getting a step-by-step hands-on approach where she can run and adjust the code on her own. She will discover highly effective analytic and visual techniques in grouping and segmenting customers, that could be applied in other context. P.S. this assumes Sindhu wants to learn Python, not just R :)

## Step 3: What Will Learners Do Along the Way?

Capstone exercises on the Teach Editor.

### Title of Exercise

For the capstone project, you will use the previously calculated customer behavioral metrics such as tenure, recency, frequency, lifetime spend, and product usage. Then, you will segment the customers based on these attributes, calculate their lifetime value, explore and visualize them, and – most importantly – provide actionable recommendations to your marketing team on how to customize CRM and marketing initiatives.

**Solution**

```
Include the code that you expect the students to write by the end of the course.
It should typically be 2 or 3 lines.
```

### Other Exercises

Write brief descriptions of 10 to 15 more exercises throughout the course.
After this step you should have a clear idea of the flow of the course.

#### Exercise title 1

- Describe the exercise.
- Mention the learning objectives.
- Two or three bullets points is enough.

**Solution**

```
Solution code here.
It should typically be 2 or 3 lines.
```

#### Exercise title 2

- Describe the exercise.
- …

**Solution**

```
Solution code here.
```

## Step 4: How Are the Concepts Connected?

*Remind yourself about [course terminology](https://authoring.datacamp.com/courses/design#terminology-and-structure), then describe the flow of the course.*

[Online-Retail dataset git repo](https://github.com/karolisurbonas/cleaning-online-retail-dataset)


**CHAPTER 1: Market Basket Analysis** (Purpose – Explore Association Rules between products that are purchased together)

[Market Basket Analysis git repo](https://github.com/karolisurbonas/association-rules-mining)

- Lesson 1.1. Introduction to Market Basket Analysis – Introduction to the business problem – understanding products that are being bought together and how to inform company’s marketing department on merchandising / bundling strategies – and how market basket analysis can uncover these association rules. Will present examples of rules.
- Lesson 1.2. Building Association Rules – Introduce the main “apriori” algorithm, import the library in Python and build the rules step by step. Introduce the concepts of antecedants, consequents, support, confidence, and lift.
- Lesson 1.3. Exploring Association Rules – Explore association rules by country, by different customer behavior types (e.g. high spenders, low spenders), and analyze the support, confidence, lift metrics.
- Lesson 1.4. Interpreting Findings – Provide a framework on how to interpret the association rules, pitfalls to watch out for (e.g. high confidence, low lift situation), and best practices in using them to draw actionable conclusions.

**CHAPTER 2: Cohort Analysis** (Purpose – Better understanding of customers based on their unique behavioral attributes)

[Cohort Analysis git repo](https://github.com/karolisurbonas/cohort-analysis)

- Lesson 2.1. Introduction to Cohort Analysis – Will introduce the concept of cohort analysis and its roots in medicine and demographics. Then will preview examples of the powerful visualizations and insights and that will be uncovered with them.
- Lesson 2.2. Types of cohorts – This section will show how to calculate different types of cohorts, and the potential business insights that can be uncovered with each. 
>> Time-based cohorts
>> Segment-based cohorts
>> Behavior-based cohorts
- Lesson 2.3. Calculate cohort metrics – After the cohorts are assigned, this section will show how to calculate and analyze metrics for each of the cohorts such as retention, average spend, frequency, and lifetime value.
- Lesson 2.4. Visualize cohorts and metrics – Learn how to build heatmaps and charts to visualize cohorts and their metrics, and how to interpret them. 

**CHAPTER 3: Recency, Frequency, Monetary Value (RFM) analysis** (Purpose – Learn how to use simple rule-based segmentation to understand and segment the customers)

[RFM and Clustering git repo](https://github.com/karolisurbonas/customer-segmentation-rfm-kmeans)

- Lesson 3.1. Introduction to RFM segmentation – Introduction to the classic rule-based RFM segmentation and how it is being used in ecommerce, retail and other companies up until today, give examples of RFM implementations.
- Lesson 3.2. Calculate RFM values and scores – Calculate RFM values, and present multiple ways to calculate RFM scores (quartile based, Pareto rule, custom business rules).
- Lesson 3.3. Build RFM segments – Using RFM scores, the students will learn how to build RFM segments and analyze the customer base using them.
- Lesson 3.4. Analyze and visualize RFM segments – Learn how to use this segmentation to filter out customers for customized  marketing campaigns, and how to build powerful visualizations to understand RFM segments, and track customer migration between the segments and RFM scores over time.

**CHAPTER 4: Behavioral Customer Segmentation** (Purpose – Use raw RFM metrics to cluster customers into behavioral segments based on their recency, frequency, monetary value and other behavioral attributes)

[RFM and Clustering git repo](https://github.com/karolisurbonas/customer-segmentation-rfm-kmeans)

- Lesson 4.1. Introduction to Clustering for Behavioral Customer Segmentation – Present examples how previous descriptive techniques can be complemented and RFM values used to build customer segments with k-means. Preview the final result, and analyze the output – customer behavioral metrics per each customer segment, and show powerful insights that will be uncovered.
- Lesson 4.2. Clustering Customers using their RFM metrics – Will teach students how to use k-means algorithm to cluster customers based on their RFM and other behavioral data which we derived in previous chapters. 
- Lesson 4.3. Analyzing the Segments – Build a framework and present best practices how segments should be analyzed and interpreted, and how the number of segments (“k” value) can be defined either analytically or based on the business insights. We will explore multiple options and interpret what insights each solution provides.
- Lesson 4.4. Visualizing the Segments – Present best practices in visualizing segments: with charts, and heatmaps, also, discuss creative techniques in naming the segments (highly important to be able to present complex analytic solutions to non-technical business teams).

## Step 5: Course Overview

**Course Description**

The most successful companies today are focused on personalizing their communication with the customers. Data scientists are key to enable this by providing in-depth insights and segmenting the customers. In this course, you will learn real-world techniques on customer segmentation and behavioral analytics. You will start by identifying which products are frequently bought together. Then, you will run cohort analysis to understand the customer trends and uncover valuable insights. Finally, you will calculate Recency, Frequency and Monetary values (RFM), use them to assign RFM scores and run K-means clustering to build customer segments. By the end of the course you will be equipped with real-world customer behavioral analytics and segmentation techniques. 

**Learning Objectives**

- Learn to identify interesting relationships between products bought together
- Learn to evaluate your customer base with cohorts analysis
- Learn to build simple, yet powerful behavioral customer segments with recency, frequency and monetary value data
- Learn to cluster customers using their behavioral data into meaningful segments
- Learn industry tips and tricks on customer behavioral analysis and segmentation.

**Prerequisites**

- [Intro to Python for Data Science](https://www.datacamp.com/courses/intro-to-python-for-data-science)
- [Intermediate Python for Data Science](https://www.datacamp.com/courses/intermediate-python-for-data-science)
- [Pandas Foundations](https://www.datacamp.com/courses/pandas-foundations)
- [Manipulating DataFrames with pandas](https://www.datacamp.com/courses/manipulating-dataframes-with-pandas)

