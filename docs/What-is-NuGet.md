---
title: NuGet とは何か。またどのような働きをするのか | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/10/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: NuGet とは何で、どのような働きをするのかについて、総合的に紹介します
keywords: NuGet パッケージ マネージャー, 消費量, パッケージの作成, パッケージのホスト, .NET パッケージ, .NET Core パッケージ
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d2094177f919d27b9a8320e60c8d1d75ec18fb6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="an-introduction-to-nuget"></a><span data-ttu-id="3eba2-105">NuGet の概要</span><span class="sxs-lookup"><span data-stu-id="3eba2-105">An introduction to NuGet</span></span>

<span data-ttu-id="3eba2-106">最新の開発プラットフォームに欠かせないツールは、開発者が役に立つコードを作成、共有、および使用するために利用できるメカニズムです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-106">An essential tool for any modern development platform is a mechanism through which developers can create, share, and consume useful code.</span></span> <span data-ttu-id="3eba2-107">多くの場合、このようなコードは "パッケージ" にバンドルされています。このパッケージにはコンパイルされたコード (DLL) に加えて、このパッケージが使用されるプロジェクトで必要なその他のコンテンツが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-107">Often such code is bundled into "packages" that contain compiled code (as DLLs) along with other content needed in the projects that consume these packages.</span></span>

<span data-ttu-id="3eba2-108">Microsoft がサポートする.NET (.NET Core を含む) のコード共有メカニズムである **NuGet** では、.NET 用のパッケージを作成、ホスト、および使用する方法が定義されており、それらの各ロール用のツールが提供されています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-108">For .NET (including .NET Core), the Microsoft-supported mechanism for sharing code is **NuGet**, which defines how packages for .NET are created, hosted, and consumed, and provides the tools for each of those roles.</span></span>

<span data-ttu-id="3eba2-109">つまり、NuGet パッケージは、拡張子が `.nupkg` の 1 つの ZIP ファイルであり、コンパイル済みのコード (DLL)、そのコードに関連する他のファイル、パッケージのバージョン番号などの情報が記述されているマニフェストが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-109">Put simply, a NuGet package is a single ZIP file with the `.nupkg` extension that contains compiled code (DLLs), other files related to that code, and a descriptive manifest that includes information like the package's version number.</span></span> <span data-ttu-id="3eba2-110">開発者はコードを共有して、パッケージを作成し、それをパブリック ホストまたはプライベート ホストに公開します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-110">Developers with code to share create packages and publish them to a public or private host.</span></span> <span data-ttu-id="3eba2-111">パッケージ利用者は、これらのパッケージを適切なホストから取得して、プロジェクトに追加した後、プロジェクトのコードでパッケージの機能を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-111">Package consumers obtain those packages from suitable hosts, add them to their projects, and then call a package's functionality in their project code.</span></span> <span data-ttu-id="3eba2-112">その過程での細部はすべて NuGet 自体が処理します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-112">NuGet itself then handles all of the intermediate details.</span></span>

<span data-ttu-id="3eba2-113">NuGet では、パブリック ホストの nuget.org に加えてプライベート ホストもサポートされるので、NuGet パッケージを使用して、組織またはワーク グループ専用のコードを共有できます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-113">Because NuGet supports private hosts alongside the public nuget.org host, you can use NuGet packages to share code that's exclusive to an organization or a work group.</span></span> <span data-ttu-id="3eba2-114">また、自身のプロジェクト以外では使用されない専用のコードを格納するための便利な方法として、NuGet パッケージを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-114">You can also use NuGet packages as a convenient way to factor your own code for use in nothing but your own projects.</span></span> <span data-ttu-id="3eba2-115">要するに、NuGet パッケージは共有可能なコード単位ですが、特定の共有手段を必要とすることも、暗黙に指定することもありません。</span><span class="sxs-lookup"><span data-stu-id="3eba2-115">In short, a NuGet package is a shareable unit of code, but does not require nor imply any particular means of sharing.</span></span>

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a><span data-ttu-id="3eba2-116">作成者、ホスト、利用者の間のパッケージのフロー</span><span class="sxs-lookup"><span data-stu-id="3eba2-116">The flow of packages between creators, hosts, and consumers</span></span>

<span data-ttu-id="3eba2-117">パブリック ホストとしての役割の NuGet は、100,000 以上の個別パッケージの中央リポジトリを [nuget.org](https://www.nuget.org) で保持します。これらのパッケージを、毎日数百万人の .NET/.NET Core 開発者が使用しています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-117">In its role as a public host, NuGet itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). These packages are employed by millions of .NET/.NET Core developers every day.</span></span> <span data-ttu-id="3eba2-118">また、NuGet を使用すると、クラウド (Visual Studio Team Services 上など)、プライベート ネットワーク、さらにはローカル ファイル システムで、プライベートにパッケージをホストすることもできます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-118">NuGet also enables you to host packages privately in the cloud (such as on Visual Studio Team Services), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="3eba2-119">こうすることにより、これらのパッケージは、ホストにアクセスできる開発者のみが使用できるようになるので、パッケージを特定の利用者グループに対して利用可能にすることができます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-119">By doing so, those packages are available to only those developers that have access to the host, giving you the ability to make packages available to a specific group of consumers.</span></span> <span data-ttu-id="3eba2-120">オプションの説明については、「[Hosting your own NuGet feeds](hosting-packages/overview.md)」(独自の NuGet フィードのホスト) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-120">The options are explained on [Hosting your own NuGet feeds](hosting-packages/overview.md).</span></span> <span data-ttu-id="3eba2-121">さらに、構成オプションを使用して、指定されたコンピューターがアクセス可能なホストを厳密に制御して、パッケージが、nuget.org などのパブリック リポジトリではなく特定のソースから取得されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-121">Through configuration options, you can also control exactly which hosts can be accessed by any given computer, thereby ensuring that packages are obtained from specific sources rather than a public repository like nuget.org.</span></span>

<span data-ttu-id="3eba2-122">ホストは、それがどのような性質であっても、パッケージ*作成者*とパッケージ*利用者* の間の接続ポイントとして機能します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-122">Whatever its nature, a host serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="3eba2-123">作成者は、便利な NuGet パッケージを作成して、ホストに公開します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-123">Creators build useful NuGet packages and publish them to a host.</span></span> <span data-ttu-id="3eba2-124">利用者は、アクセスできるホストで役に立ち互換性のあるパッケージを検索し、ダウンロードしてプロジェクトに組み込みます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-124">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="3eba2-125">プロジェクトにインストールされたパッケージの API は、プロジェクト コードの他の部分から利用できます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-125">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![パッケージ作成者、パッケージ ホスト、パッケージ利用者の間の関係](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a><span data-ttu-id="3eba2-127">互換性を目的とするパッケージ</span><span class="sxs-lookup"><span data-stu-id="3eba2-127">Package targeting compatibility</span></span>

<span data-ttu-id="3eba2-128">"互換性のある" パッケージとは、パッケージを利用するプロジェクトのターゲット フレームワークと互換性のある少なくとも 1 つの .NET Framework 用にビルドされたアセンブリが含まれていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-128">A "compatible" package means that it contains assemblies built for at least one target .NET framework that's compatible with the consuming project's target framework.</span></span> <span data-ttu-id="3eba2-129">開発者は、UWP コントロールと同様、1 つのフレームワークに固有のパッケージを作成することも、広範囲のターゲットをサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-129">Developers can create packages that are specific to one framework, as with UWP controls, or they can support a wider range of targets.</span></span> <span data-ttu-id="3eba2-130">パッケージの互換性を最大化するには、開発者は、すべての .NET および .NET Core プロジェクトで利用可能な [.NET Standard](/dotnet/standard/net-standard) をターゲットにします。</span><span class="sxs-lookup"><span data-stu-id="3eba2-130">To maximize a package's compatibility, developers target [.NET Standard](/dotnet/standard/net-standard), which all .NET and .NET Core projects can consume.</span></span> <span data-ttu-id="3eba2-131">この場合、単一のパッケージ (通常、単一のアセンブリを含む) が、パッケージを利用するすべてのプロジェクトに対して機能するので、作成者と利用者の両方にとって最も効率的な手段です。</span><span class="sxs-lookup"><span data-stu-id="3eba2-131">This is the most efficient means for both creators and consumers, as a single package (usually containing a single assembly) works for all consuming projects.</span></span>

<span data-ttu-id="3eba2-132">一方、.NET Standard 以外の API を必要とするパッケージ開発者は、サポートするさまざまなターゲット フレームワーク用に個別のアセンブリを作成し、これらのすべてのアセンブリを同じパッケージに含めます (これは、「マルチターゲット」と呼ばれています)。</span><span class="sxs-lookup"><span data-stu-id="3eba2-132">Package developers who require APIs outside of .NET Standard, on the other hand, create separate assemblies for the different target frameworks they want to support and include all of those assemblies in the same package (which is called "multi-targeting").</span></span> <span data-ttu-id="3eba2-133">利用者がこのようなパッケージをインストールすると、NuGet では、プロジェクトで必要されるアセンブリのみが抽出されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-133">When a consumer installs such a package, NuGet extracts only those assemblies that are needed by the project.</span></span> <span data-ttu-id="3eba2-134">これにより、最終的なアプリケーションやそのプロジェクトによって生成されるアセンブリでのパッケージのフットプリントが最小になります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-134">This minimizes the package's footprint in the final application and/or assemblies produced by that project.</span></span> <span data-ttu-id="3eba2-135">当然、作成者にとっては、マルチターゲット パッケージを保守する方が困難です。</span><span class="sxs-lookup"><span data-stu-id="3eba2-135">A multi-targeting package is, of course, more difficult for its creator to maintain.</span></span>

> [!Note]
> <span data-ttu-id="3eba2-136">.NET Standard をターゲットにする方法は、さまざまなポータブル クラス ライブラリ (PCL) ターゲットを使用する以前の方法よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-136">Targeting .NET Standard supercedes the previous approach of using various portable class library (PCL) targets.</span></span> <span data-ttu-id="3eba2-137">このため、このドキュメントでは、.NET Standard 用のパッケージの作成に重点を置いて説明します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-137">This documentation therefore focuses on creating packages for .NET Standard.</span></span>

## <a name="nuget-tools"></a><span data-ttu-id="3eba2-138">NuGet のツール</span><span class="sxs-lookup"><span data-stu-id="3eba2-138">NuGet tools</span></span>

<span data-ttu-id="3eba2-139">ホストのサポートに加えて、NuGet では作成者と利用者の両方が使用できるさまざまなツールも提供されています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-139">In addition to hosting support, NuGet also provides a variety of tools used by both creators and consumers.</span></span> <span data-ttu-id="3eba2-140">特定のツールの取得方法については、「[NuGet クライアント ツールのインストール](install-nuget-client-tools.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-140">See [Installing NuGet client tools](install-nuget-client-tools.md) for how to obtain specific tools.</span></span>

| <span data-ttu-id="3eba2-141">ツール</span><span class="sxs-lookup"><span data-stu-id="3eba2-141">Tool</span></span> | <span data-ttu-id="3eba2-142">プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="3eba2-142">Platforms</span></span> | <span data-ttu-id="3eba2-143">該当シナリオ</span><span class="sxs-lookup"><span data-stu-id="3eba2-143">Applicable Scenarios</span></span> | <span data-ttu-id="3eba2-144">説明</span><span class="sxs-lookup"><span data-stu-id="3eba2-144">Description</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="3eba2-145">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="3eba2-145">nuget.exe CLI</span></span>](tools/nuget-exe-cli-reference.md) | <span data-ttu-id="3eba2-146">すべて</span><span class="sxs-lookup"><span data-stu-id="3eba2-146">All</span></span> | <span data-ttu-id="3eba2-147">作成、利用</span><span class="sxs-lookup"><span data-stu-id="3eba2-147">Creation, Consumption</span></span> | <span data-ttu-id="3eba2-148">NuGet のすべての機能を提供します。パッケージ作成者のみに適用されるコマンド、利用者のみに適用されるもの、両方に適用されるものがあります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-148">Provides all NuGet capabilities, with some commands applying specifically to package creators, some applying only to consumers, and others applying to both.</span></span> <span data-ttu-id="3eba2-149">たとえば、パッケージ作成者は `nuget pack` コマンドを使用して、さまざまなアセンブリと関連ファイルからパッケージを作成し、パッケージ利用者は `nuget install` を使用して、パッケージをプロジェクトフォルダーに格納します。また、`nuget config` は、NuGet の構成変数を設定するためにすべてのユーザーによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-149">For example, package creators use the `nuget pack` command to create a package from various assemblies and related files, package consumers use `nuget install` to include packages in a project folder, and everyone uses `nuget config` to set NuGet configuration variables.</span></span> <span data-ttu-id="3eba2-150">プラットフォームに依存しないツールである NuGet CLI は、Visual Studio プロジェクトと対話しません。</span><span class="sxs-lookup"><span data-stu-id="3eba2-150">As a platform-agnostic tool, the NuGet CLI does not interact with Visual Studio projects.</span></span> |
| [<span data-ttu-id="3eba2-151">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="3eba2-151">dotnet CLI</span></span>](tools/dotnet-Commands.md) | <span data-ttu-id="3eba2-152">すべて</span><span class="sxs-lookup"><span data-stu-id="3eba2-152">All</span></span> | <span data-ttu-id="3eba2-153">作成、利用</span><span class="sxs-lookup"><span data-stu-id="3eba2-153">Creation, Consumption</span></span> | <span data-ttu-id="3eba2-154">特定の NuGet CLI 機能を、.NET Core ツール チェーン内に直接提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-154">Provides certain NuGet CLI capabilities directly within the .NET Core tool chain.</span></span> <span data-ttu-id="3eba2-155">NuGet CLI と同様、dotnet CLI も Visual Studio プロジェクトと対話しません。</span><span class="sxs-lookup"><span data-stu-id="3eba2-155">As with the NuGet CLI, the dotnet CLI does not interact with Visual Studio projects.</span></span> |
| [<span data-ttu-id="3eba2-156">パッケージ マネージャー コンソール</span><span class="sxs-lookup"><span data-stu-id="3eba2-156">Package Manager Console</span></span>](tools/package-manager-console.md) | <span data-ttu-id="3eba2-157">Windows の Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3eba2-157">Visual Studio on Windows</span></span> | <span data-ttu-id="3eba2-158">利用</span><span class="sxs-lookup"><span data-stu-id="3eba2-158">Consumption</span></span> | <span data-ttu-id="3eba2-159">Visual Studio プロジェクトでパッケージをインストールして管理するための [PowerShell コマンド](tools/Powershell-Reference.md)を提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-159">Provides [PowerShell commands](tools/Powershell-Reference.md) for installing and managing packages in Visual Studio projects.</span></span> |
| [<span data-ttu-id="3eba2-160">パッケージ マネージャー UI</span><span class="sxs-lookup"><span data-stu-id="3eba2-160">Package Manager UI</span></span>](tools/package-manager-ui.md) | <span data-ttu-id="3eba2-161">Windows の Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3eba2-161">Visual Studio on Windows</span></span> | <span data-ttu-id="3eba2-162">利用</span><span class="sxs-lookup"><span data-stu-id="3eba2-162">Consumption</span></span> | <span data-ttu-id="3eba2-163">Visual Studio プロジェクトでパッケージをインストールして管理するための使いやすい UI を提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-163">Provides an easy-to-use UI for installing and managing packages in Visual Studio projects.</span></span> |
| [<span data-ttu-id="3eba2-164">NuGet 管理 UI</span><span class="sxs-lookup"><span data-stu-id="3eba2-164">Manage NuGet UI</span></span>](/visualstudio/mac/nuget-walkthrough) | <span data-ttu-id="3eba2-165">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="3eba2-165">Visual Studio for Mac</span></span> | <span data-ttu-id="3eba2-166">利用</span><span class="sxs-lookup"><span data-stu-id="3eba2-166">Consumption</span></span> | <span data-ttu-id="3eba2-167">Visual Studio for Mac プロジェクトでパッケージをインストールして管理するための使いやすい UI を提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-167">Provide an easy-to-use UI for installing and managing packages in Visual Studio for Mac projects.</span></span> |
| [<span data-ttu-id="3eba2-168">MSBuild</span><span class="sxs-lookup"><span data-stu-id="3eba2-168">MSBuild</span></span>](reference/msbuild-targets.md) | <span data-ttu-id="3eba2-169">Windows</span><span class="sxs-lookup"><span data-stu-id="3eba2-169">Windows</span></span> | <span data-ttu-id="3eba2-170">作成、利用</span><span class="sxs-lookup"><span data-stu-id="3eba2-170">Creation, Consumption</span></span> | <span data-ttu-id="3eba2-171">パッケージを作成する機能と、プロジェクトで使用されているパッケージを、MSBuild ツール チェーンを介して直接復元する機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-171">Provides the ability to create packages and restore packages used in a project directly through the MSBuild tool chain.</span></span> |

<span data-ttu-id="3eba2-172">このように、どの NuGet ツールを使用するかは、パッケージの作成、利用、公開のいずれを行うか、およびどのプラットフォームで作業しているかによって大きく異なります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-172">As you can see, the NuGet tools you work with depend greatly on whether you're creating, consuming, or publishing packages, and the platform on which you're working.</span></span> <span data-ttu-id="3eba2-173">パッケージ作成者は、通常、他の NuGet パッケージの機能を基にして開発を行うので、利用者でもあります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-173">Package creators are typically also consumers, as they build on top of functionality that exists in other NuGet packages.</span></span> <span data-ttu-id="3eba2-174">そして、これらのパッケージは、もちろん、他のパッケージにさらに依存している場合があります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-174">And those packages, of course, may in turn depend on still others.</span></span>

<span data-ttu-id="3eba2-175">詳細については、「[パッケージ作成ワークフロー](create-packages/Overview-and-Workflow.md)」 および [パッケージ利用のワークフロー](consume-packages/Overview-and-Workflow.md)」の記事を最初にお読みください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-175">For more information, start with the [Package creation workflow](create-packages/Overview-and-Workflow.md) and [Package consumption workflow](consume-packages/Overview-and-Workflow.md) articles.</span></span>

## <a name="managing-dependencies"></a><span data-ttu-id="3eba2-176">依存関係の管理</span><span class="sxs-lookup"><span data-stu-id="3eba2-176">Managing dependencies</span></span>

<span data-ttu-id="3eba2-177">他の開発者の作業を簡単に利用できることは、パッケージ管理システムの最も強力な機能の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-177">The ability to easily build on the work of others is one of most powerful features of a package management system.</span></span> <span data-ttu-id="3eba2-178">したがって、NuGet の機能の多くは、プロジェクトに代わって、その依存関係ツリーつまり "グラフ" を管理することです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-178">Accordingly, much of what NuGet does is managing that dependency tree or "graph" on behalf of a project.</span></span> <span data-ttu-id="3eba2-179">簡単に言えば、開発者が関心を持つ必要があるのは、プロジェクト内で直接使っているパッケージだけです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-179">Simply said, you need only concern yourself with those packages that you're directly using in a project.</span></span> <span data-ttu-id="3eba2-180">そのようなパッケージ自体のいずれかで他のパッケージ (それがさらに他のパッケージを利用している場合があります) が利用されている場合、下位の依存関係はすべて NuGet で処理されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-180">If any of those packages themselves consume other packages (which can, in turn, consume still others), NuGet takes care of all those down-level dependencies.</span></span>

<span data-ttu-id="3eba2-181">次の図で示すプロジェクトは、5 つのパッケージに依存しており、それらがさらに他の複数のパッケージに依存しています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-181">The following image shows a project that depends on five packages, which in turn depend on a number of others.</span></span>

![.NET プロジェクトの NuGet 依存関係グラフの例](media/dependency-graph.png)

<span data-ttu-id="3eba2-183">依存関係グラフの複数の箇所に出現しているパッケージがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-183">Notice that some packages appear multiple times in the dependency graph.</span></span> <span data-ttu-id="3eba2-184">たとえば、パッケージ B には 3 つの異なるコンシューマーがあり、各コンシューマーがそのパッケージの異なるバージョンを指定している可能性もあります (図には示されていません)。</span><span class="sxs-lookup"><span data-stu-id="3eba2-184">For example, there are three different consumers of package B, and each consumer might also specify a different version for that package (not shown).</span></span> <span data-ttu-id="3eba2-185">特に広く使用されているパッケージの場合、これはよくあることです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-185">This is a common occurrence, especially for widely-used packages.</span></span> <span data-ttu-id="3eba2-186">さいわいなことに、すべての利用者の要求を満たすパッケージ B のバージョンを正確に特定する困難な作業はすべて、NuGet によって実行されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-186">NuGet fortunately does all the hard work to determine exactly which version of package B satisfies all consumers.</span></span> <span data-ttu-id="3eba2-187">その後、NuGet は、依存関係グラフの深さに関係なく、他のすべてのパッケージについても同じように処理します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-187">NuGet then does the same for all other packages, no matter how deep the dependency graph.</span></span>

<span data-ttu-id="3eba2-188">NuGet がこのサービスを実行する方法について詳しくは、[依存関係の解決](consume-packages/dependency-resolution.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-188">For more details on how NuGet performs this service, see [Dependency resolution](consume-packages/dependency-resolution.md).</span></span>

## <a name="tracking-references-and-restoring-packages"></a><span data-ttu-id="3eba2-189">参照の追跡とパッケージの復元</span><span class="sxs-lookup"><span data-stu-id="3eba2-189">Tracking references and restoring packages</span></span>

<span data-ttu-id="3eba2-190">プロジェクトは開発者のコンピューター、ソース管理リポジトリ、ビルド サーバーなどの間を簡単に移動するので、プロジェクトに直接バインドされた NuGet パッケージからバイナリ アセンブリを維持するのは極めて困難です。</span><span class="sxs-lookup"><span data-stu-id="3eba2-190">Because projects can easily move between developer computers, source control repositories, build servers, and so forth, it's highly impractical to keep the binary assemblies of NuGet packages directly bound to a project.</span></span> <span data-ttu-id="3eba2-191">プロジェクトの各コピーが必要以上に肥大化する (それにより、ソース管理リポジトリ内の領域を浪費する) だけでなく、</span><span class="sxs-lookup"><span data-stu-id="3eba2-191">Doing so would make each copy of the project unnecessarily bloated (and thereby waste space in source control repositories).</span></span> <span data-ttu-id="3eba2-192">パッケージのバイナリを新しいバージョンに更新する処理も、プロジェクトのすべてのコピーについて行う必要があるため、非常に困難になります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-192">It would also make it very difficult to update package binaries to newer versions as updates would have to be applied across all copies of the project.</span></span>

<span data-ttu-id="3eba2-193">代わりに、NuGet は、最上位と下位の依存関係を含めて、プロジェクトが依存する、単純なパッケージの参照リストを保持します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-193">NuGet instead maintains a simple reference list of the packages upon which a project depends, including both top-level and down-level dependencies.</span></span> <span data-ttu-id="3eba2-194">つまり、どこかのホストからプロジェクトにパッケージをインストールすると常に、NuGet によってパッケージの識別子とバージョン番号がこの参照リストに記録されます </span><span class="sxs-lookup"><span data-stu-id="3eba2-194">That is, whenever you install a package from some host into a project, NuGet records the package identifier and version number in the reference list.</span></span> <span data-ttu-id="3eba2-195">(もちろん、パッケージをアンインストールするとリストから削除されます)。その後、「[パッケージの復元](consume-packages/package-restore.md)」で説明しているように、NuGet は、参照されているすべてのパッケージを復元する手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-195">(Uninstalling a package, of course, removes it from the list.) NuGet then provides a means to restore all referenced packages upon request, as described on [Package restore](consume-packages/package-restore.md).</span></span>

![NuGet の参照リストはパッケージのインストール時に作成され、別の場所にパッケージを復元するために使うことができる](media/nuget-restore.png)

<span data-ttu-id="3eba2-197">それ以降いつでも、NuGet は、参照リストのみを使って、パブリック ホストやプライベート ホストからすべてのパッケージを再インストール、&mdash;つまり*復元*&mdash;できます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-197">With only the reference list, NuGet can then reinstall&mdash;that is, *restore*&mdash;all of those packages from public and/or private hosts at any later time.</span></span> <span data-ttu-id="3eba2-198">ソース管理にプロジェクトをコミットするとき、またはプロジェクトを他のなんらかの方法で共有する場合は、参照リストを含めるだけで済み、パッケージのバイナリを含める必要はありません (「[パッケージとソース管理](consume-packages/packages-and-source-control.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="3eba2-198">When committing a project to source control, or sharing it in some other way, you include only the reference list and exclude any package binaries (see [Packages and source control](consume-packages/packages-and-source-control.md).)</span></span>

<span data-ttu-id="3eba2-199">自動展開システムの一部としてプロジェクトのコピーを取得するビルド サーバーのような、プロジェクトを受け取るコンピューターは、必要なときに依存関係を復元するよう NuGet に要求するだけです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-199">The computer that receives a project, such as a build server obtaining a copy of the project as part of an automated deployment system, simply asks NuGet to restore dependencies whenever they're needed.</span></span> <span data-ttu-id="3eba2-200">Visual Studio Team Services などのビルド システムでは、この目的のための "NuGet 復元" ステップが提供されています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-200">Build systems like Visual Studio Team Services provide "NuGet restore" steps for this exact purpose.</span></span> <span data-ttu-id="3eba2-201">同様に、開発者は、プロジェクトのコピーを取得する場合 (リポジトリを複製するときと同じように)、`nuget restore` (NuGet CLI)、`dotnet restore` (dotnet CLI)、または `Install-Package` (パッケージ マネージャー コンソール) などのコマンドを呼び出して、すべての必要なパッケージを取得できます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-201">Similarly, when developers obtain a copy of a project (as when cloning a repository), they can invoke command like `nuget restore` (NuGet CLI), `dotnet restore` (dotnet CLI), or `Install-Package` (Package Manager Console) to obtain all the necessary packages.</span></span> <span data-ttu-id="3eba2-202">この部分については、Visual Studio では、プロジェクトを構築するときに自動的にパッケージを復元します (「ただし、「[パッケージの復元](consume-packages/package-restore.md)」で説明されているように、自動復元が有効になっていることが条件です)。</span><span class="sxs-lookup"><span data-stu-id="3eba2-202">Visual Studio, for its part, automatically restores packages when building a project (provided that automatic restore is enabled, as described on [Package restore](consume-packages/package-restore.md)).</span></span>

<span data-ttu-id="3eba2-203">その場合に開発者が関係する NuGet の主要な役割は明らかに、プロジェクトに代わってその参照リストを維持し、参照されているパッケージを効率的に復元 (および更新) する手段を提供することです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-203">Clearly, then, NuGet's primary role where developers are concerned is maintaining that reference list on behalf of your project and providing the means to efficiently restore (and update) those referenced packages.</span></span> <span data-ttu-id="3eba2-204">このリストは、次の 2 つの*パッケージ管理形式*のいずれかで保持されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-204">This list is maintained in one of two *package management formats*, as they're called:</span></span>

- <span data-ttu-id="3eba2-205">[`packages.config`](reference/packages-config.md): *(NuGet 1.0 以降)* プロジェクト内のすべての依存関係のフラット リストを保持する XML ファイルです。インストールされている他のパッケージの依存関係も含みます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-205">[`packages.config`](reference/packages-config.md): *(NuGet 1.0+)* An XML file that maintains a flat list of all dependencies in the project, including the dependencies of other installed packages.</span></span> <span data-ttu-id="3eba2-206">インストールまたは復元されたパッケージは、`packages` フォルダーに保管されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-206">Installed or restored packages are stored in a `packages` folder.</span></span>

- <span data-ttu-id="3eba2-207">[PackageReference](consume-packages/package-references-in-project-files.md) (または "プロジェクト ファイルでのパッケージ参照") | *(NuGet 4.0 以降)*プロジェクトの最上位の依存関係のリストがプロジェクト ファイル内に直接保持されるので、個別のファイルは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="3eba2-207">[PackageReference](consume-packages/package-references-in-project-files.md) (or "package references in project files") | *(NuGet 4.0+)* Maintains a list of a project's top-level dependencies directly within the project file, so no separate file is needed.</span></span> <span data-ttu-id="3eba2-208">関連するファイル `obj/project.assets.json` は、プロジェクトがすべての下位レベルの依存関係と共に使用するパッケージの依存関係の全体グラフを管理するために、動的に作成されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-208">An associated file, `obj/project.assets.json`, is dynamically generated to manage the overall dependency graph of the packages that a project uses along with all down-level dependencies.</span></span> <span data-ttu-id="3eba2-209">PackageReference は常に、.NET Core プロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-209">PackageReference is always used by .NET Core projects.</span></span>

<span data-ttu-id="3eba2-210">指定されたプロジェクトでどのパッケージ管理形式が採用されるかは、プロジェクトの種類と、NuGet (および Visual Studio) の使用可能なバージョンによって異なります。</span><span class="sxs-lookup"><span data-stu-id="3eba2-210">Which package management format is employed in any given project depends on the project type, and the available version of NuGet (and/or Visual Studio).</span></span> <span data-ttu-id="3eba2-211">使用されている形式を確認するには、最初のパッケージをインストールした後で、プロジェクトのルートにある `packages.config` を調べるだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-211">To check what format is being used, simply look for `packages.config` in the project root after installing your first package.</span></span> <span data-ttu-id="3eba2-212">そのファイルが見つからない場合は、プロジェクト ファイルで直接 \<PackageReference\> 要素を調べます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-212">If you don't have that file, look in the project file directly for a \<PackageReference\> element.</span></span>

<span data-ttu-id="3eba2-213">いくつかの選択肢がある場合は、PackageReference を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3eba2-213">When you have a choice, we recommend using PackageReference.</span></span> <span data-ttu-id="3eba2-214">`packages.config` はレガシを目的として保持され、アクティブな開発からは除外されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-214">`packages.config` is maintained for legacy purposes and is no longer under active development.</span></span>

> [!Tip]
> <span data-ttu-id="3eba2-215">`nuget install` などのさまざまな `nuget.exe` CLI コマンドが、パッケージを参照リストに自動追加することはありません。</span><span class="sxs-lookup"><span data-stu-id="3eba2-215">Various `nuget.exe` CLI commands, like `nuget install`, do not automatically add the package to the reference list.</span></span> <span data-ttu-id="3eba2-216">リストは、Visual Studio パッケージ マネージャー (UI またはコンソール) でパッケージをインストールしたとき、また、`dotnet.exe` CLI によって、更新されます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-216">The list is updated when installing a package with the Visual Studio Package Manager (UI or Console), and with `dotnet.exe` CLI.</span></span>

## <a name="what-else-does-nuget-do"></a><span data-ttu-id="3eba2-217">NuGet の他の機能</span><span class="sxs-lookup"><span data-stu-id="3eba2-217">What else does NuGet do?</span></span>

<span data-ttu-id="3eba2-218">これまで、NuGet の次の特性について説明しました。</span><span class="sxs-lookup"><span data-stu-id="3eba2-218">So far you've learned the following characteristics of NuGet:</span></span>

- <span data-ttu-id="3eba2-219">NuGet は、中央リポジトリ nuget.org を提供し、プライベート ホスティングをサポートします。</span><span class="sxs-lookup"><span data-stu-id="3eba2-219">NuGet provides the central nuget.org repository with support for private hosting.</span></span>
- <span data-ttu-id="3eba2-220">NuGet は、開発者がパッケージの作成、公開、使用に必要なツールを提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-220">NuGet provides the tools developers need for creating, publishing, and consuming packages.</span></span>
- <span data-ttu-id="3eba2-221">最も重要な特性として、NuGet は、プロジェクトで使用されるパッケージの参照リストを保持し、そのリストからパッケージを復元および更新できます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-221">Most importantly, NuGet maintains a reference list of packages used in a project and the ability to restore and update those packages from that list.</span></span>

<span data-ttu-id="3eba2-222">これらの処理を効率的に実行するため、NuGet はバックグラウンドでいくつかの最適化を行います。</span><span class="sxs-lookup"><span data-stu-id="3eba2-222">To make these processes work efficiently, NuGet does some behind-the-scenes optimizations.</span></span> <span data-ttu-id="3eba2-223">注目すべき点は、NuGet ではパッケージ キャッシュとグローバル パッケージ フォルダーを管理して、インストールおよび再インストールを省略することです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-223">Most notably, NuGet manages a package cache and a global packages folder to shortcut installation and reinstallation.</span></span> <span data-ttu-id="3eba2-224">キャッシュは、コンピューターに既にインストールされているパッケージのダウンロードを回避します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-224">The cache avoids downloading a package that's already been installed on the machine.</span></span> <span data-ttu-id="3eba2-225">グローバル パッケージ フォルダーは、インストールされている同じパッケージを複数のプロジェクトで共有できるようにし、それによりコンピューター上の NuGet のフット プリント全体を減らします。</span><span class="sxs-lookup"><span data-stu-id="3eba2-225">The global packages folder allows multiple projects to share the same installed package, thereby reducing NuGet's overall footprint on the computer.</span></span> <span data-ttu-id="3eba2-226">また、キャッシュおよびグローバル パッケージ フォルダーは、ビルド サーバーなどのように多数のパッケージを頻繁に復元する場合は非常に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-226">The cache and global packages folder are also very helpful when you're frequently restoring a larger number of packages, as on a build server.</span></span> <span data-ttu-id="3eba2-227">これらのメカニズムの詳細については、「[Managing the global packages and cache folders](consume-packages/managing-the-global-packages-and-cache-folders.md)」 (グローバル パッケージおよびキャッシュ フォルダーを管理する) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-227">For more details on these mechanisms, see [Managing the global packages and cache folders](consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="3eba2-228">個々のプロジェクトでは、NuGet は依存関係グラフ全体を管理します。これにも、同じパッケージの異なるバージョンへの複数の参照の解決が含まれます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-228">Within an individual project, NuGet manages the overall dependency graph, which again includes resolving multiple references to different versions of the same package.</span></span> <span data-ttu-id="3eba2-229">プロジェクトが 1 つ以上のパッケージに依存関係を持ち、それらのパッケージ自体にも同じような依存関係があることは、ごく一般的なことです。</span><span class="sxs-lookup"><span data-stu-id="3eba2-229">It's quite common that a project takes a dependency on one or more packages that themselves have the same dependencies.</span></span> <span data-ttu-id="3eba2-230">nuget.org の最も便利なユーティリティ パッケージのいくつかは、他の多くのパッケージで使用されています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-230">Some of the most useful utility packages on nuget.org are employed by many other packages.</span></span> <span data-ttu-id="3eba2-231">依存関係グラフ全体では、同じパッケージの異なるバージョンに対する 10 個の異なる参照が簡単にできてしまいます。</span><span class="sxs-lookup"><span data-stu-id="3eba2-231">In the entire dependency graph, then, you could easily have ten different references to different versions of the same package.</span></span> <span data-ttu-id="3eba2-232">そのパッケージの複数のバージョンがアプリケーション自体に組み込まれるのを回避するために、NuGet は、すべての利用者が使用できる 1 つのバージョンを選別します </span><span class="sxs-lookup"><span data-stu-id="3eba2-232">To avoid bringing multiple versions of that package into the application itself, NuGet sorts out which single version can be used by all consumers.</span></span> <span data-ttu-id="3eba2-233">(詳細については、「[依存関係の解決](consume-packages/dependency-resolution.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="3eba2-233">(For more information, see [Dependency Resolution](consume-packages/dependency-resolution.md).)</span></span>

<span data-ttu-id="3eba2-234">さらに、NuGet は、パッケージの構成方法 ([ローカライズ](create-packages/creating-localized-packages.md)と[デバッグ シンボル](create-packages/symbol-packages.md)を含みます) およびパッケージの参照方法 ([バージョン参照](reference/package-versioning.md#version-ranges-and-wildcards)と[プレリリース バージョン](create-packages/prerelease-packages.md)を含みます) に関するすべての仕様を保持しています。NuGet は、そのサービスとプログラムで連携する各種の API を提供し、Visual Studio 拡張機能およびプロジェクト テンプレートを作成する開発者用のサポートも提供します。</span><span class="sxs-lookup"><span data-stu-id="3eba2-234">Beyond that, NuGet maintains all the specifications related to how packages are structured (including [localization](create-packages/creating-localized-packages.md) and [debug symbols](create-packages/symbol-packages.md)) and how they are referenced (including [version ranges](reference/package-versioning.md#version-ranges-and-wildcards) and [pre-release versions](create-packages/prerelease-packages.md).) NuGet also provides various APIs to work with its services programmatically, and provides support for developers who write Visual Studio extensions and project templates.</span></span>

<span data-ttu-id="3eba2-235">このドキュメントの目次を見るとわかるように、これらすべての機能に関するトピックと、最初の NuGet からのすべてのリリース ノートが提供されています。</span><span class="sxs-lookup"><span data-stu-id="3eba2-235">Take a moment to browse the table of contents for this documentation, and you see all of these capabilities represented there, along with release notes dating back to NuGet's beginnings.</span></span>

## <a name="comments-contributions-and-issues"></a><span data-ttu-id="3eba2-236">コメント、投稿、問題</span><span class="sxs-lookup"><span data-stu-id="3eba2-236">Comments, contributions, and issues</span></span>

<span data-ttu-id="3eba2-237">最後に、このドキュメントに関するコメントや投稿をお寄せください。&mdash;各ページの上部にある **[ご意見ご感想]** および **[編集]** コマンドを選択するか、GitHub の[ドキュメント リポジトリ](https://github.com/NuGet/docs.microsoft.com-nuget/)および[ドキュメント問題リスト](https://github.com/NuGet/docs.microsoft.com-nuget/issues)にアクセスしてください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-237">Finally, we very much welcome comments and contributions to this documentation&mdash;just select the **Feedback** and **Edit** commands on the top of any page, or visit the [docs repository](https://github.com/NuGet/docs.microsoft.com-nuget/) and [docs issue list](https://github.com/NuGet/docs.microsoft.com-nuget/issues) on GitHub.</span></span>

<span data-ttu-id="3eba2-238">また、[さまざまな GitHub リポジトリ](https://github.com/NuGet/Home)から NuGet 自体への投稿も歓迎します。NuGet の問題については、[https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-238">We also welcome contributions to NuGet itself through its [various GitHub repositories](https://github.com/NuGet/Home); NuGet issues can be found on [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).</span></span>

<span data-ttu-id="3eba2-239">NuGet のエクスペリエンスをお楽しみください。</span><span class="sxs-lookup"><span data-stu-id="3eba2-239">Enjoy your NuGet experience!</span></span>