

# The Challenge
---

Here at Mediar, we use the data described below in order to generate metrics and insights to costumers and partners. In this challenge, you will do the same. 

We provide you one month of real, in-store data, located in the `data/` folder that will be sent to you after our first talk. The provided files are the following, all as described below.

* `sales/`: Folder with sales data 
* `location/`:  Folder with location data
* `mapping.csv`: CSV with mapping between category and store area 
* `store.png`:  A high-res blueprint of the store, with some of the areas of interest shown in red (The image is not necesseraly from the same store).


Every analysis that we perform on the data relies on, at least, the following three metrics, calculated for each category and for each area of the store:

* Exposure :  How many people were exposed to that category or area? Meaning, how many people were identified on the area of that item? 

* Engagement : What is the average engagement power of a given category or area? Meaning, how long does someone, on average, spend on a given area? It's defined as the average time spent by shoppers spent on each area.

* Conversion : On average, how many people need to be exposed to an item so one purchase will be made? This can be defined as #_baskets\_sold/exposure (We define one basket as one shopper that purchased that item)

Every other basic metric and analysis that we use are crafted by combining these three base metrics and other variants on that.

## What we are looking for
___
What we ask you to do is the following:

1. First, we ask you to Calculate the three metrics above on the sample data given. The first two must be calculated for each each category and each area. The conversion, for each category.

2. If you find any inconsistence with the data, we want you to try to come up with plausible explanations as why that happened.

3. Since the role of a Data Scientist also involves the creation of new and interesting metrics and insights, we also want you to **suggest** (and **calculate**, of course) other metrics and insights from this data. We want to see how well you can use your imagination and knowledge in order to find patterns and insights on the data. **We are looking forward to see what else can we do with the data provided. Please, surprise us!**


Note that the data, both location and sales, is real. Therefore, any inconsistence should be considered and will probably come up on your daily work at Mediar (and any other data company). Therefore, it's up to you how to handle these. Some inconsistences that may occour are (but not limited to): 0-seconds exposure, more baskets on a area than exposure, missing data and others. 

We want to see how you deal with these inconsistences, and it would be great if you could come up with your own explanations on why these issues may happen.

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

Each row on the data can be interpreted as a single event (Say, one shopper captured on that given area, starting at the given tiemstamp and ending after the number of seconds indicated.

Below, we show the blueprint of one store, with the areas that we are interested shown in red. The green and blue squares are cameras that are used to track users in store. Only the blue ones were used on this data.


```python
from IPython.display import Image
Image(filename='data/store.png') 
```




![png](output_6_0.png)



The sales data is more complete, and has the following columns:

* `external_id`: An unique ID representing the complete basket. You can understand this information as the ID of this shopper. 
* `date`: Date and hour that the given item was scanned on the Point of Sale.
* `sku`: An unique product identifer, unique to this retailer.
* `upc`: An unique product identifier, unique to the product (AKA the barcode of the product)
* `product_name`: The description of the product, given by the retailer
* `manufacturer_id`: the ID of the manufacturer, given by the retailer
* `category_[1-5]_id`: IDs of the category and every subdivision of the category, given by the retailer
* `category_[1-5]_name`: Names of the category and every subdivision of the category, given by the category, given by the category
* `value`: Price of one unity of the item
* `quantity`: How many items were sold
* `discount`: How much were given as discount to that item (if any)
* `total_value`: Total value paid for that item (Calculated as (value*quantity)-discount


Finally, we also have a CSV file, called `mapping.csv`, formatted as such:

| area | category_name      | Comentario | 
|------|--------------------|------------| 
| X    | VINHOS SUAVES      |            | 
| 424  | VODKA              |            | 
| 424  | WHISKY             |            | 
| 425  | CEREAIS MATINAIS   |            | 
| 425  | LEITES             |            | 
| 424  | CERVEJAS           |            | 
| 424  | CERVEJAS ESPECIAIS |            | 
| 421  | CHOC.CKOUT         |            | 


In that sample, the area 424 Contains products with the categories VODKA, WHISKY, CERVEJAS and CERVEJAS ESPECIAIS, for instance. An `X` means that the given category has no mapped area.



### The report

You are NOT required to complete this using any specific tool or language. Use whathever you are more confortable with.
You are required to write a report, explaining what, how and why you did what you did, specifically, why do you think the extra metrics you generated are usefull. As stated before, you do not need to use any specific tool, but, for the report, we would love to see it using the Jupyter Notebook. If you are not familiar with it, you can check http://jupyter.org/ in order to install and give your first steps with it. Again, it's not required to use it, but it would be nice to.

Finally, your code should be avaiable on a **private** github repository. If you can't make it private, you can use bitbucket.

### The delivery proccess

You can send your reports and link to repository to the email jobs-dev@idxpanalytics.com. 

We believe that one week is enough time to complete this challenge with interesting results. But, if you think you will need more time, let us know as soon as possible. If you need any further clarification, also let us know, so we can help you through the proccess.
