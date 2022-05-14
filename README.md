# wikipedia_ja_ngram
2021年7月時点の日本語Wikipediaの記事をダウンロードし、ひらがなのn-gramを抽出しました。

## wikipedia.hiragana-ized.1-3gram.txt
1. 漢字およびカタカナをひらがなに変換
1. ひらがなが1～4文字連続する部分を切り出し
1. ひらがなの小書き文字「ぁぃぅぇぉゃゅょゎ」が後接するものは 1-gram としてカウント
1. 3-gram 以下になるものを抽出
1. 頻度順に並べ、上位100,000個を出力したものです。

- wikipedia.hiragana-ized.1gram.txt
- wikipedia.hiragana-ized.2gram.txt
- wikipedia.hiragana-ized.3gram.txt
これらはそれぞれ、1gram、2gram、3gram のものを抽出したリストです。

## wikipedia.hiragana-asis.1-3gram.txt
前項の 1. を実行せずに、初めからひらがなの部分だけを対象にして n-gram を抽出したものです。

- wikipedia.hiragana-asis.1gram.txt
- wikipedia.hiragana-asis.2gram.txt
- wikipedia.hiragana-asis.3gram.txt
これらはそれぞれ、1gram、2gram、3gram のものを抽出したリストです。

## 形式
各行は、「出現頻度<TAB>出現形<TAB>gram数」という形式になっています。

```
83679794        ん      1
```

上記の例は、1-gramの「ん」が 83,679,794回出現したことを表しています。


```
3651157 ている     3
```

上記の例は、3-gramの「ている」が 3,651,157回出現したことを表しています。
