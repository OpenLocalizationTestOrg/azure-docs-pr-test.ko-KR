---
title: "REST API 및 서식 파일을 사용 하 여 aaaDeploy 리소스 | Microsoft Docs"
description: "리소스 tooAzure toodeploy Azure 리소스 관리자 및 리소스 관리자 REST API를 사용 합니다. hello 리소스는 리소스 관리자 서식 파일에 정의 됩니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="523da-104">리소스 관리자 템플릿과 리소스 관리자 REST API로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="523da-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="523da-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="523da-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="523da-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="523da-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="523da-107">포털</span><span class="sxs-lookup"><span data-stu-id="523da-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="523da-108">REST API</span><span class="sxs-lookup"><span data-stu-id="523da-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="523da-109">이 문서에서는 어떻게 toouse hello 리소스 관리자 REST API와 리소스 관리자 템플릿 toodeploy 리소스 tooAzure 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="523da-110">배포 중 발생하는 오류 디버깅에 대한 도움을 받으려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523da-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="523da-111">[배포 작업을 보려면](resource-manager-deployment-operations.md) toolearn 하는 데 유용한 정보를 가져오는 방법에 대 한 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="523da-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="523da-112">[Azure 리소스 관리자 리소스 tooAzure를 배포할 때 일반적인 오류 문제 해결](resource-manager-common-deployment-errors.md) toolearn 어떻게 tooresolve 일반적인 배포 오류</span><span class="sxs-lookup"><span data-stu-id="523da-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="523da-113">템플릿은 로컬 파일이거나 URI를 통해 사용 가능한 외부 파일일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523da-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="523da-114">서식 파일에는 저장소 계정에 있는 access toohello 서식 파일을 제한할 수 있으며 공유 액세스 서명 (SAS) 토큰을 배포 하는 동안 제공 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523da-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="523da-115">Hello REST API를 사용 하 여 배포</span><span class="sxs-lookup"><span data-stu-id="523da-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="523da-116">인증 토큰을 포함하여 [공통 매개 변수 및 헤더](https://docs.microsoft.com/rest/api/index)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="523da-117">기본 리소스 그룹이 없는 경우 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523da-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="523da-118">구독 ID, hello 이름 hello 새 리소스 그룹 및 솔루션에 필요한 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="523da-119">자세한 내용은 [리소스 그룹 만들기](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523da-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="523da-120">Hello를 실행 하 여 실행 하기 전에 배포 확인 [템플릿 배포의 유효성을 검사](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="523da-121">Hello 배포를 테스트할 때는 하 듯 hello 배포 (hello 다음 단계에 표시)를 실행할 때 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="523da-122">배포를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523da-122">Create a deployment.</span></span> <span data-ttu-id="523da-123">구독 ID, hello 리소스 그룹의 이름을 hello, hello 배포의 hello 이름 및 링크 tooyour 템플릿을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="523da-124">Hello 템플릿 파일에 대 한 정보를 참조 하십시오. [매개 변수 파일](#parameter-file)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="523da-125">Hello REST API toocreate 리소스 그룹에 대 한 자세한 내용은 참조 [템플릿 배포를 만드는](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="523da-126">공지 hello **모드** 너무 설정**증분**합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="523da-127">toorun 완전 한 배포 설정 **모드** 너무**완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="523da-128">서식 파일에 있지 않은 리소스를 실수로 삭제할 수 있습니다 때 hello 전체 모드를 사용 하는 경우 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="523da-129">Toolog 응답 콘텐츠, 요청 콘텐츠 또는 둘 다를 원하는 경우 포함 **debugSetting** hello 요청에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="523da-130">공유 액세스 서명 (SAS) 토큰을 저장소 계정 toouse를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523da-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="523da-131">자세한 내용은 [공유 액세스 서명을 사용하여 액세스 위임](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523da-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="523da-132">Hello 템플릿 배포의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="523da-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="523da-133">자세한 내용은 [템플릿 배포에 대한 정보 가져오기](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523da-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="523da-134">매개 변수 파일 </span><span class="sxs-lookup"><span data-stu-id="523da-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="523da-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="523da-135">Next steps</span></span>
* <span data-ttu-id="523da-136">비동기 REST 작업을 처리 하는 방법에 대 한 toolearn 참조 [Azure 비동기 작업을 추적](resource-manager-async-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="523da-137">리소스를 hello.NET 클라이언트 라이브러리를 통해 배포의 예제를 보려면 [.NET 라이브러리 및 서식 파일을 사용 하 여 리소스를 배포](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="523da-138">서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="523da-139">솔루션 toodifferent 환경 배포에 대 한 지침을 참조 하십시오. [Microsoft Azure에서 개발 및 테스트 환경](solution-dev-test-environments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="523da-140">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="523da-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

