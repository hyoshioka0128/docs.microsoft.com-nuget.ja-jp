---
title: NuGet パッケージの復元 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。
keywords: NuGet パッケージの復元, NuGet パッケージのインストール, パッケージのインストール, パッケージの復元, 依存関係のバージョン, 自動復元の無効化, パッケージのバージョンの制約
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: d5c9c9f571ea25f8877f78c3fba114562d31fcd8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="package-restore"></a><span data-ttu-id="cb9d1-104">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="cb9d1-104">Package Restore</span></span>

<span data-ttu-id="cb9d1-105">開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクト ファイルまたは `packages.config`のいずれかに一覧表示されたすべてのプロジェクトの依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all a project's dependencies as listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="cb9d1-106">Visual Studio では、プロジェクトがビルドされるときに、パッケージを自動的に復元できます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-106">Visual Studio can restore packages automatically when a project is built.</span></span> <span data-ttu-id="cb9d1-107">`dotnet build` および `dotnet run` コマンド (.NET Core 2.0 以降) でも、自動復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-107">The `dotnet build` and `dotnet run` commands (.NET Core 2.0+) also perform an automatic restore.</span></span> <span data-ttu-id="cb9d1-108">また、Visual Studio、`nuget restore`、`dotnet restore`、および Mono の xbuild を利用すると、パッケージをいつでも復元できます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-108">You can also restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="cb9d1-109">パッケージの復元によって、ソース コントロール内にそれらのパッケージを格納しなくても、確実にすべてのプロジェクトの依存関係が使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-109">Package restore makes sure that all a project's dependencies are available without storing those packages in source control.</span></span> <span data-ttu-id="cb9d1-110">パッケージ バイナリを除外するようにリポジトリを構成する方法については、[パッケージとソースの管理](../consume-packages/packages-and-source-control.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-110">See [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries.</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="cb9d1-111">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="cb9d1-111">Package restore overview</span></span>

<span data-ttu-id="cb9d1-112">パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-112">Restoring packages first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="cb9d1-113">パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-global-packages-and-cache-folders.md)からのパッケージの取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-113">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="cb9d1-114">パッケージがキャッシュにない場合、NuGet は有効なすべてのソースからパッケージをダウンロードしようとします (「[Configuring NuGet behavior](Configuring-NuGet-Behavior.md)」(NuGet の動作を構成する) を参照してください。ソースは Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージ ソース]** リストにも表示されます)。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-114">If the package is not in the cache, NuGet then attempts to download the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="cb9d1-115">復元時には、NuGet は、要求に最初に応答するソースのパッケージを使用して、パッケージ ソースの順序を無視します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-115">During restore, NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="cb9d1-116">NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-116">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="cb9d1-117">このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-117">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="cb9d1-118">このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-118">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="cb9d1-119">パッケージの復元は、次の方法でトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-119">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="cb9d1-120">**dotnet CLI**: [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用します。このコマンドは、プロジェクト ファイルに列記されたパッケージを復元します (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-120">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="cb9d1-121">.NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-121">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="cb9d1-122">**パッケージ マネージャー UI (Windows 上の Visual Studio)**: プロジェクトは、テンプレートから作成されとき、およびビルドされたときに自動的に復元されます (ただし、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」で説明するオプションに基づきます)。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-122">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="cb9d1-123">NuGet 4.0 以降では、NET Core SDK ベースのプロジェクトを変更した場合も復元が自動的に発生します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-123">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="cb9d1-124">手動で復元するには、ソリューション エクスプローラーでソリューションを右クリックして、**[NuGet パッケージの復元]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-124">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="cb9d1-125">1 つ以上の個別のパッケージが、まだ適切にインストールされない場合 (ソリューション エクスプローラーにエラー アイコンが表示されます)、パッケージ マネージャー UI を使用して、影響を受けるパッケージをアンインストールし、再インストールします。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-125">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="cb9d1-126">「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-126">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="cb9d1-127">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」の手順に従って、自動復元を有効にしてください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-127">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span> <span data-ttu-id="cb9d1-128">[パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-128">Also see [Package restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="cb9d1-129">**NuGet CLI**: [nuget restore](../tools/cli-ref-restore.md) コマンドを使用します。このコマンドは、プロジェクト ファイルまたは `packages.config`に列記されたパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-129">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file or in `packages.config`.</span></span> <span data-ttu-id="cb9d1-130">ソリューション ファイルを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-130">You can also specify a solution file.</span></span>

- <span data-ttu-id="cb9d1-131">**MSBuild**: [msbuild /t:restore](../reference/msbuild-targets.md#restore-target)コマンドを使用します。このコマンドは、プロジェクト ファイル (PackageReference のみ) に列記されたパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-131">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (PackageReference only).</span></span> <span data-ttu-id="cb9d1-132">NuGet 4.x 以降および MSBuild 15.1 以降でのみ使用できます。これらは、Visual Studio 2017 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-132">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="cb9d1-133">`nuget restore` と `dotnet restore` はどちらも、このコマンドを該当するプロジェクトに使います。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-133">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="cb9d1-134">**Visual Studio Team Services**: Team Services でビルド定義を作成する場合、ビルド タスクの前に、[NuGet の復元](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) タスクまたは [.NET Core の復元](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages)タスクが定義に追加されます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-134">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="cb9d1-135">このタスクは、多くのビルド テンプレートに既定で含まれます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-135">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="cb9d1-136">**Team Foundation Server**: TFS 2013 以降では、TFS 2013 以降用のチーム ビルド テンプレートを使用していれば、ビルド時にパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-136">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="cb9d1-137">以前のバージョンの TFS では、前に説明したように、ビルド ステップを含めるだけでコマンド ラインの復元オプションのいずれかを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-137">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="cb9d1-138">必要に応じて、ビルド テンプレートを TFS 2013 に移行できます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-138">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="cb9d1-139">詳細については、[Team Foundation ビルドでのパッケージの復元](../consume-packages/team-foundation-build.md)に関するチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-139">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="cb9d1-140">パッケージの復元の有効化と無効化</span><span class="sxs-lookup"><span data-stu-id="cb9d1-140">Enabling and disabling package restore</span></span>

<span data-ttu-id="cb9d1-141">パッケージの復元を有効にするには、主に Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を使います。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-141">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![NuGet パッケージ マネージャーのオプションによるパッケージ復元動作の制御](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="cb9d1-143">**見つからないパッケージのダウンロードを NuGet に許可**: 次に示すように、`NuGet.Config` ファイル (Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) の `packageRestore/enabled` の設定を変更することによって、パッケージ復元のすべての形式を制御します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-143">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="cb9d1-144">Visual Studio では、この設定を使用して、ソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドを実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-144">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="cb9d1-145">`packageRestore/enabled` の設定は、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定することにより、グローバルに上書きできます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-145">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="cb9d1-146">**Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: 次に示すように、`NuGet.Config` ファイル (Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-146">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="cb9d1-147">このオプションをオンにして Visual Studio からビルドを実行すると、欠落しているパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-147">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="cb9d1-148">このオプションは、MSBuild を使用してコマンド ラインから実行されるビルドには影響しません。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-148">The option does not affect builds run from the command line using MSBuild.</span></span>

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="cb9d1-149">詳しくは、「NuGet config file」(NuGet config ファイル) の「[packageRestore section](../reference/nuget-config-file.md#packagerestore-section)」(packageRestore セクション) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-149">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="cb9d1-150">開発者や会社が、すべてのユーザーに対して、コンピューターでのパッケージの復元を有効または無効にすることが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-150">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="cb9d1-151">これを行うには、`%ProgramData%\NuGet\Config` (Windows、潜在的に Visual Studio 用の特定の `\{IDE}\{Version}\{SKU}\` フォルダー下にある) または `~/.local/share` (Mac/Linux) に配置されているグローバル NuGet 構成ファイルに上記の同じ設定を追加します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-151">To do this, add the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config` (Windows, potentially under a specific `\{IDE}\{Version}\{SKU}\` folder for Visual Studio) or `~/.local/share` (Mac/Linux).</span></span> <span data-ttu-id="cb9d1-152">その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-152">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="cb9d1-153">NuGet が複数の構成ファイルの優先順位を決定する方法の詳細については、「[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-153">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

> [!Important]
> <span data-ttu-id="cb9d1-154">`nuget.config` の `packageRestore` 設定を直接編集する場合は、オプションのダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-154">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="cb9d1-155">復元でのパッケージのバージョンの制約</span><span class="sxs-lookup"><span data-stu-id="cb9d1-155">Constraining package versions with restore</span></span>

<span data-ttu-id="cb9d1-156">NuGet は、いずれかの方法でパッケージを復元する際、`packages.config`またはプロジェクト ファイルで指定されている制約に従います。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-156">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="cb9d1-157">`packages.config`: 依存関係の `allowedVersion` プロパティでバージョンの範囲を指定します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-157">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="cb9d1-158">「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-158">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="cb9d1-159">例:</span><span class="sxs-lookup"><span data-stu-id="cb9d1-159">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="cb9d1-160">プロジェクト ファイル (PackageReference): 依存関係のバージョン番号でバージョンの範囲を直接指定します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-160">Project file (PackageReference): Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="cb9d1-161">例:</span><span class="sxs-lookup"><span data-stu-id="cb9d1-161">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="cb9d1-162">いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-162">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="forcing-restore-from-package-sources"></a><span data-ttu-id="cb9d1-163">パッケージ ソースから強制的に復元する</span><span class="sxs-lookup"><span data-stu-id="cb9d1-163">Forcing restore from package sources</span></span>

<span data-ttu-id="cb9d1-164">[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、既定では、NuGet の復元操作では、"*グローバル パッケージ*" および "*HTTP キャッシュ*" フォルダーのパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-164">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="cb9d1-165">"*グローバル パッケージ*" フォルダーの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-165">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="cb9d1-166">`nuget locals global-packages -clear` または `dotnet nuget locals global-packages --clear` を使用して、フォルダーをクリアする</span><span class="sxs-lookup"><span data-stu-id="cb9d1-166">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`</span></span>
- <span data-ttu-id="cb9d1-167">次のいずれかの方法を使った復元操作の前に、"*グローバル パッケージ*" フォルダーの場所を一時的に変更する</span><span class="sxs-lookup"><span data-stu-id="cb9d1-167">Temporarily change the location of the *global-packages* folder before the restore operation using one of the following methods:</span></span>
  - <span data-ttu-id="cb9d1-168">NUGET_PACKAGES 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-168">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="cb9d1-169">`globalPackagesFolder` (PackageReference を使用している場合) または `repositoryPath` (`packages.config` を使用している場合) を別のフォルダーに設定した `NuGet.Config` ファイルを作成する ([構成設定](../reference/nuget-config-file.md#config-section)に関するページを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-169">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder (see [configuration settings](../reference/nuget-config-file.md#config-section)</span></span>
  - <span data-ttu-id="cb9d1-170">MSBuild のみ: `RestorePackagesPath` プロパティで別のフォルダーを指定する。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-170">MSBuild only: specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="cb9d1-171">HTTP ソースのキャッシュの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-171">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="cb9d1-172">`nuget restore` で `-NoCache` オプションを使用するか、または `dotnet restore` で `--no-cache` オプションを使用する。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-172">Use the `-NoCache` option with `nuget restore` or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="cb9d1-173">これらのオプションは、Visual Studio パッケージ マネージャーの UI またはコンソールを経由した復元操作には影響しません。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-173">These options do not affect restore operations through the Visual Studio Package Manager UI or Console.</span></span>
- <span data-ttu-id="cb9d1-174">`nuget locals http-cache -clear` または `dotnet nuget locals http-cache --clear` を使用してキャッシュをクリアする。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-174">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="cb9d1-175">一時的に、NUGET_HTTP_CACHE_PATH 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-175">Temporarily set of the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cb9d1-176">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="cb9d1-176">Troubleshooting</span></span>

<span data-ttu-id="cb9d1-177">[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cb9d1-177">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>