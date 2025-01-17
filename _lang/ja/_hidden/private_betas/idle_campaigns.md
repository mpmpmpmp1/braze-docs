---
nav_title: "アイドルキャンペーンとキャンバス"
permalink: "/idle_campaigns_canvases/"
hidden: true
---

# アイドル状態のキャンペーンとキャンバス

> このリファレンス記事では、キャンペーンとキャンバスのアイドルステータスについて説明し、よくある質問への回答を提供します。

{% alert note %}
2024年、キャンバスは**アイドル**とマークされ、キャンペーンs と同様に停止します。キャンバスがアイドル状態または停止状態になると、このドキュメントのロジックに従います。
{% endalert %}

キャンペーンとキャンバスには、しばらくの間、メッセージを送信したり、ユーザーs を入力したりしなかったときに、アイドルステータスが割り当てられます。これらのキャンペーンとキャンバスは、関連付けられた停止日時に自動的に停止します。アイドル状態のキャンペーンやキャンバスをフィルターすると、キャンペーンやキャンバスの一覧を並べ替えたり管理したりできます。

## アイドルキャンペーンs

継続的に、次の基準を満たすアイドルキャンペーンs は停止されます。
 
- スケジュールされたのワンタイム送信は、送信日を7日間過ぎています
- 終了日があるスケジュールされたまたはアクション ベースのキャンペーンは、終了日を7 日過ぎています
- 1年間にメールを送信しなかった、終了日のないキャンペーン

終了日のないキャンペーンの場合、メッセージが送信されるか、キャンペーンが更新dの場合、キャンペーンを停止するための1年間のカウントダウンが再設定されます。キャンペーン s が停止すると、Braze は顧客にダッシュボードとメールで通知します。

キャンペーンは、デフォルト終了日の後日、および最後に発生したコンバージョン期限の1 日後に停止されます。Winning またはPersonalized Variant の送信はスケジュールされた送信として扱われ、Winning またはPersonalized Variant の送信から7 日後に停止されます。すべてのキャンペーンs は、すべてのBraze ユーザーs について毎日UTC の午前4 時に停止します。

コンテンツカードは、期限が切れるまで停止せず、上記の基準およびコンバージョン期限規則を遵守します。

アイドルキャンペーンを有効にする方法については、このテーブルを参照してください。

| アイドルステータスの理由                                                                              | キャンペーンを有効にする手順                     |
|-----------------------------------------------------------------------------------------------------|---------------------------------------------------|
| スケジュールされた1回送信されるキャンペーンで、送信日の7日間が過ぎています                 | 今後の送信をスケジュールする                            |
| スケジュールされたベースまたはアクションベースのキャンペーンで、終了日があり、終了日の7 日後のキャンペーン | 終了日の延長                               |
| 1年以内にメッセージを送信しなかった終了日のないキャンペーン                                | メールを1件送信するか、キャンペーンに修正する |
{: .reset-td-br-1 .reset-td-br-2}

## アイドルキャンバス

継続的に、次の基準を満たすアイドル状態のキャンバスは停止されます。

- スケジュールされたのワンタイム送信が送信日を超えており、最長で7日間
- 終了日が指定されたスケジュールされたまたはアクションベースのキャンバスは、終了日を過ぎており、最長で7 日間継続します
- 終了日のないキャンバスがユーザーに入力されていないか、12 か月以上編集されていないか、その最長継続時間

終了日のないキャンバスの場合、ユーザーが入力されているか、キャンバスが更新d の場合、キャンバスを停止するための1 年間のカウントダウンがリセットされます。キャンバスが停止すると、Brazeは顧客にダッシュボードとメールで通知します。

キャンバスの[最大継続時間]({{site.baseurl}}/user_guide/engagement_tools/canvas/create_a_canvas/create_a_canvas/)は、ユーザーが特定のキャンバスを完成するのに要する最長時間です。この期間には、コンテンツカードとアプリ内メッセージの有効期限が含まれます。

アイドル状態のキャンバスをアクティブにする方法については、次の表を参照してください。

| アイドルステータスの理由                                                                                                  | キャンバスをアクティブにする手順                     |
|-------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| 1 回限りの送信をスケジュールされたするキャンバスで、送信日の7 日後で最長継続時間です                 | 今後の送信をスケジュールする                          |
| スケジュールされたベースまたはアクションベースで、終了日があり、終了日の7 日後で最長継続時間が経過しているキャンバス | 終了日の延長                             |
| 1年以内にメッセージを送信しなかった終了日のないキャンバス                                                      | 1 つのメッセージを送信するか、キャンバスに編集を加えます |
{: .reset-td-br-1 .reset-td-br-2}

## よくある質問

#### このアプリはどのキャンペーンやキャンバスに向いていますか?

これにより、すでにリストされている基準を満たしているキャンペーン s とキャンバス、および前に進む基準を満たすキャンペーン s とキャンバスがアプリされます。

#### キャンペーンまたはキャンバスがアイドル状態かどうかは、どのようにすればわかりますか?

アイドルキャンペーンs とキャンバスは、アイドルカテゴリのキャンペーンとキャンバスリストページに表示されます。キャンペーンまたはキャンバスを停止する日が、一覧の列として表示されます。

#### アイドル状態のキャンペーンまたはキャンバスが更新dの場合、どのアプリが終了しますか?

メッセージを送信していないキャンペーン、またはユーザーに入力されていないキャンバスが更新 d の場合、カウントダウンは再設定されます。

#### 1年以内にメッセージを送っていない(または、1年以内にユーザーに入っていないキャンバス)が、将来終了日を持っているキャンペーンに寄るアプリは?

このキャンペーンとキャンバスは、終了日から7日後にストップします。

#### 停止したキャンペーンのSとキャンバスに関するメール 通知を受け取るのは?

デフォルトでは、管理者権限を持つすべてのユーザーは、キャンペーンとキャンバスの自動停止に関するメール 通知に選択されます。キャンペーンまたはキャンバスの作成者は、停止すると必ず通知されます。ユーザは、**Company Settings**> **通知 Preferences**に移動し、通知**Campaign Automatically Stopped**と通知**Canvas Automatically Stopped**から受信者sを追加または削除することで、メール 通知の環境設定を管理できます。

#### コンテンツカードの停止はどのように機能しますか?

キャンペーン s のコンテンツカードは、有効期限とアプリの適切なバッファー期限まで停止されません。これらは、バッファー期間の後半(キャンペーンがワンタイム送信であるか、終了日があるか、終了日がないかに対応) と有効期限で停止されます。 

たとえば、コンテンツカードが4 月1 日に期限切れになり、ワンタイム送信であり、コンバージョンの期限が10 日である場合、4 月12 日(コンバージョンの期限の10 日後に1 日を加算) に停止されます。コンテンツカードが4月1日に期限切れになり、API-トリガーが期限切れになり、3月15日以降にメッセージを送信していない場合、期限は来年の3月15日となります。

キャンバスは、コンテンツカードが停止した後でのみ停止します。つまり、最大継続時間が経過したことを意味します。