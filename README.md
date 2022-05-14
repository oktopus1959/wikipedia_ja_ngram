# wikipedia_ja_ngram
2021年7月時点の日本語Wikipediaの記事をダウンロードし、ひらがなのn-gramを抽出しました。

## wikipedia.hiragana-ized.1-3gram.txt
1. 漢字およびカタカナをひらがなに変換
1. ひらがなが1～4文字連続する部分を切り出し
1. ひらがなの小書き文字「ぁぃぅぇぉゃゅょゎ」が後接するものは 1-gram としてカウント
1. 3-gram 以下になるものを抽出
1. 頻度順に並べ、上位100,000個を出力したものです。

例：
```
83679750	ん	1
79819780	い	1
77832093	う	1
40342561	の	1
39778339	か	1
37527443	と	1
36727889	た	1
36225871	し	1
34111892	く	1
33378972	に	1
・・・
9863297	え	1
9583379	ねん	2
9372874	しょ	1
9291217	そ	1
9237828	め	1
9183887	こう	2
8505262	てい	2
7772452	る。	2
7690383	しゅ	1
7430109	み	1
・・・
72490	しょうじょ	3
```

- wikipedia.hiragana-ized.1gram.txt
- wikipedia.hiragana-ized.2gram.txt
- wikipedia.hiragana-ized.3gram.txt

これらはそれぞれ、1gram、2gram、3gram のものを抽出したリストです。

## wikipedia.hiragana-asis.1-3gram.txt
前項の 1. を実行せずに、初めからひらがなの部分だけを対象にして n-gram を抽出したものです。

例：
```
36052011	の	1
29817945	、	1
24832645	に	1
21089776	。	1
20232878	た	1
19569440	る	1
18826089	は	1
18744353	ー	1
17016045	と	1
16079403	を	1
・・・
5882501	も	1
5788887	して	2
5692972	てい	2
5676808	こ	1
5458679	す	1
5251170	され	2
4893159	した	2
4392244	った	2
4250795	する	2
4157981	は、	2
・・・
```

- wikipedia.hiragana-asis.1gram.txt
- wikipedia.hiragana-asis.2gram.txt
- wikipedia.hiragana-asis.3gram.txt
これらはそれぞれ、1gram、2gram、3gram のものを抽出したリストです。

## 形式
各行は、「出現頻度<TAB>出現形<TAB>gram数」という形式になっています。

```
83679750        ん      1
```

上記の例は、1-gramの「ん」が 83,679,750回出現したことを表しています。


```
3651156 ている     3
```

上記の例は、3-gramの「ている」が 3,651,156回出現したことを表しています。

## 漢字からひらがなへの変換方法
mecab を使っています。

表層形が漢字を含んでいる場合は、発音形に置き換えます。
ただし発音形は、「多い」が「オーイ」になったり「続く」が「ツズク」になったりするので、「ー」「ズ」「ジ」については、読み形から対応する位置の文字を取ってきて置換しています。

mecabの出力例：（表層形、発音形、読み、原形、の順になっています）
```
多く続いている
多く    オーク  オオイ  多い    形容詞-一般     形容詞  連用形-一般
続い    ツズイ  ツヅク  続く    動詞-非自立可能 五段-カ行       連用形-イ音便
て      テ      テ      て      助詞-接続助詞
いる    イル    イル    居る    動詞-非自立可能 上一段-ア行     終止形-一般
EOS
```

この文では「オオクツヅイている」という出力が得られます。
最終的にカタカナをひらがなに変換して出来上がりです。
