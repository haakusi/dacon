안녕하세요, 데이크루 3기 ‘투데이💰︎' 팀입니다! 

팀 투데이는 “투자에 데이터를 이용하다"의 약자입니다. 금융 데이터 수집&가공&모델링을 학습하면서 Financial Domain Knowledge와 Data Analysis Technologies 향상을 목적으로 하고 있습니다.

저희는 ‘금융데이터 전반’을 함께 공부하고, 공부한 내용을 게시글로써 데이콘 이용자분들과 함께 공유하고 있습니다. ‘투데이💰︎’의 첫번째 포스팅의 주제는 ‘금융 데이터수집’입니다. 

아래 링크를 들어가시면 ‘투데이💰︎’의 전 커리큘럼을 보실 수 있습니다. 

→ [투데이_1편] 금융 데이터수집💥 :

본 포스팅은 데이콘 서포터즈 “데이크루" 3기 활동의 일환입니다.

# 1. 주가 데이터 수집
## <img src = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAQlBMVEXw8PCKXdb19/GIWtaefdvy8vCDUdTd1uujhNzZ0er09fGBTdTg2+yZddmGVtWuld7s6+98RNPKvOW1n+DY0OmZdtmPAqRuAAABjklEQVR4nO3dSVYCQRBFUaQ6qIZO3f9WdeqoQk9kkSX3LiD4j8M4ORwAAADgVXUhO151GyLmjRMTV3XDvV83LcfiUaVWdUP/tq5pty7MW6VQYRkKFZa6lUehwlK38ihUWOpWHoUKS93Ko1BhqVt5FCosdSuPQoWlbuVRqLDUrTwKFZa6lUehwlK38ij8XeHUrLtsXpi3qpuXNuA6Fq8qtqo7RmwbWOsqAAAAAAAAAAAAAAAAAAAAeDVj6AWARFv/Zcj4ftpWO2yceDxdAi9xJJo+Ni9sAq+pJOrPChUqVKhQoUKFChUqVKhQoUKFChUqVKhQoUKFChUqVKjwD7qAJxSOkV2hwNsQMLdTv+4SGt8ELvXTIzQrktgN98gHLsN53SOS2HyGTkW+0WlJ/Z+Z9Z/M+IRTmYV7PVXpLIUK65+lUGH9sxQqrH+WQoX1z1KosP5ZChXWP0uhwvpnKVRY/yyFCuufpVBh/bMUKvx5awo8AHCJzarx1KGblzbgOu711Pex0EMcOz4FAAAA/9EXPLVeT6J/mGwAAAAASUVORK5CYII=" width=40 height=40> 1-1. Pykrx 

https://github.com/sharebook-kr/pykrx <br><br>
Pykrx는 (NAVER·KRX) 에서 주가정보를 스크래핑 합니다. <br>
국내 주가데이터 수집에 특화된 함수가 많습니다. 장중에 사용할 경우, 지연율이 높습니다. <br>

대표적으로 사용하는 함수 세가지를 살펴보겠습니다. <br>
- get_index_ticker_list(index) : 모든 지수(index)의 티커 조회
- get_market_trading_value_by_date(fromdate, todate, ticker) : 투자자별 거래실적 일별추이
- stock.get_index_ohlcv(fromdate, todate, ticker) : 특정 종목의 지정된 기간 OHLCV 조회 (...거래대금, 지수명, 코스피외국주포함)

        ! pip install pykrx

-

        import pandas as pd
        import numpy as np
        from pykrx import stock
        from pykrx import bond

### get_index_ticker_list(index) <br>
: 모든 지수(index)의 티커 조회 <br>

        for ticker in stock.get_index_ticker_list()[:10]:
            tickerName = stock.get_index_ticker_name(ticker)
            print(ticker, tickerName)
    
### get_market_trading_value_by_date(fromdate, todate, ticker) <br>
: 투자자별 거래실적 일별추이 <br>

        samsungTradingResult = stock.get_market_trading_value_by_date("20220101","20220505","005930")
            print(samsungTradingResult.head())

### stock.get_index_ohlcv(fromdate, todate, ticker) 
: 특정 종목의 지정된 기간 OHLCV 조회 (시가 고가 저가 종가 거래량 거래대금 지수명 코스피외국주포함..) <br>

        kospi = stock.get_index_ohlcv("20190101", "20220711", "1001")
            kospi[:10]

            
##<img src = "data:image/png;base64,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" width = 40 height=40> 1-2. FinanceDataReader

https://github.com/FinanceData/FinanceDataReader/wiki/<br><br>
FinanceDataReader는 (위키피디아·FRED·Investing·krx·nasdaq) 에서 주가정보를 스크래핑 합니다. <br>
한국/미국 주식 가격, 지수, 환율, 암호화폐 가격, 종목 리스팅 등 금융 데이터 수집 라이브러리 입니다.
