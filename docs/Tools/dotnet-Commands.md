---
title: "dotNet の NuGet コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Dotnet コマンド ライン インターフェイスを使用して NuGet に関連するコマンドの短いリファレンスです。"
keywords: "dotnet の NuGet コマンド、dotnet パック、dotnet 復元、dotnet nuget ローカル変数、dotnet nuget プッシュ、dotnet nuget の削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d020e62b8bd04c8f4a75756fb30ebcf13ffdb1b3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="d0620-104">dotNet コマンド</span><span class="sxs-lookup"><span data-stu-id="d0620-104">dotNet commands</span></span>

<span data-ttu-id="d0620-105">Windows、Mac OS X、Linux で実行され、DotNet コマンド ライン インターフェイスは、次に示すように不可欠な nuget.exe コマンドの数を提供します。</span><span class="sxs-lookup"><span data-stu-id="d0620-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d0620-106">Dotnet の必要なコマンドを提供、場所、nuget.exe をダウンロードする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d0620-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="d0620-107">[**dotnet パック**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet パッケージに、コードをパックします。</span><span class="sxs-lookup"><span data-stu-id="d0620-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d0620-108">NuGet 4.0 の時点でと同じコードが実行されて`nuget pack`です。</span><span class="sxs-lookup"><span data-stu-id="d0620-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d0620-109">[**dotnet 復元**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 依存関係およびプロジェクトのツールを復元します。</span><span class="sxs-lookup"><span data-stu-id="d0620-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d0620-110">NuGet 4.0 の時点でと同じコードが実行されて`nuget restore`です。</span><span class="sxs-lookup"><span data-stu-id="d0620-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d0620-111">[**dotnet nuget ローカル**](/dotnet/core/tools/dotnet-nuget-locals): http などのローカルの NuGet リソースは、要求を一覧表示をオフまたはキャッシュ、一時的なキャッシュ、またはコンピューター全体のグローバル packages フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="d0620-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="d0620-112">[**dotnet nuget プッシュ**](/dotnet/core/tools/dotnet-nuget-push): サーバーにパッケージをプッシュし、公開、nuget.org、Visual Studio Team Services、または任意のサードパーティ NuGet サーバーに適用します。</span><span class="sxs-lookup"><span data-stu-id="d0620-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="d0620-113">[**dotnet nuget 削除**](/dotnet/core/tools/dotnet-nuget-delete): unlists nuget.org、Visual Studio Team Services、または任意のサードパーティ製 NuGet サーバーに適用できる、サーバーからパッケージを削除するか。</span><span class="sxs-lookup"><span data-stu-id="d0620-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>