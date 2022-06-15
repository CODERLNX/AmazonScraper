# AmazonScraper
This is a tool that allows you to get time series data from any amazon item.

#----------------------------------------------------------------------FULL CODE------------------------------------------------------------------------#

    #IMPORT LIBRARIES
    from bs4 import BeautifulSoup as bs #Used to Scrape the data from Amazon
    import requests as rq #Used to send the GET Requests
    import time
    import datetime
    import pandas as pd
    import csv

    import smtplib

    url = "https://www.amazon.com/Logitech-MK345-Wireless-Combo-Right-Handed/dp/B00QXT5T3U/ref=pd_sim_cpf_related_desktop_sccl_4_2/140-2880311-0562538?pd_rd_w=wBgTW&content-id=amzn1.sym.87783053-6326-44fc-9007-8a529451ab67&pf_rd_p=87783053-6326-44fc-9007-8a529451ab67&pf_rd_r=0A14T5B5G58TASBTG29A&pd_rd_wg=39KWL&pd_rd_r=9eb27239-2525-4673-85c9-f8c8b2683d76&pd_rd_i=B00QXT5T3U&psc=1"
    headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36 OPR/86.0.4363.70"}
    #You get This header^^ From this page --> httpbin.org/get, on the user agent line.

    page = rq.get(url, headers=headers) #This Starts Bringing in the data W/ the GET request    

    soup1 = bs(page.content, 'html.parser') #This pulls in all the content from the page as HTML.
    soup1_pretty = bs(soup1.prettify(), "html.parser") #This makes the data more readable.

    title = soup1_pretty.find(id='productTitle').get_text() #Pulls in the name of the Item
    price = soup1_pretty.find('span', {'class': 'a-offscreen'}).get_text() #Pulls in the price of the item
    availability = soup1_pretty.find('span', {'class': 'a-size-medium a-color-success'}).get_text() #Pulls in if its in stock or not


    #Formating
    title = title.strip() #Clears the WhiteSpaces
    price = price.split()[0] #Clears the WhiteSpaces
    price = price.strip()[1:]
    availability = availability.strip() #Clears the WhiteSpaces
    availiability

    date = datetime.date.today() #Sets the date variale to todays date
    availiability

    #ONLY RUN THIS ONCE
    header = ['Title', 'Price', 'Availability', 'Date'] #Sets the names of the columns
    data = [title, price, availability, date] #Set the data to the appropiate column order

    with open("AmazonWebScraperDataset.csv", 'w', newline='', encoding='UTF8') as f: #Makes the CSV File
        writer = csv.writer(f) #writes the CSV File
        writer.writerow(header) #Sets theh Columns
        writer.writerow(data) # Sets the Rows of data
    #Now We Append Data
    data = [title, price, availability, date]
    with open("AmazonWebScraperDataset.csv", 'a+', newline='', encoding='UTF8') as f: #This Adds data to the file
        writer = csv.writer(f)
        writer.writerow(data) #Adds more rows of data

    #USE THIS TO AUTOMATE IT

    def CheckPrice():

        url = "https://www.amazon.com/Logitech-MK345-Wireless-Combo-Right-Handed/dp/B00QXT5T3U/ref=pd_sim_cpf_related_desktop_sccl_4_2/140-2880311-0562538?pd_rd_w=wBgTW&content-id=amzn1.sym.87783053-6326-44fc-9007-8a529451ab67&pf_rd_p=87783053-6326-44fc-9007-8a529451ab67&pf_rd_r=0A14T5B5G58TASBTG29A&pd_rd_wg=39KWL&pd_rd_r=9eb27239-2525-4673-85c9-f8c8b2683d76&pd_rd_i=B00QXT5T3U&psc=1"

        headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36 OPR/86.0.4363.70"}
        page = rq.get(url, headers=headers) #This Starts Bringing in the data W/ the GET request    


        soup1 = bs(page.content, 'html.parser') #This pulls in all the content from the page as HTML.
        soup1_pretty = bs(soup1.prettify(), "html.parser") #This makes the data more readable.

        title = soup1_pretty.find(id='productTitle').get_text() #Pulls in the name of the Item
        price = soup1_pretty.find('span', {'class': 'a-offscreen'}).get_text() #Pulls in the price of the item
        availability = soup1_pretty.find('span', {'class': 'a-size-medium a-color-success'}).get_text() #Pulls in if its in stock or not


        #Formating

        title = title.strip() #Clears White Spaces

        price = price.split()[0] #Clears whiteSpaces

        price = price.strip()[1:] #Takes away the $ sign

        availability = availability.strip() #Clears White Spaces



        #Gets Date

        date = datetime.date.today() #gets todays Date

        #Sets Data ready for CSV

        data = [title, price, availability, date] #sets new data ni order of columns


        #Appends the data to the CSV

        with open("AmazonWebScraperDataset.csv", 'a+', newline='', encoding='UTF8') as f: #This Adds new data to the file

            writer = csv.writer(f)

            writer.writerow(data) #adds the new rows of data

