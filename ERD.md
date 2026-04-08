``` mermaid

erDiagram
    USERS ||--o{ TICKETS : "擁有"
    USERS ||--o{ USER_QUESTS : "參與"
    EVENTS ||--o{ TICKETS : "包含"
    QUESTS ||--o{ USER_QUESTS : "被執行"

    USERS {
        string user_id PK
        string email
        string wallet_address "託管錢包地址"
        int total_points "總貢獻分數"
    }

    EVENTS {
        string event_id PK
        string title
        string contract_address "智能合約地址"
        int total_tickets
        int remained_tickets "搶票庫存"
    }

    TICKETS {
        string ticket_id PK
        string user_id FK
        string event_id FK
        int token_id "鏈上 Token ID"
        string metadata_url "NFT 圖片路徑"
        string status "未使用/已核銷/轉售中"
    }

    QUESTS {
        string quest_id PK
        string title
        string quest_type "Social/Check-in"
        int point_reward
    }

    USER_QUESTS {
        string record_id PK
        string user_id FK
        string quest_id FK
        datetime completed_at
        boolean is_on_chain "是否已寫入貢獻證明"
    }
```
