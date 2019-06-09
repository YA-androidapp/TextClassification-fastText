# fastText 環境構築

## 仮想環境を用意

```sh
y@localhost:~$ python3 -m venv create fasttext
y@localhost:~$ . fasttext/bin/activate
```

## 必要なパッケージをインストール

```sh
(fasttext) y@localhost:~$ pip install --upgrade pip
(fasttext) y@localhost:~$ pip install cython janome
```

## fastText をインストール

### Python パッケージをインストール

```sh
(fasttext) y@localhost:~$ mkdir -p work && cd work
(fasttext) y@localhost:~/work$ git clone https://github.com/facebookresearch/fastText.git
(fasttext) y@localhost:~/work$ cd fastText
(fasttext) y@localhost:~/work/fastText$ make
(fasttext) y@localhost:~/work/fastText$ pip install .
```

```sh
(fasttext) y@localhost:~/work/fastText$ cd ..
(fasttext) y@localhost:~/work$ python
```

インポートした際にエラーが発生しないことを確認する。

> Python 3.6.7 (default, Oct 22 2018, 11:32:17)
>
> [GCC 8.2.0] on linux
>
> Type "help", "copyright", "credits" or "license" for more information.
>
> &gt;&gt;&gt; import fastText
>
> &gt;&gt;&gt; exit()

### バイナリをインストール

```sh
(fasttext) y@localhost:~/work$ sudo apt install cmake -y
(fasttext) y@localhost:~/work$ cd fastText
(fasttext) y@localhost:~/work/fastText$ mkdir -p build && cd build && cmake ..
(fasttext) y@localhost:~/work/fastText/build$ make && sudo make install
```

```sh
(fasttext) y@localhost:~/work/fastText/build$ cd
(fasttext) y@localhost:~$ which fasttext
```

> /usr/local/bin/fasttext

```sh
(fasttext) y@localhost:~$ fasttext
```

> usage: fasttext &lt;command&gt; &lt;args&gt;
>
> The commands supported by fasttext are:
>
> supervised train a supervised classifier
>
> quantize quantize a model to reduce the memory usage
>
> test evaluate a supervised classifier
>
> test-label print labels with precision and recall scores
>
> predict predict most likely labels
>
> predict-prob predict most likely labels with probabilities
>
> skipgram train a skipgram model
>
> cbow train a cbow model
>
> print-word-vectors print word vectors given a trained model
>
> print-sentence-vectors print sentence vectors given a trained model
>
> print-ngrams print ngrams given a trained model and word
>
> nn query for nearest neighbors
>
> analogies query for analogies
>
> dump dump arguments,dictionary,input/output vectors

```sh
(fasttext) y@localhost:~$ deactivate
y@localhost:~$ which fasttext
```

> /usr/local/bin/fasttext

# データファイル準備

## プレーンテキストを用意

以下の形式で、訓練用／テスト用テキストファイルを用意

```sh
(fasttext) y@localhost:~/work/fastText$ cat inputdata.txt
```

```

```

```sh
(fasttext) y@localhost:~/work/fastText$ cat pred.txt
```

```

```

## ラベル付け

訓練用テキストファイルの各行に対して、ラベルを追加

```sh
(fasttext) y@localhost:~/work/fastText$ cat inputdata.txt
```

```
__label__LABELTEXT, TEXT
```

## 分かち書き

# 学習

```sh
(fasttext) y@localhost:~/work/fastText$ ./fasttext supervised -input inputdata.txt -output model
```

> Read 0M words
>
> Number of words: 419
>
> Number of labels: 2
>
> Progress: 100.0% words/sec/thread: 3695 lr: 0.000000 loss: 0.694113 ETA: 0h 0m

# 予測

```sh
(fasttext) y@localhost:~/work/fastText$ ./fasttext predict-prob model.bin pred.txt 1
```
