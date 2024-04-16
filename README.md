# Botasaurus🦖

Botasaurus adalah sebuah framework web scraping all-in-one yang memungkinkan untuk membuat engine scraper yang dalam waktu yang lebih singkat. Framework ini mengatasi masalah utama yang saya hadapi saat melakukan web scraping pada web modern.
## ⚙️Installation

Install botasaurus dengan pip
```bash
pip install botasaurus
```    
## 🚀Set up Botasaurus Project

1. Buatlah sebuah direktori khusus dan masuk ke dalamnya dengan perintah berikut:
```bash
mkdir botasaurus-project 
cd botasaurus-project
code . #ini akan membuka vscode jika sudah      menginstallnya
``` 
2. Sekarang buatlah file `main.py` dan masukan kode berikut
```python
from botasaurus import *

@browser
def scrape_heading_task(driver: AntiDetectDriver, data):
    # Arahkan ke situs web Webscraper
    driver.get("https://webscraper.io/test-sites")
    
    # Ambil Heading element
    heading = driver.text("h1")

    # Save data sebagai JSON file di output/scrape_heading_task.json
    return {
        "heading": heading
    }
    
if __name__ == "__main__":
    # jalankan program web scraping
    scrape_heading_task()
```
Karena base dari botasaurus adalah module selenium, maka syntax syntaxnya sama persis dengan selenium.

3. Jalankan engine scrapingnya
```bash
python main.py
```
Setelah engine berjalan, engine akan:
- Membuka Google chrome
- Membuka situs https://webscraper.io/test-sites
- Ekstrak teks heading
- Otomatis tersave di output/scrape_heading_task.json




## 💡 Fitur di Botasaurus

#### 1. Mengakses website yang di lindungi oleh cloudflare contoh websitenya adalah : https://www.g2.com/products/github/reviews
Jalankan program berikut :
```python
from botasaurus import *

@browser()
def scrape_heading_task(driver: AntiDetectDriver, data):
    driver.google_get("https://www.g2.com/products/github/reviews")
    heading = driver.text('h1')
    print(heading)
    return heading

scrape_heading_task()
```
Hasilnya adalah website terakses sempurna :)
![App Screenshot](https://raw.githubusercontent.com/omkarcloud/botasaurus/master/images/botasurussuccesspage.png)

#### 2. Scraping multiple links/points
Untuk menscraping multiple links/points kita harus mendefine variable data terlebih dahulu.
```python
from botasaurus import *

@browser(data=["https://webscraper.io/test-sites","https://stackoverflow.com/","https://crawler-test.com/"])
def scrape_heading_task(driver: AntiDetectDriver, data):
    driver.google_get(data)
    heading = driver.text('h1')
    print(heading)
    return heading

scrape_heading_task()
```
#### 3. Scraping dengan cara parallel
Untuk menscraping secara paralel kita harus menambahkan option parallel terlebih dahulu di browser decorator.
```python
@browser(parallel=3,data=["https://webscraper.io/test-sites","https://stackoverflow.com/","https://crawler-test.com/"])
def scrape_heading_task(driver: AntiDetectDriver, data):
    #...
```
Untuk mengoptimalkan jumlah paralel scraper kita bisa menggunakan fungsi `bt.calc_max_parallel_browsers`. Fungsi tersebut mengkalkulasikan jumlah maksimal browser yang bisa kita jalankan dengan RAM yang tersisa di Komputer kita
```python
@browser(parallel=bt.calc_max_parallel_browsers,data=["https://webscraper.io/test-sites","https://stackoverflow.com/","https://crawler-test.com/"])
def scrape_heading_task(driver: AntiDetectDriver, data):
    #...
```
#### 4. Caching hasil Scraping

Untuk menyimpan hasil web scraping ke dalam cache dan menghindari pengambilan data ulang yang sama, atur `cache=True` dalam decorator:
```python
@browser(cache=True,data=["https://webscraper.io/test-sites","https://stackoverflow.com/","https://crawler-test.com/"])
def scrape_heading_task(driver: AntiDetectDriver, data):
    #...
```

