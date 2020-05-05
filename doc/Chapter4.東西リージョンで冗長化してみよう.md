# Chapter4.東西リージョンで冗長化してみよう

## 参考サイト

- [Traffic Manager のしくみ](https://docs.microsoft.com/ja-jp/azure/traffic-manager/traffic-manager-how-it-works)

- [Traffic Manager のルーティング方法](https://docs.microsoft.com/ja-jp/azure/traffic-manager/traffic-manager-routing-methods)

- [Load Balancer と Application Gateway の通信の違い](https://docs.microsoft.com/ja-jp/archive/blogs/jpaztech/lb_appgw_traffic_different)

- [Traffic Manager の価格](https://azure.microsoft.com/ja-jp/pricing/details/traffic-manager/)


## コマンド集

#### 自動フェールオーバーの動作確認
```bash
# 名前解決の結果を確認
dig paas-tm.trafficmanager.net +short

# HTTPリクエストの結果を確認
curl http://paas-tm.trafficmanager.net
```
