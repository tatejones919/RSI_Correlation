#import the libraries
from fastquant import get_stock_data
from fastquant import get_crypto_data
from pandas_datareader import data as pdr
import yfinance as yf
import plotly.graph_objects as go
import pandas as pd
from datetime import datetime
#set a date variable
now = datetime.today().strftime('%Y-%m-%d')
print('current date: ', now)
#pull in the data
BTC = get_crypto_data("BTC/USDT", "2020-01-01", now) 
print('1/16 done')
LINK = get_crypto_data("LINK/USDT", "2020-01-01", now) 
print('2/16 done')
ZRX = get_crypto_data("ZRX/USDT", "2020-01-01", now) 
print('3/16 done')
YFI = get_crypto_data("YFI/USDT", "2020-01-01", now) 
print('4/16 done')
UNI = get_crypto_data("UNI/USDT", "2020-01-01", now) 
print('5/16 done')
OMG = get_crypto_data("OMG/USDT", "2020-01-01", now) 
print('6/16 done')
ETH = get_crypto_data("ETH/USDT", "2020-01-01", now)
print('7/16 done')
XRP = get_crypto_data("XRP/USDT", "2020-01-01", now)
print('8/16 done')
LTC = get_crypto_data("LTC/USDT", "2020-01-01", now)
print('9/16 done')
COMP = get_crypto_data("COMP/USDT", "2020-01-01", now)
print('10/16 done')
BNB = get_crypto_data("BNB/USDT", "2020-01-01", now)
print('11/16 done')
SUSHI = get_crypto_data("SUSHI/USDT", "2020-01-01", now)
print('12/16 done')
TRX = get_crypto_data("TRX/USDT", "2020-01-01", now)
print('13/16 done')
BAND = get_crypto_data("BAND/USDT", "2020-01-01", now)
print('14/16 done')
EOS = get_crypto_data("EOS/USDT", "2020-01-01", now)
print('15/16 done')
ZEC = get_crypto_data("ZEC/USDT", "2020-01-01", now)
print('16/16 done')
#reset the indexes of each df
BTC = BTC.reset_index()
LINK = LINK.reset_index()
ZRX = ZRX.reset_index()
YFI = YFI.reset_index()
UNI = UNI.reset_index()
OMG = OMG.reset_index()
ETH = ETH.reset_index()
XRP = XRP.reset_index()
LTC = LTC.reset_index()
COMP = COMP.reset_index()
BNB = BNB.reset_index()
SUSHI = SUSHI.reset_index()
TRX = TRX.reset_index()
BAND = BAND.reset_index()
EOS = EOS.reset_index()
ZEC = ZEC.reset_index()
print('btc: ', BTC.head())
#keep only the date and the close column
#rename the cloumns
BTC = BTC[['dt','close']].rename(columns={"dt": "Date", "close": "btc_close"})
LINK = LINK[['dt','close']].rename(columns={"dt": "Date", "close": "link_close"})
ZRX = ZRX[['dt','close']].rename(columns={"dt": "Date", "close": "zrx_close"})
YFI = YFI[['dt','close']].rename(columns={"dt": "Date", "close": "yfi_close"})
UNI = UNI[['dt','close']].rename(columns={"dt": "Date", "close": "uni_close"})
OMG = OMG[['dt','close']].rename(columns={"dt": "Date", "close": "omg_close"})
ETH = ETH[['dt','close']].rename(columns={"dt": "Date", "close": "eth_close"})
XRP = XRP[['dt','close']].rename(columns={"dt": "Date", "close": "xrp_close"})
LTC = LTC[['dt','close']].rename(columns={"dt": "Date", "close": "ltc_close"})
COMP = COMP[['dt','close']].rename(columns={"dt": "Date", "close": "comp_close"})
BNB = BNB[['dt','close']].rename(columns={"dt": "Date", "close": "bnb_close"})
SUSHI = SUSHI[['dt','close']].rename(columns={"dt": "Date", "close": "sushi_close"})
TRX = TRX[['dt','close']].rename(columns={"dt": "Date", "close": "trx_close"})
BAND = BAND[['dt','close']].rename(columns={"dt": "Date", "close": "band_close"})
EOS = EOS[['dt','close']].rename(columns={"dt": "Date", "close": "eos_close"})
ZEC = ZEC[['dt','close']].rename(columns={"dt": "Date", "close": "zec_close"})
print('btc: \n ', BTC.head())
#merge all the dataframes
df = pd.merge(BTC, LINK, on='Date', how='left')
df = pd.merge(df, ZRX, on='Date', how='left')
df = pd.merge(df, YFI, on='Date', how='left')
df = pd.merge(df, UNI, on='Date', how='left')
df = pd.merge(df, OMG, on='Date', how='left')
df = pd.merge(df, ETH, on='Date', how='left')
df = pd.merge(df, XRP, on='Date', how='left')
df = pd.merge(df, LTC, on='Date', how='left')
df = pd.merge(df, COMP, on='Date', how='left')
df = pd.merge(df, BNB, on='Date', how='left')
df = pd.merge(df, SUSHI, on='Date', how='left')
df = pd.merge(df, TRX, on='Date', how='left')
df = pd.merge(df, BAND, on='Date', how='left')
df = pd.merge(df, EOS, on='Date', how='left')
df = pd.merge(df, ZEC, on='Date', how='left')
print(df.info)
#rsi function
def computeRSI (data, time_window):
    diff = data.diff(1).dropna() # diff in one field(one day)
#this preservers dimensions off diff values
    up_chg = 0 * diff
    down_chg = 0 * diff
    
    # up change is equal to the positive difference, otherwise equal to zero
    up_chg[diff > 0] = diff[ diff>0 ]
    
    # down change is equal to negative deifference, otherwise equal to zero
    down_chg[diff < 0] = diff[ diff < 0 ]
    
    # check pandas documentation for ewm
    # https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.ewm.html
    # values are related to exponential decay
    # we set com=time_window-1 so we get decay alpha=1/time_window
    up_chg_avg = up_chg.ewm(com=time_window-1, min_periods=time_window).mean()
    down_chg_avg = down_chg.ewm(com=time_window-1, min_periods=time_window).mean()
    
    rs = abs(up_chg_avg/down_chg_avg)
    rsi = 100 - 100/(1+rs)
    return rsi
#run the function for each column
df['btc_close'] = computeRSI(df['btc_close'], 14)
df['link_close'] = computeRSI(df['link_close'], 14)
df['zrx_close'] = computeRSI(df['zrx_close'], 14)
df['yfi_close'] = computeRSI(df['yfi_close'], 14)
df['uni_close'] = computeRSI(df['uni_close'], 14)
df['omg_close'] = computeRSI(df['omg_close'], 14)
df['eth_close'] = computeRSI(df['eth_close'], 14)
df['xrp_close'] = computeRSI(df['xrp_close'], 14)
df['ltc_close'] = computeRSI(df['ltc_close'], 14)
df['comp_close'] = computeRSI(df['comp_close'], 14)
df['bnb_close'] = computeRSI(df['bnb_close'], 14)
df['sushi_close'] = computeRSI(df['sushi_close'], 14)
df['trx_close'] = computeRSI(df['trx_close'], 14)
df['band_close'] = computeRSI(df['band_close'], 14)
df['eos_close'] = computeRSI(df['eos_close'], 14)
df['zec_close'] = computeRSI(df['zec_close'], 14)
#set the high and low lines (as columns)
df['low'] = 30
df['high'] = 70
df.head(20)
#plot it!
fig = go.Figure()
#create lines/traces
fig.add_trace(go.Scatter(x=df['Date'], y=df['btc_close'],
                    mode='lines',
                    name='BTC',
                    line=dict(color="Silver", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['link_close'],
                    mode='lines',
                    name='LINK',
                    line=dict(color="orange", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['zrx_close'],
                    mode='lines',
                    name='ZRX',
                    line=dict(color="royalblue", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['yfi_close'],
                    mode='lines',
                    name='YFI',
                    line=dict(color="LightGreen", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['uni_close'],
                    mode='lines',
                    name='UNI',
                    line=dict(color="MediumPurple", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['omg_close'],
                    mode='lines',
                    name='OMG',
                    line=dict(color="Red", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['eth_close'],
                    mode='lines',
                    name='ETH',
                    line=dict(color="Aqua", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['xrp_close'],
                    mode='lines',
                    name='XRP',
                    line=dict(color="Gold", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['ltc_close'],
                    mode='lines',
                    name='LTC',
                    line=dict(color="Yellow", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['comp_close'],
                    mode='lines',
                    name='COMP',
                    line=dict(color="lightseagreen", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['bnb_close'],
                    mode='lines',
                    name='BNB',
                    line=dict(color="darkturquoise", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['sushi_close'],
                    mode='lines',
                    name='SUSHI',
                    line=dict(color="slateblue", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['trx_close'],
                    mode='lines',
                    name='TRX',
                    line=dict(color="firebrick", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['band_close'],
                    mode='lines',
                    name='BAND',
                    line=dict(color="turquoise", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['eos_close'],
                    mode='lines',
                    name='EOS',
                    line=dict(color="olivedrab", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['zec_close'],
                    mode='lines',
                    name='ZEC',
                    line=dict(color="maroon", width=1),))
fig.add_trace(go.Scatter(x=df['Date'], y=df['high'],
                         fill=None,
                         mode='lines',
                         line=dict(width=0.5, color='rgb(222, 196, 255)', dash='dash')))
fig.add_trace(go.Scatter(x=df['Date'],y=df['low'],
                         fill='tonexty', # fill area between trace0 and trace1
                         mode='lines',
                         line=dict(width=0.5, color='rgb(222, 196, 255)', dash='dash')))
#update axis ticks
fig.update_yaxes(nticks=30,showgrid=True)
fig.update_xaxes(nticks=12,showgrid=True)
#update layout
fig.update_layout(title="<b>Daily RSI</b>"
                 , height = 700
                 , xaxis_title='Date'
                 , yaxis_title='Relative Strength Index'
                 , template = "plotly" #['ggplot2', 'seaborn', 'simple_white', 'plotly', 'plotly_white', 'plotly_dark']
                 )
#update legend
fig.update_layout(legend=dict(
    orientation="h",
    yanchor="bottom",
    y=1.02,
    xanchor="right",
    x=1
))
#show the figure
fig.show()