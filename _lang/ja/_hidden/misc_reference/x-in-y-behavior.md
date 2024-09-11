---
nav_title: X in Y フィルターの動作
permalink: /x-in-y-behavior/
---

# 現在のX in Y フィルタの動作

これらのフィルターの動作はほとんど変わらず、以下の特性によって定義される：

- カレンダーの日数（午前0時で終了）を設定して実行する。
- 「日」はUTCで定義されている。
- 現在のUTCの日は "0 "と定義される。

{% details UTCの定義が "1 "から "0 "に変わったのはなぜか？ %}
ローカルタイムゾーンのスケジューリングでは、ユーザーが24時間セグメント内に留まる必要がある。Y=1日の場合、キャンペーンやキャンバスの対象者を決定する際に、24時間未満のユーザー履歴を評価しているケースがあった。

この変更は、フィルタをより直感的なものにし、「1日以内」に送信するスケジュールオプションなど、他のカレンダー機能の動作との一貫性を高める。
{% enddetails %}

<br>

## ユースケース

4月16日午後9時から、以下のキャンペーンを実施する。オーディエンスのセグメンテーションは「過去3日間に2回以上購入した」である。

![キャンペーンスケジュール][1]

4月16日午後9時（東部標準時）は4月17日午前1時（UTC）となる。

4月17日が「0日目」、4月16日が「1日目」、4月15日が「2日目」、4月14日が「3日目」となる。

4月14日午前12時（UTC）から現在（4月17日午前1時（UTC））までの履歴である。
これは、ユーザーの履歴の73時間を含むウィンドウに蓄積されることになる。

## カレンダー通り

暦日は、「X in Y」フィルターだけでなく、より多くの用途で使われる：

- メッセージのスケジューリング
- フリークエンシーキャップ
- 「X in Y」フィルター

`Calendar Days` とは、午前12:00に始まり同日午後11:59に終わる、番号の振られた1日の期間を指す（6月8日午前12:00から6月8日午後11:59までは1暦日となる）。

### フリークエンシーキャップ

`Frequency Capping` で "days "または "weeks "を選択すると、カレンダー・デーが使用される。

- `Every 1 day` は、ユーザーの現地時間における現在の暦日に上限を制限する（現地時間の深夜に終了する）。
- `Every 2 days` は、上限をユーザーの現地時間における前および現在の暦日に制限する（現在の暦日の現地時間午前0時に終了する）。

### 会社と現地時間

会社のタイムゾーンにおける現在のカレンダーの日が、日としてカウントされる`0` 。

`Send in 1 Calendar days at 11:05 am company time` または`send in 1 Calendar days at 11:05 am local time` 、それぞれ会社のタイムゾーンまたはローカルのタイムゾーンで、現在のカレンダーの日に`1` 、次に来る会社時間の午前11時5分にメッセージをスケジュールする。

会社時間または現地時間が太平洋時間の場合、ユーザーが4/13の8:00PTにキャンバスステップを入力すると、Brazeはこのキャンバスステップを4/14の11:05am PTにスケジュールする。

## 前へ X in Y フィルターの動作

Brazeには「X in Yフィルター」と呼ばれるセグメンテーション・フィルターがある。これらのフィルターはそれぞれ、以下の特徴によって定義された同様の機能を持つ：

- カレンダーの日数（午前0時で終了）を設定して実行する。
- 「日」はUTCで定義されている。
- 現在のUTCの日は "1 "と定義される。



[1]:{% image_buster /assets/img/campaign-schuedule-example.png %}