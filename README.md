# ASP.NETでブログアプリの開発
- Udemy:【入門者向け】ASP.NET MVCでWebアプリ開発のノウハウを学ぼう！


## ソース

## 作業進捗
### プロジェクトの作成
- asp.netフレームワーク,C#を選択
- MVCを選択
- NuGetパッケージの管理からentityframeworkインストール

### モデルの準備
- `Atricle.cs`作成
    - ID,タイトル,本文,カテゴリー,投稿日,更新日,コメントのコレクション
- `Comment.cs`作成
    - ID,コメント,投稿日,対応する記事,記事のIDを持つ
- `Category.cs`作成
    - ID,Category名,記事のコレクション,記事の個数
- 作成したモデルをDBと接続するために`BlogContext.cs`作成
    - 上3つを持つ
    - ツール->nugetパッケージコンソールからmigration実行
    - `Migrations/Configuration.cs`が作成される

### 認証機能の実装
- Modelの作成
    - `LoginViewModel.cs`作成
    - `CustomMembershipProvider.cs`作成
    - `CustomRoleProvider.cs`作成
    - ユーザー管理機能は省略するため固定文字列で認証実装
- Controllerの作成
    - `LoginController.cs`作成
- Viewの作成
    - `LoginController.cs`の`Index()`を右クリックして`Views/Login/Index.cshtml`作成

### ArticlesControllerの実装
- Create,Edit,Delete実装
- Articleが追加されたときにCategoryの管理もこのコントローラで行う

### CategoriesControllerの実装
- Create,Editはない
- Delete実装

### 共通レイアウトの実装
- Viewから作成
- 参照のNugetパッケージからbootstrapインストール

###　viewの実装
- ArticlesのView
- CategoriesのView
- LoginのView

### ルーティング、認証の実装
- App_start/RouteConfig.cs変更
- Web.config変更
- 動作確認してバグ修正した

### サイドメニューの実装
- 共通処理として`CategoryFilterAttribute.cs`をCOntroller内でクラスとして実装
    - `OnActionExecuted`メソッドは実行が終了すると毎回呼び出される
- `ArticleController.cs`に適用する
    - アノテーションするときは`[CategoryFilter]`のようにAttribute取り除く
- `CategoriesController.cs`に適用
- これによって各アテンションメソッドが実行された後にOnActonExecutedが呼び出されてdbからviewbagにカテゴリーがセットされる
- 次に共通レイアウトページ編集

### カテゴリーの入力候補の表示
- Articleのcreateとeditのビューを編集
    - optionタグで表示するようにする