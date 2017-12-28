Nexus4やNexus5ではイヤホンジャックからUARTが出てるということだったので、L-01Fでも試してみた結果。

## 準備
参考にしたサイトによるとイヤホンジャックに挿したケーブルがUARTだと認識されるためには、MIC入力に3.3Vが必要らしい。  
また、UARTの信号レベルは1.8Vでないといけないらしい。  
というわけで、3.3Vの電源と信号レベル1.8VなUSB-シリアル変換ケーブル、イヤホンジャックに接続する3.5mm 4極ステレオミニプラグを用意することにした。

### 実際に使用したパーツ
実際に使用したパーツは以下のとおり。  
1.8Vな信号レベルが出ているUSB-シリアル変換ケーブルは探した限り１つしかなかった。  
残念なことにこのケーブルの電源電圧も1.8Vだったので、それを3.3Vにするためレギュレータも必要になった。

1. [1.8VなUSB-シリアル変換ケーブル](http://jp.rs-online.com/web/p/interface-development-kits/7158525/)
2. 3.5mm 4極ステレオミニプラグ
3.  [3.3Vステップアップ電圧レギュレータ](http://www.switch-science.com/catalog/1391/)

#### つなぎ方
* 1の橙(TXD)と2の白
* 1の黄(RXD)と2の赤
* １の黒(GND)と2の黄
* 1の黒(GND)と3のGND
* 1の赤(VCC)と3のVIN
* 2の裸の線(MIC)と3のVOUT

## 結果
L-01Fに挿して電源を入れるとログが取れた。

### 取得できたログ
[電源ONから電源OFFまでの全ログ](https://gist.github.com/hiikezoe/11390036)  
Nexus4やNexus5ではbootloaderのログも取得できているみたいなのに、L-01FではLinuxカーネルが起動してからのログしか取れなかった。  
ただ、カーネルのcmdlineに
`uart_console=detected`
と出ているので、bootloaderもUARTケーブルが刺さっていることは認識しているよう。

## 参考にしたサイト
* [Building a Nexus 4 UART Debug Cable](https://blog.accuvant.com/jduckandryan/building-a-nexus-4-uart-debug-cable/)
* [Serial Console on Google Nexus 5](http://www.abclinuxu.cz/blog/Lorris/2013/12/serial-console-on-google-nexus-5)