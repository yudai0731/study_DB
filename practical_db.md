# データベース応用
ここではデータウェアハウス, 多次元データベース, データマイニング, NoSQL, ブロックチェーンについて述べる.

## データウェアハウス
企業の持つ大量のデータを整理・統合して蓄積しておき, 意思決定支援などに利用するデータベースおよびその管理システムをデータウェアハウスという. データウェアハウスは基幹系データベースからデータ抽出, 変換, データウェアハウスへのロードという一連のETL(Extract/Transform/Load)という処理によって構築される.

## 多次元データベース
分析対象となるデータと, 分析の軸となる属性項目から構成されるデータベースを多次元データベースという. データウェアハウスに蓄積された大量のデータをもとに, 例えば時間, 地域, 製品など様々な視点から多次元的に分析を行うためにこのようなデータベースが用いられる.  
多次元データを様々な視点から対話的に分析する処理形態・技術をOLAP(Online Analytical Processing;オンライン分析処理)という. また多次元データをそのままの形で管理するデータベースをMOLAP(Multi-dimensional OLAP), 関係データベースを利用してスタースキーマ構造で管理するROLAP(Relational OLAP)がある. スタースキーマとは多次元構造に適合したリレーショナルスキーマで, 分析対象となるデータを格納したファクトテーブルと, その周りに分析の切り口となるディメンションテーブルを配置したスキーマ構造である.

## データマイニング
蓄積された膨大なデータから統計的, 数学的手法を用いてデータの法則性や因果関係を見つけ出す手法をデータマイニングという. 代表的なデータマイニング手法にマーケットバスケット分析(一緒に購入されている商品の分析), 決定木分析, NN, クラスタ分析がある. 

## NoSQL
NoSQL(Not only SQL)はビッグデータの中心的な技術基盤で, データへのアクセス方法をSQLに限定しないデータベースの総称である. 従来のSQLでは大規模データや頻繁に発生するトランザクションデータの処理, 分散データベース環境での処理において性能の低下を招く可能性があるが, NoSQLはスキーマレスであるため柔軟で大量のデータを扱うことに適している.  
NoSQLではビッグデータなどの膨大なデータを高速に処理する必要がある. そこで一時的なデータの不整合を許容することで整合性保証のための処理負担を軽減し, 最終的に一貫性が保たれていればよいうという考え方を採用している. これを結果整合性といい, 結果整合性を保証する考え方がBASE特性である. BASE特性は'Basically Available(可用性が高い)', 'Soft state(厳密な状態を要求しない)', 'Eventually consistent(結果整合性)'の3つの特性からなる.

## ブロックチェーン
ブロックチェーンはネットワーク上のコンピュータにデータを分散保持させる技術で, 改ざん不可能, 高い可用性と透明性という特徴を持つ. ブロックチェーンの仕組みとしては, 一定期間内の取引データを格納したブロックを, 前のブロックのハッシュ値とジョイントして鎖のように繋ぐことで, 他のブロックで改ざんが発生すると整合性が保たれなくなるような仕組みになっている. この仕組みを支えている技術がP2P(peer to peer)ネットワークで, 取引データを参加者全員で持ち合うことで一部のノードに障害がでてもシステムを維持することができる. 

