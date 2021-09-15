---
title: "gitのブランチ戦略"
date: "2021-09-13"
---

求人情報を眺めていると、GitHub Flow、git-flow という言葉を目にすることがあり、何のことか疑問に思いググったら、[この記事](https://qiita.com/trsn_si/items/cfecbf7dff20c64628ea)

要するに、開発・テスト・リリース・運用というソフトウェアのライフサイクルを効率よく回すために、どうブランチを使い分けるかという話なんだな。

ぼくは、これまで小規模の個人開発しかやってこなかったので（OSS にプルリクを送ったこともあるが、メンテされてないレポジトリで放置されたまま。。）、master ブランチに都度コミットするだけで、せいぜい remote ブランチを CI 通らなければ push しない、というブランチ保護程度の機能しか触っていない。

しかし、世の中のアプリやプログラムは、たいていの場合グループでの協業で作られ、しかも一旦大勢に使われ始めたら、セキュリティやパフォーマンス上の影響も大きいし、破壊的な変更もそうそうできない。だから、master 以外のブランチが必要になることも当然理解できる。

しかし、GitHub FLow 以外のブランチ戦略は習熟が難しそうだよなあ。ブランチの頻繁な切り替えはミスを誘発するので、ブランチ数が多い場合はミスの確率はあがる。マイルストーンベースの開発は、スマホみたいにリリーススケジュールがある程度決まっているものならいいが、web アプリみたいに日常的に機能変更する場合には混乱の元になりそう。

というか、GitHub Flow のわかりやすさはすごいな。コンソールゲームや金融機関のシステムでの採用は難しそうだけど、どうなんだろう？

ユーザが自分以外に多数いるサービスや、共同での開発を経験しないと、それはわからない。精進しよう。