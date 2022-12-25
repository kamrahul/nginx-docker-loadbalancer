# Nginx docker setup

# Setting up for nginx

1. create folder conf.d/custom.conf
2. Add conf to listen 80
3. Setting up proxy_pass

# Understanding the Nginx Conf file
```python

# server {} is the main code block
server{
    # This port 80 will listen to all the request coming in this port
    listen 80;

    # This  is for IPV6 support
    listen [::]:80;

    # Server_name is ideally your domain name Eg abc.com
    server_name localhost;

    # Location configuration helps to define URL rules
    location /appone{

        # Proxy_pass will pass/redirect the request to the specific container .
        #[NOTE: This port number is the internal port of the cotainer as we are using container name here Eg.flask_app_one ]
        proxy_pass http://flask_app_one:5000/;

        #proxy_pass_header Server;
        #proxy_set_header Host $http_host;
        #proxy_redirect off;
        #proxy_set_header X-Real-IP $remote_addr;
        #proxy_set_header X-Scheme $scheme;
        #proxy_set_header X-Forwarded-For #$proxy_add_x_forwarded_for;

        # This configuration helps to define time out for api requests
        proxy_connect_timeout 30;
        proxy_read_timeout 30;
    }
```

## Docker compose changes for nginx
1. Add network for all containers
2. Mount configuration file via volume


## Check Reverse proxy for Nginx 
1. navivate to localhost/appone it will redirect to App One ( 5001)
2. Navigate to localhost/apptwo will redirect to App Two ( 5002)

