---
title: "ローカル NuGet フィードを設定する | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "ローカル ネットワーク上のフォルダーを使用して、NuGet パッケージのローカル フィードを作成する方法"
keywords: "NuGet フィード、NuGet ギャラリー、ローカル パッケージ フィード"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a><span data-ttu-id="ae461-104">ローカル フィード</span><span class="sxs-lookup"><span data-stu-id="ae461-104">Local feeds</span></span>

<span data-ttu-id="ae461-105">ローカル NuGet パッケージのフィードは単に、パッケージを配置するローカル ネットワーク上 (または独自のコンピューターだけ) の階層フォルダー構造です。</span><span class="sxs-lookup"><span data-stu-id="ae461-105">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="ae461-106">これらのフィードは、CLI、パッケージ マネージャー UI、およびパッケージ マネージャー コンソールを使用して、その他すべての NuGet の操作でパッケージ ソースとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="ae461-106">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="ae461-107">ソースを有効にするには、[パッケージ マネージャー UI](../tools/package-manager-ui.md#package-sources) または [`nuget sources`](../tools/cli-ref-sources.md) コマンドを使用して、そのパス名 (`\\myserver\packages` など) をソースの一覧に追加します。</span><span class="sxs-lookup"><span data-stu-id="ae461-107">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="ae461-108">階層フォルダーの構造は、NuGet 3.3 以降でサポートされます。</span><span class="sxs-lookup"><span data-stu-id="ae461-108">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="ae461-109">古いバージョンの NuGet は、パフォーマンスが階層構造よりもはるかに劣る、パッケージを含む 1 つのフォルダーのみを使用します。</span><span class="sxs-lookup"><span data-stu-id="ae461-109">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="ae461-110">階層フォルダーの初期化と維持</span><span class="sxs-lookup"><span data-stu-id="ae461-110">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="ae461-111">階層でバージョン管理されたフォルダー ツリーは、次の一般的な構造になります。</span><span class="sxs-lookup"><span data-stu-id="ae461-111">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="ae461-112">[`nuget add`](../tools/cli-ref-add.md) コマンドを使用してパッケージをフィードにコピーすると、NuGet ではこの構造が自動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="ae461-112">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="ae461-113">`nuget add` コマンドは、一度に 1 つのパッケージを使用して動作します。これは、複数のパッケージを含むフィードを設定するときに、不便な場合があります。</span><span class="sxs-lookup"><span data-stu-id="ae461-113">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="ae461-114">このような場合、[`nuget init`](../tools/cli-ref-init.md) コマンドを使用して、それぞれ個別に `nuget add` を実行するように、フォルダーのすべてのパッケージをフィードにコピーします。</span><span class="sxs-lookup"><span data-stu-id="ae461-114">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="ae461-115">たとえば、次のコマンドでは、すべてのパッケージを `c:\packages` から `\\myserver\packages` の階層ツリーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="ae461-115">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="ae461-116">`add` コマンドのように、`init` では、パッケージの識別子ごとにフォルダーを作成します。各フォルダーには、バージョン番号のフォルダーが含まれ、そこには適切なパッケージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ae461-116">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>