📦 メルカリ商品情報スクレイピング

📝 概要
本プロジェクトは、フリマアプリ「メルカリ」上の特定キーワード検索結果から、商品情報を自動取得するスクレイピングツールです。
Python と BeautifulSoup、Selenium を用いて構築しており、初学者から実務利用まで対応できる汎用的な構成になっています。

🔍 取得対象データ
項目	内容
商品名	商品のタイトルテキスト
価格	表示されている販売価格
商品詳細URL	商品の個別ページへのリンク
商品画像URL（任意）	商品画像のURL（※必要に応じて追加可能）

🛠 使用技術・ライブラリ
Python 3.x
requests
BeautifulSoup
Selenium（動的ページ対応）
pandas（CSV出力用）

🚀 実行方法
必要なライブラリをインストール
pip install requests beautifulsoup4 selenium pandas
ChromeDriver を環境に合わせて設置（※Chromeバージョンに対応するもの）

スクリプトを実行
python mercari_scraper.py
💡 応用可能なユースケース
ECサイト価格モニタリング
売れ筋商品の傾向分析
在庫トラッキングシステムの原型
マーケット調査用のデータ収集

📁 出力形式
取得データはCSV形式で保存され、Excelなどで開いてすぐに確認・分析が可能です。

✨ 今後の拡張予定（オプション）
商品説明やカテゴリ、在庫状況の取得
データの定期自動取得（cron連携）
GUI対応やWebアプリ化（Streamlitなど）
必要に応じて「mercari_scraper.py」や「sample_output.csv」も含めてGitHubにアップしておくと、より魅力的なポートフォリオになりますよ！
必要であれば mercari_scraper.py のサンプルコードもお渡しできますので、お声がけください 😊
