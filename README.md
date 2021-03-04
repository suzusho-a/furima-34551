# テーブル 設計

## users テーブル

| Column             | Type                  | Options                   |
|--------------------|-----------------------|---------------------------|
| email              | string                | null: false, unique: true |
| encrypted_password | string                | null: false               |
| nickname           | string                | null: false               |
| first_name         | string                | null: false               |
| last_name          | string                | null: false               |
| first_kana         | string                | null: false               |
| last_name_kana     | string                | null: false               |
| birth_year         | date                  | null: false               |

### Association

- has_many :items
- has_many :trades

## items テーブル

| Column               | Type    | Options                        |
|----------------------|---------|--------------------------------|
| name                 | string  | null: false                    |
| price                | integer | null: false                    |
| item description     | integer | null: false                    |
| category_id          | integer | null: false, foreign_key: true |
| product_condition_id | integer | null: false, foreign_key: true |
| shipping_charges_id  | integer | null: false, foreign_key: true |
| shipping_area_id     | integer | null: false, foreign_key: true |
| shipping_date_id     | integer | null: false, foreign_key: true |
| user                 | integer | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_one :trade
- belongs_to_active_hash :product_condition
- belongs_to_active_hash :shipping_charges
- belongs_to_active_hash :shipping_area
- belongs_to_active_hash :shipping_date
- belongs_to_active_hash :category

## shipping_address テーブル

| Column            | Type    | Options                        |
|-------------------|---------|--------------------------------|
| postal_code       | string  | null: false                    |
| shipping_area_id  | integer | null: false                    |
| city              | string  | null: false                    |
| street_address    | string  | null: false                    |
| room_number       | string  |                                |
| phone_number      | string  | null: false                    |
| trades_id         | string  | null: false                    |

### Association

- belongs_to :trade
- belongs_to_active_hash :shipping_area

## Trades テーブル

| Column  | Type       | Options                        |
|---------|------------|--------------------------------|
| buyer   | references | null: false, foreign_key: true |
| item    | references | null: false, foreign_key: true |
| user    | integer    | null: false, foreign_key: true |

### Association

- belongs_to :item
- belongs_to :user
- has_one :shipping_address