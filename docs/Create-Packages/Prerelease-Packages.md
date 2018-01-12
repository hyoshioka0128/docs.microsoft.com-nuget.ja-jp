---
title: "NuGet パッケージのプレリリース版 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df6a366a-22c1-47bb-8017-18231311ce88
description: "プレリリース パッケージのビルド ガイド"
keywords: "バージョン管理, NuGet パッケージ バージョン管理, NuGet プレリリース バージョン, NuGet プレリリース パッケージ, パッケージ バージョンのプレビュー, RC パッケージ バージョン, ベータ パッケージ バージョン, NuGet セマンティック バージョン管理"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07cb9b9bdeeea6f283e95a11a06d7f2043c9b17c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="56df5-104">プレリリース パッケージのビルド</span><span class="sxs-lookup"><span data-stu-id="56df5-104">Building pre-release packages</span></span>

<span data-ttu-id="56df5-105">更新したパッケージを新しいバージョン番号でリリースすると、NuGet はそれを "最新の安定版リリース" として見なし、たとえば、Visual Studio 内のパッケージ マネージャー UI で下記のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="56df5-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![最新の安定版リリースを示すパッケージ マネージャー UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="56df5-107">安定版リリースとは、実稼働環境で使用するだけの信頼性があると見なされるリリースです。</span><span class="sxs-lookup"><span data-stu-id="56df5-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="56df5-108">最新の安定版リリースは、パッケージ更新またはパッケージ復元でインストールされるリリースでもあります (「[Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) の説明にある制約に左右されます)。</span><span class="sxs-lookup"><span data-stu-id="56df5-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="56df5-109">ソフトウェア リリース ライフサイクルをサポートするために、NuGet 1.6 以降では、プレリリース パッケージを配信できます。バージョン番号には、`-alpha`、`-beta`、`-rc` のようなセマンティック バージョン管理サフィックスが含まれます。</span><span class="sxs-lookup"><span data-stu-id="56df5-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="56df5-110">詳細については、「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56df5-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="56df5-111">このようなバージョンは 2 つの方法で指定できます。</span><span class="sxs-lookup"><span data-stu-id="56df5-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="56df5-112">`.nuspec` ファイル: `version` 要素にセマンティック バージョン サフィックスを含めます:</span><span class="sxs-lookup"><span data-stu-id="56df5-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="56df5-113">アセンブリ属性: Visual Studio プロジェクト (`.csproj` または `.vbproj`) からパッケージをビルドするとき、`AssemblyInformationalVersionAttribute` を使用してバージョンを指定します:</span><span class="sxs-lookup"><span data-stu-id="56df5-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="56df5-114">NuGet は、セマンティック バージョン管理に対応していない `AssemblyVersion` 属性に指定されている値ではなく、この値を選択します。</span><span class="sxs-lookup"><span data-stu-id="56df5-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="56df5-115">安定版バージョンをリリースする用意ができたら、サフィックスを削除します。このパッケージはあらゆるプレリリース版に優先します。</span><span class="sxs-lookup"><span data-stu-id="56df5-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="56df5-116">繰り返しになりますが、「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56df5-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>


## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="56df5-117">プレリリース パッケージのインストールと更新</span><span class="sxs-lookup"><span data-stu-id="56df5-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="56df5-118">既定で、NuGet ではパッケージの使用時にプレリリース版を含めませんが、この動作は次のように変更できます。</span><span class="sxs-lookup"><span data-stu-id="56df5-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="56df5-119">**Visual Studio のパッケージ マネージャー UI**: **[NuGet パッケージの管理]** UI で、**[プレリリースを含める]** ボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="56df5-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio の [プレリリースを含める] チェックボックス](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="56df5-121">このボックスをオンまたはオフにするとパッケージ マネージャー UI とインストールできるバージョンの一覧が更新されます。</span><span class="sxs-lookup"><span data-stu-id="56df5-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="56df5-122">**パッケージ マネージャー コンソール**: `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package`、`Update-Package` コマンドで `-IncludePrerelease` スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="56df5-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="56df5-123">「[PowerShell リファレンス](../tools/powershell-reference.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56df5-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="56df5-124">**NuGet CLI**: `install`、`update`、`delete`、`mirror` コマンドで `-prerelease` スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="56df5-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="56df5-125">「[NuGet CLI reference](../tools/nuget-exe-cli-reference.md)」(NuGet CLI リファレンス) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="56df5-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>


## <a name="semantic-versioning"></a><span data-ttu-id="56df5-126">セマンティック バージョン管理</span><span class="sxs-lookup"><span data-stu-id="56df5-126">Semantic versioning</span></span>

<span data-ttu-id="56df5-127">「[Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html)」 (セマンティック バージョン管理または SemVer 規則) では、バージョン番号の文字列を活用し、基礎となっているコードの意味を伝える方法が説明されています。</span><span class="sxs-lookup"><span data-stu-id="56df5-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="56df5-128">この規則では、各バージョンが 3 つの部分、`Major.Minor.Patch` から構成されています。それぞれ次のような意味があります。</span><span class="sxs-lookup"><span data-stu-id="56df5-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="56df5-129">`Major`: 互換性に影響する変更点</span><span class="sxs-lookup"><span data-stu-id="56df5-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="56df5-130">`Minor`: 新機能、ただし下位互換性あり</span><span class="sxs-lookup"><span data-stu-id="56df5-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="56df5-131">`Patch`: 下位互換性のバグ修正のみ</span><span class="sxs-lookup"><span data-stu-id="56df5-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="56df5-132">プレリリース版には、パッチ番号の後にハイフンと文字列が付きます。</span><span class="sxs-lookup"><span data-stu-id="56df5-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="56df5-133">技術的に言えば、ハイフンの後には*あらゆる*文字列を使用できます。それで NuGet はパッケージをプレリリースとして扱います。</span><span class="sxs-lookup"><span data-stu-id="56df5-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="56df5-134">NuGet は該当 UI に完全なバージョン番号を表示します。利用者はその意味を自分で解釈します。</span><span class="sxs-lookup"><span data-stu-id="56df5-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="56df5-135">それを踏まえた上で、次のような認められている命名規則に従うことが一般的に推奨されます。</span><span class="sxs-lookup"><span data-stu-id="56df5-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="56df5-136">`-alpha`: アルファ リリース。一般的に、進行中の製品または実験に使用されます。</span><span class="sxs-lookup"><span data-stu-id="56df5-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="56df5-137">`-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="56df5-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="56df5-138">`-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。</span><span class="sxs-lookup"><span data-stu-id="56df5-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="56df5-139">NuGet は、`1.0.1-build.23` のようにドット付きで表記される、[SemVer 互換 (v2.0.0)](http://semver.org/spec/v2.0.0.html) プレリリース番号に対応していません。</span><span class="sxs-lookup"><span data-stu-id="56df5-139">NuGet does not support [SemVer-compatible (v2.0.0)](http://semver.org/spec/v2.0.0.html) prerelease numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="56df5-140">`1.0.1-build23` のようなフォームを利用できますが、常にプレリリース版と見なされます。</span><span class="sxs-lookup"><span data-stu-id="56df5-140">You can use a form like `1.0.1-build23` but this is always considered a pre-release version.</span></span>

<span data-ttu-id="56df5-141">ただし、どのようなサフィックスを使用する場合でも、NuGet はアルファベットの逆順で優先順序を与えます。</span><span class="sxs-lookup"><span data-stu-id="56df5-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta12
1.0.1-beta05
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
```

<span data-ttu-id="56df5-142">このように、サフィックスのないバージョンは常にプレリリース版に優先します。</span><span class="sxs-lookup"><span data-stu-id="56df5-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="56df5-143">数値のサフィックスとプレリリース タグを使用するとき、番号が 2 桁 (以上) になる場合、beta01 や beta05 のように、先行ゼロを使用してください。それにより、番号が大きくなっても正しく並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="56df5-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>