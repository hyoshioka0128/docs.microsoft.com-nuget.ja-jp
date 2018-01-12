---
title: "NuGet パッケージの公開方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "NuGet パッケージを nuget.org やプライベート フィードに公開する方法と nuget.org でパッケージ所有権を管理する方法に関する詳細。"
keywords: "NuGet パッケージ公開, NuGet パッケージを公開する, NuGet パッケージ所有権, nuget.org に公開する, プライベート NuGet フィード"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a><span data-ttu-id="32a28-104">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="32a28-104">Publishing packages</span></span>

<span data-ttu-id="32a28-105">`nuget pack` で[パッケージを作成](../create-packages/creating-a-package.md)したら、簡単な手順を踏むだけで他の開発者に利用してもらうことができます。公開と非公開を選択できます。</span><span class="sxs-lookup"><span data-stu-id="32a28-105">Once you have [created a package](../create-packages/creating-a-package.md) with `nuget pack`, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="32a28-106">公開パッケージの場合、このトピックで説明するように、[nuget.org](https://www.nuget.org/packages/manage/upload) 経由で世界中の開発者が利用できます。</span><span class="sxs-lookup"><span data-stu-id="32a28-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="32a28-107">非公開パッケージの場合、ファイル共有、プライベート NuGet サーバー、 [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish)、あるいは myget、ProGet、Nexus Repository、Artifactory のようなサードパーティ リポジトリで保存することで、チームや組織だけが利用できます。</span><span class="sxs-lookup"><span data-stu-id="32a28-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="32a28-108">詳細については、「[Hosting Packages Overview](../hosting-packages/overview.md)」 (パッケージ ホストの概要) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32a28-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="32a28-109">このトピックでは、nuget.org に公開する方法を採り上げます。Visual Studio Team Services に公開する方法については、「[Package Management](https://www.visualstudio.com/docs/package/nuget/publish)」 (パッケージ管理) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="32a28-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="32a28-110">nuget.org に公開する</span><span class="sxs-lookup"><span data-stu-id="32a28-110">Publish to nuget.org</span></span>

<span data-ttu-id="32a28-111">nuget.org の場合、最初に[無料アカウントを作成する](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)必要があります。登録済みの場合、サインインしてください。</span><span class="sxs-lookup"><span data-stu-id="32a28-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![NuGet 登録とサインインの場所](media/publish_NuGetSignIn.png)

<span data-ttu-id="32a28-113">次に、nuget.org Web ポータルからパッケージをアップロードするか、コマンド ラインから nuget.org にプッシュするか、次のセクションで説明するように、Visual Studio Team Services から CI/CD プロセスの一部として公開できます。</span><span class="sxs-lookup"><span data-stu-id="32a28-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line, or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="32a28-114">Web ポータル: nuget.org の [Upload Package ] タブを使用する:</span><span class="sxs-lookup"><span data-stu-id="32a28-114">Web portal: use the Upload Package tab on nuget.org:</span></span>

![NuGet Package Manager でパッケージをアップロードする](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="32a28-116">コマンド ライン:</span><span class="sxs-lookup"><span data-stu-id="32a28-116">Command line:</span></span>
> [!Important]
> <span data-ttu-id="32a28-117">nuget.org にパッケージをプッシュするには、[nuget.exe v4.1.0 以降](https://www.nuget.org/downloads)を使用する必要があります。これは必須の [NuGet プロトコル](../api/nuget-protocols.md)を実装します。</span><span class="sxs-lookup"><span data-stu-id="32a28-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="32a28-118">ユーザー名をクリックし、アカウント設定に移動します。</span><span class="sxs-lookup"><span data-stu-id="32a28-118">Click on your user name to navigate to your account settings.</span></span>
2. <span data-ttu-id="32a28-119">**[API キー]** の下で、**[クリップボードにコピー]** をクリックし、CLI で必要となるアクセス キーを取得します。</span><span class="sxs-lookup"><span data-stu-id="32a28-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you'll need in the CLI:</span></span>

    ![アカウント設定から API キーをコピーする](media/publish_APIKey.png)

3. <span data-ttu-id="32a28-121">コマンド プロンプトで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="32a28-121">At a command prompt, run the following command:</span></span>

    ```
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="32a28-122">この操作により、コンピューターに API キーが格納されます。同じコンピューターでこの手順を繰り返す必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="32a28-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

4. <span data-ttu-id="32a28-123">コマンドを利用し、NuGet ギャラリーにパッケージをプッシュする:</span><span class="sxs-lookup"><span data-stu-id="32a28-123">Push your package to NuGet Gallery using the command:</span></span>

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. <span data-ttu-id="32a28-124">一般公開前に、nuget.org にアップロードされたすべてのパッケージはウイルス スキャンが行われ、見つかった場合、拒否されます。</span><span class="sxs-lookup"><span data-stu-id="32a28-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="32a28-125">nuget.org の一覧にあるすべてのパッケージも定期的にスキャンされます。</span><span class="sxs-lookup"><span data-stu-id="32a28-125">All packages listed on nuget.org are also scanned periodically.</span></span>

6. <span data-ttu-id="32a28-126">nuget.org のアカウントで、**[Manage my packages]** をクリックし、公開したパッケージを確認します。また、確認の電子メールが届きます。</span><span class="sxs-lookup"><span data-stu-id="32a28-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you'll also receive a confirmation email.</span></span> <span data-ttu-id="32a28-127">パッケージにインデックスが付けられ、検索結果に表示されるようになり、他のユーザーが検索可能になるまで時間がかかることがあります。その間、パッケージ ページには次のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="32a28-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you'll see the following message on your package page:</span></span>

    ![パッケージのインデックスがまだ作成されていないことを示すメッセージ](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="32a28-129">パッケージの検証とインデックスの作成</span><span class="sxs-lookup"><span data-stu-id="32a28-129">Package Validation and Indexing</span></span>

<span data-ttu-id="32a28-130">NuGet.org にプッシュされたパッケージはいくつかの検証を受けます。</span><span class="sxs-lookup"><span data-stu-id="32a28-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="32a28-131">パッケージがすべての検証に合格すると、インデックスが作成され、検索結果に表示されるようになりますが、それには時間がかかることがあります。</span><span class="sxs-lookup"><span data-stu-id="32a28-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="32a28-132">インデックス作成が完了すると、パッケージが正常に公開されたことを示す確認の電子メールが届きます。</span><span class="sxs-lookup"><span data-stu-id="32a28-132">Once indexing is complete, you'll receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="32a28-133">パッケージが検証で不合格になった場合、パッケージの詳細ページが更新され、関連エラーが表示されます。それに関する電子メールも届きます。</span><span class="sxs-lookup"><span data-stu-id="32a28-133">If the package fails a validation check, the package details page will update to display the associated error and you'll also receive an email notifying you about it.</span></span>

<span data-ttu-id="32a28-134">パッケージの検証とインデックスの作成は、通常、15 以内で完了します。</span><span class="sxs-lookup"><span data-stu-id="32a28-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="32a28-135">パッケージ公開に予想以上の時間がかかる場合、[status.nuget.org](https://status.nuget.org/) にアクセスし、NuGet.org に中断が発生していないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="32a28-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="32a28-136">すべてのシステムが動作しているとき、1 時間以内にパッケージが正常に公開されない場合、NuGet.org にログインし、パッケージ ページの [Contact Support] リンクからお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="32a28-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="32a28-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="32a28-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="32a28-138">CI/CD (継続的インテグレーション/配置) の一部として Visual Studio Team Services を利用して nuget.org にパッケージをプッシュする場合、NuGet タスクで nuget.exe 4.1 以上を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32a28-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use nuget.exe 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="32a28-139">詳細は、Microsoft DevOps ブログの「[Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)」 (ビルドで最新の NuGet を利用する) にあります。</span><span class="sxs-lookup"><span data-stu-id="32a28-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="32a28-140">nuget.org でパッケージ所有者を管理する</span><span class="sxs-lookup"><span data-stu-id="32a28-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="32a28-141">各 NuGet パッケージの `.nuspec` はパッケージの作成者を定義するものですが、nuget.org ギャラリーでは、所有権の定義にそのメタデータは使用されません。</span><span class="sxs-lookup"><span data-stu-id="32a28-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="32a28-142">nuget.org では、パッケージを公開した人に最初の所有権が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="32a28-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="32a28-143">これは nuget.org UI からパッケージをアップロードしたログイン ユーザーになるか、`nuget SetApiKey` または `nuget push` と共に API キーが使用されたユーザーになります。</span><span class="sxs-lookup"><span data-stu-id="32a28-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="32a28-144">パッケージ所有者にはすべて、パッケージの完全アクセス許可が与えられます。他の所有者を追加したり、削除したり、更新内容を公開したりできます。</span><span class="sxs-lookup"><span data-stu-id="32a28-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="32a28-145">パッケージの所有権は次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="32a28-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="32a28-146">パッケージの現在の所有者になっているアカウントで nuget.org にサインインします。</span><span class="sxs-lookup"><span data-stu-id="32a28-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="32a28-147">ユーザー名、**[Manage my packages]**、管理するパッケージの順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="32a28-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="32a28-148">左側にある **[Manage owners]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="32a28-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="32a28-149">ここにはいくつかのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="32a28-149">From here you have several options:</span></span>

1. <span data-ttu-id="32a28-150">所有者を追加するには、その NuGet アカウント名を入力し、**[Add]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="32a28-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="32a28-151">これでその新しい共同所有者に確認リンクを含む電子メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="32a28-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="32a28-152">確認後、その人に所有者を追加したり、削除したりできる完全アクセス許可が与えられます。</span><span class="sxs-lookup"><span data-stu-id="32a28-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="32a28-153">(確認されるまで、**[Manage owners]** ページにはその人の "pending approval" (承認待ち) が表示されます。)</span><span class="sxs-lookup"><span data-stu-id="32a28-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="32a28-154">所有者を削除するには、**[Manage owners]** で名前を選択し、**[Remove]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="32a28-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="32a28-155">所有権を譲渡するには (所有権が変更された場合や間違ったアカウントでパッケージが公開された場合)、新しい所有者を追加します。新しい所有者は所有権を確認したら、一覧から他の所有者を削除できます。</span><span class="sxs-lookup"><span data-stu-id="32a28-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="32a28-156">会社またはグループに所有権を割り当てるには、適切なチーム メンバーに転送される電子メール エイリアスを利用して nuget.org アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="32a28-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="32a28-157">たとえば、そのようなエイリアスである [microsoft](http://nuget.org/profiles/microsoft) アカウントや [aspnet](http://nuget.org/profiles/aspnet) アカウントでさまざまな Microsoft ASP.NET パッケージが共同所有されています。</span><span class="sxs-lookup"><span data-stu-id="32a28-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="32a28-158">パッケージ所有権を回復する</span><span class="sxs-lookup"><span data-stu-id="32a28-158">Recovering package ownership</span></span>

<span data-ttu-id="32a28-159">パッケージにアクティブな所有者が与えられていないことがあります。</span><span class="sxs-lookup"><span data-stu-id="32a28-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="32a28-160">たとえば、パッケージを作る会社を元々の所有者が去った場合、nuget.org 資格情報をなくした場合、ギャラリーの早期のバグが原因でパッケージが所有者なしになった場合などです。</span><span class="sxs-lookup"><span data-stu-id="32a28-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="32a28-161">自分がパッケージの正当な所有者であり、所有権を取り戻す必要がある場合、nuget.org の[問い合わせフォーム](https://www.nuget.org/policies/Contact)を利用し、NuGet チームに状況を説明してください。</span><span class="sxs-lookup"><span data-stu-id="32a28-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="32a28-162">その後、パッケージの所有権を検証するプロセスが開始します。パッケージのプロジェクト URL、Twitter、電子メール、その他の手段で既存の所有者が確認されます。</span><span class="sxs-lookup"><span data-stu-id="32a28-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="32a28-163">いずれの方法でも確認できない場合、所有者になるための新しい招待を送信します。</span><span class="sxs-lookup"><span data-stu-id="32a28-163">But if all else fails, we can send you a new invite to become an owner.</span></span>