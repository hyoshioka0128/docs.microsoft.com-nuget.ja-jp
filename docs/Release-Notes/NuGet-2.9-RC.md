---
title: "NuGet 2.9 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 04d76a22-63b0-41d1-9c27-799f4b35058f
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.9 RC のリリース ノートします。"
keywords: "NuGet 2.9 RC リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64b4cd17394ddb902c7101b9117039f381dc8488
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="69449-104">NuGet 2.9 RC のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="69449-104">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="69449-105">[NuGet 2.8.7 リリース ノート](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 プレビューのリリース ノート](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="69449-105">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="69449-106">NuGet 2.9 は 2015 年 9 月 10 日を 2.8.7 に更新プログラムとしてリリースされた Visual Studio 2012 および 2013 用の VSIX です。</span><span class="sxs-lookup"><span data-stu-id="69449-106">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="69449-107">このリリースで更新プログラム</span><span class="sxs-lookup"><span data-stu-id="69449-107">Updates in this release</span></span>

* <span data-ttu-id="69449-108">場合、パッケージの処理をスキップしていますので、含まれている`.nuspec`ドキュメント形式が正しくありません - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="69449-108">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="69449-109">Unix または Linux のシナリオ - \r\n の multipartwebrequest 処理を修正[776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="69449-109">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="69449-110">Visual Studio 2013 Community edition - のビルド イベントとの統合を修正[1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="69449-110">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="69449-111">GitHub でのこのリリースで修正プログラムの完全な一覧が見つかりません、 [2.8.8 マイルス トーン](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="69449-111">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>