# README

# アプリケーション名
platune  
※現在作成途中となります。実装が追加される毎にREADMEを更新予定です。

# アプリケーション概要
アーティストや楽曲に関連する内容を投稿し、他のファンと交流できるプラットフォーム。

# 利用方法

## アーティスト追加
1．トップページのヘッダーからユーザーの新規登録を行う  
2．アーティスト追加ボタンから、アーティストを作成する

## 楽曲追加
1．アーティストのページより楽曲追加ボタンを押す

## 情報投稿
1．投稿先のアーティストもしくは楽曲を選択する  
2．情報投稿ボタンから、情報（LIVE情報、TV出演情報、楽曲の感想、楽曲の制作秘話など）を入力し投稿する

## コメント
1．コメントしたい投稿を選択する  
2．コメントボタンから、内容を入力し投稿する

# アプリケーションを作成した背景
ファンにとってアーティストの過去のインタビュー記事や楽曲の制作秘話などは興味深いものである。しかし、現状ではそのような貴重な情報を集めるための専用の場は限られており、情報が散逸してしまっていることが多い。platuneで投稿閲覧することによって新規ファンも過去の情報を辿ることができ、より音楽を楽しめるだろう。

# データベース設計
## users テーブル
| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| name       | string     | null: false                    |
| email      | string     | null: false, unique: true      |
| password   | string     | null: false                    |


### Association
- has_many :posts
- has_many :comments


## artists テーブル
| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| name       | string     | null: false, unique: true      |


### Association
- has_one :list
- has_many :songs

## songs テーブル
| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| title      | string     | null: false                    |
| artist     | references | null: false, foreign_key: true |


### Association
- belongs_to :artist


## posts テーブル
| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| user       | references | null: false, foreign_key: true |
| list       | references | null: false, foreign_key: true |
| content    | text       | null: false                    |


### Association
- belongs_to :user
- belongs_to :list
- has_many :comments


## comments テーブル
| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| user       | references | null: false, foreign_key: true |
| post       | references | null: false, foreign_key: true |
| content    | text       | null: false                    |

### Association
- belongs_to :user
- belongs_to :post

## lists テーブル
| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| artist     | references | null: false, foreign_key: true |
| name       | string     | null: false                    |


### Association
- belongs_to :artist
- has_many :posts


  

# 開発環境
| カテゴリ        | 技術          |
| --------------- | ----------   |
| フロントエンド   | CSS          |
| バックエンド     | Ruby on Rails|
| インフラ         | Render       |
| テスト           | RSpec        |
| テキストエディタ  | VS Code      |
| タスク管理       | GitHub Issues |

# 今後実装予定の内容
- ユーザーのお気に入りアーティスト機能
- 投稿に「いいね」機能を実装
- 投稿に「タグ」機能を追加する