# InsertCoinScrapper

//A beginner code using the beautiful soup library

    import requests
    from bs4 import BeautifulSoup
    import smtplib

    #A webscrapper for an item prices on insertcoinclothing.com using the beautiful soup library.

    URLS = ('http://www.insertcoinclothing.com/hoodies/ryuji-777.html')

    headers = {'Insert the your user agent from the browser'}


    def check_price():
        page = requests.get(URLS, headers=headers)

    soup = BeautifulSoup(page.content, 'lxml')

    title = soup.find(attrs="l-product-info-heading").get_text()
    price = soup.find(attrs="l-product-info-price").get_text()
    converted_price = float(price[2:5])

    if (converted_price > 3900):
        send_mail()

    print(converted_price)
    print(title.strip())


    def send_mail():
        server = smtplib.SMTP('smtp.gmail.com', 587) #smtp mail and code go here. One can find them with a quick google search
        server.ehlo()
        server.starttls()
        server.ehlo()

    server.login('', '') #Place your email and email API key in the following quotes as server.login("Email", "API Key")

    subject = 'Price fell down for Ryuji Hoodie'
    body = 'Check the link https://www.insertcoinclothing.com/hoodies/ryuji-777.html'

    msg = f"Subject: {subject}\n\n{body}"

    server.sendmail(
        '',//Insert your from email here
        '',//Insert your "To" email here
        msg
    )
    print("Hey email has been sent!")

    server.quit()


    check_price()


