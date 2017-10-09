---
title: "Linux VM 확장을 사용 하 여 aaaAuthoring 템플릿을 | Microsoft Docs"
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
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="fa1ed-103">Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="fa1ed-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="fa1ed-104">Azure CLI에서 hello 없었습니다 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="fa1ed-105">이 명령은 반환 hello 게시자 이름, 확장 프로그램 이름 및 다음과 같이 버전:</span><span class="sxs-lookup"><span data-stu-id="fa1ed-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="fa1ed-106">이 세 가지 속성을 너무 매핑할 "publisher", "type" 및 "typeHandlerVersion" 템플릿 조각 위에 hello에 각각 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="fa1ed-107">패턴은 항상 권장된 toouse hello 최신 확장 버전 tooget hello 가장 업데이트 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="fa1ed-108">확장 구성 매개 변수 hello에 대 한 hello 스키마를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="fa1ed-109">hello와 확장 템플릿을 제작 하 고 다음 단계는 구성 매개 변수를 제공 하는 데 tooidentify hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="fa1ed-110">각 확장은 자체 매개 변수 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="fa1ed-111">Linux 확장용 샘플 구성에서 toolook 클릭 참조에 대 한 hello 설명서 [Linux eExtensions 샘플](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fa1ed-112">Toohello tooget VM 확장 작업이 모두 완료 된 템플릿이 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="fa1ed-113">Linux VM의 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="fa1ed-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="fa1ed-114">Hello 서식 파일을 작성 한 후 hello Azure CLI를 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa1ed-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

