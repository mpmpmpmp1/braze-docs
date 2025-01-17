---
nav_title: ユーザーアーカイブ
article_title: ユーザーアーカイブ
permalink: /user_archival/
page_order: 0
page_type: reference
description: "この参考記事では、ユーザーアーカイブの定義、スパムのブロック、およびユーザーアーカイブポリシーのカスタマイズ方法について説明する。"

---
# ユーザーアーカイブ

> 毎週日曜日の午前5時30分（米国東部標準時間）に、BrazeはBrazeサービスから非アクティブユーザーと休眠ユーザーを削除するプロセスを実行する。なお、Brazeは、ワークスペースのユーザー数が250,000のしきい値に達しない限り、ユーザーをアーカイブしない。 

このプロセスは、Brazeがキャンペーンの到達可能なオーディエンスに関する正確な統計を提供することを目的としている。また、[GDPRの][1]2つの重要な概念に従っている：

1. 保存制限の原則-処理され保存された個人データは、必要な期間を超えて保存されるべきではない。
2. 個人データを処理する正当な事業目的を有すること。

すなわち、処理され保存された個人データは必要以上の期間保存されるべきではなく、個人データは合法的な業務目的のためにのみ処理されるべきである。アーカイブされたユーザーは、GDPRに準拠して配信停止ステータスも削除される。

{% alert note %} 顧客は、ユーザーが非アクティブか休止状態かを完全にコントロールできる。Braze Canvasは、この機能を自動的に実行する機能を提供しており、非アクティブまたは休止状態のユーザーの一部または全員に対して、この機能を効果的にオフにすることができる。 {% endalert %}

## ユーザー・アーカイブ定義

### アクティブユーザー

Brazeは、一定期間の「アクティブユーザー」を、モバイルアプリやウェブサイトでセッションを記録したユーザー、更新を受けたユーザー、メッセージを送信したユーザー、メッセージと対話したユーザーと定義している。

新規ユーザーがログインしたときにユーザーを識別するためにユーザーIDを設定した場合、そのユーザーは別のアクティブユーザーとしてカウントされる。API 経由で更新されたユーザーも、更新の期間中はアクティブユーザーとしてカウントされます。

{% alert important %}
以下に挙げる理由でアーカイブから除外されない限り、非アクティブユーザーと休眠ユーザーの両方がアーカイブされる。
{% endalert %}

### 非アクティブユーザー

「非アクティブ・ユーザー」とは、連絡が取れず、解約した可能性が高いユーザーのことである。非アクティブ・ユーザーとは、これらの条件をすべて満たすユーザーのことである：

- メールが受信できない。例えば、電子メールアドレスを持っていなかったり、すべての電子メールリストの配信を停止していたりする。
- SMSを受信できない。例えば、有効な電話番号を持っていなかったり、すべてのSMS購読グループから登録解除されていたりする。
- プッシュを受けられない。例えば、アプリをアンインストールしたとか、プッシュ許可を無効にしたとか。
- WhatsAppメッセージを受信できない。例えば、有効な電話番号を持っていなかったり、全てのWhatsApp購読グループから退会している。
- 半年以上、ワークスペースでモバイルアプリを使ったり、ウェブサイトを見たりしたことがない。
- 半年以上、ワークスペースからメッセージを受け取っていない。
- 半年以上更新されていない。

この場合、これらのユーザーはメッセージを送ることができず、ブランドとエンゲージしていない。これらのユーザーは事実上、解約している。

### 休眠ユーザー

「休眠ユーザー」とは、過去12ヶ月間まったく活動をしていないユーザーのことである：

- 12ヶ月以上、モバイルアプリを使用したり、ワークスペースのウェブサイトを閲覧したことがない。
- 12ヶ月以上、ワークスペースからメッセージを受け取っていない。
- 12ヶ月以上更新されていない。

## グローバル・コントロール・グループのユーザー

グローバル・コントロール・グループのユーザーは、たとえ非アクティブまたは休眠ユーザーの 定義に合致していたとしても、アーカイブされることはない。 

### 治療サンプル群

治療サンプルグループユーザーは、グローバルコントロールグループレポート内のアーカイブから除外される。

## テストユーザー

テストユーザーは、たとえ非アクティブユーザーや休眠ユーザーの定義に合致していたとしても、決してアーカイブされることはない。

## スパムブロック

Brazeは、500万セッションを超える個々のユーザー（「ダミーユーザー」）をブロックし、SDKイベントをインジェストしなくなった。正当なユーザーにこのようなことが起こった場合は、Brazeの[サポートに]({{site.baseurl}}/braze_support/)チケットを提出すること。

ダッシュボードのダミーユーザーを見つけるには、以下の手順を実行する：

1. [セグメントを]({{site.baseurl}}/user_guide/engagement_tools/segments/creating_a_segment/)作成する。
2. フィルター`Session Count` を選択し、`more than 5,000,000` に設定する。
3. CSVでセグメントをエクスポートする。

必要であれば、[`/users/delete` エンドポイント]({{site.baseurl}}/api/endpoints/user_data/post_user_delete/)経由でユーザーを削除できる。

[1]: {{site.baseurl}}/dp-technical-assistance/#the-right-to-erasure
[2]: {% image_buster /assets/img_archive/user_archival_policy1.png %}
[3]: {% image_buster /assets/img_archive/user_archival_policy2.png %}
[4]: {% image_buster /assets/img_archive/user_archival_policy3.png %}

## ユーザー・アーカイブ・ポリシーをカスタマイズする

Brazeは、ユーザーアーカイバルポリシーをカスタマイズできるデータオーケストレーション機能を提供する。Canvas[ユーザー・アップデート・]({{site.baseurl}}/user_update/)コンポーネントを使用して、両方の長所を備えたユーザー・アーカイブ・ポリシーを作成する。

これにより、次のことが可能になる：

- 価値がなくなったユーザープロファイルを削除することで、GDPRとプライバシーのベストプラクティスを遵守する。
- 正当な業務上の必要性があるユーザープロファイルは保持する。

### ステップ

1. アーカイブ基準を満たし、保持したいユーザーを対象とする。<br><br>
      ![最後にメッセージを受け取ったのが23週間以上前、キャンペーンやキャンバスステップからのメッセージを受け取ったことがない、最後にこれらのアプリを利用したのが23週間以上前、これらのアプリを利用した回数が0回というユーザーを対象とする。][2]<br><br>
2. 再入国資格を6カ月弱に設定する。<br><br>
      ![エントリーコントロールでは、再資格をオンとし、再資格ウィンドウを23週に設定した。][3]<br><br>
3. ユーザ更新ステップを構成して、各プロファイルにイベントを追加する。<br><br>
      ![ユーザーのプロファイルに "do_not_archive "イベントを追加するユーザー更新ステップ。][4]
{% details サンプル・ユーザー更新オブジェクト %}

{% raw %}
```json
{
    "events": [
        {
            "name": "do_not_archive",
            "time": "{{ 'now' | time_zone: 'UTC' | date: '%Y-%m-%dT%H:%M:%SZ' }}"
        }
    ]
}
```
{% endraw %}

{% enddetails %}
