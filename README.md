---
title: "【GIF付き】写経で学ぶ Unity - 玉転がしゲームを作ろう (2025年版)"
date: "2025-05-28"
author: "sugawa197203"
---

難易度: ★☆☆☆☆ 入門レベル

# 1. はじめに

* この記事は Unity 講習会 2025 の資料です.
* Unity やってみたいけど何をすればいいのかわからない人を0を1にするための講習会です.
* 2024年度版とほぼほぼ一緒です. Unity6用に書き換えちょっと修正した感じです.

## 1.1. 前提条件, 注意事項

* Unity Hub と Unity と任意の IDE (Visual studio, Rider など) をインストール済みであることを前提です.
* 本資料では Unity 6.0(6000.0.51f1) を使用します.
* Mac の人は Visual Studio は使えないことに注意してください.
* 任意のIDEが無い方は[こちら](https://tuatmcc.com/blog/UnityLec2024Step0/)の記事を読んでください.
* プログラミングは, A科の1年生が6月ぐらいまでの授業で習ったことを前提に解説が書いてあります.
* この記事では, WindowsでコードエディタにRiderを使う前提に書いています. Mac, Linuxの人, Visual Studioの人は適宜読み替えてください.

## 1.2. やる内容と学ぶ内容

玉転がしゲームを作ります. Unityでゲームを作るための基本的なことを学びます.

# 2. Unityのプロジェクトを作る

ここでは, Unityのプロジェクトを作成します.

## 2.1. Unity Hub

Unity Hubを起動します. Unity HubはUnityのプロジェクトを管理するためのツールです. Unity Hubを起動すると, プロジェクトの一覧が表示されます. 以下の写真では, 何もプロジェクトがない状態です.

![Unity Hub](./hubhome.png)

左にある `Install` を開くとパソコンにインストール済みのUnity Editor本体の一覧を見ることができます.

![Unity Editor](./editors.png)

Unity のプロジェクトを作ります. 左の `Projects` をクリックして, プロジェクト一覧に戻ってください. そして, 右上の `New Project` ボタンをクリックします.

![Create Project](./createproject.png)

プロジェクトの初期化画面が表示されます. 以下のように設定してください.

* 真ん中の項目はテンプレートです. `Universal 3D` を選択してください. デフォルトになっているはずです.
* 右側の `Project name` はプロジェクト名をきめる場所です. プロジェクト名は `RollingBall` としてください.
* `Location` はプロジェクトの保存場所です. デフォルトのままで大丈夫です. お好みで変更しても構いません.
* `Connect to Unity` はチェックを外してください.

設定が終わったら, 右下の `Create Project` ボタンをクリックしてください.

![Create Setting](./createsetting.png)

しばらくすると, Unityのエディタが起動します. これでプロジェクトの作成は完了です. 以下の様な画面が表示されるはずです.

![Open Project](./openproject.png)

## 2.2. Unity Editor のタブとレイアウト

デフォルトのレイアウトでは, 以下のタブが見えています。

|タブの名前|説明|
|---|---|
|Scene|シーンを編集する (神視点)|
|Game|レンダリングされたゲーム画面|
|Hierarchy|シーンに配置されたオブジェクトのリスト|
|Project|プロジェクトのファイル一覧 (Explorer や Finder のようなもの)|
|Inspector|選択したオブジェクトのプロパティ|
|Console|ログの表示|

![Exprain Editor](./expraineditor.png)

重なってるタブの切り替えは, タブの右上のタブの名前の部分をクリックすることで切り替えることができます.

![scene-gametab](scene-gametab.gif)

それぞれのタブの詳しい説明は, 実際にゲームを作りながら説明していきます.

# 3. オブジェクトを配置する

ここでは, シーンにオブジェクトを配置します. 現在, `SampleScene` という名前のシーンが開いています. `Hierarchy` タブに `SampleScene` と書かれた項目があるはずです. これが現在開いているシーンです. シーンとは, ゲームの1つの画面を表すものです. Unityでは, シーンごとにゲームの場面を管理します.

タイトルシーンや, バトルシーン, マップシーンなど, ゲームの場面ごとにシーンを分けて管理することができます.

`SampleScene` となってる名前を `MainScene` に変更しましょう. `Assets` タブで, `Scenes` フォルダを開き, `SampleScene` を右クリックして, `Rename` を選択します. そして, `MainScene` と入力してください.

![remenesamplescene](./renamesamplescene.gif)

これで, `Hierarchy` タブにあるシーンの名前が `MainScene` に変更されました.

![renamedsamplescene](renamedsamplescene.png)

## 3.1. 板を配置する

シーンに板を配置します. まず, `Hierarchy` タブ上で右クリックして, `3D Object` → `Plane` を選択します. すると, シーンに板が配置されます.

![Create Plane](./createplane.gif)

シーン名に `*` がついているのは, シーンが保存されていないことを示しています. `ctrl + S` でシーンを保存してください.

Hierarchyで`Plane`を選択すると、Inspectorに`Plane`のプロパティが表示されます。

`Plane`には`Trasform`, `Mesh Filter`, `Mesh Renderer`, `Mesh Collider`の要素(Component)がついています。それぞれの役針は以下の通りです。

* Transform
  * 座標や傾きといった3D空間の位置情報プロパティ

* Mesh Filter, Mesh Renderer
  * レンダリングに関するプロパティ

* Collider (Mesh Collider)
  * 3Dモデルに当たり判定をつけるプロパティ

* (Material)
  * マテリアルを設定するプロパティ

![Inspector Plane](./planeproperties.png)

## 3.2. ボールを作る

Hierarchyで右クリック -> 3D Object -> Sphere を選択

![Create Sphere](./createball.gif)

このままでは地面にめり込んでいるので、`Sphere`の`Trasform`の`Position`の`Y`を`5`に変更します。

![ChangePos](./changepos.png)

いい感じの位置になりました！

![set Sphere Position](./setballposition.png)

`Ctrl + S` で定期的に保存することを忘れないでください。

# 4. ボールを重力で落下させる

ここでは、ボールを重力で落下させます。

エディターの上の方にある再生ボタン▶を押すと、ゲームが実行されます。押してみましょう．停止ボタン■を押すと、ゲームが停止します。

![Play Button](./playnorb.gif)

何も起こりません！

先ほど作成した`Sphere`には,物理演算を行う要素(コンポーネント)がついていません。そのため,ボールが重力で落下することはありません。`Sphere`に物理演算を行う要素を追加しましょう。

## 4.1. Rigidbody を追加する

`Hierarchy`で`Sphere`を選択し、`Inspector`で下の方にある`Add Component` -> `Physics` -> `Rigidbody` をクリック

![setrbody](./setrb.gif)

`Sphere`に`Rigidbody`が追加されました！

![addedrb](./addedrb.png)

上の方にある再生ボタン▶を押してみてください。ボールが落下します。

![checkrb](./checkrb.gif)

ボールが自由落下するのを確認できたら、必ず停止ボタン■を押して再生を停止してください。

また, こまめに`Ctrl + S` で保存することを忘れないでください。

# 5. ボールを操作する

ここでは、ボールを操作するためのスクリプトを作成します。

## 5.1. スクリプトを作成する

`Project`タブで `Assets` フォルダー上で右クリック -> `Create` -> `MonoBehaviour Script` を選択してください. このとき、ファイル名を `BallController` にしてください。

![create ball script](./createballscript.gif)

作成時に名前を `BallController` にし忘れた場合は `BallController` を右クリックして `Rename` を選べばファイル名を変更できます。

![named ball controller](./namedballcontroller.png)

`BallController`　をダブルクリックして開くと、Rider が起動します。(※このとき、visual studio が起動しても OK です. Visual Studio Code が開いた場合はなにか設定が間違っている可能性があります。)

![open ball controller](./openballcontroller.png)

`BallController.cs` が開かれていることを確認してください。`.cs` は C# の拡張子です。(C言語だと`.c`, C++だと`.cpp`, pythonだと`.py`)

## 5.2. スクリプトを書き換える

以下のようにスクリプトを書き換えてください。プログラムの説明は後で行います。

```csharp title="BallController.cs" showLineNumbers
using UnityEngine;

public class BallController : MonoBehaviour
{
+   private Rigidbody _rb;

    // Start is called before the first frame update
    void Start()
    {
        _rb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void Update()
    {
+       if(Input.GetKey(KeyCode.W))
+       {
+           _rb.AddForce(new Vector3(0, 0, 1));
+       }
+       if(Input.GetKey(KeyCode.S))
+       {
+           _rb.AddForce(new Vector3(0, 0, -1));
+       }
+       if(Input.GetKey(KeyCode.A))
+       {
+           _rb.AddForce(new Vector3(-1, 0, 0));
+       }
+       if(Input.GetKey(KeyCode.D))
+       {
+           _rb.AddForce(new Vector3(1, 0, 0));
+       }
    }
}
```

3行目の `public class BallController : MonoBehaviour` の部分で、 `class` の後が `BallController` になっていることを確認してください。大文字小文字、全角半角の違いにも注意してください。

## 5.3. スクリプトを Sphere にアタッチする

Project にある `BallController` を `Sphere` にドラッグアンドドロップしてください。

![attach script](./attachscript.gif)

`Sphere` の Inspector に `BallController` がコンポーネントとして追加されるのがわかります。これで、スクリプトをゲームオブジェクトにアタッチできました。

![attached script](./attachedscript.png)

Unityでは,スクリプトを書いてコンポーネント(要素)を作ります.そしてそのコンポーネントをゲームオブジェクトにアタッチすることで,ゲームオブジェクトに要素を追加します.

## 5.4. ゲームを再生してみる

再生ボタン▶を押してみてください。`W`, `A`, `S`, `D` キーを押すと、ボールが前後左右に動くことがわかります。(周りに壁とか無いから落ちるけど...)

![playtest](./playtest.gif)

確認ができたら、停止ボタン■を押して再生を停止してください。再生を停止すると、ゲームの状態がリセットされ,ボールが元の位置に戻ります。

# 5.5. プログラムの説明

`BallController` をダブルクリックして開いてください。

![expreinballcontroller](./expreinballcontroller.png)

1行目の `using UnityEngine;` は、Unity の機能を使うための宣言です。C言語の `#include` のようなものです。Unity の機能を使うためには、この呪文が必要です

3行目の `public class BallController : MonoBehaviour` は、`BallController` という**クラス**を定義しています。クラスはC#のオブジェクトというものの設計図です.コンポーネントはC#のオブジェクトとして存在してます.

![exeprainclass](./exeprainclass.png)

変数 `rb` は `Rigidbody` 型の変数です。任意のゲームオブジェクトに付いている `Rigidbody` コンポーネントを取得して代入することで、その `Rigidbody` を**参照**できます。

`Start` 関数は、再生ボタンを押したら最初に一度だけ実行される関数です。 Unity が呼び出してくれます。ここでは、Start 関数の中で、そのスクリプトがアタッチしている `Rigidbody` コンポーネントを `GetComponent` 関数で取得しています。`GetComponent` 関数は、アタッチしているゲームオブジェクトの指定したコンポーネントを取得する関数です。ここでは、`Rigidbody` コンポーネントを指定しています。

`Update` 関数は、再生ボタンを押したら毎フレーム実行される関数です。 Unity が呼び出してくれます。ここでは、 `Input.GetKey` 関数を使って、引数で指定されたキーボードのキーが入力されたかをif文で判定しています.

キーが入力されたら `Rigidbody` の `AddForce` 関数を使って、玉に力を加えています。 `Input.GetKey` 関数では、引数で指定されたキーボードのキーが押されている間、true を返します。そうでなければ、false を返します。 `AddForce` 関数は、引数で指定されたベクトルの力を加えます。`w` キーが押されたら、Z軸に対して`+1`の力、`s` キーが押されたら、Z軸に対して`-1`の力、`a` キーが押されたら、X軸に対して`-1`の力、`d` キーが押されたら、X軸に対して`+1`の力を加えます。 `new Vector3` で Unity のベクトル情報を生成し、`AddForce` 関数の引数に渡しています。
