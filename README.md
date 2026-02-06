# DATA-DRIVEN-TESTING-

NAME : ATHARVA MANOJ JADGE

INTERN ID : CTIS2823

DOMAIN : DATA DRIVEN TESTING 

DURATION : 1 MONTH 

MONTOR  : NEELA SANTOSH

DISCRIPTION OF TASK HOW YOU PERFORMED AND WHAT YOU HAVE DONE AND PASTE CODES OF OUTPUT

OUTPUT..

import csv
import logging
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

Configure logging

logging.basicConfig(
filename="test_results.log",
level=logging.INFO,
format="%(asctime)s - %(levelname)s - %(message)s"
)

Initialize WebDriver

driver = webdriver.Chrome()
driver.maximize_window()

Open CSV file

with open("testdata.csv", newline='') as csvfile:
reader = csv.DictReader(csvfile)

for row in reader:  
    try:  
        driver.get("https://example.com/login")  # Demo URL  
        time.sleep(2)  

        # Locate elements  
        username = driver.find_element(By.ID, "username")  
        password = driver.find_element(By.ID, "password")  

        # Clear and enter data  
        username.clear()  
        password.clear()  

        username.send_keys(row['username'])  
        password.send_keys(row['password'])  
        password.send_keys(Keys.RETURN)  

        time.sleep(3)  

        # Validation (example condition)  
        if "dashboard" in driver.current_url:  
            logging.info(f"PASS - Login successful for user: {row['username']}")  
        else:  
            logging.warning(f"FAIL - Login failed for user: {row['username']}")  

    except Exception as e:  
        logging.error(f"ERROR for user {row['username']} - {str(e)}")

driver.quit()
