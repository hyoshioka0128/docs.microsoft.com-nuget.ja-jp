---
title: "NuGet CLI ローカル コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Nuget.exe [ローカル] コマンドのリファレンス"
keywords: "nuget ローカル変数の参照、[ローカル] コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="1fa9b-104">[ローカル] コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1fa9b-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="1fa9b-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="1fa9b-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="1fa9b-106">消去または http 要求のキャッシュ、パッケージ キャッシュ、および、コンピューター全体のグローバル パッケージ フォルダーなどのローカルの NuGet リソースを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="1fa9b-107">`locals`コマンドを使用してこれらの場所の一覧を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="1fa9b-108">詳細については、次を参照してください。 [NuGet キャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)です。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1fa9b-109">使用方法</span><span class="sxs-lookup"><span data-stu-id="1fa9b-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="1fa9b-110">ここで`<cache>`の 1 つ`all`、 `http-cache`、 `packages-cache`、 `global-packages`、および`temp` *(3.4 以降)*です。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="1fa9b-111">オプション</span><span class="sxs-lookup"><span data-stu-id="1fa9b-111">Options</span></span>

| <span data-ttu-id="1fa9b-112">オプション</span><span class="sxs-lookup"><span data-stu-id="1fa9b-112">Option</span></span> | <span data-ttu-id="1fa9b-113">説明</span><span class="sxs-lookup"><span data-stu-id="1fa9b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1fa9b-114">Clear</span><span class="sxs-lookup"><span data-stu-id="1fa9b-114">Clear</span></span> | <span data-ttu-id="1fa9b-115">指定されたキャッシュをクリアします。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="1fa9b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1fa9b-116">ConfigFile</span></span> | <span data-ttu-id="1fa9b-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1fa9b-118">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1fa9b-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1fa9b-119">ForceEnglishOutput</span></span> | <span data-ttu-id="1fa9b-120">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1fa9b-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="1fa9b-121">Help</span></span> | <span data-ttu-id="1fa9b-122">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1fa9b-123">リスト</span><span class="sxs-lookup"><span data-stu-id="1fa9b-123">List</span></span> | <span data-ttu-id="1fa9b-124">指定されたキャッシュの場所またはを使用すると、すべてのキャッシュの場所を一覧表示*すべて*です。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="1fa9b-125">非対話型</span><span class="sxs-lookup"><span data-stu-id="1fa9b-125">NonInteractive</span></span> | <span data-ttu-id="1fa9b-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1fa9b-127">詳細度</span><span class="sxs-lookup"><span data-stu-id="1fa9b-127">Verbosity</span></span> | <span data-ttu-id="1fa9b-128">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="1fa9b-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1fa9b-129">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1fa9b-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1fa9b-130">例</span><span class="sxs-lookup"><span data-stu-id="1fa9b-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```