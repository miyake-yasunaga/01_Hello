***
Hello Worldの仕組み
***

Androidアプリは
新規プロジェクトを作成すると
｢Hello world!｣を表示するプログラムを
自動で作ってくれます。

![00](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/00.png)

では、このソースを軽く追ってみましょう。

Androidアプリは
最初に｢java｣フォルダにある
MainActivityクラスのonCreateメソッドに
書かれた処理で初期画面を作ります。
（Ｃ言語やJavaのmain関数、iアプリのviewDidLoadにあたる。）

![01](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/01.png)

ここの
>setContentView(R.layout.activity_main);
という部分で画面表示をしているようです。

ということで、
｢res｣フォルダの｢layout｣の下のactivity_main.xml
の内容を確認してみます。

![02](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/02.png)

Androidアプリの画面レイアウトはＸＭＬで記述されています。
ここに｢android:text="Hello world!｣と書いてる部分があります。

ここの文字を変えると
画面表示が変わるかもしれません。

ということで、マウスを近づけると・・・
｢android:text="@string/hello_world"｣
という表示に切り替わってしまいました。

![03](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/03.png)


どうやら、どこかにstringsというファイルがあって
そこに何か書いてあるようです。
ということで捜してみると・・・
｢res｣フォルダの｢values｣の下にstrings.xml
というファイルがありました。

<string name="app_name">App_001</string>
<string name="hello_world">Hello world!</string>
という記述があります。
ここで画面の表示を設定しているようです。

![04](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/04.png)

では表示部分を
日本語に変えてみます。

<string name="app_name">さんぷるあぷり</string>
<string name="hello_world">こんにちわ！</string>

![05](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/05.png)

ビルドしてみると・・・
見事、日本語に変わりました！

![05_2](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/05_2.png)

では、テキストをもう１行追加するには
どうすればよいでしょうか？

｢こんにちは！｣の下に
｢さようなら！｣という文字を追加してみましょう。

まずstrings.xmlに
<string name="bye_world">さようなら！</string>
を追加します。

![06](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/06.png)

｢res｣フォルダの｢layout｣の下のactivity_main.xmlの

    <TextView
        android:text="@string/hello_world"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
    />
の部分をコピペ

![08](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/08.png)

追加したhello_worldの部分をbye_worldに変更すればＯＫ・・・
と思いきや文字が重なって表示されてしまいました。

![09](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/09.png)

![09_2](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/09_2.png)

どうやらRelativeLayoutは
画面のオブジェクト同士の
相対的な位置関係を設定してやる
必要があるようです。

具体的には
①
｢こんにちは！｣を表示する
TextViewにidを設定

>android:id ="@+id/text01"

②
｢さようなら！｣を表示する
TextViewの位置を
｢こんにちは！｣を表示する
TextViewの下と設定

>android:layout_below="@id/text01"

![10](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/10.png)

これでうまく表示することができました。

![10_2](https://github.com/miyake-yasunaga/01_Hello/blob/master/images/10_2.png)

固定文字の画面表示だけでも
結構奥が深いですね。


