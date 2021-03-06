===========================
ソースコード管理リポジトリ
===========================

本プロジェクトでは :term:`Mercurial HG` を使用してソースコードを管理します。



インストール
-------------
.. todo:: hgのインストール方法を記載

コマンドの使い方
-----------------
大まかなコマンドの使い方を記載します。

hg clone [clone元リポジトリ] [clone先ディレクトリ名]
    リポジトリを複製します。clone元となるリポジトリは同一PC上のディレクトリ
    でもよいし、httpやsshプロトコルで指定したリモートサーバー上にあっても
    大丈夫です。cloneを行うとリポジトリは `clone元` を.hg/hgrcに `default`
    として記録します。

hg addr
    hg add と hg remove を同時に行うコマンドです。新しいファイルを追加し、
    削除されたファイルをリポジトリから除外します。このコマンドの実行後は
    登録削除を反映するために hg ci してください。

hg ci
    リポジトリに変更差分を記録します。これをコミットと言います。
    コミットするとリビジョンが一つ増加します。

hg push [push先リポジトリ]
    push先のリポジトリに差分を送信します。push先リポジトリを指定しない
    場合はdefaultを指定したことになります。 `default` が.hg/hgrcに無い場合は
    エラーになります。

    pushしただけでは、送った先のリポジトリはファイルシステム上で最新状態
    にはならないため、送信先リポジトリのあるディレクトリで hg up する必要
    があります。

    もし、push先でもコミットが行われていた場合には、「headが増えるからpush
    できません」というエラーになります。その場合はいちどpullして問題を解決
    してからpushしてください。

hg pull [pull元リポジトリ]
    pull元のリポジトリから差分を取得します。pull元リポジトリを指定しない
    場合はdefaultを指定したことになります。 `default` が.hg/hgrcに無い場合は
    エラーになります。

    pushしただけでは、送った先のリポジトリはファイルシステム上で最新状態
    にはならないため、送信先リポジトリのあるディレクトリで hg up する必要
    があります。

    手元のリポジトリとリモートのリポジトリとの双方でコミットしていた場合、
    headが2つに増えます。この状態で hg up することはできません。この場合
    hg merge して問題を解消してください。

hg up
    リポジトリを最新状態にします。

    headが2つある状態では hg up することはできません。この場合 hg merge
    して問題を解消してください。

hg merge
    分岐したheadを1つに統合します。

    hg mergeを行うと2つのheadの差分がコミット前の状態としてファイルシステム
    上に置かれます。競合(conflict)が発生していなければ、そのまま hg ci
    でコミットを行えばmerge完了です。


tag付けルール
--------------
tag付けはパッケージのリリース時に行います（リリースについて詳しくは
:doc:`develop-cycle` を参照して下さい）。リリースを行うとパッケージの
リリースバージョンが決まり、リリース配布物が作成されます。この時点で例えば
``0.10.3`` リリースであればtagに ``0.10.3`` を付けます。

tag一覧::

    $ hg tags
    tip          453:0e3d67e74ebe
    0.10.0       407:672a6a7bf039
    0.1.0         66:176a2e55a828

tag付け::

    $ hg tag 0.10.3

再度tag一覧を確認::

    $ hg tags
    tip          454:5619c3823753
    0.10.3       453:0e3d67e74ebe
    0.10.0       407:672a6a7bf039
    0.1.0         66:176a2e55a828

``tip`` はsvnなどのHEADと同義で、常に最新のリビジョンを指しているtagです。
0.10.3をタグ付けしたこと自体が差分として記録されたため、tipはリビジョンが
一つ進んでいます。

この差分をpush/pullで同期することで他のリポジトリにもタグ付けが同期されます。

branchルール
--------------

.. todo:: branch作成ルール

