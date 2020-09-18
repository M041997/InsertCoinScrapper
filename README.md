import requests
from bs4 import BeautifulSoup
import smtplib


#Website that you want to scrape
URLS = ('http://www.insertcoinclothing.com/hoodies/ryuji-777.html')

headers = {'include browser user agent here'}

#Function checks the price of the site using BS4
def check_price():
    page = requests.get(URLS, headers=headers)

    soup = BeautifulSoup(page.content, 'lxml')

    title = soup.find(attrs="l-product-info-heading").get_text()
    price = soup.find(attrs="l-product-info-price").get_text()
    converted_price = float(price[2:5])
#Email price point
    if (converted_price > 3900):
        send_mail()

    print(converted_price)
    print(title.strip())

#Function that sends the email
def send_mail():
    server = smtplib.SMTP('smtp.gmail.com', 587)#smtp and code, Can be found using google search
    server.ehlo()
    server.starttls()
    server.ehlo()

    server.login('youremailhere@gmail.com', 'email api key')

    subject = 'Price fell down for Ryuji Hoodie'
    body = 'Check the link https://www.insertcoinclothing.com/hoodies/ryuji-777.html'

    msg = f"Subject: {subject}\n\n{body}"

    server.sendmail(
        'youremail@gmail.com',
        'youremail@gmail.com',
        msg
    )
    print("Hey email has been sent!")

    server.quit()


check_price()


