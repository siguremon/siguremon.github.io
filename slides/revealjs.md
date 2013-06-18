# reveal.js+Markdown
## お手軽スライド作成

@siguremon
/[twitter](twitter.com/siguremon)
/[github](http://siguremon.github.io)
/[Qiita](http://qiita.com/users/siguremon)

---

## reveal.jsって

HTMLで書けるプレゼンツールです

[reveal.js - The HTML Presentation Framework](http://lab.hakim.se/reveal-js/)

--

### 特徴
- スライドが横だけでなく、縦にも配置できる
- Overviewがみれて、プレゼンの途中で行ったり来たりできる(Escキー)
- コードスニペットが書ける上にsyntax highlightもしてくれる
- Pdfにも出力できる

---

## reveal.jsの簡単な使い方

このページが詳しいので以下略

(reveal.jsで作ったスライドによる説明)

[reveal.jsを使ってみた](http://tmlife-storage.googlecode.com/svn/trunk/reveal.js-guide/index.html)

---

## スライドを作る

でもhtmlをせっせと書くのはめんどくさい…

hamlとかmarkdownで書けるといいなー

--

同じようなことを考えた先人たちがいました

- [Reveal.jsとMarkdownでちょっとしたスライドを手軽に作る](http://n.blueblack.net/articles/2013-03-02_reveal_js_and_markdown_presentation/)

- [あのreveal.jsでのプレゼンをMarkdownで簡単に書けるようにした](http://blog.nishimiyahara.net/2013/02/revealjs-markdown.html)

--

でも実は公式の機能そのままでできます！

---

## markdownでスライドを作る

通常は以下のようにhtmlタグで書きます

```html
<div class="slides">
    <section>
        <h2>スライドタイトル</h2>
	    <p>
		本文　本文　本文　本文　本文
		本文　本文　本文　本文　本文
		本文　本文　本文　本文　本文
		</p>
	</section>
    <section>
        <h2>スライドタイトル</h2>
		<p>
		...
		</p>
	</section>
</div>
```


--

こんな感じでページの内容をmarkdownで書けます

ただし、markdownの中に&lt;&#47;script&gt;があるとだめなようです(markdown.jsの制約？)


```
<div class="slides">
    <section date-markdown>
   	    <script type="text/template">
        ## スライドタイトル

		本文　本文　本文　本文　本文
		本文　本文　本文　本文　本文
		本文　本文　本文　本文　本文

     	<//script><!-- そのままだと書けないので/を余計に書いています -->
    </section>	
</div>

```

--

さらに、以下のようにページ区切りの文字列を指定すると

複数ページをmarkdownで書けます

```html
<div class="slides">
  <section data-markdown 
           data-separator="\n---\n$"
		   data-vertical="\n--\n">
	<script type="text/template">
        ## スライドタイトル

		本文　本文　本文　本文　本文

        ---

        ## 2ページめ

		本文　本文　本文　本文　本文
	<//script><!-- そのままだと書けないので/を余計に書いています -->
  </section>
</div>
```

--

さらにさらに、data-markdownにファイル名を指定することで、
スライドの中身を別ファイルに切り出すことができます

```html
<div class="slides">
  <section data-markdown="revealjs.md"
           data-separator="\n---\n$"
		   data-vertical="\n--\n">
  </section>
</div>
```

--

ちなみに、このスライドもmarkdownで書かれています

- [markdownとしてみた場合](http://qiita.com/users/siguremon/)
- [slideとしてみた場合](http://siguremon.github.io/slides/revealjs.html)

---


こんな感じでお手軽にスライドを作ることができるので、
使ってみてはいかがでしょうか


---

## おわり
