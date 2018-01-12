---
title: "NuGet 2.6 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d99bbf29-2b9a-4dc5-a823-5eb4f9e30f7f
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 2.6 リリース ノートです。"
keywords: "NuGet 2.6 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b34c0049a5ba42f6bcd5b36fa5b0ba261e27ecd5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-26-release-notes"></a><span data-ttu-id="8afff-104">NuGet 2.6 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="8afff-104">NuGet 2.6 Release Notes</span></span>

<span data-ttu-id="8afff-105">[NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md) | [WebMatrix のリリース ノートについては、NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md)</span><span class="sxs-lookup"><span data-stu-id="8afff-105">[NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md)</span></span>

<span data-ttu-id="8afff-106">NuGet 2.6 は、2013 年 6 月 26 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="8afff-106">NuGet 2.6 was released on June 26, 2013.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="8afff-107">リリースで注目に値する機能</span><span class="sxs-lookup"><span data-stu-id="8afff-107">Notable features in the release</span></span>

### <a name="support-for-visual-studio-2013"></a><span data-ttu-id="8afff-108">Visual Studio 2013 のサポート</span><span class="sxs-lookup"><span data-stu-id="8afff-108">Support for Visual Studio 2013</span></span>

<span data-ttu-id="8afff-109">NuGet 2.6 は、Visual Studio 2013 のサポートを提供する最初のリリースです。</span><span class="sxs-lookup"><span data-stu-id="8afff-109">NuGet 2.6 is the first release that provides support for Visual Studio 2013.</span></span> <span data-ttu-id="8afff-110">および Visual Studio のすべてのエディションの Visual Studio 2012 と同様に、NuGet Package Manager 拡張機能が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8afff-110">And like Visual Studio 2012, the NuGet Package Manager extension is included in every edition of Visual Studio.</span></span>

<span data-ttu-id="8afff-111">まだ Visual Studio 2010 と Visual Studio 2012 の両方をサポートをできるだけ小さく拡張サイズを保持する方法の中に Visual Studio 2013 の最大限のサポートを提供するのには、中に Visual Studio 2013 用の別個の拡張機能を作成する、元の拡張子は、Visual Studio 2010 および 2012 の両方を対象に続行します。</span><span class="sxs-lookup"><span data-stu-id="8afff-111">In order to provide the best possible support for Visual Studio 2013 while still supporting both Visual Studio 2010 and Visual Studio 2012, and keeping the extension sizes as small as possible, we are producing a separate extension for Visual Studio 2013 while the original extension continues to target both Visual Studio 2010 and 2012.</span></span>

<span data-ttu-id="8afff-112">NuGet 2.6 以降では、次に示す 2 つの拡張機能が公開します。</span><span class="sxs-lookup"><span data-stu-id="8afff-112">Starting with NuGet 2.6, we will publish two extensions as below:</span></span>

1. <span data-ttu-id="8afff-113">[NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 および 2012 に適用されます)</span><span class="sxs-lookup"><span data-stu-id="8afff-113">[NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (applies to Visual Studio 2010 and 2012)</span></span>
1. [<span data-ttu-id="8afff-114">Visual Studio 2013 用の NuGet パッケージ マネージャー</span><span class="sxs-lookup"><span data-stu-id="8afff-114">NuGet Package Manager for Visual Studio 2013</span></span>](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

<span data-ttu-id="8afff-115">この分割と、 [nuget.org](https://nuget.org) "NuGet のインストール"ボタンのホーム ページの処理を実行する、 [NuGet をインストールする](../guides/install-nuget.md) ページで、さまざまな NuGet クライアントのインストールに関する詳細についてを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="8afff-115">With this split, the [nuget.org](https://nuget.org) home page's "Install NuGet" button will now take you to the [installing NuGet](../guides/install-nuget.md) page, where you can find more information about installing the different NuGet clients.</span></span>

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a><span data-ttu-id="8afff-116">XDT Web.config 変換のサポート</span><span class="sxs-lookup"><span data-stu-id="8afff-116">XDT Web.config transformation support</span></span>

<span data-ttu-id="8afff-117">Visual Studio のビルド構成の変換で使用されている XDT 変換エンジンを使用してより強力な XML 変換をサポートするために、NuGet クライアントの高から要求された機能の 1 つがされました。</span><span class="sxs-lookup"><span data-stu-id="8afff-117">One of the most highly-requested features for the NuGet client has been to support more powerful XML transformations using the XDT transformation engine which is used in Visual Studio build configuration transformations.</span></span>

<span data-ttu-id="8afff-118">2013 年 4 月、XDT 用の NuGet のサポートに関する 2 つの大規模なお知らせを行いました。</span><span class="sxs-lookup"><span data-stu-id="8afff-118">In April 2013, we made two big announcements regarding NuGet support for XDT.</span></span> <span data-ttu-id="8afff-119">1 つでした XDT ライブラリ自体はされていた自体[NuGet パッケージとしてリリース](https://nuget.org/packages/Microsoft.Web.Xdt)と[CodePlex でのオープン ソース](http://xdt.codeplex.com/)です。</span><span class="sxs-lookup"><span data-stu-id="8afff-119">The first was that the XDT library itself was being itself [released as a NuGet package](https://nuget.org/packages/Microsoft.Web.Xdt) and [open sourced on CodePlex](http://xdt.codeplex.com/).</span></span> <span data-ttu-id="8afff-120">この手順は、NuGet クライアントを含む、他のオープン ソース ソフトウェアで自由に使用する XDT エンジンを有効になります。</span><span class="sxs-lookup"><span data-stu-id="8afff-120">This step enabled the XDT engine to be used freely by other open-source software, including the NuGet client.</span></span> <span data-ttu-id="8afff-121">次のお知らせは、NuGet クライアントでの変換に XDT エンジンの使用をサポートするために、プランをでした。</span><span class="sxs-lookup"><span data-stu-id="8afff-121">The second announcement was the plan to support use of the XDT engine for transformations in the NuGet client.</span></span> <span data-ttu-id="8afff-122">NuGet 2.6 には、この統合が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8afff-122">NuGet 2.6 includes this integration.</span></span>

#### <a name="how-it-works"></a><span data-ttu-id="8afff-123">しくみ</span><span class="sxs-lookup"><span data-stu-id="8afff-123">How it works</span></span>

<span data-ttu-id="8afff-124">NuGet の XDT サポートを利用するしくみについては、検索と同様、[現在の構成変換機能](../create-packages/source-and-config-file-transformations.md)します。</span><span class="sxs-lookup"><span data-stu-id="8afff-124">To take advantage of NuGet’s XDT support, the mechanics look similar to those of the [current config transformation feature](../create-packages/source-and-config-file-transformations.md).</span></span>
<span data-ttu-id="8afff-125">変換ファイルは、パッケージのコンテンツ フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="8afff-125">Transformation files are added to the package’s content folder.</span></span> <span data-ttu-id="8afff-126">ただし、構成の変換は、インストールとアンインストールの両方の 1 つのファイルを使用して、XDT 変換は、次のファイルを使用してこれらのプロセスの両方に対して、きめ細かい制御を有効にします。</span><span class="sxs-lookup"><span data-stu-id="8afff-126">However, while config transformations use a single file for both installation and uninstallation, XDT transformations enable fine-grained control over both of these processes using the following files:</span></span>

- <span data-ttu-id="8afff-127">Web.config.install.xdt</span><span class="sxs-lookup"><span data-stu-id="8afff-127">Web.config.install.xdt</span></span>
- <span data-ttu-id="8afff-128">Web.config.uninstall.xdt</span><span class="sxs-lookup"><span data-stu-id="8afff-128">Web.config.uninstall.xdt</span></span>

<span data-ttu-id="8afff-129">さらに、NuGet はファイルのサフィックスを使用して既存 web.config.transforms を使用してパッケージを正しく動作させるための変換を実行するには、どのエンジンを確認します。</span><span class="sxs-lookup"><span data-stu-id="8afff-129">Additionally, NuGet uses the file suffix to determine which engine to run for transformations, so packages using the existing web.config.transforms will continue to work.</span></span> <span data-ttu-id="8afff-130">XDT 変換は、任意の XML ファイル (だけでなく、web.config ファイル) にも適用できますこのに他のアプリケーション プロジェクトで利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8afff-130">XDT transformations can also be applied to any XML file (not just web.config), so you can leverage this for other applications in your project.</span></span>

#### <a name="what-you-can-do-with-xdt"></a><span data-ttu-id="8afff-131">XDT で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="8afff-131">What you can do with XDT</span></span>

<span data-ttu-id="8afff-132">XDT の大きなメリットの 1 つは、その[簡易かつ強力な構文](http://msdn.microsoft.com/library/dd465326.aspx)XML DOM の構造を操作します。</span><span class="sxs-lookup"><span data-stu-id="8afff-132">One of XDT’s greatest strengths is its [simple but powerful syntax](http://msdn.microsoft.com/library/dd465326.aspx) for manipulating the structure of an XML DOM.</span></span> <span data-ttu-id="8afff-133">別の構造に 1 つの固定のドキュメントの構造を単純にオーバーレイするではなく XDT は一致するさまざまな名前の一致条件を完全な XPath のサポートを単純な属性からの方法で要素のコントロールを提供します。</span><span class="sxs-lookup"><span data-stu-id="8afff-133">Rather than simply overlaying one fixed document structure onto another structure, XDT provides controls for matching elements in a variety of ways, from simple attribute name matching to full XPath support.</span></span> <span data-ttu-id="8afff-134">つまり、追加、更新、または属性の削除、特定の場所に新しい要素を配置することまたは交換または全体を削除するかどうか、XDT が、要素を操作する豊富な一連の関数を提供、一致する要素または要素のセットが見つかると、要素とその子要素です。</span><span class="sxs-lookup"><span data-stu-id="8afff-134">Once a matching element or set of elements is found, XDT provides a rich set of functions for manipulating the elements, whether that means adding, updating, or removing attributes, placing a new element at a specific location, or replacing or removing the entire element and its children.</span></span>

### <a name="machine-wide-configuration"></a><span data-ttu-id="8afff-135">コンピューター全体の構成</span><span class="sxs-lookup"><span data-stu-id="8afff-135">Machine-Wide Configuration</span></span>

<span data-ttu-id="8afff-136">NuGet の優れた長所の 1 つが、それ以外の場合の大きな実行可能ファイルまたはライブラリにできる、統合された最も重要なメンテナンスとバージョン管理された個別にモジュール型のコンポーネントのセットを中断します。</span><span class="sxs-lookup"><span data-stu-id="8afff-136">One of the great strengths of NuGet is that it breaks down an otherwise large executable or library into a set of modular components which can be integrated, and most importantly maintained and versioned independently.</span></span> <span data-ttu-id="8afff-137">これには、副作用の 1 つがの製品または製品ファミリの従来のアイデアがより断片化可能性のあります。</span><span class="sxs-lookup"><span data-stu-id="8afff-137">One side effect of this, however, is that the conventional idea of a product or product family becomes potentially more fragmented.</span></span>
<span data-ttu-id="8afff-138">NuGet のカスタム パッケージのソース機能は、パッケージを整理するための 1 つの方法を提供します。ただし、カスタムのパッケージ ソースは、単独で検出可能ではありません。</span><span class="sxs-lookup"><span data-stu-id="8afff-138">NuGet’s custom package source feature provides one way of organizing packages; however, custom package sources are not discoverable on their own.</span></span>

<span data-ttu-id="8afff-139">NuGet 2.6 では、パス %programdata%/nuget/config 下のフォルダー階層を検索して NuGet を構成するためのロジックを拡張します。製品インストーラーには、自社製品のカスタム パッケージ ソースを登録するには、このフォルダーの下のカスタムの NuGet 構成ファイルを追加できます。</span><span class="sxs-lookup"><span data-stu-id="8afff-139">NuGet 2.6 extends the logic for configuring NuGet by searching the folder hierarchy under the path %ProgramData%/NuGet/Config. Product installers can add custom NuGet configuration files under this folder to register a custom package source for their products.</span></span> <span data-ttu-id="8afff-140">さらに、フォルダー構造は、製品、バージョン、および IDE の偶数の SKU のセマンティクスをサポートします。</span><span class="sxs-lookup"><span data-stu-id="8afff-140">Additionally, the folder structure supports semantics for product, version, and even SKU of the IDE.</span></span> <span data-ttu-id="8afff-141">これらのディレクトリからの設定は、"wins"で最後の優先順位戦略は、次の順序で適用されます。</span><span class="sxs-lookup"><span data-stu-id="8afff-141">Settings from these directories are applied in the following order with a "last in wins" precedence strategy.</span></span>

1. <span data-ttu-id="8afff-142">%ProgramData%\NuGet\Config\*.config</span><span class="sxs-lookup"><span data-stu-id="8afff-142">%ProgramData%\NuGet\Config\*.config</span></span>
2. <span data-ttu-id="8afff-143">%ProgramData%\NuGet\Config\{IDE}\*.config</span><span class="sxs-lookup"><span data-stu-id="8afff-143">%ProgramData%\NuGet\Config\{IDE}\*.config</span></span>
3. <span data-ttu-id="8afff-144">%ProgramData%\NuGet\Config\{IDE}\{バージョン}\*.config</span><span class="sxs-lookup"><span data-stu-id="8afff-144">%ProgramData%\NuGet\Config\{IDE}\{Version}\*.config</span></span>
4. <span data-ttu-id="8afff-145">%ProgramData%\NuGet\Config\{IDE}\{バージョン}\{SKU}\*.config</span><span class="sxs-lookup"><span data-stu-id="8afff-145">%ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config</span></span>

<span data-ttu-id="8afff-146">この一覧で、{IDE} プレース ホルダーは、"VisualStudio"の場合は、Visual Studio できるように、NuGet が実行されている IDE に固有です。</span><span class="sxs-lookup"><span data-stu-id="8afff-146">In this list, the {IDE} placeholder is specific to the IDE in which NuGet is running, so in the case of Visual Studio, it will be "VisualStudio".</span></span> <span data-ttu-id="8afff-147">{バージョン} と {SKU} プレース ホルダーが (たとえば、IDE によって提供されます。「11.0」と"WDExpress"、"VWDExpress"、"Pro"それぞれ)。</span><span class="sxs-lookup"><span data-stu-id="8afff-147">The {Version} and {SKU} placeholders are provided by the IDE (e.g. "11.0" and "WDExpress", "VWDExpress" and "Pro", respectively).</span></span> <span data-ttu-id="8afff-148">フォルダーでは、多くの異なる *.config ファイルを含めることができますし、します。</span><span class="sxs-lookup"><span data-stu-id="8afff-148">The folder can then contain many different *.config files.</span></span>
<span data-ttu-id="8afff-149">したがって、ACME コンポーネント会社の一部として、製品インストーラー、カスタム パッケージ ソースの追加、次のファイル パスを作成して Visual Studio 2012 の Professional、および Ultimate バージョンでのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="8afff-149">Therefore, the ACME component company can, as a part of their product installer, add a custom package source which will be visible only in the Professional and Ultimate versions of Visual Studio 2012 by creating the following file path:</span></span>

<span data-ttu-id="8afff-150">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span><span class="sxs-lookup"><span data-stu-id="8afff-150">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span></span>

<span data-ttu-id="8afff-151">フォルダー構造では、NuGet の構成にコンピューター全体のパッケージ ソースを追加するソフトウェア インストーラーなどのプログラムに簡単です、中に、NuGet の構成ダイアログ ボックスが更新されとしてパッケージ ソースの登録を許可するにはいずれかのユーザー固有 (例: %appdata%/nuget/nuget.config で登録されている) またはコンピューター全体です。</span><span class="sxs-lookup"><span data-stu-id="8afff-151">While the folder structure makes it straightforward for programs like software installers to add machine-wide package sources to NuGet's configuration, the NuGet configuration dialog has also been updated to allow for the registration of package sources as either user-specific (e.g. registered in %AppData%/NuGet/NuGet.Config) or machine-wide.</span></span>

<span data-ttu-id="8afff-152">ファイルがインストールされている Visual Studio 2013 でこの機能を利用するとします。</span><span class="sxs-lookup"><span data-stu-id="8afff-152">This feature is utilized by Visual Studio 2013, where a file is installed at:</span></span>

<span data-ttu-id="8afff-153">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span><span class="sxs-lookup"><span data-stu-id="8afff-153">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span></span>

<span data-ttu-id="8afff-154">このファイルでは「.NET Framework パッケージ」と呼ばれる新しいパッケージ ソースが構成されています。</span><span class="sxs-lookup"><span data-stu-id="8afff-154">Within this file, a new package source called ".NET Framework Packages" is configured.</span></span>

![NuGet Config ファイル マシン全体の設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a><span data-ttu-id="8afff-156">検索を付けた</span><span class="sxs-lookup"><span data-stu-id="8afff-156">Contextualizing Search</span></span>

<span data-ttu-id="8afff-157">NuGet ギャラリーで処理されたパッケージの数が指数のペースで拡大するように NuGet の優先度リストの上部にあることは検索を向上します。</span><span class="sxs-lookup"><span data-stu-id="8afff-157">As the number of packages served by the NuGet gallery continues to grow at an exponential pace, improving search remains ever at the top of the NuGet priority list.</span></span> <span data-ttu-id="8afff-158">NuGet の計画的な機能の 1 つは、コンテキストにより検索、つまり、潜在的な検索の妥当性を決定するための条件として NuGet は、バージョンと SKU の Visual Studio を使用していること、およびビルドするプロジェクトの種類に関する情報を使用結果。</span><span class="sxs-lookup"><span data-stu-id="8afff-158">One of the planned features for NuGet is contextual search, meaning that NuGet will use information about the version and SKU of Visual Studio that you are using and the type of project that you are building as criteria for determining the relevance of potential search results.</span></span>

<span data-ttu-id="8afff-159">NuGet 2.6 以降では、パッケージをインストールするたびに、インストールのコンテキストとして記録されますインストール操作データの一部。</span><span class="sxs-lookup"><span data-stu-id="8afff-159">Starting with NuGet 2.6, each time a package is installed, the context for the installation is recorded as part of the installation operation data.</span></span>  <span data-ttu-id="8afff-160">検索では、コンテキストのインストールの傾向で検索結果を向上させる NuGet ギャラリーで、同じコンテキスト情報も送信します。</span><span class="sxs-lookup"><span data-stu-id="8afff-160">Searches also send the same context information, which will allow the NuGet Gallery to boost search results by contextual installation trends.</span></span>  <span data-ttu-id="8afff-161">NuGet ギャラリーへの今後の更新プログラムは、この状況に応じた関連性の向上を有効になります。</span><span class="sxs-lookup"><span data-stu-id="8afff-161">A future update to the NuGet Gallery will enable this context-sensitive relevance boosting.</span></span>

### <a name="tracking-direct-installs-vs-dependency-installs"></a><span data-ttu-id="8afff-162">Vs の直接インストールを追跡します。依存関係のインストール</span><span class="sxs-lookup"><span data-stu-id="8afff-162">Tracking Direct Installs vs. Dependency Installs</span></span>

<span data-ttu-id="8afff-163">パッケージ作成者は、証明書利用者のより多くの[パッケージ統計](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)NuGet ギャラリーで提供します。</span><span class="sxs-lookup"><span data-stu-id="8afff-163">Package authors are relying more and more on the [Package Statistics](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) provided on the NuGet Gallery.</span></span>  <span data-ttu-id="8afff-164">大量の不足しているデータ ポイントの作成者ご要望を 1 つは、直接パッケージをインストールし、依存関係のインストールとの違いです。</span><span class="sxs-lookup"><span data-stu-id="8afff-164">One significant missing data point that authors have asked for is a differentiation between direct package installs and dependency installs.</span></span>  <span data-ttu-id="8afff-165">これまでは、NuGet クライアントは、開発者が直接パッケージをインストールするかどうか、または依存関係を満たすためにインストールされているかどうかのインストール操作を囲むすべてのコンテキストを送信しませんでした。</span><span class="sxs-lookup"><span data-stu-id="8afff-165">Until now, the NuGet client did not send any context around the installation operation for whether the developer directly installed the package or if it was installed to satisfy a dependency.</span></span>
<span data-ttu-id="8afff-166">データがそのインストール操作の今すぐ送信されることを NuGet 2.6 で開始しています。</span><span class="sxs-lookup"><span data-stu-id="8afff-166">Starting with NuGet 2.6, that data will now be sent for the installation operation.</span></span>  <span data-ttu-id="8afff-167">NuGet ギャラリー パッケージの統計情報がそのデータとして公開する、別のインストール操作で、"-依存関係"サフィックス。</span><span class="sxs-lookup"><span data-stu-id="8afff-167">Package Statistics on the NuGet Gallery will expose that data as separate install operations, with a "-Dependency" suffix.</span></span>

* <span data-ttu-id="8afff-168">インストール</span><span class="sxs-lookup"><span data-stu-id="8afff-168">Install</span></span>
* <span data-ttu-id="8afff-169">依存関係のインストール</span><span class="sxs-lookup"><span data-stu-id="8afff-169">Install-Dependency</span></span>
* <span data-ttu-id="8afff-170">更新</span><span class="sxs-lookup"><span data-stu-id="8afff-170">Update</span></span>
* <span data-ttu-id="8afff-171">依存関係の更新</span><span class="sxs-lookup"><span data-stu-id="8afff-171">Update-Dependency</span></span>
* <span data-ttu-id="8afff-172">再インストール</span><span class="sxs-lookup"><span data-stu-id="8afff-172">Reinstall</span></span>
* <span data-ttu-id="8afff-173">依存関係の再インストール</span><span class="sxs-lookup"><span data-stu-id="8afff-173">Reinstall-Dependency</span></span>

<span data-ttu-id="8afff-174">異なる操作名に加えて、依存パッケージ id をインストールするためにも記録されます。</span><span class="sxs-lookup"><span data-stu-id="8afff-174">In addition to the different operation name, the dependent package id is also recorded for the installation.</span></span>  <span data-ttu-id="8afff-175">NuGet ギャラリーへの今後の更新では、パッケージ作成者は、開発者がそのパッケージをインストールする方法を十分に理解できるように、レポート内でそのデータを公開します。</span><span class="sxs-lookup"><span data-stu-id="8afff-175">A future update to the NuGet Gallery will expose that data within reports, allowing package authors to fully understand how developers are installing their packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="8afff-176">バグ修正</span><span class="sxs-lookup"><span data-stu-id="8afff-176">Bug Fixes</span></span>

<span data-ttu-id="8afff-177">NuGet 2.6 には、いくつかのバグ修正も含まれています。</span><span class="sxs-lookup"><span data-stu-id="8afff-177">NuGet 2.6 also includes several bug fixes.</span></span> <span data-ttu-id="8afff-178">作業の完全な一覧アイテムを固定 NuGet 2.6 にしてください。 ビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。</span><span class="sxs-lookup"><span data-stu-id="8afff-178">For a full list of work items fixed in NuGet 2.6, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>