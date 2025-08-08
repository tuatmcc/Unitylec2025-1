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

# 6. 得点を生成させる

ここでは、ステージ上に得点をランダムな場所に生成させます。

## 6.1. 得点となるゲームオブジェクトのPrefabを作成する

`Hierarchy`で右クリック -> `3D Object` -> `Cube` を選択

オブジェクト名は `Score` に変更してください。作成時に名前を変更し忘れた際は,ゲームオブジェクトを右クリックして `Rename` を選択するか,選択してF2キーを押して名前を変更できます。

![create score](./createscore.gif)

`Ctrl + S` でこまめに保存することを忘れないでください。

`Score` を Project にドラッグアンドドロップしてください。 Prefab として保存されます。Project タブの `Assets` フォルダに `Score` という 水色の四角いアイコンのファイルが作成されます。

![create score prefab](./createscoreprefab.gif)

Prefab とは、ゲームオブジェクトの**設計図**のようなものです。ゲームオブジェクトそのものではありません(C#のクラスみたいですね！)。今回はこの `Score` の Prefab を元に、スコアのゲームオブジェクトを生成します。

`Score` の Prefab が作成できたら、 Hierarchy にある `Score` を削除してください。削除は、ゲームオブジェクトを選択して右クリックして `Delete` を選択するか, Delete キーを押して削除できます。

![delete cube](./deletecube.gif)

## 6.2. ScoreManager を作成する

得点のオブジェクトを生成するスクリプトを作成します。

`Project`タブで `Assets` フォルダー上で右クリック -> `Create` -> `MonoBehaviour Script`を選択してください.

スクリプトの名前を `ScoreManager` にしてください。

![create score manager](./createscoremanager.gif)

`ScoreManager` をダブルクリックして開いてください。

以下のようにスクリプトを書き換えてください。プログラムの説明は後で行います。

```csharp title="ScoreManager.cs" showLineNumbers
using UnityEngine;

public class ScoreManager : MonoBehaviour
{
+   [SerializeField] private GameObject scoreObject;
+   [SerializeField] private int scoreAmount = 10;

    // Start is called before the first frame update
    void Start()
    {
+       for (int i = 0; i < scoreAmount; i++)
+       {
+           float x = Random.Range(-10.0f, 10.0f);
+           float z = Random.Range(-10.0f, 10.0f);
+
+           Instantiate(scoreObject, new Vector3(x, 0.5f, z), Quaternion.identity);
+       }
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

スコアを管理するゲームオブジェクトを作成します.

Hierarchy で右クリック -> `Create Empty` を選択

ゲームオブジェクト名を `ScoreManager` にしてください。

![create score manager obj](./createscoremanagerobj.gif)

EmptyObject は、コンポーネントが何もついていないゲームオブジェクトです(座標の概念はあります)。inspector を開くと、何も表示されていないことがわかります。

![emptyobject](./emptyobject.png)

このゲームオブジェクトに`ScoreManager`をアタッチします。`ScoreManager` スクリプトを Project から ScoreManager ゲームオブジェクトにドラッグアンドドロップしてください。

![attach score manager script](./atachscoremanager.gif)

Inspector に `ScoreManager` がコンポーネントとして追加されていることがわかります。

次に, `ScoreManager` ゲームオブジェクトの Inspector にある `ScoreManager` コンポーネントの `Score Object` の欄に `Score` Prefab をドラッグアンドドロップしてください。

![set score obj](./setscoreobj.gif)

再生ボタン▶を押してみてください。ステージ上にランダムな位置に `Score` が生成されることがわかります。停止ボタン■を押して再び再生をすると,さっきと違う位置に `Score` が生成されます。

![playcheckscore](./playcheckscore.png)

確認ができたら、停止ボタン■を押して再生を停止してください。また,こまめに `Ctrl + S` で保存することを忘れないでください。

少し Score が大きいので、 `Score` の `Scale` を (0.3, 0.3, 0.3) に変更してください。

## 6.3. プログラムの説明

`ScoreManager` をダブルクリックして開いてください。

![exeprainscoremanager](./exeprainscoremanager.png)

変数 `scoreObject` は `GameObject` 型の変数です。今回は `Score` の Prefab を代入することで、その Prefab を**参照**しています.

変数 `scoreAmount` は `int` 型の変数です。`Score` の Prefab を元に、 Score オブジェクトを生成する回数を指定しています。

この2つの変数は、`[SerializeField]` という**属性**というものをつけています。これを変数につけることで、Unity Editor の Inspector から変数を代入できるようにしています。こうすれば、必要なパラメーターを Inspector から設定できるので、スクリプトを変更する必要がなくなります。 `BallController` の `_rb` には `[SerializeField]` をつけていないので, Sphere の Inspector の `BallController` コンポーネントには `_rb` を見ることができないのがわかります.

![ballcontrollernone](./ballcontrollernone.png)

`Random.Range` 関数は、引数で指定された範囲のランダムな値を返します。ここでは、`-10` から `10` の範囲のランダムな少数値を `x` と `z` に代入しています。

`Instantiate` 関数は、第1引数で指定されたゲームオブジェクトを元に、第2引数指定された位置に、第3引数で指定した角度でゲームオブジェクトを生成します。ここでは、`scoreObject` を `new Vector3(x, 0.5f, z)` の位置に生成しています。角度は `Quaternion.identity` で指定しています。`Quaternion.identity` は、回転がないことを表します(元のPrefabと同じ傾きって意味)。

Prefab はゲームオブジェクトの設計図なので,Prefabで適応させた設定は、生成されたゲームオブジェクトにも適応されます。`Score` Prefab の `Scale` を `(0.3, 0.3, 0.3)` に変更して見ましょう.

![setzerothree](./setzerothree.gif)

これで再生すれば,生成された `Score` の大きさが小さくなっていることがわかります。

![fixedscoresize](./fixedscoresize.png)

## 6.4. カメラをボールに追従させる

ここでは、カメラをボールに追従させます。

`Project`タブで `Assets` フォルダー上で右クリック -> `Create` -> `MonoBehaviour Script`を選択して `CameraController` という名前のスクリプトを作成して、以下のように書き換えてください。

```csharp title="CameraController.cs" showLineNumbers
using UnityEngine;

public class CameraController : MonoBehaviour
{
    // Start is called before the first frame update

+   [SerializeField] private Transform playerObject;
+   [SerializeField] private Vector3 offset;

    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
+       transform.position = playerObject.position + offset;
    }
}
```

`CameraController` をドラッグアンドドロップで `Main Camera` にアタッチしてください。

そして、`Main Camera` の Inspector にある `CameraController` コンポーネントの `Player Object` に `Sphere` をドラッグアンドドロップしてください。そして `Main Camera` の Inspector にある `CameraController` コンポーネントの `Offset` を `(0, 5, -10)` に変更してください。また、 `Main Camera` の `Transform` コンポーネントの Position を `(0, 10, -10)`, Rotation を `(30, 0, 0)` に変更してください。

![cameracontroller](./cameracontroller.gif)

再生ボタン▶を押してみてください。`WASD`でボールを操作すると,カメラが追従してきます。

![playcheckcamera](./playcheckcamera.gif)

## 6.5. スクリプトの説明

`CameraController` をダブルクリックして開いてください。

変数 `playerObject` は `Transform` 型の変数です。`Sphere` の Transform コンポーネントを代入することで、`Sphere` の Transform を**参照**できます。

変数 `offset` は `Vector3` 型の変数です。カメラの位置を調整するための変数です。`playerObject` の座標に `offset` を加えた座標にカメラを移動させます。

`transform.position` は、そのスクリプトをアタッチしたゲームオブジェクトの座標を表します。`transform` というTransform型の変数の中に `position` というVector3型の変数が入っています(C言語の構造体みたいですね！). `CameraController` は `Main Camera` ゲームオブジェクトにアタッチしてるので、`playerObject` (`Sphere`) の座標(`playerObject.position`)に `offset` を加えた座標にカメラを移動させています。`Transform` コンポーネントは,`GetComponent` 関数を使わなくても**参照**することができます. `playerObject.position` と `offset` は `+` 演算子で加算できます。`Vector3` 型の変数同士は、`+` 演算子が,各要素の加算をするように定義されています。なので,`new Vector3(playerObject.position.x + offset.x, playerObject.position.y + offset.y, playerObject.position.z + offset.z)` のように書く必要はありません(便利ですね！)。

# 7. 得点を回収する

ここでは、ボールが得点に触れたら得点を回収する処理を追加します。

## 7.1. `BallController` が得点を回収するできるようにする

`BallController` を以下のように書き換えてください。

```csharp title="BallController.cs" showLineNumbers
using UnityEngine;

public class BallController : MonoBehaviour
{
    private Rigidbody _rb;
+   private int _score = 0;

    // Start is called before the first frame update
    void Start()
    {
        _rb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void Update()
    {
        if(Input.GetKey(KeyCode.W))
        {
            _rb.AddForce(new Vector3(0, 0, 1));
        }

        if(Input.GetKey(KeyCode.S))
        {
            _rb.AddForce(new Vector3(0, 0, -1));
        }

        if(Input.GetKey(KeyCode.A))
        {
            _rb.AddForce(new Vector3(-1, 0, 0));
        }

        if(Input.GetKey(KeyCode.D))
        {
            _rb.AddForce(new Vector3(1, 0, 0));
        }
    }

+   private void OnCollisionEnter(Collision collision)
+   {
+       if(collision.gameObject.name == "Score(Clone)")
+       {
+           score++;
+           Debug.Log("Score: " + score);
+           Destroy(collision.gameObject);
+       }
+   }
}
```

実行して、ボールが得点に触れると、得点が回収されることを確認してください。

下の方のコンソールタブを見てください。得点を取ると、コンソールに現在のスコアが表示されます。また、得点を取ると、 Hierarchy にある `Score` が消えることがわかります。

確認ができたら、再生ボタンを押して再生を停止してください。

![checkdestroyscore](./checkdestroyscore.gif)

![debuglog](./debuglog.png)

## 7.2. スクリプトの説明

`BallController` をダブルクリックして開いてください。

変数 `score` は `int` 型の変数です。得点を保持します。

`OnCollisionEnter` 関数は、ゲームオブジェクトが他のゲームオブジェクトに衝突(Collision)したときに呼び出される関数です。Unity が自動的に呼び出してくれます.

`OnCollisionEnter` 関数の引数で渡された `Collision` 型の変数 `collision` に衝突したゲームオブジェクトの情報が入っています。`collision.gameObject.name` で衝突したゲームオブジェクトの名前を取得できます。ここでは、`collision.gameObject.name` が `Score(Clone)` と文字列が同じなら得点を加算し、コンソールに現在のスコアを表示し、衝突したゲームオブジェクトを削除しています。C#では,文字列同士を比較する場合は `==` 演算子を使います(C言語ではできないよ！)。

`Debug.Log` 関数は、コンソールにログを表示する関数です。C#では便利なことに、文字列型と数値型を足すと、数値が文字列に変換され,自動的に文字列連結になります。`Destroy` 関数は、引数で指定されたゲームオブジェクトを削除します。ここでは、衝突したゲームオブジェクト(`Score`)を削除しています。

# 8. ステージの調整

ここでは、ステージを調整します。

`Plane` の `Scale` を (5, 1, 5) に変更してください。

![planescale](./planescale.png)

ステージの壁も作りましょう。`Hierarchy`で右クリック -> `3D Object` -> `Cube` を選択。名前は `Wall` に変更してください。そして 4 方向分作るので、`Wall` を選択したまま `Ctrl + D` で複製してください。以下の画像のようになります。

![wall4](./wall4.png)

4 つの Wall の Position と Scale をそれぞれ以下のように変更してください。(写真は1つ目)

* Position (0, 2, 20), Scale (40, 4, 1)
* Position (0, 2, -20), Scale (40, 4, 1)
* Position (20, 2, 0), Scale (1, 4, 40)
* Position (-20, 2, 0), Scale (1, 4, 40)

![changewallpos](./changewallpos.png)

また、今のままでは、スコアにふれると一瞬ボールの動きが止まってしまいます。これは物理演算をするための当たり判定があるためです。このゲームでは,スコアの当たり判定は物理演算の当たり判定ではなく,スコアに触れたかどうかを判定するだけで十分です。そこで、Project にある `Score` プレバブの `Box Collider` の `Is Trigger` にチェックを入れてください。

![changetrigger](./changetrigger.png)

そして、`BallController` の `OnCollisionEnter` 関数を `OnTriggerEnter` 関数に変更してください。

```csharp title="BallController.cs" showLineNumbers
using UnityEngine;

public class BallController : MonoBehaviour
{
    private Rigidbody _rb;
+   private int _score = 0;

    // Start is called before the first frame update
    void Start()
    {
        _rb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void Update()
    {
        if(Input.GetKey(KeyCode.W))
        {
            _rb.AddForce(new Vector3(0, 0, 1));
        }

        if(Input.GetKey(KeyCode.S))
        {
            _rb.AddForce(new Vector3(0, 0, -1));
        }

        if(Input.GetKey(KeyCode.A))
        {
            _rb.AddForce(new Vector3(-1, 0, 0));
        }

        if(Input.GetKey(KeyCode.D))
        {
            _rb.AddForce(new Vector3(1, 0, 0));
        }
    }

-   private void OnCollisionEnter(Collision collision)
+   private void OnTriggerEnter(Collider collision)
    {
        if(collision.gameObject.name == "Score(Clone)")
        {
            score++;
            Debug.Log("Score: " + score);
            Destroy(collision.gameObject);
        }
    }
}
```

再生ボタンを押してみてください。スコアにふれてもボールの動きが止まらなくなりました。

![playcheckdestryscore](./playcheckdestryscore.gif)

## 8.1. スクリプトの説明

ただの当たり判定は,物理演算に影響を与えます.しかし,今回のように触れたら回収するアイテムといったものや,特定のエリアへの侵入検知などは,物理演算に影響を与えない当たり判定が必要です.そこで,`Collider` コンポーネントの `Is Trigger` を有効にします。これにより、当たり判定はあるけど物理演算には影響を与えない状態になります。`Is Trigger` を有効にした `Collider` コンポーネントは、`OnTriggerEnter` 関数を使って当たり判定を検知します。
