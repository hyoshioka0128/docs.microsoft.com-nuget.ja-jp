---
title: NuGet 3.0 Beta リリース ノート
description: 既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.0 Beta リリース ノートです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819628"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta リリース ノート

[NuGet 3.0 プレビューのリリース ノート](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC のリリース ノートには](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta は、Visual Studio 2015 CTP の 6 リリースの 2015 年 2 月 23 日にリリースされました。 このリリースを意味ずっと私たちのチームを共有するには、アーキテクチャとパフォーマンスの向上の数があるし、ご案内 nuget.org サービスのパフォーマンスの設定のチューニングを開始します。

この新しいバージョンをインストールする前に、NuGet の Visual Studio 2015 の拡張機能のより前のバージョンをアンインストールすることを強くお勧めします。  拡張機能のこのバージョンで問題があれば、ことをお勧めする元に戻す、[以前のバージョン](http://nuget.codeplex.com/downloads/get/909582)Visual Studio 2015 preview で使用するためです。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

この NuGet 3.0 Beta は、Visual Studio 2015 CTP 6 拡張機能ギャラリーにインストールできるようにします。 Visual Studio 2012 および Visual Studio 2013 プレビューのドロップを非常に早く取得に努めています。 目的とした共有していた[for Visual Studio 2010 の更新プログラムを中止](http://blog.nuget.org/20141002/visual-studio-2010.html)、難しい判断するためでした。

## <a name="new-clientserver-api"></a>新しいクライアント/サーバー API

NuGet のクライアント/サーバー プロトコルの実装の詳細お操作しました。 実行した作業は、パッケージをインストールするパッケージの復元など、重要なシナリオの高可用性を軸に設計されている NuGet の"API v3"を作成します。 新しい API は REST に基づいており、Hypermedia と選択[JSON %LD](http://json-ld.org)として、リソース形式。

NuGet 3.0 Beta bits がパッケージ ソースのドロップダウン リストに"api.nuget.org"と呼ばれる新しいパッケージ ソースが表示されます。   そのパッケージのソースを選択すると、nuget.org への接続にではなく、新しい API が使用されます。NuGet 3.0 RC では、この新しい API v3 ベースのパッケージ ソースは v2 ベース"nuget.org"のパッケージ ソースに置き換えます。  すべての他のパブリックのパッケージ ソースを無効にすることを勧めし、としてのみ公開パッケージ リポジトリのみ api.nuget.org のままにします。

V3 API の構築に多くの時間を配置したして、パブリック リポジトリへのアクセスにシークする古いクライアントの標準 v2 API を維持するために続行されます。

## <a name="updated-ui"></a>更新された UI

コンボ ボックスには、パッケージを実行するアクションを選択することが、画面の [オプション] 領域でチェック ボックスをオンに移行して、[プレビュー] ボタンを含めるには、このリリースではユーザー インターフェイスを拡張しました。  [オプション] 領域では、折りたたみが適用されなくし、今すぐ使用可能なオプションを説明するヘルプ リンクを提供します。

![新しい NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>操作のログ記録

モーダル ウィンドウにすばやく表示し、インストールまたはアンインストール中に非表示にログ情報を削除しました。  実際にする情報を参照してください。 またはからコピーして貼り付けることができる場合に、このウィンドウに値が追加されていません。  代わりに、お今すぐをリダイレクトしてすべての出力は、出力ウィンドウの [パッケージ マネージャー] ウィンドウにログを記録します。  これより快適で検査する通常のビルド レポートと同様と思います。


### <a name="focus-on-performance"></a>パフォーマンスを焦点します。

ここには、多数の NuGet 検索、およびフェッチのパフォーマンスを向上させる名前の変更が行われます。  これは、懸案事項、マイクロソフトのお客様からおよび、このリリースで対処しだったことを確認します。  新しい CDN では、構築、サーバーをチューニングおよびできれば関連性を提供するためのロジックに一致するクエリが向上したし、高速のパッケージ検索結果します。

NuGet 3.0 の開発のこのフェーズを続けていくおチューニングとする、改善を配信することを確認する nuget.org サービスを監視します。  おはありません、ダウンタイムに関与する計画を追加してするサービスでリソースを変更します。  注意を続け、 [twitter フィード](http://twitter.com/nuget)詳細については、サービスの構成を変更するときにします。

## <a name="building-nuget-with-nuget"></a>NuGet を使ってビルド NuGet

おが今すぐを再構築し、NuGet クライアント自体は NuGet パッケージに組み込まれているいくつかのコンポーネントにします。 独自のライブラリの再使用正しくをパッケージ化し、再利用可能ななっているコンポーネントを作成することを強制します。  コードの重複を排除し、改善、ソリューション全体でパッケージを作成する必要性をサポートするために、開発プロセスを構成する方法について学習しましたできました。  コード プロジェクトの構造し、ビルド処理のしくみについては話を早く、ブログの投稿を探します。

## <a name="stay-tuned"></a>待ち

くださいに注意[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。