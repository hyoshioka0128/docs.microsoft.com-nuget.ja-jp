---
title: "NuGet project.json ファイルと UWP プロジェクト | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 37caf4d7-dabd-4a78-aad2-7d445f818457
description: "project.json ファイルを使用してユニバーサル Windows プラットフォーム (UWP) プロジェクトで NuGet の依存関係を追跡する方法の説明。"
keywords: "NuGet 依存関係, NuGet および UWP, UWP および project.json, NuGet project.json ファイル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40507e541997cea368052c373a4124d9c4a00a51
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="cb495-104">project.json および UWP</span><span class="sxs-lookup"><span data-stu-id="cb495-104">project.json and UWP</span></span>

<span data-ttu-id="cb495-105">このドキュメントでは、NuGet 3 + (Visual Studio 2015 以降) の機能を採用するパッケージの構造について説明します。</span><span class="sxs-lookup"><span data-stu-id="cb495-105">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="cb495-106">`.nuspec` の `minClientVersion` プロパティを使用して、3.1 に設定することで、ここで説明する機能が必要であることを示すことができます。</span><span class="sxs-lookup"><span data-stu-id="cb495-106">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="cb495-107">既存のパッケージへの UWP サポートの追加</span><span class="sxs-lookup"><span data-stu-id="cb495-107">Adding UWP support to an existing package</span></span>

<span data-ttu-id="cb495-108">既存のパッケージがあり、UWP アプリケーションのサポートを追加する場合、ここで説明するパッケージ化形式を採用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-108">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="cb495-109">説明されている機能が必要で、NuGet クライアントをバージョン 3+ に更新したクライアントでのみ使用する場合に、この形式を採用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-109">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="cb495-110">netcore45 が既にターゲットとなっている</span><span class="sxs-lookup"><span data-stu-id="cb495-110">I already target netcore45</span></span>

<span data-ttu-id="cb495-111">既に `netcore45` がターゲットとなっており、ここに示す機能を利用する必要がない場合は、何もする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-111">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="cb495-112">`netcore45` パッケージは UWP アプリケーションで使用することができます。</span><span class="sxs-lookup"><span data-stu-id="cb495-112">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="cb495-113">Windows 10 固有の API を活用したい</span><span class="sxs-lookup"><span data-stu-id="cb495-113">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="cb495-114">この場合は、パッケージに `uap10.0` ターゲット フレームワーク モニカー (TFM または TxM) を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-114">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="cb495-115">パッケージで新しいフォルダーを作成し、そのフォルダーに、Windows 10 で動作するようにコンパイルされたアセンブリを追加します。</span><span class="sxs-lookup"><span data-stu-id="cb495-115">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="cb495-116">Windows 10 固有の API は必要ないが、新しい .NET 機能が必要であるか netcore45 がまだ存在しない</span><span class="sxs-lookup"><span data-stu-id="cb495-116">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="cb495-117">この場合は、パッケージに `dotnet` TxM を追加します。</span><span class="sxs-lookup"><span data-stu-id="cb495-117">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="cb495-118">他の TxMs とは異なり、`dotnet` ではセキュリティ、外部からのアクセスやプラットフォームは暗黙的に指定されません。</span><span class="sxs-lookup"><span data-stu-id="cb495-118">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="cb495-119">これは、依存関係が動作するプラットフォームでパッケージが動作することを示しています。</span><span class="sxs-lookup"><span data-stu-id="cb495-119">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="cb495-120">`dotnet` TxM でパッケージをビルドする場合、`System.Text` や `System.Xml` など、依存する BCL パッケージを定義する必要があるため、`.nuspec` にはさらに多くの TxM 固有の依存関係が存在する可能性があります。これらの依存関係が動作する場所で、パッケージが動作する場所が定義されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-120">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="cb495-121">依存関係を確認する方法</span><span class="sxs-lookup"><span data-stu-id="cb495-121">How do I find out my dependencies</span></span>

<span data-ttu-id="cb495-122">次のように、リストする依存関係を確認する方法は 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="cb495-122">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="cb495-123">[NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) という**サードパーティ** ツールを使用します。</span><span class="sxs-lookup"><span data-stu-id="cb495-123">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="cb495-124">このツールはプロセスを自動化し、ビルドに依存するパッケージで `.nuspec` ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="cb495-124">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="cb495-125">NuGet パッケージの [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) から入手できます。</span><span class="sxs-lookup"><span data-stu-id="cb495-125">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>
2. <span data-ttu-id="cb495-126">(難しい方法) `ILDasm` を使用して、`.dll` で、実行時に実際に必要となるアセンブリを確認します。</span><span class="sxs-lookup"><span data-stu-id="cb495-126">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="cb495-127">次に、それぞれ元の NuGet パッケージを判別します。</span><span class="sxs-lookup"><span data-stu-id="cb495-127">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="cb495-128">`dotnet` TxM をサポートするパッケージの作成に役立つ機能の詳細については、[`project.json`](../Schema/project-json.md) に関するトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cb495-128">See the [`project.json`](../Schema/project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="cb495-129">パッケージを PCL プロジェクトで動作させる場合は、警告や潜在的な互換性の問題を回避するために、`dotnet` フォルダーを作成することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="cb495-129">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>


## <a name="directory-structure"></a><span data-ttu-id="cb495-130">ディレクトリの構造</span><span class="sxs-lookup"><span data-stu-id="cb495-130">Directory structure</span></span>

<span data-ttu-id="cb495-131">この形式を使用する NuGet パッケージには、次のよく知られているフォルダーとビヘイビアーがあります。</span><span class="sxs-lookup"><span data-stu-id="cb495-131">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="cb495-132">フォルダー</span><span class="sxs-lookup"><span data-stu-id="cb495-132">Folder</span></span> | <span data-ttu-id="cb495-133">ビヘイビアー</span><span class="sxs-lookup"><span data-stu-id="cb495-133">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="cb495-134">ビルド</span><span class="sxs-lookup"><span data-stu-id="cb495-134">Build</span></span> | <span data-ttu-id="cb495-135">このフォルダーには MSBuild ターゲットおよびプロパティ ファイルが含まれ、異なる方法でプロジェクトに統合されますが、それ以外は変わりません。</span><span class="sxs-lookup"><span data-stu-id="cb495-135">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="cb495-136">ツール</span><span class="sxs-lookup"><span data-stu-id="cb495-136">Tools</span></span> | <span data-ttu-id="cb495-137">`install.ps1` および `uninstall.ps1` は実行されません。</span><span class="sxs-lookup"><span data-stu-id="cb495-137">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="cb495-138">`init.ps1` は従来どおり動作します。</span><span class="sxs-lookup"><span data-stu-id="cb495-138">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="cb495-139">Content</span><span class="sxs-lookup"><span data-stu-id="cb495-139">Content</span></span> | <span data-ttu-id="cb495-140">コンテンツは、ユーザーのプロジェクトに自動的にコピーされません。</span><span class="sxs-lookup"><span data-stu-id="cb495-140">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="cb495-141">プロジェクトへのコンテンツの追加サポートは、今後のリリースで予定されています。</span><span class="sxs-lookup"><span data-stu-id="cb495-141">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="cb495-142">Lib</span><span class="sxs-lookup"><span data-stu-id="cb495-142">Lib</span></span> | <span data-ttu-id="cb495-143">多くのパッケージに対して、`lib` は NuGet 2.x の場合と同じように動作しますが、内部で使用できる名前に関するオプションが拡張されており、パッケージを使用する際に正しいサブフォルダーを選択するためのロジックが改善されています。</span><span class="sxs-lookup"><span data-stu-id="cb495-143">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="cb495-144">ただし、`ref` と組み合わせて使用する場合、`lib` フォルダーには、`ref` フォルダーのアセンブリで定義されたセキュリティ、外部からのアクセスを実装するアセンブリが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb495-144">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="cb495-145">参照</span><span class="sxs-lookup"><span data-stu-id="cb495-145">Ref</span></span> | <span data-ttu-id="cb495-146">`ref` は省略可能なフォルダーであり、ここには、コンパイル対象のアプリケーションのパブリック公開領域 (パブリック型とメソッド) を定義する .NET アセンブリが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb495-146">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="cb495-147">このフォルダー内のアセンブリには実装が存在しない可能性があり、単にコンパイラのセキュリティ、外部からのアクセスを定義する場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-147">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="cb495-148">パッケージに `ref` フォルダーがない場合は、`lib` が参照アセンブリと実装アセンブリの両方になります。</span><span class="sxs-lookup"><span data-stu-id="cb495-148">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="cb495-149">runtimes</span><span class="sxs-lookup"><span data-stu-id="cb495-149">Runtimes</span></span> | <span data-ttu-id="cb495-150">`runtimes` は省略可能なフォルダーであり、ここには CPU アーキテクチャや OS 固有またはその他のプラットフォームに依存するバイナリなど、OS 固有のコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb495-150">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |


## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="cb495-151">パッケージ内の MSBuild ターゲットおよびプロパティ ファイル</span><span class="sxs-lookup"><span data-stu-id="cb495-151">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="cb495-152">NuGet パッケージには `.targets` および `.props` ファイルを含めることができます。これらのファイルは、パッケージのインストール先となる MSBuild プロジェクトにインポートされます。</span><span class="sxs-lookup"><span data-stu-id="cb495-152">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="cb495-153">NuGet 2.x では、これは `<Import>` ステートメントを `.csproj` ファイルに挿入することで行われていました。NuGet 3.0 では、特定の "プロジェクトへのインストール" アクションはありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-153">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="cb495-154">代わりに、パッケージの復元プロセスで `[projectname].nuget.props` および `[projectname].NuGet.targets` という 2 つのファイルが記述されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-154">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="cb495-155">MSBuild はこれら 2 つのファイルを検索することを認識しており、プロジェクトのビルド プロセスの開始および終了が近づいたときにこれらのファイルを自動的にインポートします。</span><span class="sxs-lookup"><span data-stu-id="cb495-155">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="cb495-156">これは NuGet 2.x とよく似たビヘイビアーを提供しますが、*この場合、ターゲット/プロパティ ファイルの順序が保証されない*という 1 つの大きな違いがあります。</span><span class="sxs-lookup"><span data-stu-id="cb495-156">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="cb495-157">ただし、MSBuild では、`<Target>` 定義の `BeforeTargets` および `AfterTargets` 属性を使用してターゲットの順序を指定する方法が提供されます (「[Target 要素 (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="cb495-157">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild).</span></span>


## <a name="lib-and-ref"></a><span data-ttu-id="cb495-158">lib および ref</span><span class="sxs-lookup"><span data-stu-id="cb495-158">Lib and Ref</span></span>

<span data-ttu-id="cb495-159">NuGet v3 では、`lib` フォルダーのビヘイビアーに大幅な変更はありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-159">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="cb495-160">ただし、すべてのアセンブリは TxM にちなんだ名前の付いたサブフォルダー内にある必要があり、`lib` フォルダーの直下に配置できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="cb495-160">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="cb495-161">TxM は、パッケージ内の指定された資産の動作対象として想定されるプラットフォームの名前です。</span><span class="sxs-lookup"><span data-stu-id="cb495-161">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="cb495-162">論理的には、ターゲット フレームワーク モニカー (TFM) を拡張したものです。たとえば、`net45`、`net46`、`netcore50`、および `dnxcore50` はすべて TxM の例です (「[Target Frameworks](../Schema/Target-Frameworks.md)」 (ターゲット フレームワーク) を参照)。</span><span class="sxs-lookup"><span data-stu-id="cb495-162">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../Schema/Target-Frameworks.md).</span></span> <span data-ttu-id="cb495-163">TxM は、フレームワーク (TFM) と他のプラットフォーム固有のセキュリティ、外部からのアクセスを表す場合があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-163">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="cb495-164">たとえば、UWP TxM (`uap10.0`) は、.NET のセキュリティ、外部からのアクセスと、UWP アプリケーションの Windows のセキュリティ、外部からのアクセスを表します。</span><span class="sxs-lookup"><span data-stu-id="cb495-164">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="cb495-165">lib 構造の例を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="cb495-165">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="cb495-166">`lib` フォルダーには、実行時に使用されるアセンブリが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb495-166">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="cb495-167">ほとんどのパッケージでは、各ターゲット TxM の `lib` の下のフォルダーはすべて必要になります。</span><span class="sxs-lookup"><span data-stu-id="cb495-167">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="cb495-168">参照</span><span class="sxs-lookup"><span data-stu-id="cb495-168">Ref</span></span>

<span data-ttu-id="cb495-169">場合によっては、コンパイル時に異なるアセンブリを使用する必要があります (現時点では、.NET 参照アセンブリでこれを行います)。</span><span class="sxs-lookup"><span data-stu-id="cb495-169">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="cb495-170">このような場合は、`ref` ("参照アセンブリ" の省略形) と呼ばれるトップ レベルのフォルダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="cb495-170">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="cb495-171">ほとんどのパッケージの作成者には `ref` フォルダーは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-171">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="cb495-172">これは、コンパイルや IntelliSense のために一貫性のあるセキュリティ、外部からのアクセスを提供する必要があるものの、TxM ごとに実装が異なるパッケージの場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="cb495-172">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="cb495-173">この最大のユース ケースは、NuGet における .NET Core の配布の一環として生成される `System.*` パッケージです。</span><span class="sxs-lookup"><span data-stu-id="cb495-173">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="cb495-174">これらのパッケージには、一貫性のある ref アセンブリ セットで統合されているさまざまな実装があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-174">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="cb495-175">機械的に、`ref` フォルダーに含まれるアセンブリはコンパイラに渡される参照アセンブリとなります。</span><span class="sxs-lookup"><span data-stu-id="cb495-175">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="cb495-176">csc.exe を使用している場合、これらは [C# /reference オプション](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) スイッチに渡されるアセンブリとなります。</span><span class="sxs-lookup"><span data-stu-id="cb495-176">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="cb495-177">`ref` フォルダーの構造は `lib` と同じです。たとえば、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cb495-177">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll


<span data-ttu-id="cb495-178">この例では、`ref` ディレクトリ内のアセンブリはすべて同じになります。</span><span class="sxs-lookup"><span data-stu-id="cb495-178">In this example the assemblies in the `ref` directories would all be identical.</span></span>


## <a name="runtimes"></a><span data-ttu-id="cb495-179">runtimes</span><span class="sxs-lookup"><span data-stu-id="cb495-179">Runtimes</span></span>

<span data-ttu-id="cb495-180">runtimes フォルダーには、通常はオペレーティング システムおよび CPU アーキテクチャで定義される、特定の "ランタイム" で実行するために必要なアセンブリとネイティブ ライブラリが含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb495-180">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="cb495-181">これらのランタイムは、`win`、`win-x86`、`win7-x86`、`win8-64` などの[ランタイム識別子 (RID)](https://docs.microsoft.com/dotnet/core/rid-catalog) を使用して識別されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-181">These runtimes are identified using [Runtime Identifiers (RIDs)](https://docs.microsoft.com/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="cb495-182">ネイティブの特徴</span><span class="sxs-lookup"><span data-stu-id="cb495-182">Native light-up</span></span>

<span data-ttu-id="cb495-183">次の例では、いくつかのプラットフォームの単なるマネージされた実装を持つものの、Windows 8 固有のネイティブ API を呼び出すことができる Windows 8 のネイティブ ヘルパーを使用するパッケージを示します。</span><span class="sxs-lookup"><span data-stu-id="cb495-183">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="cb495-184">上記のパッケージを指定する場合、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cb495-184">Given the above package the following things happen:</span></span>

- <span data-ttu-id="cb495-185">Windows 8 でない場合は、`lib/net40/MyLibrary.dll` アセンブリが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-185">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="cb495-186">Windows 8 の場合は、`runtimes/win8-<architecture>/lib/MyLibrary.dll` が使用され、`native/MyNativeHelper.dll` がビルドの出力にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="cb495-186">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="cb495-187">上記の例では、`lib/net40` アセンブリは単なるマネージ コードであるのに対して、runtimes フォルダー内のアセンブリはネイティブ ヘルパー アセンブリの p/invoke を行って Windows 8 固有の API を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="cb495-187">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="cb495-188">これまでは単一の `lib` フォルダーのみが選択されているため、ランタイム固有のフォルダーがある場合は、非ランタイム固有の `lib` より優先されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-188">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it is chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="cb495-189">ネイティブ フォルダーが付加的なものであり、存在する場合はビルドの出力にコピーされます。</span><span class="sxs-lookup"><span data-stu-id="cb495-189">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="cb495-190">マネージ ラッパー</span><span class="sxs-lookup"><span data-stu-id="cb495-190">Managed wrapper</span></span>

<span data-ttu-id="cb495-191">ランタイムを使用するもう 1 つの方法として、ネイティブ アセンブリではなく、単なるマネージ ラッパーであるパッケージを配布する方法があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-191">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="cb495-192">このシナリオでは、次のようにパッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="cb495-192">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="cb495-193">この場合、対応するネイティブ アセンブリに依存しないこのパッケージの実装がない限り、トップレベルの `lib` フォルダーはありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-193">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="cb495-194">マネージ アセンブリ `MyLibrary.dll` がこれらの両方のケースでまったく同じであった場合は、トップレベルの `lib` フォルダーに配置することはできます。ただし、win-x86 または win-x64 ではないプラットフォームにインストールされた場合、ネイティブ アセンブリがないとパッケージのインストールに失敗するため、トップレベルの lib は使用されますが、ネイティブ アセンブリはコピーされません。</span><span class="sxs-lookup"><span data-stu-id="cb495-194">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>


## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="cb495-195">NuGet 2 および NuGet 3 のパッケージの作成</span><span class="sxs-lookup"><span data-stu-id="cb495-195">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="cb495-196">`packages.config` を使用するプロジェクトで利用できるパッケージと、`project.json` を使用するパッケージを作成する場合は、以下が適用されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-196">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="cb495-197">ref と runtimes は NuGet 3 のみで動作します。</span><span class="sxs-lookup"><span data-stu-id="cb495-197">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="cb495-198">NuGet 2 では両方とも無視されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-198">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="cb495-199">`install.ps1` や `uninstall.ps1` に依存して機能させることはできません。</span><span class="sxs-lookup"><span data-stu-id="cb495-199">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="cb495-200">これらのファイルは `packages.config` を使用する場合は実行されますが、`project.json` では無視されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-200">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="cb495-201">したがって、実行せずにパッケージを使用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-201">So your package needs to be usable without them running.</span></span> <span data-ttu-id="cb495-202">`init.ps1` は NuGet 3 で引き続き実行されます。</span><span class="sxs-lookup"><span data-stu-id="cb495-202">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="cb495-203">ターゲットとプロパティのインストールは異なるため、両方のクライアントでパッケージが予期したとおりに動作することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="cb495-203">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="cb495-204">NuGet 3 では、lib のサブディレクトリは TxM である必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-204">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="cb495-205">`lib` フォルダーのルートにライブラリを配置することはできません。</span><span class="sxs-lookup"><span data-stu-id="cb495-205">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="cb495-206">NuGet 3 では、コンテンツは自動的にコピーされません。</span><span class="sxs-lookup"><span data-stu-id="cb495-206">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="cb495-207">パッケージのコンシューマーはファイル自体をコピーするか、タスク ランナーなどのツールを使用して、ファイルのコピーを自動化できます。</span><span class="sxs-lookup"><span data-stu-id="cb495-207">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="cb495-208">NuGet 3 では、ソースと構成ファイルの変換は実行されません。</span><span class="sxs-lookup"><span data-stu-id="cb495-208">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="cb495-209">NuGet 2 と 3 をサポートする場合、`minClientVersion` は、パッケージが動作する最も古いバージョンの NuGet 2 クライアントである必要があります。</span><span class="sxs-lookup"><span data-stu-id="cb495-209">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="cb495-210">既存のパッケージの場合は、変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="cb495-210">In the case of an existing package it shouldn't need to change.</span></span>