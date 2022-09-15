## ラボ環境の使用方法

- [Cloud Skills Boost (Qwiklabs) へのログイン手順](https://qualia906.github.io/skillsboost/how-to-login/)
- [ラボの開始手順 (AWS / GCP)](https://qualia906.github.io/skillsboost/how-to-use-lab/)

<br />    

## ラボ (演習)


### 演習 1：[Introduction to Amazon EC2 Auto Scaling (日本語版)](https://amazon.qwiklabs.com/focuses/37760?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=16787010)【AWS】

<br /> 

### 演習 2：[Docker の概要](https://www.qwiklabs.com/focuses/1029?catalog_rank=%7B%22rank%22%3A3%2C%22num_filters%22%3A1%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=4806504)【Google Cloud】


-   初回にdocker buildコマンドを実行した際に、「Cloud Shell の承認」というダイアログが表示されることがありますが、そのまま承認してください。
    
-   「公開」で Docker イメージを Google Container Registry に push した後の手順では、Cloud Shell ではなく GCP コンソール (GUI) から [ナビゲーション  メニュー] > [Container Registry] をクリックします。
    
-   任意のエディタで内容を書き換える手順において、vi や nano の操作が不安な方は、次のコマンドをコピーして実行してください。  

    ```
    cp -p app.js app.js.org  
    sed -ie 's/Hello World/Welcome to Cloud/' app.js
    ```
  
<br />

### 演習 3：[DataStore: Qwik Start](https://www.qwiklabs.com/focuses/941?catalog_rank=%7B%22rank%22%3A5%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=9212410)   
  AWSのDynamoDB に相当する Google Cloud の NoSQL データベース サービスです。

<br />

### 演習 4：クラウドデザインパターンの適用

-   [AWS クラウドデザインパターン](http://aws.clouddesignpattern.org/index.php/%E3%83%A1%E3%82%A4%E3%83%B3%E3%83%9A%E3%83%BC%E3%82%B8)    
-   [AWS クラウドデザインパターン](http://web.archive.org/web/20171008040110/http:/aws.clouddesignpattern.org/index.php/%E3%83%A1%E3%82%A4%E3%83%B3%E3%83%9A%E3%83%BC%E3%82%B8)（上記が表示されない場合はこちら）
    
<br />  

## Reference

- AWS
  -  [AWS Well-Architected – 安全で効率的なクラウド対応アプリケーション](https://aws.amazon.com/jp/architecture/well-architected/)

 
 - Microsoft Azure   
   -   [Microsoft Azure クラウド設計パターン](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/)
   -   [Microsoft Azure Well-Architected Framework](https://docs.microsoft.com/ja-jp/azure/architecture/framework/)    


- Google Cloud
  -  [Google Cloud ソリューション デザインパターン](https://events.withgoogle.com/solution-design-pattern/)
  -  [Google Cloud アーキテクチャ フレームワーク ](https://cloud.google.com/architecture/framework)
  -  [ハイブリッドクラウドのパターン (ハイブリッドクラウドと Google Cloud)](https://www.slideshare.net/GoogleCloudPlatformJP/cloud-onair-google-cloud-201927-133656441)

<br>
<br>


# 演習補足手順

*インストラクターから指示があった場合はこちらの手順を参照しながら演習を進めてください。*


## ラボ1 Introduction to Amazon EC2 Auto Scaling


このラボでは以下のことを試します。

- 起動テンプレートを作成する

- Auto Scaling グループを作成する

- Auto Scaling インフラストラクチャをテストする

- Auto Scaling 起動の結果を表示する

### タスク1:起動テンプレートを作成する

  

まずは、Auto Scalingグループを作成するために、仮想マシンのレシピとなる「起動テンプレート」を作成します。

  

1.  **画面左上の「サービス」で「コンピューティング ＞ EC2」をクリック**  
      
    
2.  **左側のナビゲーションペイン**で「インスタンス」の下にある**「起動テンプレート」**をクリック  
      
    
3.  **「起動テンプレートを作成」**をクリック  
      
    
4.  **「起動テンプレート名と説明」**で、次のように設定します。  
    **・起動テンプレート名**：Lab-template
    

**・テンプレートバージョンの説明**：version 1

※Lab-templateがすでに作成済みと表示される場合には「Lab-template2」としてください。  
  

5.  **「アプリケーションおよび OS イメージ (Amazon マシンイメージ) 」**で、次のように設定します。  
    ・**検索ボックス**に**「Amazon Linux」**と入力して**Enterキー**  
    ・「**Amazon Linux 2 AMI (HVM)」**と表示される一番上のマシンイメージの選択をクリック  
      
    
6.  **「インスタンスタイプ」**で、ドロップダウンの一覧から**「t3.micro」**を選択  
      
    
7.  **「ネットワーク設定」**までスクロールして**「セキュリティグループ」**ドロップダウンの一覧から**「MySecurityGroup」**を選択  
      
    
8.  画面の下までスクロールして**「起動テンプレートを作成」**をクリック  
      
    
9.  **「起動テンプレートを表示」**をクリック。作成したテンプレートが表示されることを確認します。  
      
    

### タスク2:Auto Scaling グループを作成する

  

次に、作成した起動テンプレートを使用してAuto Scalingグループを作成します。

今回は自動スケーリングは設定しませんが、Auto Scalingグループで設定した台数を自動的に維持するインスタンスの自動回復を試します。

  

1.  **左側のナビゲーションペイン**で下までスクロールして**「Auto Scaling」**の下にある**「Auto Scaling グループ」**をクリックします。  
      
    
2.  **「Auto Scaling グループを作成」**をクリックして、次のように設定します。  
    **・Auto Scaling グループ名**：Lab-Group
    

**・起動テンプレート：**作成した起動テンプレート（Lab-template）を選択

・**「次へ」**をクリック  
  

3.  **「ネットワーク」**で、次のように設定します。
    

**・VPC：**Lab VPC  
（ドロップダウンから最後に（Lab VPC）と記載のある方を選択）

**・アベイラビリティーゾーンとサブネット：**両方のサブネットを選択  
（ドロップダウンから表示される二つのサブネットを両方クリックして選択）  
**・「次へ」**をクリック  
  

4.  **「詳細オプションを設定」**で次のように設定します。
    

・**「ヘルスチェック」**の**「ヘルスチェックの猶予期間」**：60秒

・**「その他の設定」**の**「モニタリング」**：「CloudWatch 内でグループメトリクスの収集を有効にする」**チェックボックスをオン**

・**「次へ」**をクリック  
  

5.  **「グループサイズとスケーリングポリシーを設定する」**で、次のように設定します。
    

**・最小容量**：1

**・最大容量**：2

**・「次へ」**をクリック  
  

6.  **「次へ」を何回かクリック**して、**「確認」ページ**に移動します。  
      
    
7.  **「Auto Scaling グループを作成」**をクリック  
      
    ページが切り替わり、作成したAuto Scalingグループが表示されます。  
      
    

### タスク3:Auto Scaling グループを確認する

  

作成したAuto Scalingグループを確認してみます。

  

1.  **作成したAuto Scalingグループ（Lab-Group）**をクリックします。
    

**「詳細」タブ**でAuto Scalingグループについての情報を確認します。  
  

2.  **「アクティビティ」タブ**をクリックします。
    

ステータス列にインスタンスの現在のステータスが表示されます。

**インスタンス作成中はPreInService**と表示され、**インスタンスが作成されると、ステータスがSuccessfulに変わります。**変わらない場合は更新アイコンをクリックしてみてください。  
  

3.  **「インスタンス管理」タブ**をクリックします。
    

作成されたインスタンスの情報が表示されます。右にスクロールすると、ヘルスステータス列にEC2インスタンスヘルスチェックの結果が問題ないことを表す「**Healthy**」表示されます。

### タスク4：Auto Scaling （インスタンスの自動回復）をテストする

  

作成したAuto Scalingグループのインスタンスを終了（削除）することで、Auto Scalingグループで設定した台数を自動的に維持する、インスタンスの自動回復を試します。

  

1.  **「インスタンス管理」タブ**で作成された**インスタンスIDの値をクリック**する。
    

作成された、Amazon EC2インスタンスのページが別タブで開きます。  
  

2.  **「インスタンスの状態」**ドロップダウンメニューをクリックします。
    

・**「インスタンスを終了」**を選択（※インスタンスを停止ではありません）

・続けて**「終了」**をクリック

**・左側のナビゲーションペイン**で**インスタンス**をクリックします。

インスタンスの状態が**「シャットダウン中」**になっています。

インスタンスの状態が**「終了済み」**に変わるまで待ちます。  
  

3.  **左側のナビゲーションペイン**で**「Auto Scaling グループ」**をクリックします。  
      
    
4.  **作成したAuto Scaling グループ（Lab-Group）**をクリックします。  
      
    
5.  **「アクティビティ」タブ**を開きます。  
    最初のインスタンスの作成と終了のエントリ、続いて新規インスタンス作成のエントリが表示されることを確認できます。  
      
    
6.  **左側のナビゲーションペイン**でインスタンスをクリックします。終了したインスタンスとともに、新規に作成されたインスタンスが表示されています。
    

  

ラボ１は以上です。お疲れ様でした。
<br>
<br>
  

----------

## ラボ3Datastore: Qwik Start

NoSQLデータベースのDataStoreを試してみます。DataStoreにデータを格納し、検索してみます。オンプレミスで使用しているリレーショナルデータベースとの違いを意識しながら進めていきましょう。

  

1.  左上の [Google Cloud Platform] の横にある**ナビゲーション メニュー**をクリック
![](assets/images/image1.png)

2.  Cloud Platform Console の左側のメニューの、**Datastore > エンティティ**に移動します。（Datastoreが表示されない場合はメニュー下部のMORE PRODUCTSをクリックして開いてください）
    
3.  [Datastore モード] 列で、**Datastore モードを選択 **をクリックします。
    
4.  次に、データベースを作成する場所を選択します。プルダウン メニューを使用してt東京リージョンの**asia-northeast1(Tokyo)**を選択します。  
    (ここでデータベースを作成するをクリックする必要がある場合があります)  
    次のステップに進むまで1～2分ほど時間がかかります。
    
5.  **エンティティを作成**をクリックします。エンティティはDatastoreにおける一行のデータのような扱いです。  
    ![](assets/images/image2.png)
    

6.  エンティティの作成画面に以下のように設定を行います。  
    Datastoreの種類はリレーショナルデータベースのテーブルのようなものです。  
    ![](assets/images/image3.png)  
    **続けてプロパティを入力します**。Datastoreのプロパティはリレーショナールデータベースの列のようなものです。  
    最初の新しいプロパティに以下のように設定を行い、**完了**をクリックします。**続けて、プロパティを追加をクリックし、以下の表のように3つのプロパティを設定します。**  
    ![](assets/images/image4.png)


|  名前| タイプ |値|
|--|--|--|
|  Artist|文字列  |Pink Floyd|
| Song | 文字列 |money|
|  Album| 文字列 |The Dark Side of the Moon|


7.  **作成** をクリックします。作成した Music エンティティがコンソールに表示されます。  
    ![](assets/images/image5.png)
    
8.  同様に以下の二つのエンティティを登録します。  
    **エンティティを作成**をクリックして登録します。  
    Datastoreはテーブル作成時テーブルの構造である「スキーマ」を設定する必要がなく、後からエンティティを追加する際に柔軟に列を定義することができます。
    
|  名前| タイプ |値|
|--|--|--|
|  Artist|文字列  |John Lennon|
| Song | 文字列 |Imagine|
|  Album| 文字列 |Imagine|
|  Year| 整数 |1971|
| Genre |文字列  |Soft rock|

|  名前| タイプ |値|
|--|--|--|
|  Artist|文字列  |Psy|
| Song | 文字列 |Gangnam Style|
|  Album| 文字列 |Psy 6 (Six Rules), Part 1|
|  Year| 整数 |2011|
| LengthSeconds |整数  |219|

9.  ３つのエンティティを設定しました。エンティティの一覧として以下のように表示されます。  
      
    ![](assets/images/image6.png)  
      
     

### 種類別クエリの実行

  

DatastoreではGUI画面から簡単にフィルタをかけてデータを検索することができます。

  

1.  **種類別のクエリ** をクリックします。(多くの場合、すでに種類別クエリ画面になっています)
    
2.  **種類** に **Music** を選択します。(多くの場合、すでにMusicが選択されています)
    
3.  **+クエリに追加** をクリックします。
    
4.  プルダウン リストで、**「WHERE」「Artist」、「==」「string」、「Psy」** を選択し、**「実行」**をクリックします。1件の検索結果が表示されます。
    

  

### GQL クエリの実行

DatastoreではSQLに似たGQLというクエリ言語を使用することができます。慣れ親しんだSQLに似たクエリを実行できるため、便利です。  
  

1.  **GQL によるクエリ** タブをクリックします。
    
2.  クエリボックスに次のように入力します。
    

    SELECT * FROM Music

  

3.  **クエリを実行** をクリックします。  
    クエリの結果として、作成した Music エンティティが表示されます。
    
<br>
ラボ3は以上です。お疲れ様でした。

<br>

早く終わった場合にGCPの他のサービスをのメニューを見ても構いませんが、ラボで指定された以外の仮想マシンを立てたり等、新たなリソースを作成したりはしないでください。

新たなエンティティを足してみたり、削除してみたり、クエリを実行してみたりするのは構いません。


<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script language="JavaScript">
$(document).ready( function () {
   $("a[href^='http']").attr('target', '_blank');
})
</script>