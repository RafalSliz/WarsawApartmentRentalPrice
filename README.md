# Warsaw Apartment Rental Price

<img src="https://user-images.githubusercontent.com/35708288/158497746-9a402e1f-a522-4d48-b558-aa2ef37eed61.png" width="81"/> &emsp; &emsp; &emsp; 
<img src="https://user-images.githubusercontent.com/35708288/158498254-d32accc7-259e-422f-8588-5b4ed4d83cd8.png" width="105"/> &emsp; &emsp; &emsp;
<img src="https://user-images.githubusercontent.com/35708288/158498353-1f996fdd-9a68-43f4-9926-3b3db5548265.png" width="97"/> &emsp; &emsp; &emsp;
<img src="https://user-images.githubusercontent.com/35708288/205467200-29352db5-d9bd-4620-bdb5-f13459863cbb.png" width="150"/> &emsp; &emsp; &emsp;
<img src="https://user-images.githubusercontent.com/35708288/205467301-52e52a12-7418-4f76-a94e-8f441ceb7235.png" width="150"/>


This data science project allows landlords and tenants to check the price of renting an apartment in particular Warsaw districts. The project consists of several parts. 
## Data
In first step I gathered data like square meters, district, number of rooms, price by scraping a website with apartments rental offers www.olx.pl. 
## ML model
In second step I built a model using sklearn and linear regression using scraped data from olx.pl. Steps 1 and 2 were done using colab.
## App
The third step includes a python flask server that uses the saved model to serve http requests. The fourth step includes website built in html, css and javascript that allows user to enter data describing the apartment like square meters, number of rooms, district and it will call python flask server to receive the predicted price.
## Deploying app in AWS EC2
In fifth step I deployed app to cloud using AWS EC2 and NGINX. I assigned the domain rentalprice.ml registered in freenom.com to the application. The application has the SSL protocol implemented. Below is a description of the application deployment process on AWS:

#### 1.Create account and log on to AWS


You can check app: www.rentalprice.ml
