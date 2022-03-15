# Intercom SSL Setup Guide

## AWS Cloudfront

### Create a cloudfront distribution

#### Origin
1. Input custom.intercom.help into origin domain
2. Select HTTP only or HTTPS only
3. Enter a name for your distribution


![origin](https://user-images.githubusercontent.com/80290537/128640641-ea5cad36-ffdf-4039-84ad-799288e2d39e.png)

#### Default Cache Behavior
1. Select "Redirect HTTP to HTTPS" for viewer protocol policy
2. Select "GET, HEAD, OPTIONS" for allowed HTTP methods
3. Toggle legacy cache settings
  * Select All for Headers, Query strings, and Cookies


![cachebehavior](https://user-images.githubusercontent.com/80290537/128640773-07eda54d-75f6-4024-9100-d83ea511172e.png)

#### Settings
1. Add an alternate domain name and enter in your custom domain
  * Ensure this includes your subdomain (ex. help.example.com)
2. Select your SSL certificate
  * If no options are available, then request a certificate through cloudfront and follow the instructions
3. Select a security policy, the most recent is recommended but at minimum ensure it is v1.2


![settings](https://user-images.githubusercontent.com/80290537/128640972-ce8cd1dc-06c6-4139-9cb0-7bb9727754fe.png)

### Create a hosted zone and A record (If using AWS as your domain provider)

#### Hosted Zone
1. Navigate to Route53 within your AWS console and create a new hosted zone
2. Input your ***main*** domain as the domain name
  * Example: if your help center is going to be on help.example.com then input example.com
![Screen Shot 2021-08-08 at 11 21 55 AM](https://user-images.githubusercontent.com/80290537/128641042-e93fece9-1019-44c7-8810-d33cf099c32c.png)

3. Navigate into your newly created hosted zone and select "create record"
4. Select an A type record
5. Input your subdomain (ex. help for help.example.com) 
6. Toggle "Alias"
7. Select "Alias to Cloudfront distribution" under route traffic to
8. Choose your distribution 
  * If you don't see your distribution then most likely the wrong domain was entered for step 2

![Screen Shot 2021-08-08 at 12 55 06 PM](https://user-images.githubusercontent.com/80290537/128641194-23add9ae-eae2-4113-bfcc-15810afacb6c.png)

### Create a CNAME record (If using another service as your domain provider)

1. Copy your distribution domain name
2. Navigate to your domain provider and create a new CNAME record
3. For host/name input your subdomain (ex help)
4. For value input your Cloudfront distribution domain name

<img width="1117" alt="Screen Shot 2021-08-08 at 1 00 50 PM" src="https://user-images.githubusercontent.com/80290537/128641258-f08b6cc6-bb9e-47e1-94f3-0aa79b049600.png">

