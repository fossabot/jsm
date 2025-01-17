[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Foceanection%2Fjsm.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Foceanection%2Fjsm?ref=badge_shield)

Overview
========

日本の株式市場の株価・財務データを取得するツールです。

各種データは、 `Yahoo!ファイナンス <http://finance.yahoo.co.jp/>`_ からスクレイピングしています。

動作は、Python2.5 - 2.7 で確認しています。

Installation
============

PyPIからのインストールが簡単です::

  easy_install jsm

Usage
=====

jsm.Quotesのインスタンスを作成::

  import jsm
  q = jsm.Quotes()

以後、作成したインスタンスを使って各種データを取得します。

当日の株価の取得（例ではYahoo!の証券コードを指定）::
  
  q.get_price(4689) 

過去の株価の取得::
  
  q.get_historical_prices(4689)

デフォルトでは当日から過去1ヶ月のデイリー株価を取得します。

週間, 月間の株価の取得::

  q.get_historical_prices(4689, jsm.WEEKLY) # 週間株価を取得
  q.get_historical_prices(4689, jsm.MONTHLY) # 月間株価を取得

指定した期間の株価の取得::
  
  import datetime
  start_date = datetime.date(2011, 1, 1)
  end_date = datetime.date(2011, 2, 1)
  q.get_historical_prices(4689, jsm.DAILY, start_date, end_date) # 2011/1/1 〜 2011/2/1までの株価を取得

2000/1/1〜現在までの株価の取得::

  q.get_historical_prices(4689, jsm.DAILY, all=True) # 負荷をかけるので要注意

株価取得メソッド（get_price, get_historical_prices）の戻り値は、PriceDataクラスのインスタンスです。

PriceDataについては、下記Data項を参照してください。

jsmには、取得した株価をCSV形式で保存する為の便利なクラスが用意されています。

株価をCSV形式で保存::

  c = jsm.QuotesCsv()
  c.save_price(4689)
  c.save_historical_prices(4689) # get_historical_pricesと同じ使い方

対象の財務情報を得る為には、以下のメソッドを利用します。

財務情報の取得::
  
  q.get_finance(4689)

財務情報取得メソッド（get_finance）の戻り値は、FinanceDataクラスのインスタンスです。

FinanceDataについては、下記Data項を参照してください。

またjsmでは、業種別の銘柄情報を得ることができます。

業種別の銘柄情報を得る為には、以下のメソッドを利用します。

業種別の銘柄情報の取得::
  
  q.get_brand() # デフォルト：全業種
  
また以下のIDを引数に渡すことで、それぞれ業種別の銘柄情報を得ることができます::

  '0050' # 農林・水産業
  '1050' # 鉱業
  '2050' # 建設業
  '3050' # 食料品
  '3100' # 繊維製品
  '3150' # パルプ・紙
  '3200' # 化学
  '3250' # 医薬品
  '3300' # 石油・石炭製品
  '3350' # ゴム製品
  '3400' # ガラス・土石製品
  '3450' # 鉄鋼
  '3500' # 非鉄金属
  '3550' # 金属製品
  '3600' # 機械
  '3650' # 電気機器
  '3700' # 輸送機器
  '3750' # 精密機器
  '3800' # その他製品
  '4050' # 電気・ガス業
  '5050' # 陸運業
  '5100' # 海運業
  '5150' # 空運業
  '5200' # 倉庫・運輸関連業
  '5250' # 情報・通信
  '6050' # 卸売業
  '6100' # 小売業
  '7050' # 銀行業
  '7100' # 証券業
  '7150' # 保険業
  '7200' # その他金融業
  '8050' # 不動産業
  '9050' # サービス業

銘柄情報取得メソッド（get_brand）の戻り値は、BrandDataクラスのインスタンスです。

BrandDataについては、下記Data項を参照してください。

Data
====

PriceData::

  date      # 日時
  open      # 初値
  high      # 高値
  low       # 安値
  close     # 終値
  volume    # 出来高

FinanceData::

  market_cap        # 時価総額
  shares_issued     # 発行済株式数
  dividend_yield    # 配当利回り
  dividend_one      # 1株配当
  per               # 株価収益率
  pbr               # 純資産倍率
  eps               # 1株利益
  bps               # 1株純資産
  price_min         # 最低購入代金
  round_lot         # 単元株数
  years_high        # 年初来高値
  years_low         # 年初来安値

BrandData::

  ccode     # 証券コード
  market    # 市場
  name      # 銘柄名
  info      # 銘柄情報



## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Foceanection%2Fjsm.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Foceanection%2Fjsm?ref=badge_large)