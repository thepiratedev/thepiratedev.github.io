---
  layout: post
  title: Facebook Auto Group Post Bot Using Python (Selenium and BeautifulSoup)
  tags: 
  categories: Python
  permalink: /blog/:title.html
---

It's easy to make a facebook bot in Python, I made this bot when I was just starting out to learn python and it only took me 2-3 days to understand how it fully works. The only thing you need to know is how to target CSS selectors and a bit of python.  

Here's the things you need to do to get started.

1. [Download](python.org) and install python in your system.
2. Pip install [selenium](http://selenium-python.readthedocs.io).
3. Pip install [beautifulsoup4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).
4. Download [WebDriver for Chrome](https://sites.google.com/a/chromium.org/chromedriver/downloads).

Once you get downloaded and installed evertyhing make a folder in your desktop called 'facebook-bot' and a file named 'bot.py' then open that file in your text editor.

All of the code below will be written inside 'bot.py'.


Import all the necessary modules we will be using in this project.

{% highlight python %}
# bot.py
import sys
import time
from random import randint
from bs4 import BeautifulSoup
import re
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.ui import WebDriverWait
from selenium.common.exceptions import NoSuchElementException
{% endhighlight %}

After importing everything we will need in the project, let's set some variables we will be using throughout the project.

{% highlight python %}
# bot.py

# Facebook settings
rootUrl = 'https://mbasic.facebook.com'
username="" # Your facebook username
password="" # Your facebook password
groups = []

message = """
Your post message here.

# Driver settings
driver = webdriver.Chrome() # Use chrome driver here unless you want a headless browser.
wait = WebDriverWait(driver, 10)
driver.implicitly_wait(30)
driver.set_window_size(400, 600)
"""
{% endhighlight %}

What we are doing in this code block.

1. We are using the url [https://mbasic.facebook.com](https://mbasic.facebook.com) for easy css targeting.
2. Setting our facebook credentials to log in.
3. Creating an array called 'groups' for later use.
4. Saving our message that the bot will use to post in each group.
5. Tell selenium to use Chrome as our browser
6. Set some settings for timeouts for waiting elements. 
7. Set our browser's window size. 

Here comes the fun part.

{% highlight python %}
# bot.py
driver.get(rootUrl)
print('Waiting for login elements')
wait.until(EC.presence_of_element_located(
    (By.XPATH, '//input[@type="password"]')))
print('Login Available')
inputUsername = driver.find_element_by_id('m_login_email')
inputPassword = driver.find_element_by_xpath('//input[@type="password"]')
inputUsername.send_keys(username)
inputPassword.send_keys(password)
inputPassword.send_keys(Keys.RETURN)
print('Successfully logged in.')
{% endhighlight %}

What we are doing in this code block.

1. Tell the bot to go to [https://mbasic.facebook.com](https://mbasic.facebook.com).
2. Wait for the password element to appear before doing anything.
3. Find the elements where we type our username and password. 
4. Type the facebook username and password.
5. Click the log in button. 

After logging in we need to go to the groups page and copy all the links of each group that we are in and push each link to the groups array. 

{% highlight python %}
driver.get('https://mbasic.facebook.com/groups/?seemore&refid=27')

html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')

for tag in soup.find_all('a', href=re.compile(r'groups/\d')):
    print('saving in fb-groups.txt: ' + tag.text)
    groups.append(rootUrl + tag['href'])
    # time.sleep(0.05)
for group in groups:
    link = rootUrl + group
{% endhighlight %}

Lastly we will go to each link saved in the groups array and find the textbox element and type the message inside the text box and submit that post.

{% highlight python %}
for group in groups:
    try:
        driver.get(group)
        wait.until(EC.presence_of_element_located(
            (By.XPATH, '//textarea[@name="xc_message"]')))
        textarea = driver.find_element_by_xpath('//textarea[@name="xc_message"]')
        print('Posting message in textarea...')
        textarea.send_keys(message)
        postBtn =  driver.find_element_by_xpath('//input[@name="view_post"]')
        postBtn.click()
        for remaining in range(randint(300,600), 0, -1):
            sys.stdout.write("\r")
            sys.stdout.write("Post submitted! wait for {:2d} seconds before next post.".format(remaining))
            sys.stdout.flush()
            time.sleep(1)

    except NoSuchElementException:
        print('Some element was not found skipping..')
        continue
{% endhighlight %}

Each post will have a random interval between 300-600 seconds or 5-10 minutes to avoid getting banned in facebook. 

That's it! We just made a bot using python, selenium and beautifulsoup4. If you'd like to see the full code you can visit this [repository](https://github.com/peicap/shadowads/blob/master/src/facebook.py) on github. 