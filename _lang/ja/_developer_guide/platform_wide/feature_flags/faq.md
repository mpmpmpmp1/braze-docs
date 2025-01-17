---
nav_title: FAQ
article_title: よくある質問
page_order: 50
description: "このページでは、特徴的なフラッグに関するよくある質問にお答えする。"
tool: Feature Flags
platform:
  - iOS
  - Android
  - Web
---

# よくある質問

> この記事では、特徴的なフラッグに関するよくある質問に対する答えを提供する。

## 機能性とサポート

### Brazeの機能フラッグはどのプラットフォームでサポートされているのか？ {#platforms}

Brazeは、以下のSDKバージョン要件で、iOS、Android、およびWebプラットフォーム上の機能フラグをサポートする：

{% sdk_min_versions swift:5.9.0 android:24.2.0 web:4.6.0 unity:4.1.0 cordova:5.0.0 reactnative:4.1.0 flutter:6.0.0 roku:1.0.0 %}

他のプラットフォームでのサポートが必要か？Eメール：[feature-flags-feedback@braze.com](mailto:feature-flags-feedback@braze.com).

### フィーチャー・フラッグを実装する際の労力はどの程度か？ {#level-of-effort}

フィーチャー・フラッグは数分で作成し、統合することができる。 

その労力の大半は、あなたが展開しようと計画している新機能を構築するエンジニアリング・チームに関連するものだ。しかし、機能フラグを追加するとなると、アプリやウェブサイトのコードに`IF`/`ELSE` ステートメントを記述するくらい簡単だ：

```javascript
import { getFeatureFlag } from "@braze/web-sdk";

if (getFeatureFlag("new_shopping_cart").enabled) {
    // Show the new homepage your team has built
}
else {
    // Show the old homepage
}
```

### 機能フラグはマーケティングチームにどのようなメリットをもたらすのか？ {#marketing-teams}

マーケティングチームは、ある機能がごく一部のユーザーにしか有効でない場合、機能フラグを使用して製品アナウンス（製品発表メールなど）を調整することができる。

例えば、Brazeのフィーチャーフラグを使えば、アプリ内の10%のユーザーに新しいカスタマー・ロイヤリティ・プログラムを展開し、キャンバスのフィーチャーフラグのステップを使って、同じ10%の有効なユーザーにEメールやプッシュなどのメッセージを送ることができる。 

### 機能フラグは製品チームにどのようなメリットをもたらすのか？ {#product-teams}

製品チームは、機能フラグを使用して、新機能の段階的なロールアウトやソフトローンチを行い、主要なパフォーマンス指標や顧客からのフィードバックをモニターしてから、全ユーザーに提供することができる。

製品チームは、[機能フラグのプロパティを][properties]使用して、ディープリンク、テキスト、画像、その他の動的コンテンツなど、アプリ内のコンテンツをリモートで入力することができる。

キャンバスのフィーチャーフラッグステップを使って、製品チームはA/Bスプリットテストを実施し、新機能が、その機能を無効にしたユーザーと比較して、コンバージョン率にどのような影響を与えるかを測定することもできる。 

### フィーチャー・フラッグはエンジニアリング・チームにどのようなメリットをもたらすのか？ {#engineering-teams}

エンジニアリングチームは、機能フラグを使用することで、新機能の立ち上げに内在するリスクを軽減し、夜中に慌ててコード修正をデプロイすることを避けることができる。

機能フラグに隠された新しいコードをリリースすることで、チームはBrazeのダッシュボードからリモートで機能のオン/オフを切り替えることができ、新しいコードのプッシュアウトやアプリストアのアップデート承認待ちの遅延を回避できる。

## 機能展開とターゲティング

### 機能フラグを一部のユーザーだけに展開することは可能か？ {#target-users}

`user_id`Brazeで特定のユーザーをターゲットにしたセグメントを作成する。そして、そのセグメントの100%にフィーチャー・フラッグを配備する。

### ロールアウト率を調整することで、以前は有効グループにバケットされていたユーザーにどのような影響があるのか？ {#random-buckets}

機能フラグのロールアウトは、デバイスやセッションを問わず、ユーザーにとって一貫したものとなる。

- ある機能フラグがランダムなユーザーの10%にロールアウトされると、その10%はその機能フラグの有効期間中、有効なまま持続する。
- ロールアウトを10%から20%に増やすと、同じ10%が有効なままとなり、さらに新たな10%のユーザーが有効なグループに追加される。
- 展開率を20%から10%に下げると、元の10%のユーザーだけが有効になる。

この戦略は、ユーザーがアプリ内で一貫した体験を提供し、セッションを行ったり来たりしないようにするのに役立つ。もちろん、ある機能を0％まで無効にすると、すべてのユーザーがその機能のフラグから外れる。

### 現在フィーチャー・フラッグにいるユーザーのセグメントを作ることはできるか？ {#feature-flag-filter}

これは我々の製品ロードマップにある。優先順位をつけるために、このフィードバックをBrazeのアカウントチームまでお寄せいただくか、Eメール（[feature-flags-feedback@braze.com](mailto:feature-flags-feedback@braze.com) ）でご連絡いただきたい。

## テクニカル・トピックス

### 機能フラグを使用して、Braze SDKが初期化されるタイミングを制御できるか？ {#initialization}

いいえ、SDKは、現在のユーザーの機能フラグをダウンロードし、同期するために初期化されなければならない。つまり、機能フラグを使用して、Brazeで作成または追跡されるユーザーを制限することはできない。

### SDKはどのくらいの頻度で機能フラグを更新するのか？ {#refresh-frequency}

フィーチャーフラグは、セッション開始時とアクティブユーザー変更時に更新される。フィーチャー・フラグは、SDKの[リフレッシュ・メソッドを][refreshing]使用して手動でリフレッシュすることもできる。フィーチャー・フラグの更新は5分に1回に制限されている（変更される可能性がある）。

優れたデータ・プラクティスでは、機能フラグをあまり早くリフレッシュしないことを推奨している（リフレッシュするとレートが制限される可能性がある）ので、ユーザーが新機能とインタラクトする前にリフレッシュするか、必要であればアプリ内で定期的にリフレッシュするのがベストであることに留意してほしい。

### ユーザーがオフラインの間、機能フラグは利用可能か？ {#offline}

機能フラグがリフレッシュされると、ユーザーの端末にローカルに保存され、オフラインの状態でもアクセスできる。

### セッションの途中でフィーチャー・フラグが更新された場合はどうなるのか？ {#listen-for-updates}

フィーチャーフラグはセッションの途中で更新されることがある。特定の変数やコンフィギュレーションが変更された場合、アプリをアップデートしたくなるシナリオもあるだろう。UIのレンダリング方法が衝撃的に変わるのを避けるために、アプリをアップデートしたくないシナリオもある。

これを制御するには、機能フラグの[更新をリッスン][listen-for-updates]し、どの機能フラグが変更されたかに基づいてアプリを再レンダリングするかどうかを決定する。 

## その他の質問は？

ご質問やご意見は？Eメール：[feature-flags-feedback@braze.com](mailto:feature-flags-feedback@braze.com).

[properties]: {{site.baseurl}}/developer_guide/platform_wide/feature_flags/create/#properties
[refreshing]: {{site.baseurl}}/developer_guide/platform_wide/feature_flags/create/#refreshing
[listen-for-updates]: {{site.baseurl}}/developer_guide/platform_wide/feature_flags/create/#updates
