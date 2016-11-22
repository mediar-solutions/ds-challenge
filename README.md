
# Data Scientist Challenge

## The Role
___
Here at IDXP, we are obsessed with data. So, we are looking for people that can extract useful insights from it.

We collect location data from brick and mortar retail stores, and, by referencing these and sales data, we generate insights and analytics for our partners.

As a Data Scientist, your role is to generate metrics, insights and reports for manufacturers and retail partners, using behaviour and sales data, in a quick and scalable manner.

### About the position
___
Righ now, we are looking for an experienced Data Scientist or Business Analyst to join our team. Our Data Science stack is composed by Python components, such as Pandas, Sklearn and Numpy. Most of our work is made on Jupyter Notebooks.

In this position, you will be part of IDXP's core team, projecting experiments and building models using machine learning and data mining techniques, on location and sales data on some of the largest retail stores in the world. You will also be responsible for deploying improvements on our current code base, improving on our algorithms and methodologies. We are looking for professionals willing to work on Belo Horizonte, Brazil

If you think you can do it, let us know by sending an email to `jobs-dev@idxpanalytics.com`, so we can talk, **before** you submit the challenge below.

### About the company
___
IDXP is a brazilian company with it's HQ in California. It was awareded as "Global Entrepreneur of the year", by IBM and "Editor's Choice" in the world biggest Shopper Marketing fair. We were cited in some of the largest media outlets, like Forbes, Wall Street Journal, Venture Beat, Revista Exame, Folha de São Paulo and many others. The company developed a Big Data and Analytics platform that monitors in real time in-store shopper behaviour for retailers. The system helps retailers and manufacturers increares it's sales and measure the efficacy of promotions and other actions in and out of store. The company has already raised multiple funding rounds in Brazil and abroad.



___
#### Requirements
If you fit most (not necessarily all) of these, let us know!

* BSc on a highly technical degree, such as (but not limited to) Computer Science, Computer Engineering, Math and  Statistics
* Experience with deploying data pipelines in production
* Experience with stastical modeling
* Knowledge in Machine Learning algorithms

#### Nice-to-have
It would be great if you have some of these.

* MSc or PhD on a related area (Statistcs, Information Retrieval, Machine Learning, Data Mining...)
* Academic experience (any published paper?)
* Experience with distributed computing frameworks (specially Spark)
* Experience with Python programming



## The challenge

Here at IDXP, we use the data described below in order to generate metrics and insights to costumers and partners. In this challenge, you will do the same. We provide you some data samples, located in the `data/` folder. The provided files are the following, all as described below.

* `sales.csv`:  The sales data
* `location.csv`:  The location data
* `shelfs.json`:  Which SKUs are present in each area
* `store.png`:  A high-res blueprint of the store, with the areas of interest shown in red.


Every analysis that we perform on the data relies on, at least, the following three metrics, calculated for each item, each category and for each area of the store:

* Exposition :  How many people were exposed to that item or area? Meaning, how many people were identified on the area of that item? 

* Engagement : What is the average engagement power of an item or area? Meaning, how long does someone, on average, spend on a given area? It's defined as the average time spent by shoppers spent on each area.

* Conversion : On average, how many people need to be exposed to an item so one purchase will be made? This can be defined as $\frac{\#\_items\_sold}{item\_exposition}$

Every other basic metric and analysis that we use are crafted by combining these three base metrics and other variants on that.

What we ask you to do is the following:

1. First, we ask you to **Calculate** the three metrics above on the sample data given. The first two must be calculated for each item, each category and each area. The conversion, for each item and each category.

2. Since the role of a Data Scientist also involves the creation of new and interesting metrics and insights, we also want you to **suggest** (and **calculate**, of course) other metrics and insights from this data. We want to see how well you can use your imagination and knowledge in order to find patterns and insights on the data. **We are looking forward to see what else can we do with the data provided. Please, surprise us!**

Note that, while the location data is real, the sales data was randomly generated. In the location data, some inconsistency may occur, such as 0-second durations. It's up to you how to deal with these. As for the sales data, some baskets may not have much of a logic sense. But you can assume that the data is correct, and you do not need to worry with that.

### The Data

Our location data is based on video information collected at the store. Our system can understand when someone enters any designated area, and for how long that person remained on that area, as such:

| AREA | TIMESTAMP  | DURATION | 
|------|------------|----------| 
| 104  | 1464752382 | 6        | 
| 104  | 1464752042 | 6        | 
| 104  | 1464753356 | 0        | 
| 104  | 1464752953 | 13       | 
| 108  | 1464752797 | 6        | 
| 108  | 1464757765 | 6        | 
| 103  | 1464775340 | 2        | 
| 104  | 1464777447 | 13       | 
| 100  | 1464787092 | 6        | 

The data has the following columns:

* `AREA`: An unique ID of a location in the store
* `TIMESTAMP`: The moment that someone entered that `AREA`
* `DURATION` : How many seconds that person remained on that `AREA`

Each row on the data can be interpreted as a single event. While there may be some inconsistence in the data, for this challenge, you may assume that the data is correct.

Below, we show the blueprint of one store, with the areas that we are interested shown in red. The green and blue squares are cameras that are used to track users in store. Only the blue ones were used on this data.


```python
from IPython.display import Image
Image(filename='data/store.png') 
```




![png](data/store.png)



Besides the location data, we also receive the sales information from the store, formatted like the table below:


| BASKET_ID | TIMESTAMP  | CATEGORY     | PRODUCT_NAME   | SKU | VALUE  | 
|-----------|------------|--------------|----------------|-----|--------| 
| 1         | 1464815896 | REFRIGERANTE | DOLLY GUARANA  | 1   | 4.99   | 
| 1         | 1464815896 | REFRIGERANTE | DOLLY GUARANA  | 1   | 4.99   | 
| 1         | 1464815896 | PET SHOP     | ET BILU        | 9   | 499.99 | 
| 1         | 1464815896 | SUPLEMENTOS  | NEGATIVA 13    | 11  | 13.13  | 
| 1         | 1464815896 | PET SHOP     | ET BILU        | 9   | 499.99 | 
| 1         | 1464815896 | FERRAMENTAS  | REPIMBOCA      | 13  | 119.49 | 
| 1         | 1464815896 | BISCOITO     | BISCOITOX      | 7   | 3.79   | 
| 1         | 1464815896 | CELULAR      | HIPHONE 72     | 17  | 1299.9 | 
| 1         | 1464815896 | FERRAMENTAS  | CHAVE DE COBRA | 14  | 99.49  | 
| 1         | 1464815896 | BISCOITO     | BOLACHOX       | 8   | 2.19   | 

The data has the following columns:

* `BASKET_ID`: An unique ID representing the complete basket. You can understand it as the ID of this costumer.
* `TIMESTAMP`: The moment that this purchase was completed
* `CATEGORY` : The category name that the product belongs to
* `PRODUCT_NAME` : The Product name
* `SKU` : An unique product identifier
* `VALUE` :  The price paid for this product

Finally, we also have a JSON file, called `shelfs.json`, where, for each store location, there is a list of SKUs located on that area, as such:

```
{"101": ["11"], "109": ["14"], "99": ["3"], "111": ["3", "4"], "103": ["10"]...
```
In that sample, the area 111 contains the products with SKUs 3 and 4.

### The report

You are NOT required to complete this using any specific tool or language. Use whathever you are more confortable with.
You are required to write a report, explaining what, how and why you did what you did, specifically, why do you think the extra metrics you generated are usefull. As stated before, you do not need to use any specific tool, but, for the report, we would love to see it using the Jupyter Notebook. If you are not familiar with it, you can check http://jupyter.org/ in order to install and give your first steps with it. Again, it's not required to use it, but it would be nice to.

Finally, your code should be avaiable on a **private** github repository. If you can't make it private, you can use bitbucket.

### The delivery proccess

You can send your reports and link to repository to the email jobs-dev@idxpanalytics.com. 

We believe that one week is enough time to complete this challenge with interesting results. But, if you think you will need more time, let us know as soon as possible. If you need any further clarification, also let us know, so we can help you through the proccess.
