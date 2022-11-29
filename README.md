# Warsaw Apartment Rental Price

<img src="https://user-images.githubusercontent.com/35708288/158497746-9a402e1f-a522-4d48-b558-aa2ef37eed61.png" width="81"/> <img src="https://user-images.githubusercontent.com/35708288/158498254-d32accc7-259e-422f-8588-5b4ed4d83cd8.png" width="105"/> <img src="https://user-images.githubusercontent.com/35708288/158498353-1f996fdd-9a68-43f4-9926-3b3db5548265.png" width="97"/>

This data science project allows landlords and tenants to check the price of renting an apartment in particular Warsaw districts. The project consists of several parts. In first step I gathered data like square meters, district, number of rooms, price by scraping 
a website with apartments rental offers www.olx.pl. In second step I built a model using sklearn and linear regression using scraped data from olx.pl. Steps 1 and 2 were done using colab. The third step includes a python flask server that uses the saved model to serve http requests. The fourth step includes website built in html, css and javascript that allows user to enter data describing the apartment like square meters, number of rooms, district and it will call python flask server to receive the predicted price. In fifth step I deployed app to cloud using AWS EC2 and NGINX. I assigned the domain warp.ml registered in freenom.com to the application. The application has the SSL protocol implemented.

## Data

## ML model

## App

## Deploying app in AWS EC2

You can check app: www.rentalprice.ml
