# TwitAuth

##### A flask library to integrate twitter authentication automatically with database compatibility 

## Installation

```
pip install twitauth
```

## Usage

##### 1) Create your twitter application on https://apps.twitter.com/
##### 2) Note down consumer key, consumer secret key and callback url(created by you)
##### 3) Add the following in your application.py (or any file that you initialize your flask application from)

```

from twitauth.twitter import twitter_login

# Then initialize your sqlalchemy db object with your flask application


twitter = twitter_login(credId=None , db=db, callback_endpoint='/example-endpoint')
twitter.twittertables(application.config['SQLALCHEMY_DATABASE_URI'])
twitter.init_lib(application)
```
##### 4) Run application.py once (without doing anything further) Notice credId is None, we will add that soon
##### 5) So, It will create 2 tables (twitter_creds and user_details) in your database
##### 6) Manually Insert row containing your values (consumer_key, consumer_secret, callback_url) in table 'twitter_creds'
##### 7) Note down id of that row and update the code as follows assuming id is 1:

```
twitter = twitter_login(credId=1 , db=db, callback_endpoint='/example-endpoint')
```
##### Note : Please provide 'callback_endpoint' as you set earlier in your twitter application WITHOUT YOUR DOMAIN NAME
##### Example: your callback url = https://127.0.0.1:5005/oauth then callback_endpoint = '/oauth'
##### 8) In your template (.html) file where you have 'twitter sign in' button 
```
<a href="{{ url_for('auth') }}"></a>
```

## That's it!
##### Now, whenever your website user click on 'twitter sign-in' it will automatically authorize
##### User details will be stored in 'user_details' table

## BOOM! Twitter authorization IS DONE!! WITH ONLY 4-5 LINES OF CODE 😁
