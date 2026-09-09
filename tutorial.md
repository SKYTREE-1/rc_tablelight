# micro:bit  リモコンルームライトチュートリアル

```package
rc_tablelight=github:SKYTREE-1/rc_tablelight
```

## micro:bit  リモコンルームライトチュートリアル @showdialog
![表紙](https://skytree-1.github.io/rc_tablelight/images/img00.png)

## STEP1 リモコンルームライトを光らせよう @showdialog
この活動では、「カラフル・ライトバーをつくろう」で学習したLEDとkeypad を組み合わせて、指定した色に切り替えるプログラムを作ってみよう」


![活動のイメージ](https://skytree-1.github.io/rc_tablelight/images/img01.png)

LEDライトを**micro:bitを使って操作する「リモコンルームライト」**を作ります。
ボタンを押して色を変えるだけでなく、周囲の明るさやmicro:bitの動きに応じてライトを変化させることもできます。


## 導入 リモコンで部屋のライトを操作しよう @showdialog

このチュートリアルでは、ライトを micro:bitを使って操作します。

micro:bitをリモコンにして、次のような操作をしてみましょう。

  * ライトをつける
  * ライトを消す
  * 色を変える

はじめには、リモコンルームライトの ON/OFF をコントロールするところから始めます。

まず、下の図を参考に micro:bit と赤外線LEDをつなぎましょう。
![接続方法](https://skytree-1.github.io/rc_tablelight/images/img11.png)

micro:bit をPCにつなぐことも忘れないでください。

## 1-1 Aボタンでライトをつけよう

micro:bit のAボタンを押したらライトが点くようにします。
``||input:入力||`` から ``||input:ボタンAが押されとき||`` をだして  ``||rc_tablelight:Rc_tablelight|`` の``||rc_tablelight:ライトを点ける||`` をセットします。

```blocks

input.onButtonPressed(Button.A, function () {
    rc_tablelight.ライトを点ける()
})


```

## 1-2 Bボタンでライト消そう

micro:bit のBボタンを押したらライトが消えるようにします。
前のページと同じようにして ``||input:ボタンBが押されとき||`` に ``||rc_tablelight:白にしてライトを消す||`` をセットします。

```blocks

input.onButtonPressed(Button.A, function () {
    rc_tablelight.ライトを点ける()
})
input.onButtonPressed(Button.B, function () {
    rc_tablelight.白にしてライトを消す()
})


```
## 1-3 動作確認しよう

ここまでのプログラムをダウンロードして、実際にON, OFF をためしてみよう。

```blocks

input.onButtonPressed(Button.A, function () {
    rc_tablelight.ライトを点ける()
})
input.onButtonPressed(Button.B, function () {
    rc_tablelight.白にしてライトを消す()
})


```

## 1-4 他の操作を追加してみよう
つぎに、「ゆさぶられたとき」に、レインボーに変わるようにします。
``||input:ゆさぶられたとき||`` と ``||rc_tablelight:グラデーション[普通]||``を使って色が変わるようにプログラムします。

```blocks

input.onGesture(Gesture.Shake, function () {
    rc_tablelight.グラデーション(Mode.Flash)
}) 

```

## 1-5 動作確認しよう

ここまでのプログラムをダウンロードして、実際にON, OFF をためしてみよう。

```blocks

input.onButtonPressed(Button.A, function () {
    rc_tablelight.ライトを点ける()
})
input.onButtonPressed(Button.B, function () {
    rc_tablelight.白にしてライトを消す()
})

input.onGesture(Gesture.Shake, function () {
    rc_tablelight.グラデーション(Mode.Flash)
}) 
```


## STEP2 加速度センサーの値でライトの色を変える @showdialog
![STEP2](https://skytree-1.github.io/rc_tablelight/images/img02.png)




## 3-1 右に傾けた時に色を変える

micro:bit を右に傾けたときにライトの色が変わるようににします。
``||input:入力||`` から ``||input:ゆさぶられたとき||`` をだして ``||input:ゆさぶられた||``の部分を ``||input:右に傾けた||``にかえます。
``||rc_tablelight:Rc_tablelight|`` の``||rc_tablelight:色を変える 赤||`` をセットして、任意の色にかえます。


```blocks

input.onGesture(Gesture.TiltRight, function () {
    rc_tablelight.色を変える(Color.Red)
})



## 3-2 左に傾けた時に色を変える

同じようにして、左に傾けたときにも色が変わるようにしてください。
このとき、操作したときの結果がわかりやすいように、はっきりと違う色を選ぶといいです。

```blocks

input.onGesture(Gesture.TiltLeft, function () {
    rc_tablelight.色を変える(Color.Blue)
})

```

## 3-3  動作確認しよう

ここまでのプログラムをダウンロードして、実際にためしてみよう。
操作は、Aボタンでライトを点ける→左右に傾けて色をかえる→Bボタンでライトを消すの順です。


```blocks

input.onButtonPressed(Button.A, function () {
    rc_tablelight.ライトを点ける()
})
input.onButtonPressed(Button.B, function () {
    rc_tablelight.白にしてライトを消す()
})

input.onGesture(Gesture.Shake, function () {
    rc_tablelight.グラデーション(Mode.Flash)
}) 

input.onGesture(Gesture.TiltRight, function () {
    rc_tablelight.色を変える(Color.Red)
})

input.onGesture(Gesture.TiltLeft, function () {
    rc_tablelight.色を変える(Color.Blue)
})


```




## STEP3 周囲の明るさによってライトを自動でON/OFFしよう @showdialog

ここまででは、micro:bit の操作してライトを制御しました。

次は、micro:bitが周囲の明るさを調べて、自動的にライトを操作するようにします。

![STEP3](https://skytree-1.github.io/rc_tablelight/images/img03.png)

## 3-1 1秒ごとにチェック

1秒ごとにチェックして明るさが 20 より小さければライトを点けることにします。
``||loops:ループ||``から``||loops:（）ミリ秒ごとに||``を出して、間隔を1秒（1000ミリ秒）にします。


```blocks

loops.everyInterval(1000, function () {
    
})

```

## 3-2 1秒ごとにチェック２

``||logic:論理||``から``||logic:もし〜なら〜でなければ||``ブロックを出して、条件の部分に``||logic:くらべる|``ブロックを使って 「``||input:明るさ||`` が 20より小さいとき」となるようにします。

```blocks

loops.everyInterval(1000, function () {
    if (input.lightLevel() < 20) {
        
    } else {
       
    }
})

```

## 3-3 1秒ごとにチェック３

``||logic:もし〜なら〜でなければ||``、``|input:明るさ||`` が 20より小さい時に ``||rc_tablelight:ライトをつける||`` ブロックをセットし、``||logic:でなければ||``の下に``||rc_tablelight:白にしてライトを消す||``ブロックをセットします。 



```blocks

loops.everyInterval(1000, function () {
    if (input.lightLevel() < 20) {
        rc_tablelight.ライトを点ける()
    } else {
        rc_tablelight.白にしてライトを消す()  
    }
})

```
## 3-4 動作確認しよう

ここまでのプログラムをダウンロードして、実際に動かしてみよう。
暗くなったらライトがついて、明るくなったら消えるというのを試してみてください。ライトの色は自由に調整しましょう。

```blocks

loops.everyInterval(1000, function () {
    if (input.lightLevel() < 20) {
        rc_tablelight.ライトを点ける()
        rc_tablelight.色を変える(Color.Light)
    } else {
        rc_tablelight.白にしてライトを消す()  
    }
})

```

## STEP3（発展）外部の明るさセンサーを使ってみよう @showdialog
 ※ 時間があったら挑戦しよう


ここまでで、micro:bitの、機能を使って周囲の明るさを測定して利用しました。
次に、TEMT6000という外部の明るさセンサーを使ってみましょう。

**TEMT6000** は、周囲の明るさを電気信号に変える光センサーです。

光が当たると電流が流れ、その大きさが明るさに応じて変化します。
そのため、TEMT6000を使うと、周囲が「明るい」「暗い」といった変化を、コンピューターで読み取ることができます。

## STEP3（発展） センサーをmicro:bitにつないでみよう @showdialog

TEMT6000には、電源をつなぐ端子と、明るさに応じた信号を出力する端子があります。

micro:bitとは、次のようにつなぎます。

| TEMT6000 | micro:bit |
| -------- | --------- |
| VCC      | 3V        |
| GND      | GND       |
| OUT      | P0        |


![接続例](https://skytree-1.github.io/rc_tablelight/images/img12.png)

VCCとGNDが電源で、OUTは明るさを表す信号です。この出力値（アナログ値）を読み取って **どれくらい明るいか** を数値で表します。

📍 ポイント
    TEMT6000から出てくる値は、そのまま「ルクス（lx）」になるわけではありません。
    センサーの値と実際の照度（ルクス）の関係を調べることで、おおよその照度を求めることもできます。

## STEP3（発展）プログラムを変更しよう
明るさ判定の``||input:明るさ||`` を ``||pins:入出力端子||`` の ``||pins:アナログで読み取る 端子 P0||``にかえる。
明るさ判定の数字を 50に変える。

```blocks
loops.everyInterval(1000, function () {
    if (pins.analogReadPin(AnalogPin.P0) < 50) {
        rc_tablelight.ライトを点ける()
        rc_tablelight.色を変える(Color.Light)
    } else {
        rc_tablelight.白にしてライトを消す()
    }
})
```

## STEP3（発展）動作確認しよう

ここまでのプログラムをダウンロードして、実際に動かしてみよう。
暗くなったらライトがついて、明るくなったら消えるというのを試してみてください。ライトの色は自由に調整しましょう。
時間があったら明るさの段階を増やしてみましょう。

```blocks

loops.everyInterval(1000, function () {
    LL = pins.analogReadPin(AnalogPin.P0)
    if (LL < 50) {
        rc_tablelight.ライトを点ける()
        rc_tablelight.色を変える(Color.Indigo)
    } else if (LL < 100) {
        rc_tablelight.ライトを点ける()
        rc_tablelight.色を変える(Color.Light)
    } else {
        rc_tablelight.白にしてライトを消す()
    }
})


```

## STEP4 リモコン制御の可能性を考えよう @showdialog
![STEP4](https://skytree-1.github.io/rc_tablelight/images/img04.png)

## FINISH! @showdialog
![ゴール](https://skytree-1.github.io/rc_tablelight/images/img05.png)
