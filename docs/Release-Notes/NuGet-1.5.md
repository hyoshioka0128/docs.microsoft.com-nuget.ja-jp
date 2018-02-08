---
title: "NuGet 1.5 のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.5 のリリース ノートします。"
keywords: "NuGet 1.5 のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="492e1-104">NuGet 1.5 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="492e1-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="492e1-105">[NuGet 1.4 のリリース ノート](../release-notes/nuget-1.4.md) | [NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="492e1-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="492e1-106">NuGet 1.5 は、2011 年 8 月 30 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="492e1-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="492e1-107">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="492e1-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="492e1-108">プレインストールされた NuGet パッケージとプロジェクト テンプレート</span><span class="sxs-lookup"><span data-stu-id="492e1-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="492e1-109">新しい ASP.NET MVC 3 プロジェクト テンプレートを作成するときにプロジェクトに含まれる jQuery スクリプト ライブラリが実際にによって配置された NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="492e1-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="492e1-110">ASP.NET MVC 3 プロジェクト テンプレートには、一連プロジェクト テンプレートが呼び出されたときにインストールされる NuGet パッケージにはが含まれています。</span><span class="sxs-lookup"><span data-stu-id="492e1-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="492e1-111">プロジェクト テンプレートを使用して NuGet パッケージを含めるには、この機能は、NuGet の機能では今すぐを_任意_プロジェクト テンプレートに得られる利点がようになりました。</span><span class="sxs-lookup"><span data-stu-id="492e1-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="492e1-112">この機能の詳細については、このテキストを読み取る[、機能の開発者がブログの投稿](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="492e1-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="492e1-113">明示的にアセンブリ参照</span><span class="sxs-lookup"><span data-stu-id="492e1-113">Explicit Assembly References</span></span>

<span data-ttu-id="492e1-114">追加された新しい`<references />`内で対象のアセンブリを明示的に指定するための要素、パッケージを参照してください。</span><span class="sxs-lookup"><span data-stu-id="492e1-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="492e1-115">たとえば、次のコードを追加するとします。</span><span class="sxs-lookup"><span data-stu-id="492e1-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="492e1-116">のみ、`xunit.dll`と`xunit.extensions.dll`適切な参照される[framework/プロファイル サブフォルダー](../schema/nuspec.md#explicit-assembly-references)の`lib`フォルダー、フォルダー内に他のアセンブリがある場合でもです。</span><span class="sxs-lookup"><span data-stu-id="492e1-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../schema/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="492e1-117">この要素を省略したかどうかは、内のすべてのアセンブリを参照しているので、通常の動作が適用されます、`lib`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="492e1-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="492e1-118">__この機能で使用されますか。__</span><span class="sxs-lookup"><span data-stu-id="492e1-118">__What is this feature used for?__</span></span>

<span data-ttu-id="492e1-119">この機能は、デザイン時アセンブリのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="492e1-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="492e1-120">たとえば、コード コントラクトを使用する場合、コントラクト アセンブリしなければなりません Visual Studio は、それらを見つけることができますが、コントラクト アセンブリは実際には参照できません、プロジェクトにコピーしてはならないように、補強ランタイム アセンブリの横にあります。`bin`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="492e1-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="492e1-121">同様に、機能は、ランタイムのアセンブリの横にあるが、プロジェクト参照から除外するには、そのツール アセンブリが必要になる XUnit などのユニット テスト フレームワークに使用できます。</span><span class="sxs-lookup"><span data-stu-id="492e1-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="492e1-122">追加の機能で、.nuspec ファイルを除外するには</span><span class="sxs-lookup"><span data-stu-id="492e1-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="492e1-123">`<file>`内の要素、`.nuspec`ファイルを使用して、特定のファイルまたはワイルドカードを使用してファイルのセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="492e1-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="492e1-124">ワイルドカードを使用する場合、含まれているファイルの特定のサブセットを除外する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="492e1-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="492e1-125">たとえば、特定の 1 つを除く、フォルダー内のすべてのテキスト ファイルを必要とします。</span><span class="sxs-lookup"><span data-stu-id="492e1-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="492e1-126">セミコロンを使用すると、複数のファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="492e1-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="492e1-127">または、ワイルドカードを使用して、すべてのバックアップ ファイルなどのファイルのセットを除外するには</span><span class="sxs-lookup"><span data-stu-id="492e1-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="492e1-128">ダイアログ ボックスを使用してパッケージを削除する依存関係を削除するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="492e1-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="492e1-129">NuGet が表示されたら、依存関係を使用してパッケージをアンインストールする場合は、パッケージとパッケージの依存関係の削除を許可します。</span><span class="sxs-lookup"><span data-stu-id="492e1-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![依存パッケージの削除](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="492e1-131">`Get-Package`コマンドの向上</span><span class="sxs-lookup"><span data-stu-id="492e1-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="492e1-132">`Get-Package`コマンドをサポートするようになりました、`-ProjectName`パラメーター。</span><span class="sxs-lookup"><span data-stu-id="492e1-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="492e1-133">したがって、コマンド</span><span class="sxs-lookup"><span data-stu-id="492e1-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="492e1-134">A. をプロジェクトにインストールされているすべてのパッケージが一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="492e1-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="492e1-135">認証を必要とするプロキシのサポート</span><span class="sxs-lookup"><span data-stu-id="492e1-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="492e1-136">NuGet を使用して認証を必要とするプロキシの背後にある、NuGet では、プロキシの資格情報を求められますようになりました。</span><span class="sxs-lookup"><span data-stu-id="492e1-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="492e1-137">リモート リポジトリへの接続に NuGet を使用する資格情報を入力できます。</span><span class="sxs-lookup"><span data-stu-id="492e1-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="492e1-138">認証を必要とするリポジトリのサポート</span><span class="sxs-lookup"><span data-stu-id="492e1-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="492e1-139">NuGet への接続を今すぐサポート[プライベート リポジトリ](../hosting-packages/local-feeds.md)基本認証または NTLM 認証を必要とします。</span><span class="sxs-lookup"><span data-stu-id="492e1-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="492e1-140">ダイジェスト認証のサポートは、将来のリリースで追加されます。</span><span class="sxs-lookup"><span data-stu-id="492e1-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="492e1-141">Nuget.org リポジトリにパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="492e1-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="492e1-142">Nuget.org ギャラリー パッケージを一覧表示して、検索を高速化にいくつかのパフォーマンスが向上をしました。</span><span class="sxs-lookup"><span data-stu-id="492e1-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="492e1-143">ソリューション ダイアログのプロジェクトがフィルター処理</span><span class="sxs-lookup"><span data-stu-id="492e1-143">Solution dialog project filtering</span></span>
<span data-ttu-id="492e1-144">ソリューション レベル ダイアログ ボックスでどのようなプロジェクトをインストールする指示されたときに、選択したパッケージと互換性があるプロジェクトだけ表示されます。</span><span class="sxs-lookup"><span data-stu-id="492e1-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="492e1-145">パッケージのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="492e1-145">Package Release Notes</span></span>
<span data-ttu-id="492e1-146">NuGet パッケージの管理には、リリース ノートのサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="492e1-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="492e1-147">このリリース ノートにのみ表示を表示するときに_更新_パッケージのため、意味がないため、最初のリリースに追加します。</span><span class="sxs-lookup"><span data-stu-id="492e1-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![更新プログラム タブ内のリリース ノート](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="492e1-149">リリース ノートをパッケージに追加するには、新しい使用`<releaseNotes />`NuSpec ファイル内のメタデータの要素。</span><span class="sxs-lookup"><span data-stu-id="492e1-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="492e1-150">.nuspec & ltfiles/&gt;向上</span><span class="sxs-lookup"><span data-stu-id="492e1-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="492e1-151">`.nuspec`ファイルできるようになりました空`<files />`要素は、パッケージのすべてのファイルを含めない nuget.exe が示されます。</span><span class="sxs-lookup"><span data-stu-id="492e1-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="492e1-152">バグ修正</span><span class="sxs-lookup"><span data-stu-id="492e1-152">Bug Fixes</span></span>
<span data-ttu-id="492e1-153">NuGet 1.5 では、作業項目の固定 107 の合計がありました。</span><span class="sxs-lookup"><span data-stu-id="492e1-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="492e1-154">これらの 103 はバグとしてマークされています。</span><span class="sxs-lookup"><span data-stu-id="492e1-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="492e1-155">作業の完全な一覧の項目で修正 NuGet 1.5 では、くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="492e1-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="492e1-156">注目すべきバグ修正:</span><span class="sxs-lookup"><span data-stu-id="492e1-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="492e1-157">[問題 1273](http://nuget.codeplex.com/workitem/1273): 行われた`packages.config`パッケージをアルファベット順に並べ替え、余分な空白を削除してわかりやすい複数のバージョン管理します。</span><span class="sxs-lookup"><span data-stu-id="492e1-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="492e1-158">[問題 844](http://nuget.codeplex.com/workitem/844): バージョン番号を今すぐ正規化ように`Install-Package 1.0`バージョンのパッケージで動作`1.0.0`です。</span><span class="sxs-lookup"><span data-stu-id="492e1-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="492e1-159">[問題 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe を使用してパッケージを作成するときに、`-Version`上書きフラグ、`<version />`要素。</span><span class="sxs-lookup"><span data-stu-id="492e1-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>