graph DT
    subgraph Client_Layer ["前端展示層"]
        App["Mobile App (React Native)"]
    end

    subgraph Logic_Layer ["後端邏輯層 (Web 2.5)"]
        API["Node.js / Express API"]
        KMS["Cloud KMS (私鑰代管)"]
    end

    subgraph Data_Layer ["資料存儲層"]
        DB[(PostgreSQL)]
        IPFS["IPFS (NFT 圖片儲存)"]
    end

    subgraph Web3_Layer ["區塊鏈協定層"]
        SC["Solidity Smart Contract"]
        BC["Polygon (Layer 2)"]
    end

    App <--> API
    API <--> DB
    API <--> KMS
    API <--> SC
    SC --- BC
    SC -.-> IPFS
