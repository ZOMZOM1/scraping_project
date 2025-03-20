from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from bs4 import BeautifulSoup
import time
import pandas as pd

# ChromeDriverのパスを指定（適宜変更）
chrome_driver_path = "/path/to/chromedriver"  # 例: "/usr/local/bin/chromedriver"

# Seleniumの設定
options = webdriver.ChromeOptions()
options.add_argument("--headless")  # ヘッドレスモード（ブラウザを開かずに実行）
service = Service(chrome_driver_path)
driver = webdriver.Chrome(service=service, options=options)

# **スクレイピング対象のURL（メルカリの検索結果ページ）**
search_url = "https://jp.mercari.com/search?keyword=PS5"  # ここを好きなキーワードに変更
driver.get(search_url)

# ページが完全に読み込まれるまで待機
time.sleep(3)

# **BeautifulSoupでページ解析**
soup = BeautifulSoup(driver.page_source, "html.parser")

# **取得するデータのリスト**
products = []

# **商品情報を取得**
for item in soup.find_all("div", class_="sc-5bb1edfb-9 PSMbT"):  # メルカリの商品枠のクラス名（適宜変更）
    try:
        # 商品名
        title = item.find("p", class_="merText caption__5616e150 primary__5616e150").text.strip()

        # 価格
        price = item.find("div", {"data-testid": "price"}).text.strip()

        # 商品URL
        link_tag = item.find("a", href=True)
        if link_tag:
            product_url = "https://jp.mercari.com" + link_tag["href"]
        else:
            product_url = "なし"

        # 取得したデータをリストに追加
        products.append({"商品名": title, "価格": price, "商品URL": product_url})

    except AttributeError:
        continue

# **取得結果をデータフレーム化**
df = pd.DataFrame(products)

# **CSVファイルに保存**
df.to_csv("mercari_products.csv", index=False, encoding="utf-8-sig")

# **完了メッセージ**
print("✅ スクレイピング完了！データは 'mercari_products.csv' に保存しました。")

# **ブラウザを閉じる**
driver.quit()
# scraping_project
スクレイピングとデータ分析のポートフォリオ
