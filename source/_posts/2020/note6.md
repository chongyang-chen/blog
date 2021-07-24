---
title: CTP Java API Demo
date: 2018-01-29 20:36:03
tags:
- CTP
categories:
- CTP
---

### Java Demo

1. 打开Eclipse，新建traderapidemo工程。

2. 在工程中新建lib文件夹，将刚刚的thosttraderapi.jar包拷贝到该文件夹底下，刷新工程，在工程中jar包上右击选择BuildPath/Add to Build Path将jar包导入到工程。
<!-- more -->
3. 将如下动态库文件
thosttraderapi.dll 
thosttraderapi_wrap.dll
拷贝到你电脑环境变量path路径底下，如果自己不清楚，可以在Java中用如下代码获得:
```
System.out.println(System.getProperty("java.library.path"));
```

我直接拷贝到了\Java\jdk1.8.0_111底下。 

#### 完整的tradeapidemo代码如下：

```
package traderapidemo;

import test.thosttraderapi.*;;

class TraderSpiImpl extends CThostFtdcTraderSpi{    
    final static String m_BrokerId = "8000";
    final static String m_UserId = "000326";
    final static String m_InvestorId = "000326";
    final static String m_PassWord = "password"; 
    final static String m_TradingDay = "20161111";
    final static String m_AccountId = "000326";
    final static String m_CurrencyId = "CNY";
    TraderSpiImpl(CThostFtdcTraderApi traderapi)
    {
        m_traderapi =  traderapi;
    }

    @Override
    public void OnFrontConnected(){
        System.out.println("On Front Connected");
        CThostFtdcReqUserLoginField field = new CThostFtdcReqUserLoginField();
        field.setBrokerID(m_BrokerId);
        field.setUserID(m_UserId);
        field.setPassword(m_PassWord);
        field.setUserProductInfo("JAVA_API");
        m_traderapi.ReqUserLogin(field,0);
        System.out.println("Send login ok");
    }

    @Override
    public void OnRspUserLogin(CThostFtdcRspUserLoginField pRspUserLogin, CThostFtdcRspInfoField pRspInfo, int nRequestID, boolean bIsLast)
    {
        if (pRspInfo != null && pRspInfo.getErrorID() != 0)
        {
            System.out.printf("Login ErrorID[%d] ErrMsg[%s]\n", pRspInfo.getErrorID(), pRspInfo.getErrorMsg());

            return;
        }
        System.out.println("Login success!!!");
        CThostFtdcQryTradingAccountField qryTradingAccount = new CThostFtdcQryTradingAccountField();
        qryTradingAccount.setBrokerID(m_BrokerId);
        qryTradingAccount.setCurrencyID(m_CurrencyId);;
        qryTradingAccount.setInvestorID(m_InvestorId);
        m_traderapi.ReqQryTradingAccount(qryTradingAccount, 1);

    }

    @Override
    public void OnRspQryTradingAccount(CThostFtdcTradingAccountField pTradingAccount, CThostFtdcRspInfoField pRspInfo, int nRequestID, boolean bIsLast) 
    {
        if (pRspInfo != null && pRspInfo.getErrorID() != 0)
        {
            System.out.printf("OnRspQryTradingAccount ErrorID[%d] ErrMsg[%s]\n", pRspInfo.getErrorID(), pRspInfo.getErrorMsg());

            return;
        }

        if (pTradingAccount != null)
        {
            System.out.printf("Balance[%f]Available[%f]WithdrawQuota[%f]Credit[%f]\n",
                pTradingAccount.getBalance(), pTradingAccount.getAvailable(), pTradingAccount.getWithdrawQuota(),
                pTradingAccount.getCredit());
        }
        else
        {
            System.out.printf("NULL obj\n");
        }
    }   

    private CThostFtdcTraderApi m_traderapi;
}

public class demo {

    static{
        System.loadLibrary("thosttraderapi");
        System.loadLibrary("thosttraderapi_wrap");
    }
    final static String ctp1_TradeAddress = "tcp://180.168.146.187:10010";
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        CThostFtdcTraderApi traderApi = CThostFtdcTraderApi.CreateFtdcTraderApi();
        TraderSpiImpl pTraderSpi = new TraderSpiImpl(traderApi);
        traderApi.RegisterSpi(pTraderSpi);
        traderApi.RegisterFront(ctp1_TradeAddress);
        traderApi.SubscribePublicTopic(THOST_TE_RESUME_TYPE.THOST_TERT_RESTART);
        traderApi.SubscribePrivateTopic(THOST_TE_RESUME_TYPE.THOST_TERT_RESTART);
        traderApi.Init();
        traderApi.Join();
        return;
    }
}
```

#### 行情mdapidemo如下:

```

package mdapidemo;

import test.thostmduserapi.*;

class mdspiImpl extends CThostFtdcMdSpi{
    final static String m_BrokerId = "8000";
    final static String m_UserId = "000326";
    final static String m_InvestorId = "000326";
    final static String m_PassWord = "1"; 
    final static String m_TradingDay = "20161111";
    final static String m_AccountId = "000326";
    final static String m_CurrencyId = "CNY";
    mdspiImpl(CThostFtdcMdApi mdapi)
    {
        m_mdapi =  mdapi;
    }

    public void OnFrontConnected(){
        System.out.println("On Front Connected");
        CThostFtdcReqUserLoginField field = new CThostFtdcReqUserLoginField();
        field.setBrokerID(m_BrokerId);
        field.setUserID(m_UserId);
        field.setPassword(m_PassWord);
        m_mdapi.ReqUserLogin(field, 0);

    }

    public void OnRspUserLogin(CThostFtdcRspUserLoginField pRspUserLogin, CThostFtdcRspInfoField pRspInfo, int nRequestID, boolean bIsLast) {
        if (pRspUserLogin != null) {
            System.out.printf("Brokerid[%s]\n",pRspUserLogin.getBrokerID());            
        }

        String[] instruementid = new String[1];
        instruementid[0]="sc1308";      
        m_mdapi.SubscribeMarketData(instruementid,1);
    }

    public void OnRtnDepthMarketData(CThostFtdcDepthMarketDataField pDepthMarketData) {
        if (pDepthMarketData != null)
        {
            System.out.printf("AskPrice1[%f]BidPrice1[%f]\n",
                pDepthMarketData.getAskPrice1(),pDepthMarketData.getBidPrice1());
        }
        else
        {
            System.out.printf("NULL obj\n");
        }
    }   
    private CThostFtdcMdApi m_mdapi;
}

public class MdapiDemo {
    static{
        System.loadLibrary("thostmduserapi");
        System.loadLibrary("thostmduserapi_wrap");
    }
    final static String ctp1_MdAddress = "tcp://172.19.125.39:50235";
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        CThostFtdcMdApi mdApi = CThostFtdcMdApi.CreateFtdcMdApi();
        mdspiImpl pMdspiImpl = new mdspiImpl(mdApi);
        mdApi.RegisterSpi(pMdspiImpl);
        mdApi.RegisterFront(ctp1_MdAddress);
        mdApi.Init();
        mdApi.Join();       
        return;
    }
}
```
