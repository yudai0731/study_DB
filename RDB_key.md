# RDBのキー
ここではRDBのキーの種類と特徴について述べる.

## スーパキー(super key)
表中の行を一意に特定できるアトリビュート, またはアトリビュートの組をスーパキーという. 極端な例では, 表中に重複する行が存在しなければ, すべてのアトリビュートをスーパキーに指定してもよい.

## 候補キー(candidate key)
スーパキーの中で余分なアトリビュートを含まない, つまり行を一意に識別するための最小限のアトリビュートで構成されるスーパキーを候補キーという. 候補キーについては表中に同じ値があってはいけないという一意性制約が設けられている.

## 主キー(primary key)
複数存在する候補キーの中から任意に選んだ候補キーを主キー, 選ばれなかった候補キーを代理キー(alternate key)という. 主キーには一意性制約およびNOT NULL制約が設定されている. この主キーが持つ制約を主キー制約という. 

## 外部キー(foreign key)
関連する他の表を参照するアトリビュート, あるいはその組を外部キーという. 1対多の関係がある場合は, 多側の表に1側の表の主キーあるいは主キー以外の候補キーを参照する属性を持たせて, これを外部キーとする. これによって外部キーの値が被参照表に存在するという参照制約を確保する. 