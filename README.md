# Warsaw Apartment Rental Price

<img align="center" src="https://user-images.githubusercontent.com/35708288/158497746-9a402e1f-a522-4d48-b558-aa2ef37eed61.png" width="81"/> &emsp; &emsp;
<img align="center" src="https://user-images.githubusercontent.com/35708288/158498254-d32accc7-259e-422f-8588-5b4ed4d83cd8.png" width="105"/> &emsp; &emsp;
<img align="center" src="https://user-images.githubusercontent.com/35708288/158498353-1f996fdd-9a68-43f4-9926-3b3db5548265.png" width="97"/> &emsp; &emsp;
<img align="center" src="https://user-images.githubusercontent.com/35708288/205513438-96be622b-e861-4b96-b5c1-56ad2be7e569.png" width="100"/> &emsp; &emsp;
<img align="center" src="https://user-images.githubusercontent.com/35708288/205513437-1e401566-5467-4a12-82e9-594a9989a0fa.png" width="60"/> &emsp; &emsp;
<img align="center" src="https://user-images.githubusercontent.com/35708288/205486116-8f026d62-71cf-425b-acc3-8f8ec55f0b51.png" width="150"/>



This data science project allows landlords and tenants to check the price of renting an apartment in particular Warsaw districts. The project consists of several parts. 
## Data
In first step I gathered data like square meters, district, number of rooms, price by scraping a website with apartments rental offers www.olx.pl. 
## ML model
In second step I built a model using sklearn and linear regression using scraped data from olx.pl. Steps 1 and 2 were done using colab.
## App
The third step includes a python flask server that uses the saved model to serve http requests. The fourth step includes website built in html, css and javascript that allows user to enter data describing the apartment like square meters, number of rooms, district and it will call python flask server to receive the predicted price.
## Deploying app in AWS EC2
In fifth step I deployed app to cloud using AWS EC2 and NGINX. I assigned the domain rentalprice.ml registered in freenom.com to the application. The application has the SSL protocol implemented. Below is a description of the application deployment process on AWS:

#### 1.Create free account and log on to AWS

#### 2.Select EC2 service

#### 3.Select launch instance

#### 4.Create istance like on the screen below
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495034-2f2bd627-906e-4437-9f4d-5c52011bcee0.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495035-4df16351-e8fc-4c73-90f6-2f9954195283.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495039-6a7c5300-0dc3-4eb9-a300-400f59333f96.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495041-997f7737-b969-489e-bda7-e7e122d0ebc5.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495042-45845d06-ae24-4580-9c1e-b76ad8609c8f.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495045-d5bf60a4-c836-4364-ae42-b964be29c382.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495025-3683b212-f57a-46a1-9d67-d94d3259dd09.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205495031-92b8115a-dd2f-42c2-999d-9d3c3708efe0.png" width="450"/>

#### 5.Log in to newly created VM instance
<img align="center" src="https://user-images.githubusercontent.com/35708288/205497359-439fac22-df12-47ae-8fa9-236c65ea0737.png" width="450"/>

#### 6.Update package information
```
sudo apt-get update
```
#### 7.Install NGINX
NGINX server is used to link the application to the external domain of rentalprice.ml 
```
sudo apt-get install nginx
```
#### 8.Go to location
```
cd /etc/nginx/sites-enabled
```
#### 9.Remove symlink for default file
```
sudo unlink default
```
#### 10.Go to sites-available and create rentalprice.ml file
```
cd ../sites-available
```
rentalprice.ml file should look like below:
```
server {
    root /home/ubuntu/WarsawApartmentPrice/client;
    index app.html;
	server_name rentalprice.ml www.rentalprice.ml;
	location / {
		try_files $uri $uri/ =404;
	}

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/rentalprice.ml/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/rentalprice.ml/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
	listen 80;
        listen [::]:80;
	server_name rentalprice.ml www.rentalprice.ml;
	root /home/ubuntu/WarsawApartmentPrice/client;
	index app.html;
	location /api/ {
		rewrite ^/api(.*) $1 break;
                proxy_pass http://127.0.0.1:5000;
	}
}

server {
    if ($host = www.rentalprice.ml) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    if ($host = rentalprice.ml) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


	listen 80 default_server;
	listen [::]:80 default_server;

	server_name rentalprice.ml www.rentalprice.ml;
    return 404; # managed by Certbot
}
```
#### 11.Create symlink
```
sudo ln -v -s /etc/nginx/sites-available/bhp.conf
```

#### 12.Restart NGINX
```
sudo service nginx restart
```
#### 13.Install pip
```
sudo apt-get install python3-pip
```
#### 14.Install python 3.8
```
sudo apt install python3.8 python3.8-dev  python3.8-venv
```
#### 15.Upload all application files to server using FileZilla

#### 16.Install requirements
```
sudo pip3 install -r /home/ubuntu/WarsawApartmentPrice/server/requirements.txt
```
#### 17. Run the application using tmux
Start a new session in the console
```
tmux new -s rentalprice
```
Run App
```
python3 /home/ubuntu/WarsawApartmentPrice/server/server.py
```
#### 18. Domain configuration on the Freenom platform
<img align="center" src="https://user-images.githubusercontent.com/35708288/205497360-d36a94cd-54f5-439c-ad02-6feacf631a61.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205497362-4fb0f822-1452-4703-b24f-c89b6cee3a1c.png" width="450"/>
<img align="center" src="https://user-images.githubusercontent.com/35708288/205497364-94715be8-2fc9-4a94-b5bd-fb320b038c12.png" width="450"/>

You can check app: www.rentalprice.ml
