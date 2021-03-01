# テーブル 設計

## users テーブル

| Column           | Type                  | Options                                  |
|------------------|-----------------------|------------------------------------------|
| email            | string                | null: false, unique: true, index: true   |
| password         | string                | null: false                              |
| nickname         | string                | null: false                              |
| first_name       | string                | null: false                              |
| last_name        | string                | null: false                              |
| first_kana       | string                | null: false                              |
| family_name_kana | string                | null: false                              |
| birth_year       | t.date                | null: false                              |

### Association

- has_many :items
- has_many :shipping_address

## items テーブル

| Column            | Type       | Options                        |
|-------------------|------------|--------------------------------|
| name              | string     | null: false                    |
| price             | integer    | null: false                    |
| seller            | references | null: false, foreign_key: true |
| category          | references | null: false, foreign_key: true |
| product_condition | integer    |                                |
| shipping_charges  | integer    | null: false, foreign_key: true |
| shipping_area     | integer    | null: false, foreign_key: true |
| shipping_date     | integer    | null: false, foreign_key: true |
| brand             | integer    | null: false                    |
| image             | references | null: false, foreign_key: true |

### Association

- belongs_to :users
- has_one :shipping_address
- belongs_to_active_hash :product_condition
- belongs_to_active_hash :shipping_charges
- belongs_to_active_hash :shipping_area
- belongs_to_active_hash :shipping_date
- belongs_to_active_hash :brand

## shipping_address テーブル

| Column         | Type   | Options                        |
|----------------|--------|--------------------------------|
| postal_code    | string | null: false                    |
| prefecture     | string | null: false                    |
| city           | string | null: false                    |
| street_address | string | null: false                    |
| room_number    | string |                                |
| phone_number   | string | null: false                    |
| user           | string | null: false, foreign_key: true |

### Association

- belongs_to :users
- belongs_to :items