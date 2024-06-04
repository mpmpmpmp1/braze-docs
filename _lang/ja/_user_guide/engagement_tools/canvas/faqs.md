---
nav_title: FAQ
article_title: キャンバスに関する FAQ
page_order: 8
alias: "/canvas_v2_101/"
description: "この記事では、キャンバスとキャンバスフローに関するよくある質問にお答えします。"
tool: Canvas

---

# よくある質問

> この記事では、キャンバスと[キャンバスフロー](#canvas-flow)に関するよくある質問にお答えします。

{% alert important %}
2023 年 2 月 28 日以降、従来のキャンバスエクスペリエンスを使用したキャンバスの作成や複製ができなくなりました。Braze では、元のキャンバスエクスペリエンスを使用しているお客様に、キャンバスフローへの移行をお勧めしています。これは、キャンバスの構築と管理をより良く行う目的で改良された編集エクスペリエンスです。「[キャンバスからキャンバスフローへの複製]({{site.baseurl}}/user_guide/engagement_tools/canvas/managing_canvases/cloning_canvases/)」を参照してください。
{% endalert %}

## 全般的な質問

### バリアントが 1 つで、分岐が複数あるキャンバスで、オーディエンスと送信時刻が同一の場合はどうなりますか?

それぞれのステップのジョブがキューに入れられます。これらがほぼ同時に実行され、どちらかが「勝利」します。実際には、双方がほぼ均等な結果となるかも知れませんが、最初に作成されたステップが若干有利となる可能性が高くなると思われます。 

また、この分布がどのようになるかを正確に保証することはできません。均等に分けたい場合は、[ランダムバケット番号]({{site.baseurl}}/user_guide/engagement_tools/campaigns/ideas_and_strategies/ab_testing_with_random_buckets/)フィルターを追加してください。

### キャンバスを停止するとどうなりますか?

キャンバスを停止すると、以下のことが起こります。

- ユーザーがキャンバスに入れなくなる。
- ユーザーがフローのどの位置にいても、メッセージはそれ以上送信されない。
- **例外:** メールを使ったキャンバスはすぐには停止されません。送信リクエストが SendGrid に送られた後は、ユーザーへの配信を即停止するために Braze ができることは何もありません。

#### キャンバスのアプリ内メッセージ 
次のセッション開始時にアプリ内メッセージが送信されます。つまり、キャンバスが停止される前にユーザーがキャンバスステップに入った場合、アプリ内メッセージが有効期限内であれば、次のセッション開始時にアプリ内メッセージを受け取ることができます。

{% alert note %}
キャンバスを停止しても、メッセージの受信を待っているユーザーがジャーニーを終了することはありません。キャンバスを再度有効にし、ユーザーがまだメッセージを待っている場合、ユーザーはメッセージを受け取ります (ただし、メッセージの予定受信時刻が過ぎている場合には受け取りません)。
{% endalert %}

### 例外イベントはいつトリガーされますか?

[例外イベント]({{site.baseurl}}/user_guide/engagement_tools/canvas/create_a_canvas/exception_events/)がトリガーされるのは、ユーザーがそれに関連するキャンバスコンポーネントの受信を待つ間だけです。ユーザーが事前にアクションを実行した場合、例外イベントはトリガーされません。特定のイベントを事前に実行したユーザーを除外したい場合は、代わりに[フィルター]({{site.baseurl}}/user_guide/engagement_tools/segments/segmentation_filters/)を使用してください。

### キャンバスの編集は、すでにキャンバスに入っているユーザーにどのような影響を与えますか?

マルチステップキャンバスの一部のステップを編集した場合、すでにオーディエンスでありながらステップを受け取っていないユーザーは、更新後のバージョンのメッセージを受け取ることになります。これは、まだそのステップで評価されていない場合のみに該当することに注意してください。

開始後に編集できる内容については、「[開始後にキャンバスを変更する]({{site.baseurl}}/user_guide/engagement_tools/canvas/create_a_canvas/change_your_canvas_after_launch/)」を参照してください。

### キャンバスでは、ユーザーのコンバージョンがどのようにトラッキングされますか?

ユーザーがコンバートできるのは、キャンバスのエントリごとに 1 回のみです。コンバージョンは、そのエントリでユーザーが受信した最新のメッセージに割り当てられます。キャンバスの最初にある要約ブロックには、メッセージを受け取ったかどうかに関わらず、そのパス内でユーザーが行ったすべてのコンバージョンが反映されます。それ以降の各ステップには、そのユーザーが最後に受け取ったステップの最中に起こったコンバージョンのみが反映されます。

{% details 例 %}

**例 1**

キャンバスのパスに 10 個のプッシュ通知があり、コンバージョンイベントは「セッション開始」 (「アプリを開く」) になっているとします。

- ユーザー A はエントリ後、最初のメッセージを受け取る前にアプリを開きます。
- ユーザー B はプッシュ通知のたびにアプリを開きます。

**結果:** 要約には 2 つのコンバージョンが表示されますが、個々のステップでは最初のステップのコンバージョンが 1、それ以降のステップではすべてゼロとなります。

{% alert note %}
コンバージョンイベントが発生したときにサイレント時間がアクティブな場合、同じルールが適用されます。
{% endalert %}

**例 2**

サイレント時間を有効にしたステップが 1 つのキャンバスがあるとします。

1. ユーザーがキャンバスに入ります。
2. 最初のステップに遅延はありませんが、設定されたサイレント時間内なので、メッセージは抑制されます。
3. ユーザーがコンバージョンイベントを実行します。

**結果:** ユーザーは、キャンバスのバリアント全体ではコンバージョン済みとしてカウントされますが、ステップを受け取っていないため、ステップに対してはカウントされません。

{% enddetails %}

### コンバージョン率のタイプによって何が異なりますか?

- キャンバスのコンバージョン総数は、何人のユニークユーザーがコンバージョンイベントを完了したかを反映するもので、彼らがそれぞれ何件のコンバージョンを完了したかを反映するものではありません。 
- バリアントのコンバージョン率またはキャンバスの冒頭にある要約ブロックには、メッセージを受け取ったかどうかに関わらず、そのパス内でユーザーが行ったすべてのコンバージョンが反映されます。 
- ステップのコンバージョン率には、そのメッセージステップを受信し、設定されたコンバージョンイベントのいずれかを完了した個人の数が反映されます。

### コンポーネントとステップの違いは何ですか?

[コンポーネント]({{site.baseurl}}/user_guide/engagement_tools/canvas/canvas_components)とは、キャンバスの効果を判断するために使用できる、キャンバスの個々の部分です。コンポーネントには、ユーザージャーニーの分割、遅延の追加、複数のキャンバスパスのテストなどのアクションを含めることができます。キャンバスのステップとは、キャンバスの分岐におけるパーソナライズされたユーザージャーニーのことです。基本的に、キャンバスはユーザージャーニーのステップを作成する個々のコンポーネントから構成されています。

### キャンバスの各コンポーネントの分析はどのようにしたら表示できますか?

キャンバスコンポーネントの分析を表示するには、キャンバスに移動して [**キャンバスの詳細**] ページを下にスクロールします。ここには各コンポーネントの分析が表示されます。詳しくは、「[キャンバスの分析]({{site.baseurl}}/user_guide/engagement_tools/canvas/testing_canvases/measuring_and_testing_with_canvas_analytics/)」を参照してください。

### ユニークユーザー数を見る場合、キャンバス分析とセグメンターのどちらがより正確ですか?

セグメンターは、キャンバスやキャンペーンの統計と比較して、より正確なユニークユーザーデータ統計を提供します。これは、キャンバスやキャンペーンの統計値は、何かが起こると Braze によってインクリメントされるためです。したがって、変数によってはこの数値がセグメンターの数値と異なる可能性があります。例えば、ユーザーは 1 つのキャンバスやキャンペーンで複数回コンバージョンする可能性があります。

### キャンバスに入るユーザー数が予想数と一致しないのはなぜですか?

キャンバスに入るユーザー数は、オーディエンスやトリガーの評価方法によっては予想数と異なる場合があります。Braze では、オーディエンスはトリガーの前に評価されます (ただし、[属性の変更]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/triggered_delivery/attribute_triggers/#change-custom-attribute-value)トリガーを使用する場合を除きます)。そのため、選択したオーディエンスに含まれない場合、ユーザーはトリガーアクションが評価される前にキャンバスから脱落します。

### キャンバスのステップコンバージョン率とキャンバスのバリアント合計コンバージョン率が一致しないのはなぜですか?

キャンバスのバリアントのコンバージョンの合計が、そのステップの合計よりも大きくなることはよくあります。これが発生するのは、ユーザーがバリアントに入ってすぐにバリアントのコンバージョンイベントを実行する可能性があるためです。しかし、このコンバージョンイベントはキャンバスのステップにはカウントされません。つまり、キャンバスに入り、最初のキャンバスのステップを受け取る前にコンバージョンイベントを実行したユーザーは、バリアントのコンバージョンの合計にはカウントされても、ステップの合計にはカウントされません。キャンバスに入ったユーザーが、ステップを受け取る前にキャンバスを退出した場合も同様です。

### キャンバスのオーディエンスはどのように評価されますか? 

デフォルトでは、キャンバス内のフルステップのフィルターとセグメントは、送信時にチェックされます。キャンバスフローの場合、条件分岐コンポーネントは、前のステップを受信した直後 (または遅延の前) に評価を実行します。

## キャンバスフロー

### キャンバスフローとは何ですか?

キャンバスフローは、マーケターがキャンバスユーザージャーニーを構築し管理する方法を簡素化する、改良された編集エクスペリエンスです。キャンバスビルダーではキャンバスコンポーネントを簡単に表示したり使用したりできます。また、ステップ間の接続を編集したり、ステップやバリアントを削除したり、ユーザーを別のステップにリダイレクトしたり、開始後の編集機能もさらに充実しています。

### 既存のキャンバスをキャンバスフローに変換するにはどうしたらよいですか?

[キャンバスをキャンバスフローに複製]({{site.baseurl}}/cloning_canvases/)することができます。これにより、キャンバスフローのワークフローに元のキャンバスのコピーが作成されます。

### 元のエディターを使って作成したキャンバスはどうなりますか?

既存のすべてのキャンバスと元のキャンバスエディターは、Braze で引き続きサポートされています。キャンバスフローへの早期アクセスを選択したお客様は、元のワークフローあるいはフローのワークフローのどちらかを使用してキャンバスを作成できます。

### 含めることのできるステップ数に制限はありますか?

はい。キャンバスフローを使用して構築されたキャンバスには、最大 200 のステップを含めることができます。

### 切断されたステップのあるキャンバスを開始できますか?

はい、できます。キャンバスフローは、切断されたステップのあるキャンバスを開始できます。また、開始後に、切断されたステップのあるキャンバスを保存することもできます。 

### 切断されたステップに到達したとき、ユーザーはどこへ進みますか?

ユーザーがキャンバスフローのワークフローの切断されたステップにいる場合、後続のステップがあればそちらに進み、ステップの設定によってユーザーの進み方が決まります。これは、ユーザーがキャンバスの他の部分に直接接続することなく、ステップに変更を加えることができるようにするためのものです。また、すぐにライブにする前にテストする余地を与え、下書きを保存できるようにする効果もあります。

ステップを切断する前に、キャンバスステップで保留中のユーザーの分析ビューをチェックすることを推奨します。

### キャンバスフローと元のキャンバスエディターの主な違いは何ですか?

#### キャンバスコンポーネントツールバー

以前の元のキャンバスエディターでは、ユーザージャーニーのステップを作成すると、デフォルトでフルステップが追加されました。キャンバスフローでは、これらのフルステップが異なるキャンバスコンポーネントに置き換えられ、編集エクスペリエンスの可視性とカスタマイゼーションが改善されています。キャンバスステップツールバーから、すべてのキャンバスコンポーネントをすぐに見ることができます。

#### ステップの動作

以前は、各フルステップに、遅延やスケジュールの設定、例外イベント、オーディエンスフィルター、メッセージ設定、メッセージの昇進オプションといった情報がすべて 1 つのコンポーネントに含まれていました。キャンバスフローではこれらが個別の設定となっています。そのため、キャンバスの作成エクスペリエンスがさらにカスタマイズ可能となり、機能にも若干の違いがあります。

#### メッセージコンポーネントのユーザー昇進

[メッセージコンポーネント]({{site.baseurl}}/user_guide/engagement_tools/canvas/canvas_components/message_step/)は、そのステップに入るすべてのユーザーを先に進めます。メッセージの昇進動作を指定する必要はなく、全体的なステップの設定がより簡単になります。[**メッセージの送信時にユーザーを昇進させる**] オプションを実装する場合は、別のオーディエンスパスを追加して、前のステップを受信しなかったユーザーをフィルタリングします。  

#### 暦日での延期期間の動作

[遅延コンポーネント]({{site.baseurl}}/user_guide/engagement_tools/canvas/canvas_components/delay_step/)は、次のステップに進む前に、遅延時間が経過するまで待ちます。 

例えば、4 月 12 日に、遅延コンポーネントがあり、1 日後の午後 2 時にユーザーを次のステップに送るように遅延が設定されたとします。あるユーザーが 4 月 13 日午後 2 時 1 分にこのコンポーネントに入ったとします。
\- 元のワークフローでは、ユーザーは 4 月 14 日の午後 2 時に次のステップに進みます。その時点ではエントリ時刻から 1 日が経過していません。
\- キャンバスフローでは、ユーザーが 4 月 15 日の午後 2 時に次のステップに進みます。この場合、時刻は同じでも、エントリ時刻から 1 日以上経過していることに注意してください。 

#### インテリジェントタイミングの動作

[インテリジェントタイミング]({{site.baseurl}}/user_guide/sage_ai/intelligence/intelligent_timing/)はメッセージコンポーネントに保存されるため、インテリジェントタイミングの計算の前に遅延が適用されます。したがって、ユーザーがコンポーネントに入るタイミングによっては、元のキャンバスのワークフローで作られたキャンバスよりもメッセージを受け取るタイミングが遅くなる可能性があります。

例えば、遅延を 2 日間に設定し、インテリジェントタイミングをオンにして、メッセージを送信するのに最適な時間を午後 2 時と判断したとします。そしてユーザーが午後 2 時 1 分に遅延ステップに入るとします。
- **キャンバスフロー:** 遅延が経過するまで 48 時間かかるので、ユーザーは 3 日目の午後 2 時にメッセージを受け取ります。
- **元のワークフロー:** ユーザーは 2 日目の午後 2 時にメッセージを受け取ります。

インテリジェントタイミングがオンになっている場合、メッセージは、ユーザーがメッセージコンポーネントに入ってから 24 時間以内に、インテリジェントタイミングで特定された時刻に送信されることに注意してください (これは遅延コンポーネントがない場合でも同様です)。

#### 例外イベント

##### サイレント時間

キャンバスフローの例外イベント機能は、メッセージステップとは別のアクションパスを使用して適用されます。サイレント時間はメッセージコンポーネント内で適用されます。つまり、ユーザーがすでにアクションパスを通過し (そこで例外イベントによって除外されず)、メッセージコンポーネントに到達したときにサイレント時間になり、そのキャンバスがサイレント時間の後にメッセージを再送するように設定されていた場合、例外イベントは適用されなくなります。このユースケースは一般的ではないことに注意してください。

セグメントとフィルターについては、キャンバスフローのメッセージコンポーネントに配信検証という新機能が追加され、送信時に検証される追加のセグメントとフィルターをユーザーが設定できるようになりました。これにより、前述したようなサイレント時間のエッジケースを防ぐことができます。

##### 「期間 X」または「次の X」を指定したスケジュール設定

キャンバスフローの例外イベントは、アクションパスを使用して作成されます。アクションパスでは「時間枠 X の後」という設定のみがサポートされ、「期間 X の経過後」や「次の X に」という設定はサポートされません。