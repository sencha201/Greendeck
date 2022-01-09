
# Flask Restful-API with Docker and PyMongo



Now-a-days, it’s very common to dockerize and deploy the Docker image in the production with the help of container orchestration engines such as Docker 

We are going to Dockerize the REST API and create an image and run it on Docker on our local machine. We could also push that Image into the Docker hub and pull it whenever and wherever we need it.

We are working on two important **concept *API and Containerization***

Here is the complete guide on how to develop a [Python REST API](https://flask-restful.readthedocs.io/en/latest/) with Flask library. 

--------------------------------------
##  Pre-requisite :-

 * You have to install [python](https://www.python.org/downloads/) and [MongoDB](https://www.mongodb.com/try/download/community).
 * As a pre-requisite, you also have to install [Docker](https://www.docker.com/products/docker-desktop) for Desktop.
 * Also,install [postman](https://www.postman.com/) for testing URL's
Once installed you can check the Docker info or version with the following commands.

--------
                                        `docker info`
                                      `docker --version`
-----------------
* Before run build command , you have to make `Dockerfile` in your project directory.
* you also have required `requirements.txt` file
 
 -----------------------





## `How to deploy the  Docker Container`
 * Firstly on your system open the command prompt or terminal.
 * Change Directory to the project directory.
 * Note : Before building or composing image on Docker , Docker Daemon must be running .
 * Run command `docker-compose build`, this will build the containers and prepare them to run the project.
 * Run command `docker-compose up`, this will start the process and containers.
 * In case of any error, yoy can also check logs with typing command `docker logs <Container Name>`
 * Use Postman or Curl to test the APIs with `http://localhost:5000/mongodb` as request URL.
---
## `Running project with only MongoDB on Docker`
 * Firstly on your system open the command prompt or terminal.
 * Note : Before building or composing image on Docker , Docker Daemon must be running .
 * Run command `docker pull mongo`, this will pull the image mongo from Docker Hub.
 * Run command `docker create -it --name MongoContainer -p 5000:27017 mongo`, this will make a container MongoContainer and pulling image mongo on given port.
 * Run command `docker start MongoContainer` to start it.
 * You can see the MongoDB database and collections and access them through MongoDB Campass, just paste `mongodb://localhost:27017/` in connection string.
 * To test the APIs with `http://localhost:5000/mongodb` use POSTMAN or CURL for request URL.
## API Reference :-

## `REST-API methods with uses`
| ***Method***  | ***Function*** | ***Description*** |
| ------------- | ------------- | ------------- |
| **GET**  | Fetch  | *It is the most common method which can be used to fetch data in the unencrypted form from the server.*|
| **POST**  | Insert  | *It is used to Inserts the  data in the collection.* |
| **PUT**  | Update  | *It is used to replace all the current representation of the target resource with the uploaded content* |
| **Delete**  | Delete |*It is used to delete all the current representation of the target resource specified in the URL.*  |
| **PATCH**  | Distinct/list_unique_brands | *Used to create new data or update/modify existing data at the specified resource / Bonus Task - How many unique brands are present in the collection?*  |
| **COPY**  | count_discounted_products | *Bonus Task - How many products have a discount on them?* |
| **VIEW**  | count_high_offer_price | *Bonus Task - How many products have offer price greater than 300?*
| **LOCK**  | count_high_discount | *Bonus Task -How many products have discount % greater than 30%?* |
| **UNLINK**  | Drop collection | *Drops the given table in case of data redundancy*  |
| **LINK**  | Import Data | *Imports the collection data* |

* If docker-compose up is used 2nd time without clearing the pervious data to overcome this type of problem LINK and UNLINK method are created.
* UNLINK drops the whole redundant data and LINK makes a new collection with required data.
----------

## How to send request API :-
**In Postman or Curl** 
* **Step 1:** Paste ths URL- `http://localhost:5000/mongodb` in URL.
* **Step 2:** Choose an API Method for which you want to perform operation .
* **Step 3:** Select Body -> Raw-> Json format.
* **Step 4:** Write valid code snippet below.
* **Step 5:** Click Send.
----------------------------

**(i).*GET Method***: GET method is used for fetching all the data from the collection.
  - This is the default database and collection in project.

 ``` 
  {
  "database": "Greendeck",
  "collection": "products"
  }
  ```
  
  
  - GET Method with filter constraint, will only show records where brand name is found in the database
  ```
{
  "database": "Greendeck",
  "collection": "products",
  "Filter": {
    "brand_name": "john lewis & partners"
  }
  }
  ```
  
  
  - `GET Method` with filter and count constraint, will give count of records.
  ```
   {
  "database": "Greendeck",
  "collection": "products",
  "Filter": {
    "brand_name": "john lewis & partners"
  }
  "count":""
  }
  ```

  
**(ii).*POST Method***: This method is used for data insertion in the  collection. 

  - The document keyword is required to insert data here.
  ```
  {
  "database": "Greendeck",
  "collection": "products",
  "Document": {
    "name": "shampoo", 
    "brand_name": "clinic_plus", 
    "regular_price_value": 1.0, 
    "offer_price_value": 0.5, 
    "currency": "GBP", 
    "classification_l1": "women", 
    "classification_l2": "women's hairs", 
    "classification_l3": "", 
    "classification_l4": "", 
    "image_url": ""
  }
  }
  ```
  
**(iii).*PUT Method***: Updates data in collection
 
 - The filter keyword identifies the old data and DataToBeUpdated keyword is for new data here.
 ```
 {
  "database": "Greendeck",
  "collection": "products,
  "Filter": {
    "brand_name": "clinic_plus"
  },
  "DataToBeUpdated": {
    "name": "shampoo", 
    "brand_name": "dove", 
    "regular_price_value": 10, 
    "offer_price_value": 5
  }
  }
  ```
  
  
**(iv).*Delete Method***: Delete method is uesd for deleting the data that matches the field .

  
  ```
   {
  "database": "Greendeck",
  "collection": "products",
  "Filter": {
    "name": "Jellycat Blossom Tulip Bunny Grabber, pink"
  }
  }
  ```
 
**(v).*PATCH Method***: fetch distinct records according to field.

  - Bonus Task - How many unique brands are 
present in the collection?
 

   ```
   {
  "database": "Greendeck",
  "collection": "products",
  "Distinct": "brand_name"
  }
  ```


**(vi).*COPY Method***: Bonus Task - How many products have a discount on them

  - This method will work only for default collection or a collection with fields regular_price_value and offer_price_value.
  ```
   {
  "database": "Greendeck"
  "collection": "products"
  }
  ```
 
  - This solution task could be achieved by `GET Method` too.
  ```
  {
  "database": "Greendeck",
  "collection": "products",
  "Filter": {
    "$expr":{"$gt":["$regular_price_value", 
"$offer_price_value"]}
  },
  "count":""
  }
  ```


  
**(vii).*VIEW Method***: Bonus Task - How many products have offer price greater than 300?

  - This method will work only for default collection.
  ```
   {
  "database": "Greendeck",
  "collection": "products"
  }
  ```
  
  
  -  solution to this task  achieved by `GET Method` too.
  ```
  {
  "database": "Greendeck",
  "collection": "products",
  "Filter": {
    'offer_price_value' : {'$gt' : 300 }}
  },
  "count":""
  }
  ```


**(viii).*LOCK Method***: Bonus Task - How many 
products have discount % greater than 30%?

  - This method will work only for default collection
  ```
   {
  "database": "Greendeck",
  "collection": "products"
  }
  ```
   

  - This solution to this task could be achieved by `GET Method` too.
  ```
  {
"database": "Greendeck",
"collection": "products",
"Filter": {
  "$expr":{"$gt":[{"$subtract":["$regular_price_value","$offer_price_value"]},{"$multiply":[0.3,
"$regular_price_value"]}]}
},
"count":""
}
  ```


**(ix).*UNLINK Method***: Drops the given collection.
   
   ```
   {
  "database": "Greendeck",
  "collection": "products"
  }
  ```
 

**(x).*LINK Method***: Imports data in given collection.

   ```
   {
  "database": "Greendeck",
  "collection": "products"
  }
  ```
 