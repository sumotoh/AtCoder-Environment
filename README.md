# Atcoder Environment

現在、RとJulia用です。

## Prerequisites
- install Docker Desktop
- install VSCode and [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Setup

clone(2.)するだけで使用できます。<br>
このリポジトリをテンプレートとして使用し、自分のプライベートリポジトリで管理したいときは以下を参考にしてください。

1. 空のリポリトジを作っておく。

2. このリポジトリをclone
    ```{.shell}
    git clone https://github.com/sumotoh/AtCoder-Environment.git
    ```

3. リモートブランチの切り替え

    まずリモートブランチを確認。このリポジトリの情報があるはず。
    ```{.shell}
    git remote -v
    ```

    ```{.shell}
    git remote set-url origin <1で作成した自分のリポジトリのurl>
    ```

    もう一度以下で確認すると情報が更新されているはず。
    ```{.shell}
    git remote -v
    ```

    4. これでpush先が自分のリポジトリになります。

## setting

1. VSCode左下の青い四角形を押して、「コンテナで再度開く(Reopen in Container)」を押してください。Ctrl+Shift+Pで「開発コンテナー：コンテナで再度開く(DevContainer: Reopen in Container)」を探しても問題ありません。

2. atcoder-cliとonline-judge-toolsの連携を確認

    それぞれヘルプが出ることを確認してください。
    ```{.shell}
    acc -h
    ```

    ```{.shell}
    oj -h
    ```

    atcoder-cliとonline-judge-toolsが連携していることを確認してください。
    ```{.shell}
    acc check-oj
    ```

3. AtCoderにログインする。

    ```{.shell}
    acc login
    ```

    ```{.shell}
    oj login https://beta.atcoder.jp/
    ```

4. accの設定を変更（必須ではない）

    Rをメインに使用する場合は以下のようにしておくと便利かもしれません。
    こうしておくと問題を読み込んだとき、Rのテンプレートが一緒に付いてきます。 <br>
    Juliaを使う場合は、rの部分をjuliaにしてください。
    ```{.shell}
    acc config default-template: r
    ```

    問題を読み込むとき、(例えばabc101を読み込んだとき)a問題からe問題のすべての問題を自動で読み込みたいときは以下を設定してください。
    デフォルトではinquireが設定されていて、これは読み込むときにどの問題か聞かれます。
    ```{.shell}
    acc config default-task-choice all
    ```

## How to use

初回の設定からそのままここに来た場合は1.,2.を無視してください。

1. VSCode左下の青い四角形を押して、「コンテナで再度開く(Reopen in Container)」を押してください。Ctrl+Shift+Pで「開発コンテナー：コンテナで再度開く(DevContainer: Reopen in Container)」を探しても問題ありません。

2. AtCoderにログインしていない場合はログインしてください。

    ```{.shell}
    acc login
    ```

    ```{.shell}
    oj login https://beta.atcoder.jp/
    ```

3. 問題の読み込み

    左下のTASK RUNNERで"[I-abc] Init Task for Atcoder"(AtCoder Beginner Contestを読み込みたい場合)、[I-arc] Init Task for Atcoder"(AtCoder Regular Contestを読み込みたい場合)を押してください。メニューバーのターミナル -> タスクの実行からも選択できます。<br>
    画面上部にどのコンテストを読み込むか聞かれるので、abc300など読み込みたいコンテストを入力してください。

4. テストの実行

    左下のTASK RUNNERで[T-R] Test Task for Atcoder(Rコードをテストする場合)を押すとテストが実行されます。

5. 提出

    左下のTASK RUNNERで[S-R] Submit Task for Atcoder(Rコードを提出する場合)を押して指示に従ってください。このとき、"# Del テスト"のように# Delで始まるコメントは提出後削除されるように設定しています。

【注意点】
- AtCoder Beginner Selectionはうまく読み込めないかもしれません。(テストのフォルダがabcなどはtests,absはtestのため)。
- Rのバージョンを指定してインストールする方法がわからなかったため、最新版のRがインストールされています。AtCoderとの互換性がないかもしれません。

【参考サイト】

- AtCoder の環境を Docker で作りたい
https://qiita.com/tf63/items/c93c6f24d73599e637d8#%E3%83%86%E3%82%B9%E3%83%88%E3%81%AE%E5%AE%9F%E8%A1%8C

- Failing installing R Docker on Ubuntu 22.04 
https://stackoverflow.com/questions/78228725/failing-installing-r-docker-on-ubuntu-22-04

--- 

-  atcoder-cli,online-judge-toolsを入れてAtCoderのローカル自動テスト環境を構築した
https://writerman.hatenablog.jp/entry/2021/12/16/000655

-  AtCoderのテストや提出をVsCode上で自動化する（C++、Python）
https://qiita.com/suupia/items/5910beae3a340536349c

-  VSCodeでの競プロ環境構築 (Julia)
https://zenn.dev/sizk/articles/a755c65474420c

-  atcoder-cli、online-judge-toolsをjavaで環境構築する
https://qiita.com/hario/items/20b78cf56634289f79c1

-  atcoder-cliを導入してみた
https://twoooooda.net/post/introduce-atcoder-cli/

-  atcoder-cli、online-judge-toolsをjavaで環境構築する
https://zenn.dev/polysan/articles/0dd6de3d18ff29

-  AtCoder のディレクトリ作成・サンプルケースのテスト・提出を自動化する。atcoder-cli と online-judge-tools
https://qiita.com/takeaship/items/d0718066922612648eaa

-  Python と VSCode で競プロ - 標準入力の簡易化とサンプルケース判定の自動化 
https://qiita.com/ajim/items/4d350710ba70056f5f6f

-  atcoder-cli チュートリアル
http://tatamo.81.la/blog/2018/12/07/atcoder-cli-tutorial/

- rubyでテンプレート
https://qiita.com/rakudalms/items/c261a6c0cfd588e96abf

- VS Codeの設定をキレイに変数置換【VS Code使い方①】
https://qiita.com/ShortArrow/items/dc0c8cacd696154510f1

- 【VSCode】複数のコマンドを一つのキーで実行したい
https://qiita.com/mh326/items/6e2c3cf262cc1dfccdbe

- Visual Studio Codeでキーボードショートカットに外部コマンドを割り当てる
https://qiita.com/sakano/items/685b6a15dd600ccd34bd