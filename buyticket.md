```mermard
graph TD
    %% 節點樣式設定
    classDef entity fill:#f9f,stroke:#333,stroke-width:2px;
    classDef process fill:#bbf,stroke:#333,stroke-width:2px;
    classDef storage fill:#fff,stroke:#333,stroke-width:2px;

    %% 實體與程序定義
    User([粉絲前端介面]) :::entity
    Xaman([Xaman 錢包 App]) :::entity
    
    P1((1.0 <br> 票券查詢與 <br> 限購檢查)) :::process
    P2((2.0 <br> 發起交易與 <br> 簽章審查)) :::process
    P3((3.0 <br> 智慧合約 <br> 門票鑄造)) :::process
    
    D1[[(D1) 票券場次表 <br> Tickets / Events]] :::storage
    D2[[(D2) 交易紀錄表 <br> Transactions]] :::storage

    %% 資料流向連線
    User -->|選擇場次與座位| P1
    P1 -->|查詢剩餘票數與錢包限額| D1
    D1 -->|回傳可購狀態| P1
    P1 -->|呈現購票付款 QR Code| User
    
    User -->|手機掃描 QR Code| Xaman
    Xaman -->|滑動確認授權簽章| P2
    P2 -->|轉發已簽署交易雜湊值| P3
    
    P3 -->|合約邏輯判定扣款成功| P3
    P3 -->|發動 NFTokenMint 鑄造 NFT| D1
    P3 -->|異步回傳成功區塊鏈事件| D2
    D2 -->|即時推播更新數據| User
```
