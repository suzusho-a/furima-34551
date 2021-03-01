# テーブル 設計

## users テーブル

| Column             | Type                  | Options                   |
|--------------------|-----------------------|---------------------------|
| email              | string                | null: false, unique: true |
| password           | string                | null: false               |
| encrypted_password | string                | null: false               |
| nickname           | string                | null: false               |
| first_name         | string                | null: false               |
| last_name          | string                | null: false               |
| first_kana         | string                | null: false               |
| family_name_kana   | string                | null: false               |
| birth_year         | date                  | null: false               |

### Association

- has_many :items
- has_many :shipping_address

## items テーブル

| Column               | Type    | Options                        |
|----------------------|---------|--------------------------------|
| name                 | string  | null: false                    |
| price                | integer | null: false                    |
| category             | integer | null: false, foreign_key: true |
| product_condition_id | integer |                                |
| shipping_charges_id  | integer | null: false, foreign_key: true |
| shipping_area_id     | integer | null: false, foreign_key: true |
| shipping_date_id     | integer | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_one :shipping_address
- has_one :trade
- belongs_to_active_hash :product_condition
- belongs_to_active_hash :shipping_charges
- belongs_to_active_hash :shipping_area
- belongs_to_active_hash :shipping_date

## shipping_address テーブル

| Column         | Type    | Options                        |
|----------------|---------|--------------------------------|
| postal_code    | string  | null: false                    |
| prefecture_id  | integer | null: false                    |
| city           | string  | null: false                    |
| street_address | string  | null: false                    |
| room_number    | string  |                                |
| phone_number   | string  | null: false                    |
| user           | string  | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :item
- belongs_to_active_hash :prefecture

## Trades テーブル

| Column  | Type       | Options                        |
|---------|------------|--------------------------------|
| seller  | references | null: false, foreign_key: true |
| user_id | references | null: false, foreign_key: true |
| item_id | references | null: false, foreign_key: true |

### Association

- belongs_to :item