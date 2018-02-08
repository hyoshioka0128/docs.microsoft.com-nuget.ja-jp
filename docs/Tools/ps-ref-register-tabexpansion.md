---
title: "NuGet のレジスタ TabExpansion PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールでのレジスタ TabExpansion PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、レジスタ TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="2fc10-104">レジスタ TabExpansion (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="2fc10-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2fc10-105">*内でのみ使用可能な[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="2fc10-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2fc10-106">対象のパラメーターに使用できるオプションとして、展開可能な値が表示されます] タブは、コマンドを入力するときに使用する場合など、指定されたコマンドのパラメーターにタブ拡張を登録します。</span><span class="sxs-lookup"><span data-stu-id="2fc10-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="2fc10-107">コマンドの前、展開が上書きされます。</span><span class="sxs-lookup"><span data-stu-id="2fc10-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="2fc10-108">構文</span><span class="sxs-lookup"><span data-stu-id="2fc10-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2fc10-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="2fc10-109">Parameters</span></span>

| <span data-ttu-id="2fc10-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="2fc10-110">Parameter</span></span> | <span data-ttu-id="2fc10-111">説明</span><span class="sxs-lookup"><span data-stu-id="2fc10-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2fc10-112">name</span><span class="sxs-lookup"><span data-stu-id="2fc10-112">Name</span></span> | <span data-ttu-id="2fc10-113">(必須)拡張を登録するためにコマンド。</span><span class="sxs-lookup"><span data-stu-id="2fc10-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="2fc10-114">-Name スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="2fc10-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="2fc10-115">定義</span><span class="sxs-lookup"><span data-stu-id="2fc10-115">Definition</span></span> | <span data-ttu-id="2fc10-116">(必須)構文では、引数を表すオブジェクトです。`@{'<parameter>' = {'<value1>', '<value2>', ...}}`場所`<parameter>`を変更するパラメーターとそれぞれの名前を指定`<value>`固有の展開を提供します。</span><span class="sxs-lookup"><span data-stu-id="2fc10-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="2fc10-117">両方単一引用符と二重引用符が受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="2fc10-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="2fc10-118">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="2fc10-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2fc10-119">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="2fc10-119">Common Parameters</span></span>

<span data-ttu-id="2fc10-120">`Register-TabExpansion`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="2fc10-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2fc10-121">使用例</span><span class="sxs-lookup"><span data-stu-id="2fc10-121">Examples</span></span>

<span data-ttu-id="2fc10-122">次の 3 つのプロジェクト名 EventManager、ユーティリティ、および SpecialParser を含むソリューションを検討してください。</span><span class="sxs-lookup"><span data-stu-id="2fc10-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="2fc10-123">開発者が頻繁に使用、`Update-Package`これらの各プロジェクトに異なるタイミングでコマンド。</span><span class="sxs-lookup"><span data-stu-id="2fc10-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="2fc10-124">彼女は都合のよいことが、`Update-Package`コマンドでは、オートコンプリートの展開の提供、`-ProjectName`引数ため、彼女はプロジェクト名をその都度入力する必要はありませんの。</span><span class="sxs-lookup"><span data-stu-id="2fc10-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="2fc10-125">次のコマンドがの拡張として次に、これら 3 つのプロジェクトの名前を登録、`-ProjectName`パラメーター。</span><span class="sxs-lookup"><span data-stu-id="2fc10-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="2fc10-126">開発者は入力できますし、 `Update-Package -ProjectName `、Tab キーを押して、オートコンプリートの選択肢として提示の展開を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fc10-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![レジスタ TabExpansion の使用例](media/Register-TabExpansion-Example.png)