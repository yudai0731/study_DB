# 分散データベース
ここでは分散データベースシステムの機能, 6つの透過性, 透過性の実現, 異なるサイト間での表結合, 更新同期について述べる.

## 分散データベースシステムの機能
分散データベースシステムの機能的な目的は, 複数サイトに分散されたデータやシステムを論理的に統合して1つのデータベースシステムであるかのように利用者に見せることである. そのためにはデータがどのサイトにあるか, どのサイトに移動したかということを意識せずに使える透過性が必要である.

## 6つの透過性
表やビューを代表とするデータはアクセス負荷やネットワークのトラフィックなどを考慮して各サイトに分散される. したがって分散データベースシステムではデータの位置を意識しないで利用できる位置に対する透過性, データの移動先を意識しないで使える移動に対する透過性, 表が複数に分割されていてもそれを意識しないで利用できる分割に対する透過性が不可欠である. このほかに複製に対する透過性, 障害に対する透過性, データモデルに対する透過性がある.  
透過性を実現するためには, 各サイトのデータベース管理システムが持つデータディクショナリ/ディレクトリ(DD/D)に加えて, 分散データベース全体を管理するグローバルなDD/Dが必要である. このDD/Dの管理方法には集中型と分散型の2つがある. 集中管理方式では1つのサイトにDD/Dをもたせるため負荷集中, 障害発生時に分散データベース全体に影響することが考えられる. 分散管理方式にはDD/Dの重複保有を許す方法と許さない方法がある. 

## 異なるサイト間での表結合
異なるサイト間での表結合が必要な場合, どちらか一方の表を他方に転送する必要がある. しかし表全体を送るとコストがかかるという問題がある.  
そこで結合に必要な属性のみを相手サイトに送り, 結合に成功したものだけを元のサイトに戻して最終的な結合を行うセミジョイン法がある. さらにセミジョイン法とハッシュ結合を組み合わせたハッシュセミジョイン法がある. この方法ではハッシュ値を相手サイトに送り, ハッシュ結合を用いて結合を行う. このほかにも入れ子ループ法, マージジョイン法, ハッシュ結合がある.

## 分散データベースの更新同期
分散データベースにおいて, 複数サイトにデータを重複して存在させたり, 分割・分割されている場合, 一方のサイトが更新されても他方のサイトが更新されない整合性が保たれない状態が生じることがあるため同期をとる必要がある. 同期をとる方法としてレプリケーションと2相コミットメント制御がある.  
### レプリケーション
レプリケーションは非同期型更新を実現するメカニズムの1つで, マスタデータベースと同じ内容の複製を他のサイトに作成しておき, 決められた時間間隔でマスタデータベースの内容を他のサイトに複写する機能である. 複写方法には全内容を複写する方法と更新部分のみを複写する方法がある.

### 2相コミットメント制御
分散データベースシステムにおけるトランザクションは複数のサブトランザクションに分割され, 複数のサイトで実行される. そのため1相コミットメント制御ではトランザクションの原子性, 一貫性は保証されない. 2相コミットメント制御は分散トランザクション処理に利用される方式で, 更新が可能であるか確認する第1フェーズと, 更新を確定する第2フェーズから構成される. 各サイトのトランザクションがコミットもロールバックも可能な状態(セキュア状態)にした後で, 全サイトをコミットできる場合のみコミットを行うため原子性および一貫性が保証される. これらをまとめた2相コミットメント制御の流れを次に示す.

第1フェーズ

1. 調停者はcommitの可否を問い合わせる.
2. 参加者はcommitの可否を返答する. このときに各データベースサイトはコミットもロールバックも可能なセキュア状態になる.

第2フェーズ

3. 調停者はすべての参加者からcommit可があったときのみcommitの実行要求を発行する. そうでない場合はロールバック指示を発行する.