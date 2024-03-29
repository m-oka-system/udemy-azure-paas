# Chapter5.SQLDatabaseを使ってみよう

## 参考サイト

- [Azure SQL Database の価格](https://azure.microsoft.com/ja-jp/pricing/details/azure-sql-database/single/)

- [チュートリアル: アクティブ geo レプリケーションとフェールオーバーを構成する (Azure SQL Database)](https://learn.microsoft.com/ja-jp/azure/azure-sql/database/active-geo-replication-configure-portal?view=azuresql&tabs=portal)

- [Azure SQL Database の自動フェールオーバー グループを構成する](https://learn.microsoft.com/ja-jp/azure/azure-sql/database/auto-failover-group-configure-sql-db?view=azuresql&tabs=azure-portal&pivots=azure-sql-single-db)

- [Azure Data Studio のダウンロードとインストール](https://learn.microsoft.com/ja-jp/sql/azure-data-studio/download-azure-data-studio)

## コマンド集

#### データベース照合順序
```sql
-- 1文字目のCは「大文字小文字」、Aは「アクセント(濁点、半濁点)」
-- 2文字目のS (Sensitive)は区別する、I(Insensitive)は区別しない
-- CI = 大文字と小文字を区別しない
-- AS = 濁点や半濁点などの有無を区別する
Japanese_CI_AS
```

#### テーブルの作成
```sql
-- テーブルの作成
create table cloud (id int not null primary key, name varchar(100));

-- テーブルにデータを挿入
insert into cloud values (1, 'Azure');
insert into cloud values (2, 'AWS');
insert into cloud values (3, 'GCP');

-- テーブルを表示
select * from cloud;
```

#### データベースレベルのファイアウォール規則
```sql
-- ルールの作成
-- start_ip_address、end_ip_addressには一般的には接続元PCのグローバルIPアドレスを入力
exec sp_set_database_firewall_rule
    @name=N'Client1_dblevelrule',
    @start_ip_address = 'xxx.xxx.xxx.xxx',
    @end_ip_address = 'xxx.xxx.xxx.xxx'

-- ルールの確認
select * from sys.database_firewall_rules

-- ルールの削除
exec sp_delete_database_firewall_rule N'Client1_dblevelrule'
```

#### 手動フェールオーバーの動作確認
```sql
# 読み取り/書き込みのリスナーエンドポイントのDNS応答を確認
dig paas-fog.database.windows.net +short
# 読み取り専用のリスナーエンドポイントのDNS応答を確認
dig paas-fog.secondary.database.windows.net +short

# プライマリデータベースに接続
sqlcmd -U sqladmin -P My5up3rStr0ngPaSw0rd! -S paas-fog.database.windows.net -d MyDatabase
# ホスト名を確認
select @@servername;
# cloudテーブルをSELECT
select * from cloud;

# セカンダリデータベースに接続
sqlcmd -U sqladmin -P My5up3rStr0ngPaSw0rd! -S paas-fog.secondary.database.windows.net -d MyDatabase
# ホスト名を確認
select @@servername;
# cloudテーブルをSELECT
select * from cloud;
# 読み取り専用なので削除できない
delete cloud;
```
