# copy_link_for_asana
- DOMの操作がcontent.jsからしかできないらしいのでbackground.jsとのやりとり
- urlはうまくコピーできるからcontentとbackgroundのやりとりがうまくいってない(undifinedになる)

# mytest
- titleタグの場合はcontent.jsからその内容を取得してクリップボードにコピーできたけどタスク名じゃなくて[app.asana.com]
- classから取得しようと思うとできない
- クリックによってコピーできるわけじゃなくてページを表示した時にコピーされる
- manifestのcontent.jsが使われるmatchesの編集がうまくいかない
