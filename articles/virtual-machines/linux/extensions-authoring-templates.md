---
title: "Linux VM 확장을 사용하여 템플릿 작성 | Microsoft Docs"
description: "Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="555e0-103">Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="555e0-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="555e0-104">Azure CLI에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="555e0-105">이 명령은 다음과 같이 게시자 이름, 확장 이름 및 버전을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="555e0-106">이러한 세 속성은 위의 템플릿 조각에서 각각 "게시자", "유형" 및 "typeHandlerVersion"으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="555e0-107">업데이트된 최신 기능을 얻으려면 최신 확장 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="555e0-108">확장 구성 매개 변수에 대한 스키마를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="555e0-109">확장 템플릿 작성을 사용하는 다음 단계는 구성 매개 변수를 제공하기 위한 형식을 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="555e0-110">각 확장은 자체 매개 변수 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="555e0-111">Linux 확장에 대한 샘플 구성을 보려면 [Linux 확장 샘플](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 대한 설명서를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="555e0-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="555e0-112">VM 확장으로 템플릿을 완벽하게 완료하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="555e0-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="555e0-113">Linux VM의 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="555e0-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="555e0-114">템플릿을 작성한 후 Azure CLI를 사용하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="555e0-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

