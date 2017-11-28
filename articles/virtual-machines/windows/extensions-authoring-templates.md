---
title: "Windows VM 확장을 사용하여 템플릿 작성 | Microsoft Docs"
description: "Windows VM 확장을 사용하여 Azure Resource Manager 템플릿 작성에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 338668df33783d8ef62c6710f4d96ce805296fe5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="29e9a-103">Windows VM 확장을 사용하여 Azure Resource Manager 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="29e9a-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="29e9a-104">Azure PowerShell에서 다음 Azure PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="29e9a-105">이 cmdlet은 다음과 같이 게시자 이름, 확장 이름 및 버전을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-105">This cmdlet returns the publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="29e9a-106">이러한 세 속성은 위의 템플릿 조각에서 각각 "게시자", "유형" 및 "typeHandlerVersion"으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="29e9a-107">업데이트된 최신 기능을 얻으려면 최신 확장 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="29e9a-108">확장 구성 매개 변수에 대한 스키마를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="29e9a-109">확장 템플릿 작성을 사용하는 다음 단계는 구성 매개 변수를 제공하기 위한 형식을 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="29e9a-110">각 확장은 자체 매개 변수 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="29e9a-111">Windows 확장에 대한 샘플 구성을 보려면 [Windows 확장 샘플](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29e9a-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="29e9a-112">VM 확장으로 템플릿을 완벽하게 완료하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29e9a-112">Please refer to the following to get a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="29e9a-113">Windows VM의 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="29e9a-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="29e9a-114">템플릿을 작성한 후 Azure PowerShell을 사용하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29e9a-114">After authoring the template, you can deploy it using Azure PowerShell.</span></span>

