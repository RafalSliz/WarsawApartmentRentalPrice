# WarsawApartmentRentalPrice

This data science project allows landlords and tenants to check the price of renting an apartment in particular Warsaw districts. The project consists of several parts. In first step I gathered data like square meters, district, number of rooms, price by scraping 
a website with apartments rental offers www.olx.pl. In second step I built a model using sklearn and linear regression using scraped data from olx.pl. The third step includes a python flask server that uses the saved model to serve http requests. The fourth step includes website built in html, css and javascript that allows user to enter data describing the apartment like square meters, number of rooms, district and it will call python flask server to receive the predicted price. In fifth step I deployed app to cloud using AWS EC2 and NGINX. I assigned the domain warp.ml registered in freenom.com to the application. The application has the SSL protocol implemented.

You can use the app at www.warp.ml  
