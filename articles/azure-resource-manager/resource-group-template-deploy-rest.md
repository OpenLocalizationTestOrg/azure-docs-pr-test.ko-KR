---
title: "REST API 및 템플릿으로 리소스 배포 | Microsoft Docs"
description: "Azure Resource Manager와 REST API를 사용하여 Azure에 리소스를 배포합니다. 리소스는 Resource Manager 템플릿에 정의됩니다."
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
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="a17ca-104">리소스 관리자 템플릿과 리소스 관리자 REST API로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="a17ca-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a17ca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a17ca-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="a17ca-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a17ca-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="a17ca-107">포털</span><span class="sxs-lookup"><span data-stu-id="a17ca-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="a17ca-108">REST API</span><span class="sxs-lookup"><span data-stu-id="a17ca-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="a17ca-109">이 문서에서는 리소스 관리자 템플릿으로 리소스 관리자 REST API를 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="a17ca-110">배포 중 발생하는 오류 디버깅에 대한 도움을 받으려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="a17ca-111">[배포 작업 보기](resource-manager-deployment-operations.md)에서 오류를 해결하는 데 유용한 정보를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="a17ca-112">[Azure Resource Manager로 Azure에 리소스를 배포할 때 발생하는 일반적인 오류 해결](resource-manager-common-deployment-errors.md) 에서 일반적인 배포 오류를 해결하는 방법을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="a17ca-113">템플릿은 로컬 파일이거나 URI를 통해 사용 가능한 외부 파일일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="a17ca-114">템플릿이 저장소 계정에 상주하는 경우, 템플릿에 대한 액세스를 제한하고 배포 중에 공유 액세스 서명(SAS) 토큰을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="a17ca-115">REST API를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="a17ca-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="a17ca-116">인증 토큰을 포함하여 [공통 매개 변수 및 헤더](https://docs.microsoft.com/rest/api/index)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="a17ca-117">기본 리소스 그룹이 없는 경우 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="a17ca-118">솔루션에 필요한 구독 ID, 새 리소스 그룹 이름 및 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="a17ca-119">자세한 내용은 [리소스 그룹 만들기](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="a17ca-120">배포를 실행하기 전에 [템플릿 배포 유효성 검사](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) 작업을 실행하여 배포 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="a17ca-121">배포를 테스트할 때는 배포를 실행할 때처럼 정확하게 매개 변수를 제공합니다(다음 단계에 표시됨).</span><span class="sxs-lookup"><span data-stu-id="a17ca-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="a17ca-122">배포를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-122">Create a deployment.</span></span> <span data-ttu-id="a17ca-123">템플릿의 구독 ID, 리소스 그룹 이름, 배포 이름 및 템플릿 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="a17ca-124">템플릿 파일에 대한 정보는 [매개 변수 파일](#parameter-file)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="a17ca-125">리소스 그룹을 만드는 REST API에 대한 정보는 [템플릿 배포 만들기](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="a17ca-126">**mode**가 **Incremental**로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="a17ca-127">전체 배포를 실행하려면 **mode**를 **Complete**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="a17ca-128">이 완전한 모드를 사용할 때는 템플릿에 없는 리소스를 실수로 삭제할 수 있으므로 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="a17ca-129">요청 콘텐츠와 응답 콘텐츠 중 하나 또는 둘 다를 기록하려면 요청에 **debugSetting** 을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="a17ca-130">공유 액세스 서명(SAS) 토큰을 사용하여 저장소 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="a17ca-131">자세한 내용은 [공유 액세스 서명을 사용하여 액세스 위임](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="a17ca-132">템플릿 배포의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a17ca-132">Get the status of the template deployment.</span></span> <span data-ttu-id="a17ca-133">자세한 내용은 [템플릿 배포에 대한 정보 가져오기](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="a17ca-134">매개 변수 파일 </span><span class="sxs-lookup"><span data-stu-id="a17ca-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="a17ca-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a17ca-135">Next steps</span></span>
* <span data-ttu-id="a17ca-136">비동기 REST 작업 처리에 대해 알아보려면 [Azure 비동기 작업 추적](resource-manager-async-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="a17ca-137">.NET 클라이언트 라이브러리를 통한 리소스 배포의 예제를 보려면 [.NET 라이브러리 및 템플릿을 사용하여 리소스 배포](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a17ca-138">템플릿에서 매개 변수를 정의하려면 [템플릿 작성](resource-group-authoring-templates.md#parameters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="a17ca-139">다른 환경에 솔루션 배포에 관한 지침은 [Microsoft Azure의 개발 및 테스트 환경](solution-dev-test-environments.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="a17ca-140">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a17ca-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

