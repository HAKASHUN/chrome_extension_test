# copy_link_for_asana
- DOMの操作がcontent.jsからしかできないらしいのでbackground.jsとのやりとり
- urlはうまくコピーできるからcontentとbackgroundのやりとりがうまくいってない(undifinedになる)

# mytest
- titleタグの場合はcontent.jsからその内容を取得してクリップボードにコピーできたけどタスク名じゃなくて[app.asana.com] -> タスク名だけ取得できた
- classから取得しようと思うとできない -> タイトルから取得できたから無視
- クリックによってコピーできるわけじゃなくてページを表示した時にコピーされる -> クリック時に動作するようにしたけど新たな課題(下に記載)
- manifestのcontent.jsが使われるmatchesの編集がうまくいかない -> clear
- background.jsの書き方が怪しい。
	- 今 var task_name をグローバル変数？で定義して、contentとの通信で受け取ったタスク名をtask_nameに入れている
	- その後クリック時task_nameをコピーするようにしている。
	- contentからタスク名が送られるのはページが読み込まれた時であって、asanaでタスクを表示してもページが読み込まれるわけじゃない
	- ->コピーしたいタスク名がコピーされない(ずれる)
	- ->backgroundからクリックのメッセージをcontentに送信->contentからtitleタグを読み、backgroundに送信->コピー という感じで行けるかなあという感じ

# mytest2
- mytestの通信のタイミングを改善したい
- backgroundにさせたい動作
	- クリックを待つ
	- contentへメッセージを送信(これをきっかけにcontentがタイトルを取得するようにする)
	- 送信が終わったら、contentからのメッセージを待つ
	- メッセージを受け取ったらクリップボードへ整形してコピー
- contentにさせたい動作
	- backgroundからのメッセージを待つ
	- 受けっとたらこれをきっかけにタイトルを取得しにいく
	- backgroundへメッセージを送信
- ところどころにあるreturn trueは同期処理させたいからつけたけど、今回のコードの書き方ならあまり必要ないかも(あまり利用していない)
- 結果動かない
	- background.js 18行目の時点でそもそもメッセージが遅れていないかも？
	- console.log()などで確認したが、content.jsの方が動いていなさそう(コンソールの使い方が間違ってるかも)
