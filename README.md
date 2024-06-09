# Amazon-Web-Scraper-Project
```markdown
### Code Explanation 🤖

#### Step 1: Importing Necessary Libraries
```python
from bs4 import BeautifulSoup
import requests
import time
import datetime
import smtplib
```

We import libraries that are essential for web scraping and handling email notifications.

#### Step 2: Connecting to the Website and Extracting Data
```python
URL = 'https://www.amazon.com/Funny-Data-Systems-Business-Analyst/dp/B07FNW9FGJ/ref=sr_1_3?dchild=1&keywords=data%2Banalyst%2Btshirt&qid=1626655184&sr=8-3&customId=B0752XJYNL&th=1'

headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36", "Accept-Encoding": "gzip, deflate", "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8", "DNT": "1", "Connection": "close", "Upgrade-Insecure-Requests": "1"}

page = requests.get(URL, headers=headers)

soup1 = BeautifulSoup(page.content, "html.parser")

soup2 = BeautifulSoup(soup1.prettify(), "html.parser")

title = soup2.find(id='productTitle').get_text()

price = soup2.find(id='priceblock_ourprice').get_text()
```

This section establishes a connection to the Amazon website, fetches the HTML content, and then parses it using BeautifulSoup to extract the title and price of a specific product.

#### Step 3: Cleaning Up the Data
```python
price = price.strip()[1:]
title = title.strip()
```

Here, we remove any extra spaces and currency symbols from the extracted data for better readability.

#### Step 4: Creating a Timestamp
```python
import datetime

today = datetime.date.today()

print(today)
```

A timestamp is generated to keep track of when the data was collected.

#### Step 5: Writing Data to a CSV File
```python
import csv

header = ['Title', 'Price', 'Date']
data = [title, price, today]

with open('AmazonWebScraperDataset.csv', 'w', newline='', encoding='UTF8') as f:
    writer = csv.writer(f)
    writer.writerow(header)
    writer.writerow(data)
```

The extracted data along with the timestamp is written to a CSV file for storage and analysis.

#### Step 6: Automating Data Collection
```python
# Runs check_price after a set time and inputs data into your CSV
while(True):
    check_price()
    time.sleep(86400)
```

A loop is set up to run the `check_price` function at regular intervals, ensuring continuous data collection.

#### Additional Functionality (Optional)
```python
# If you want to try sending yourself an email when a price hits below a certain level, you can use this script
def send_mail():
    # Email sending logic here
```

A function `send_mail` is defined for sending email notifications if the price of the product drops below a certain level.

Feel free to reach out if you have any questions or need further clarification! 🚀
```
This markdown provides a beginner-friendly explanation of the code along with visual elements like emojis for a more engaging presentation. You can copy and paste this into your GitHub repo. Let me know if you need further assistance!
