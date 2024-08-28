# GCP Google-Cloud-Functions
Google Cloud Function
Google API Using Yfinance to Get Stock Informations and News

# Python GCF Code to get Finacial Stock Data
requirements : python, yfinance

```python
import functions_framework
import yfinance as yf

@functions_framework.http
def yf_stock(request):
    """HTTP Cloud Function.
    Args: request (flask.Request): The request object
    Returns: The response text, or any set of values
    """
    request_json = request.get_json(silent=True)
    request_args = request.args

    if request_json and 'symbol' in request_json:
        symbol = request_json['symbol']
    elif request_args and 'symbol' in request_args:
        symbol = request_args['symbol']
    else:
        symbol = 'PLTR'  # Default symbol

    # YF Function to get info and news
    stock = yf.Ticker(symbol)
    news = stock.news
    info = stock.info
    if 'companyOfficers' in info:
        del info['companyOfficers']
    
    fnews = []
    for article in news:
        filtered_article = {
            'title': article.get('title'),
            'providerPublishTime': article.get('providerPublishTime'),
            'publisher': article.get('publisher'),
            'link': article.get('link'),
            'relatedTickers': article.get('relatedTickers')
        }
        fnews.append(filtered_article)
    info['news'] = fnews

    return info

```
> Requirements.txt file : 

```
functions_framework
yfinance
```



# How to use : 

> Curl or get to url :
```
https://europe-west1-your-project-id-xxxxxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/yf_stock` (defaut is AAPL)
```
-
> Curl a symbol :
```
https://europe-west1-your-project-id-xxxxxxxxxxxxxxxxxxxxxxx.cloudfunctions.net/yf_stock?symbol="PLTR"
```

----

> OUTPUT FOR PLTR :

```json
{
  "52WeekChange": 0.88854873,
  "SandP52WeekChange": 0.24606025,
  "address1": "1200 17th Street",
  "address2": "Floor 15",
  "ask": 30.27,
  "askSize": 1800,
  "auditRisk": 6,
  "averageDailyVolume10Day": 42579370,
  "averageVolume": 46338012,
  "averageVolume10days": 42579370,
  "beta": 2.704,
  "bid": 30.24,
  "bidSize": 900,
  "boardRisk": 10,
  "bookValue": 1.81,
  "city": "Denver",
  "compensationAsOfEpochDate": 1703980800,
  "compensationRisk": 10,
  "country": "United States",
  "currency": "USD",
  "currentPrice": 30.4095,
  "currentRatio": 5.916,
  "dateShortInterest": 1723680000,
  "dayHigh": 30.8,
  "dayLow": 30.21,
  "debtToEquity": 6.246,
  "earningsGrowth": 5,
  "earningsQuarterlyGrowth": 3.769,
  "ebitda": 325126016,
  "ebitdaMargins": 0.13114999,
  "enterpriseToEbitda": 201.19,
  "enterpriseToRevenue": 26.387,
  "enterpriseValue": 65412038656,
  "exchange": "NYQ",
  "fiftyDayAverage": 27.847,
  "fiftyTwoWeekHigh": 33.125,
  "fiftyTwoWeekLow": 13.68,
  "financialCurrency": "USD",
  "firstTradeDateEpochUtc": 1601472600,
  "floatShares": 1938672746,
  "forwardEps": 0.43,
  "forwardPE": 70.719765,
  "freeCashflow": 543769344,
  "fullTimeEmployees": 3661,
  "gmtOffSetMilliseconds": -14400000,
  "governanceEpochDate": 1722470400,
  "grossMargins": 0.81388,
  "heldPercentInsiders": 0.05149,
  "heldPercentInstitutions": 0.42481998,
  "impliedSharesOutstanding": 2239450112,
  "industry": "Software - Infrastructure",
  "industryDisp": "Software - Infrastructure",
  "industryKey": "software-infrastructure",
  "lastFiscalYearEnd": 1703980800,
  "longBusinessSummary": "Palantir Technologies Inc. builds and deploys software platforms for the intelligence community to assist in counterterrorism investigations and operations in the United States, the United Kingdom, and internationally. The company provides Palantir Gotham, a software platform which enables users to identify patterns hidden deep within datasets, ranging from signals intelligence sources to reports from confidential informants, as well as facilitates the handoff between analysts and operational users, helping operators plan and execute real-world responses to threats that have been identified within the platform. It also offers Palantir Foundry, a platform that transforms the ways organizations operate by creating a central operating system for their data; and allows individual users to integrate and analyze the data they need in one place. In addition, it provides Palantir Apollo, a software that delivers software and updates across the business, as well as enables customers to deploy their software virtually in any environment; and Palantir Artificial Intelligence Platform (AIP) that provides unified access to open-source, self-hosted, and commercial large language models (LLM) that can transform structured and unstructured data into LLM-understandable objects and can turn organizations' actions and processes into tools for humans and LLM-driven agents. The company was incorporated in 2003 and is headquartered in Denver, Colorado.",
  "longName": "Palantir Technologies Inc.",
  "marketCap": 68100558848,
  "maxAge": 86400,
  "messageBoardId": "finmb_43580005",
  "mostRecentQuarter": 1719705600,
  "netIncomeToCommon": 404552000,
  "news": [
    {
      "link": "https://finance.yahoo.com/news/analyst-says-palantir-technologies-pltr-120554926.html",
      "providerPublishTime": 1724846754,
      "publisher": "Insider Monkey",
      "relatedTickers": [
        "PLTR"
      ],
      "title": "Analyst Says Palantir Technologies’ (PLTR) AI Tech Solves Key Challenges in the Industry"
    },
    {
      "link": "https://finance.yahoo.com/m/361e5b5c-8ab0-3b71-84a8-4756f02cd6a4/better-artificial.html",
      "providerPublishTime": 1724842800,
      "publisher": "Motley Fool",
      "relatedTickers": [
        "PLTR"
      ],
      "title": "Better Artificial Intelligence Stock: Palantir vs. SoundHound AI"
    },
    {
      "link": "https://finance.yahoo.com/m/4586276d-8275-3d1a-a312-661a5af51f05/billionaires-are-buying-these.html",
      "providerPublishTime": 1724837700,
      "publisher": "Motley Fool",
      "relatedTickers": [
        "PLTR",
        "BROS"
      ],
      "title": "Billionaires Are Buying These 2 Incredible Growth Stocks"
    },
    {
      "link": "https://finance.yahoo.com/news/pltr-vs-googl-technology-stock-070200990.html",
      "providerPublishTime": 1724828520,
      "publisher": "TipRanks",
      "relatedTickers": [
        "GOOG",
        "PLTR"
      ],
      "title": "PLTR vs. GOOGL: Which Technology Stock Is Better?"
    },
    {
      "link": "https://finance.yahoo.com/news/expect-domo-domo-q2-earnings-070146100.html",
      "providerPublishTime": 1724828506,
      "publisher": "StockStory",
      "relatedTickers": [
        "DOMO",
        "PLTR"
      ],
      "title": "What To Expect From Domo’s (DOMO) Q2 Earnings"
    },
    {
      "link": "https://finance.yahoo.com/news/palantir-technologies-inc-pltr-trending-150501923.html",
      "providerPublishTime": 1724771101,
      "publisher": "Insider Monkey",
      "relatedTickers": [
        "PLTR"
      ],
      "title": "Palantir Technologies Inc. (PLTR): Trending AI Stock on Latest Analyst Ratings and News"
    },
    {
      "link": "https://finance.yahoo.com/news/paymentus-pay-outperforming-other-business-134016584.html",
      "providerPublishTime": 1724766016,
      "publisher": "Zacks",
      "relatedTickers": [
        "PAY",
        "PLTR"
      ],
      "title": "Is Paymentus (PAY) Outperforming Other Business Services Stocks This Year?"
    },
    {
      "link": "https://finance.yahoo.com/m/a52329a2-4315-3040-abf0-c6efaebf0c85/3-stocks-making-52-week-highs.html",
      "providerPublishTime": 1724753700,
      "publisher": "Motley Fool",
      "relatedTickers": [
        "MELI",
        "PLTR",
        "WMT"
      ],
      "title": "3 Stocks Making 52-Week Highs That Are Screaming Buys Right Now"
    }
  ],
  "nextFiscalYearEnd": 1735603200,
  "numberOfAnalystOpinions": 16,
  "open": 30.62,
  "operatingCashflow": 708380992,
  "operatingMargins": 0.15534,
  "overallRisk": 10,
  "pegRatio": 1.01,
  "phone": "720 358 3679",
  "previousClose": 30.84,
  "priceHint": 2,
  "priceToBook": 16.800829,
  "priceToSalesTrailing12Months": 27.47119,
  "profitMargins": 0.16319,
  "quickRatio": 5.772,
  "quoteType": "EQUITY",
  "recommendationKey": "hold",
  "recommendationMean": 2.9,
  "regularMarketDayHigh": 30.8,
  "regularMarketDayLow": 30.21,
  "regularMarketOpen": 30.62,
  "regularMarketPreviousClose": 30.84,
  "regularMarketVolume": 6927168,
  "returnOnAssets": 0.03979,
  "returnOnEquity": 0.114870004,
  "revenueGrowth": 0.272,
  "revenuePerShare": 1.127,
  "sector": "Technology",
  "sectorDisp": "Technology",
  "sectorKey": "technology",
  "shareHolderRightsRisk": 10,
  "sharesOutstanding": 2142320000,
  "sharesPercentSharesOut": 0.0269,
  "sharesShort": 60156736,
  "sharesShortPreviousMonthDate": 1721001600,
  "sharesShortPriorMonth": 81122898,
  "shortName": "Palantir Technologies Inc.",
  "shortPercentOfFloat": 0.030199999,
  "shortRatio": 1.1,
  "state": "CO",
  "symbol": "PLTR",
  "targetHighPrice": 38,
  "targetLowPrice": 9,
  "targetMeanPrice": 25.69,
  "targetMedianPrice": 28,
  "timeZoneFullName": "America/New_York",
  "timeZoneShortName": "EDT",
  "totalCash": 3998458880,
  "totalCashPerShare": 1.785,
  "totalDebt": 258459008,
  "totalRevenue": 2478981120,
  "trailingEps": 0.17,
  "trailingPE": 178.87941,
  "trailingPegRatio": 1.9114,
  "twoHundredDayAverage": 22.70145,
  "underlyingSymbol": "PLTR",
  "uuid": "0ea79370-ee21-3603-b0a1-16f5e7b345f1",
  "volume": 6927168,
  "website": "https://www.palantir.com",
  "zip": "80202"
}
```
