# 概要
- 「Pythonで始める柔らかな圏論: 読む、作る、分かる!!(永遠の相 World Structure 著)」の読書メモ
  - 挫折させない
  - ざっくりとした説明
  - 圏論を初めて学習する方のための参考書
  - 数学記号の記載はなるべく避ける
  - Pythonを利用して解説する

上記のような目標を掲げていて、かつ Kindle で 100円 だったため購入した。


---
# 対象と射 まとめ

1. 集合の要素を、圏論では対象という
2. 対象同士に関係性がある場合、対象から対象に向かって矢印を書く
3. 矢印を射という
4. 圏論は、対象と射の構造を研究する学問

---

# 合成射

`合成射.py` では 「ある対象が別の対象の一部」(対象は文字列)という関係における合成射を Python で確認した。

---

# 圏の公理

1. 対象を持つこと
2. 射を持つこと
3. 合成射を持つこと
4. 結合律を持つこと
5. 恒等射を持つこと

---

# 「圏」かどうかの検証

`1, 2, 5, 10`は圏かどうか。

圏の公理に従って、チェックする。

圏の公理

1. 対象を持つこと → OK
2. 射を持つこと
   - 例えば不等式 `1 <= 2 <= 5 <= 10` が成り立つ。
   - 不等式を射とする。
   - → OK
3. 合成射を持つこと
   - `1 →f→ 2 →g→ 5 →h→ 10`
   - 射f と 射g を合成したとして、不等式は成り立つか？成り立つ。
   - → OK
4. 結合律を持つこと
5. 恒等射を持つこと

---

# 合成射の記述方法 合成演算子

### dot(`·`) の入力方法
- Mac は unicode を記述できるため、dot(`·`)を使えるが、これは半角中黒点(`･`)と区別できない。unicode 上は、それぞれ`\u00b7`, `\uff65` であり、別の記号である。注意したい。
- Mac の場合、dot(`·`)は Shift + option + 9 キーを同時に押す。
参考資料 https://www.geoff-hart.com/resources/accents-mac.pdf
- Markdown ならば、TeX の記述方法が使える場合が多いため、`$g \cdot f$`と記述して、 $g \cdot f$ と表記できる。

---

### dot(`·`) の読み方
- dot(`·`)の読み方だが、youtube 等で英語の発話を見ると、`g·f`を`ジーアフターエフ`と読んでいる。ドット とか、サークルとか、とくに記号を読んでいるように見えなかった。意味としても" f のあとの g "ということで通りが良いため、自分も英語で `アフター` と呼ぶことにする。

```
g · f
```

$g \cdot f$

---

### 関数としての記述方法

(圏論が表現するのは関数だけにとどまらないが、)関数に置き換えると

```
h · g · f
```

は

```
h(g(f(x)))
```

と記述できる。

---
# 恒等射
- 難しいので飛ばしてもいいらしい。

### 恒等射の定義

1. 全ての対象がそれぞれ保持している
2. 対象「1」の恒等射(id_1)と 射f を合成すると 射f になる
3. 射f と対象「2」の恒等射(id_2)を合成すると 射f になる
4. $f · id_1 = f = id_2 · f$

**自分から自分へ向かう射が、無条件で恒等射と言えるわけではない** ← そうなの

4. $f · id_1 = f = id_2 · f$

つまり、対象「1」から対象「2」への射を実行するとき、 射f のあとに 恒等射を行うか、恒等射のあとに 射f を行うか、どちらでも同じことであるということ。

恒等射 id_1 の候補

対象「1」の恒等射(id_1)の候補は `1 <= 1`

この場合、不等式は成り立つため、恒等射もなりたつ。

---

# 圏と言えるかどうかの結論

圏の公理 を全て満たすことを確認した。よって、今まで見てきた集合`1, 2, 5, 10`は圏である。

1. 対象を持つこと
2. 射を持つこと
3. 合成射を持つこと
4. 結合律を持つこと
5. 恒等射を持つこと

`対象が「数字」で射が「不等号」という圏`である。

---

- python で恒等射について確認する→`恒等射.py`を参照


---

# Python の型と関数の圏

「圏論の関手」を理解するために必要となる。


<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAUsAAAEPCAYAAADLfubkAAAAAXNSR0IArs4c6QAABfN0RVh0bXhmaWxlACUzQ214ZmlsZSUyMGhvc3QlM0QlMjJFbGVjdHJvbiUyMiUyMG1vZGlmaWVkJTNEJTIyMjAyMi0wMy0xOVQwNyUzQTMwJTNBMTguNTkwWiUyMiUyMGFnZW50JTNEJTIyNS4wJTIwKE1hY2ludG9zaCUzQiUyMEludGVsJTIwTWFjJTIwT1MlMjBYJTIwMTBfMTVfNyklMjBBcHBsZVdlYktpdCUyRjUzNy4zNiUyMChLSFRNTCUyQyUyMGxpa2UlMjBHZWNrbyklMjBkcmF3LmlvJTJGMTYuNS4xJTIwQ2hyb21lJTJGOTYuMC40NjY0LjExMCUyMEVsZWN0cm9uJTJGMTYuMC43JTIwU2FmYXJpJTJGNTM3LjM2JTIyJTIwZXRhZyUzRCUyMkdZWVJ3SmVTTnh0enFUeDZNSzNWJTIyJTIwdmVyc2lvbiUzRCUyMjE2LjUuMSUyMiUyMHR5cGUlM0QlMjJkZXZpY2UlMjIlM0UlM0NkaWFncmFtJTIwaWQlM0QlMjJ2OTJ5LWxUWHM4UktrNnFkbVJRZSUyMiUyMG5hbWUlM0QlMjIlRTMlODMlOUElRTMlODMlQkMlRTMlODIlQjgxJTIyJTNFM1ZkZGI1c3dGUDAxU050REt3T0J3R1B6MGU2aHE2cDFVcmRISnpqZ3ltQmtuQWI2NjNlTlRZQ1FaSm5hYmxrZlF1emo3M1B1UFJqTG5hYmxqY0I1OHBWSGhGa09pa3JMblZtT0U0NThlQ3FnMG9BJTJGZGpRUUN4cHB5RzZCQiUyRnBDRElnTXVxWVJLWG9kSmVkTTByd1BMbm1Xa2FYc1lWZ0l2dWwzVzNIV1h6WEhNUmtBRDB2TWh1Z2pqV1NpMGNCRExmNkYwRGhwVnJhUmFVbHgwOWtBUllJanZ1bEE3dHh5cDRKenFVdHBPU1ZNY2Rmd29zZGRIMmpkYmt5UVRKNHk0UEU3ZWJwZTM5M04lMkZNZWJiMDh2V1VidDI0dVJudVVaczdVNXNObXNyQm9HU0FTRW1Db1hNdUV4enpDYnQlMkJoRThIVVdFYlVNZ2xyYjU1YnpIRUFid0NjaVpXWFV4V3ZKQVVwa3lreXJYbE10ZFBCc0JpcjRXaXpKa1FNMU1ZSkZUT1NSZnU1V0FZaGN3bE1pUlFYakJHRlkwdWYlMkJQckNKb1hqYnI2VVpDb2JwUDJEZGRvYTB6ejFyZ3F4Z3BJTFVjbndHbTU4c0JKUmlWU29CdHR3cmVES1N3Zk1UJTJGQlQyZWE5Y3QzZ0JXZGlqR0RNYVoxQmVBcU5FQVBCTWhLUVE1MWVtSWFWUnBOVWtCWDNCaTNvJTJCcFdmT2FTWnJCcnlKNWMyMmNxa0pTTGt2Q2MzZ052UzdRaDRPdzZFYVp2WUxkSWxzeDlOelZiMFZUOWJMVEg2dkR0UHB3bGVyQXVKa1Y5RHRIbDZoOFVEaVFncWxJZ2dkenExZ01sU09NWEExSmNFbW9aSTg1TGlPOUEzNDZvNldSYTZ0YmtWTGxYYUhCUmxrMEVHTzNRRDElMkJIVWJBOTUwWE05QVNjZndHdXp0Y3dUOTNwcGViVHlFTFdwTGJwTGhiYjNJUGRHTHduJTJGcVJlNVJMNHFQZVZGZGNueWNxZ0N0MiUyQm9Ka1BjeFhNbEclMkI0WHAyTko0N1BiU3hqbDNXeHFxclZjJTJCVTF2eW5YT3pKWHRJVU9lQ2xQSHNUVzVFUUklMkJvZnFqeGwyTjQ4eG5nWncyRVFkQUFzOUlzb1d0VnQzWlBCSVV6cTdUUzRMdDZYWGlpMXgyUSUyQnk5NTNaN3Jyb3A3OExyQW12dnFHYUtPJTJCJTJCMDZYNndTWmVwWWs3RyUyQnBYMElrenVlZ09ycTlaJTJGZHZNS0J5QXY0WXR5JTJCcDdKRm9mN08xUEE4MURlOFVmaHVoZ2ZWOXV0VGs5OSUyQndydnpYdyUzRCUzRCUzQyUyRmRpYWdyYW0lM0UlM0MlMkZteGZpbGUlM0Ucy/guAAAgAElEQVR4Xu1dC3gURdY9JkwwIZLEjMbFVzDgKiqRALqgsijyUAyLIisP3ZUILohR1FUeRgWNPFYFRBEVDa4CooiLxAcPWflRQQ0gZBF1TSSuoEYn5mGYQELC/512BoeQZKZ7ume6e259Xz53SVV11bl1T27dunXrGEgRBAQBQUAQ8IvAMX5rSAVBQBAQBAQBCFnKIhAEBAFBIAAEhCwDAEmqCAKCgCAgZClrQBAQBASBABAwK1l2B5AeFxfHn3Pr6+tPraurS6qtrW1z8OBBR0NDQ1RUVFRD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" style="cursor:pointer;max-width:100%;" onclick="(function(img){if(img.wnd!=null&&!img.wnd.closed){img.wnd.focus();}else{var r=function(evt){if(evt.data=='ready'&&evt.source==img.wnd){img.wnd.postMessage(decodeURIComponent(img.getAttribute('src')),'*');window.removeEventListener('message',r);}};window.addEventListener('message',r);img.wnd=window.open('https://viewer.diagrams.net/?client=1&page=0&edit=_blank');}})(this);"/>


---

# 参考資料
- category theory for programmers https://bartoszmilewski.com/2014/10/28/category-theory-for-programmers-the-preface/
  - 有志による翻訳版：プログラマのための圏論 https://zenn.dev/taketo1024/books/850b20937af93b
- category theory for python: yomutukuruwakaru (Japanese Edition). Kindle Edition.
