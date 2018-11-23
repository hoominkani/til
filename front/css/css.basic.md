# CSS基本

## 左の要素に対して横並びにする
```
p {
  float: left;
}
```

## 上下左右に余白を設定
```
/* 上に10、下に20、左に30、右に40の余白を指定 */
p {
  padding: 10px 20px 30px 40px
}

/* 上下に10px、左右に20pxの余白を指定 */
p {
  padding: 10px 20px
}
```

## 特定クラスの特定要素にだけスタイルを適用する
```
/* header-listクラスのli要素にだけスタイルを適用 */
.header-list li {
  font-size: 10px;
}
```
