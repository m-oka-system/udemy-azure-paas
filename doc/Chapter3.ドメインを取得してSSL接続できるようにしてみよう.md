# Chapter3.ドメインを取得してSSL接続できるようにしてみよう

## 参考サイト

- [Xdomainマニュアル](https://www.xdomain.ne.jp/manual/)

- [Azure App Service のカスタム ドメイン名を購入する](https://docs.microsoft.com/ja-jp/azure/app-service/manage-custom-dns-buy-domain)

- [App Service ドメインのプライバシー保護](https://jp.godaddy.com/domains/full-domain-privacy-and-protection)

- [Azure DNS による DNS ゾーンの委任](https://docs.microsoft.com/ja-jp/azure/dns/dns-domain-delegation)

- [チュートリアル:Azure DNS でドメインをホストする](https://docs.microsoft.com/ja-jp/azure/dns/dns-delegate-domain-azure-dns)


## コマンド集

#### ネームサーバ－の変更確認
```bash
dig udemy-azure-paas.xyz ns +short
```
