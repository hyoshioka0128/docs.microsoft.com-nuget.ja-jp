---
title: "プッシュ モードと NuGet API を削除します |。Microsoft ドキュメント"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "発行サービスは、クライアントが新しいパッケージを公開および非公開または既存のパッケージを削除できます。"
keywords: "NuGet API プッシュ パッケージ、パッケージを削除する NuGet API、NuGet API は、パッケージ、NuGet API アップロード パッケージを非公開、API の NuGet パッケージの作成"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="40b88-104">プッシュ モードと削除</span><span class="sxs-lookup"><span data-stu-id="40b88-104">Push and Delete</span></span>

<span data-ttu-id="40b88-105">プッシュ、削除 (またはサーバーの実装によって、非公開キーを押す)、可能であれば、NuGet V3 API を使用してパッケージを relist とします。</span><span class="sxs-lookup"><span data-stu-id="40b88-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="40b88-106">これらの操作は無効の基づいて、`PackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="40b88-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="40b88-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="40b88-107">Versioning</span></span>

<span data-ttu-id="40b88-108">次`@type`値を使用します。</span><span class="sxs-lookup"><span data-stu-id="40b88-108">The following `@type` value is used:</span></span>

<span data-ttu-id="40b88-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="40b88-109">@type value</span></span>          | <span data-ttu-id="40b88-110">メモ</span><span class="sxs-lookup"><span data-stu-id="40b88-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="40b88-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="40b88-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="40b88-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="40b88-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="40b88-113">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="40b88-113">Base URL</span></span>

<span data-ttu-id="40b88-114">次の Api のベース URL の値、`@id`のプロパティ、`PackagePublish/2.0.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="40b88-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="40b88-115">次のドキュメントでは、nuget.org の URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="40b88-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="40b88-116">検討`https://www.nuget.org/api/v2/package`のプレース ホルダーとして、`@id`サービス インデックス内の値で見つかった。</span><span class="sxs-lookup"><span data-stu-id="40b88-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="40b88-117">プロトコルが同じであるために、この URL がレガシ V2 プッシュ エンドポイントと同じ場所を指していることを注意してください。</span><span class="sxs-lookup"><span data-stu-id="40b88-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="40b88-118">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="40b88-118">HTTP methods</span></span>

<span data-ttu-id="40b88-119">`PUT`、`POST`と`DELETE`HTTP メソッドは、このリソースでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="40b88-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="40b88-120">各エンドポイントでは、どのメソッドがサポートされている、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="40b88-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="40b88-121">パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="40b88-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="40b88-122">nuget.org が[追加要件](NuGet-Protocols.md)プッシュ エンドポイントと対話するためです。</span><span class="sxs-lookup"><span data-stu-id="40b88-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="40b88-123">nuget.org には、次の API を使用してプッシュの新しいパッケージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="40b88-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="40b88-124">指定された ID とバージョンのパッケージが既に存在する場合、nuget.org は、プッシュを拒否します。</span><span class="sxs-lookup"><span data-stu-id="40b88-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="40b88-125">他のパッケージ ソースでは、既存のパッケージの交換をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="40b88-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="40b88-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="40b88-126">Request parameters</span></span>

<span data-ttu-id="40b88-127">name</span><span class="sxs-lookup"><span data-stu-id="40b88-127">Name</span></span>           | <span data-ttu-id="40b88-128">イン</span><span class="sxs-lookup"><span data-stu-id="40b88-128">In</span></span>     | <span data-ttu-id="40b88-129">型</span><span class="sxs-lookup"><span data-stu-id="40b88-129">Type</span></span>   | <span data-ttu-id="40b88-130">必須</span><span class="sxs-lookup"><span data-stu-id="40b88-130">Required</span></span> | <span data-ttu-id="40b88-131">メモ</span><span class="sxs-lookup"><span data-stu-id="40b88-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="40b88-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="40b88-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="40b88-133">Header</span><span class="sxs-lookup"><span data-stu-id="40b88-133">Header</span></span> | <span data-ttu-id="40b88-134">string</span><span class="sxs-lookup"><span data-stu-id="40b88-134">string</span></span> | <span data-ttu-id="40b88-135">可</span><span class="sxs-lookup"><span data-stu-id="40b88-135">yes</span></span>      | <span data-ttu-id="40b88-136">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="40b88-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="40b88-137">API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている非透過の文字列です。</span><span class="sxs-lookup"><span data-stu-id="40b88-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="40b88-138">特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。</span><span class="sxs-lookup"><span data-stu-id="40b88-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="40b88-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="40b88-139">Request body</span></span>

<span data-ttu-id="40b88-140">要求本文で、次の形式でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="40b88-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="40b88-141">マルチパート フォーム データ</span><span class="sxs-lookup"><span data-stu-id="40b88-141">Multipart form data</span></span>

<span data-ttu-id="40b88-142">要求ヘッダー`Content-Type`は`multipart/form-data`要求本文の最初の項目は、これはプッシュされる .nupkg の生のバイトとします。</span><span class="sxs-lookup"><span data-stu-id="40b88-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="40b88-143">マルチパート ボディ内の後続の項目は無視されます。</span><span class="sxs-lookup"><span data-stu-id="40b88-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="40b88-144">ファイルの名前またはマルチパートの項目の他のヘッダーが無視されます。</span><span class="sxs-lookup"><span data-stu-id="40b88-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="40b88-145">応答</span><span class="sxs-lookup"><span data-stu-id="40b88-145">Response</span></span>

<span data-ttu-id="40b88-146">状態コード</span><span class="sxs-lookup"><span data-stu-id="40b88-146">Status Code</span></span> | <span data-ttu-id="40b88-147">説明</span><span class="sxs-lookup"><span data-stu-id="40b88-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="40b88-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="40b88-148">201, 202</span></span>    | <span data-ttu-id="40b88-149">パッケージが正常にプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="40b88-149">The package was successfully pushed</span></span>
<span data-ttu-id="40b88-150">400</span><span class="sxs-lookup"><span data-stu-id="40b88-150">400</span></span>         | <span data-ttu-id="40b88-151">指定したパッケージが正しくありません。</span><span class="sxs-lookup"><span data-stu-id="40b88-151">The provided package is invalid</span></span>
<span data-ttu-id="40b88-152">409</span><span class="sxs-lookup"><span data-stu-id="40b88-152">409</span></span>         | <span data-ttu-id="40b88-153">指定された ID とバージョンを使用してパッケージが既に存在します。</span><span class="sxs-lookup"><span data-stu-id="40b88-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="40b88-154">サーバーの実装は、パッケージが正常にプッシュされたときに返される成功ステータス コードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="40b88-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="40b88-155">パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="40b88-155">Delete a package</span></span>

<span data-ttu-id="40b88-156">nuget.org としてパッケージの削除要求では、解釈「非公開」にします。</span><span class="sxs-lookup"><span data-stu-id="40b88-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="40b88-157">つまり、パッケージは、パッケージの既存のコンシューマーを引き続き使用できますが、パッケージで検索結果または web インターフェイスが表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="40b88-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="40b88-158">この方法の詳細については、次を参照してください。、[パッケージの削除](../policies/deleting-packages.md)ポリシー。</span><span class="sxs-lookup"><span data-stu-id="40b88-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="40b88-159">その他のサーバーの実装では、ハード削除としてこの信号を解釈し、論理削除、または、非公開に解放されます。</span><span class="sxs-lookup"><span data-stu-id="40b88-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="40b88-160">たとえば、 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (するサーバーの実装だけ古い V2 API をサポート)、unlist または構成オプションに基づくハード delete のいずれかとしてこの要求の処理をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="40b88-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="40b88-161">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="40b88-161">Request parameters</span></span>

<span data-ttu-id="40b88-162">name</span><span class="sxs-lookup"><span data-stu-id="40b88-162">Name</span></span>           | <span data-ttu-id="40b88-163">イン</span><span class="sxs-lookup"><span data-stu-id="40b88-163">In</span></span>     | <span data-ttu-id="40b88-164">型</span><span class="sxs-lookup"><span data-stu-id="40b88-164">Type</span></span>   | <span data-ttu-id="40b88-165">必須</span><span class="sxs-lookup"><span data-stu-id="40b88-165">Required</span></span> | <span data-ttu-id="40b88-166">メモ</span><span class="sxs-lookup"><span data-stu-id="40b88-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="40b88-167">ID</span><span class="sxs-lookup"><span data-stu-id="40b88-167">ID</span></span>             | <span data-ttu-id="40b88-168">URL</span><span class="sxs-lookup"><span data-stu-id="40b88-168">URL</span></span>    | <span data-ttu-id="40b88-169">string</span><span class="sxs-lookup"><span data-stu-id="40b88-169">string</span></span> | <span data-ttu-id="40b88-170">可</span><span class="sxs-lookup"><span data-stu-id="40b88-170">yes</span></span>      | <span data-ttu-id="40b88-171">削除するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="40b88-171">The ID of the package to delete</span></span>
<span data-ttu-id="40b88-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="40b88-172">VERSION</span></span>        | <span data-ttu-id="40b88-173">URL</span><span class="sxs-lookup"><span data-stu-id="40b88-173">URL</span></span>    | <span data-ttu-id="40b88-174">string</span><span class="sxs-lookup"><span data-stu-id="40b88-174">string</span></span> | <span data-ttu-id="40b88-175">可</span><span class="sxs-lookup"><span data-stu-id="40b88-175">yes</span></span>      | <span data-ttu-id="40b88-176">削除するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="40b88-176">The version of the package to delete</span></span>
<span data-ttu-id="40b88-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="40b88-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="40b88-178">Header</span><span class="sxs-lookup"><span data-stu-id="40b88-178">Header</span></span> | <span data-ttu-id="40b88-179">string</span><span class="sxs-lookup"><span data-stu-id="40b88-179">string</span></span> | <span data-ttu-id="40b88-180">可</span><span class="sxs-lookup"><span data-stu-id="40b88-180">yes</span></span>      | <span data-ttu-id="40b88-181">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="40b88-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="40b88-182">応答</span><span class="sxs-lookup"><span data-stu-id="40b88-182">Response</span></span>

<span data-ttu-id="40b88-183">状態コード</span><span class="sxs-lookup"><span data-stu-id="40b88-183">Status Code</span></span> | <span data-ttu-id="40b88-184">説明</span><span class="sxs-lookup"><span data-stu-id="40b88-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="40b88-185">204</span><span class="sxs-lookup"><span data-stu-id="40b88-185">204</span></span>         | <span data-ttu-id="40b88-186">パッケージが削除されました</span><span class="sxs-lookup"><span data-stu-id="40b88-186">The package was deleted</span></span>
<span data-ttu-id="40b88-187">404</span><span class="sxs-lookup"><span data-stu-id="40b88-187">404</span></span>         | <span data-ttu-id="40b88-188">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="40b88-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="40b88-189">パッケージを relist します。</span><span class="sxs-lookup"><span data-stu-id="40b88-189">Relist a package</span></span>

<span data-ttu-id="40b88-190">パッケージが一覧にない場合は、そのパッケージを"relist"のエンドポイントを使用して検索結果にもう一度表示することができます。</span><span class="sxs-lookup"><span data-stu-id="40b88-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="40b88-191">このエンドポイントと同じ形には、[削除 (非公開) エンドポイント](#delete-a-package)が使用して、 `POST` HTTP メソッドの代わりに、`DELETE`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="40b88-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="40b88-192">パッケージが既に表示されている場合でも、要求は成功します。</span><span class="sxs-lookup"><span data-stu-id="40b88-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="40b88-193">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="40b88-193">Request parameters</span></span>

<span data-ttu-id="40b88-194">name</span><span class="sxs-lookup"><span data-stu-id="40b88-194">Name</span></span>           | <span data-ttu-id="40b88-195">イン</span><span class="sxs-lookup"><span data-stu-id="40b88-195">In</span></span>     | <span data-ttu-id="40b88-196">型</span><span class="sxs-lookup"><span data-stu-id="40b88-196">Type</span></span>   | <span data-ttu-id="40b88-197">必須</span><span class="sxs-lookup"><span data-stu-id="40b88-197">Required</span></span> | <span data-ttu-id="40b88-198">メモ</span><span class="sxs-lookup"><span data-stu-id="40b88-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="40b88-199">ID</span><span class="sxs-lookup"><span data-stu-id="40b88-199">ID</span></span>             | <span data-ttu-id="40b88-200">URL</span><span class="sxs-lookup"><span data-stu-id="40b88-200">URL</span></span>    | <span data-ttu-id="40b88-201">string</span><span class="sxs-lookup"><span data-stu-id="40b88-201">string</span></span> | <span data-ttu-id="40b88-202">可</span><span class="sxs-lookup"><span data-stu-id="40b88-202">yes</span></span>      | <span data-ttu-id="40b88-203">Relist するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="40b88-203">The ID of the package to relist</span></span>
<span data-ttu-id="40b88-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="40b88-204">VERSION</span></span>        | <span data-ttu-id="40b88-205">URL</span><span class="sxs-lookup"><span data-stu-id="40b88-205">URL</span></span>    | <span data-ttu-id="40b88-206">string</span><span class="sxs-lookup"><span data-stu-id="40b88-206">string</span></span> | <span data-ttu-id="40b88-207">可</span><span class="sxs-lookup"><span data-stu-id="40b88-207">yes</span></span>      | <span data-ttu-id="40b88-208">Relist するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="40b88-208">The version of the package to relist</span></span>
<span data-ttu-id="40b88-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="40b88-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="40b88-210">Header</span><span class="sxs-lookup"><span data-stu-id="40b88-210">Header</span></span> | <span data-ttu-id="40b88-211">string</span><span class="sxs-lookup"><span data-stu-id="40b88-211">string</span></span> | <span data-ttu-id="40b88-212">可</span><span class="sxs-lookup"><span data-stu-id="40b88-212">yes</span></span>      | <span data-ttu-id="40b88-213">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="40b88-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="40b88-214">応答</span><span class="sxs-lookup"><span data-stu-id="40b88-214">Response</span></span>

<span data-ttu-id="40b88-215">状態コード</span><span class="sxs-lookup"><span data-stu-id="40b88-215">Status Code</span></span> | <span data-ttu-id="40b88-216">説明</span><span class="sxs-lookup"><span data-stu-id="40b88-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="40b88-217">204</span><span class="sxs-lookup"><span data-stu-id="40b88-217">204</span></span>         | <span data-ttu-id="40b88-218">パッケージが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="40b88-218">The package is now listed</span></span>
<span data-ttu-id="40b88-219">404</span><span class="sxs-lookup"><span data-stu-id="40b88-219">404</span></span>         | <span data-ttu-id="40b88-220">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="40b88-220">No package with the provided `ID` and `VERSION` exists</span></span>