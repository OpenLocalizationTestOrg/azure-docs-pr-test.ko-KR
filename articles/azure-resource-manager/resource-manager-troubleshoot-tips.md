---
title: "Azure 배포 오류 이해 | Microsoft Docs"
description: "Azure 배포 오류에 대해 알아보는 방법을 설명합니다."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "배포 오류 Azure 배포, Azure에 배포"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: b67bb30fa259fa08e37e11afec724c8b8c3eb633
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="0ecf1-104">Azure 배포 오류 이해</span><span class="sxs-lookup"><span data-stu-id="0ecf1-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="0ecf1-105">이 항목에서는 배포 오류 및 오류에 대한 자세한 정보를 검색하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="0ecf1-106">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-106">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="0ecf1-107">두 가지 오류 유형</span><span class="sxs-lookup"><span data-stu-id="0ecf1-107">Two types of errors</span></span>
<span data-ttu-id="0ecf1-108">두 가지 유형의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="0ecf1-109">유효성 검사 오류</span><span class="sxs-lookup"><span data-stu-id="0ecf1-109">validation errors</span></span>
* <span data-ttu-id="0ecf1-110">배포 오류</span><span class="sxs-lookup"><span data-stu-id="0ecf1-110">deployment errors</span></span>

<span data-ttu-id="0ecf1-111">다음 이미지는 그룹에 대한 활동 로그를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-111">The following image shows the activity log for a subscription.</span></span> <span data-ttu-id="0ecf1-112">또한 두 개의 배포를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-112">It represents two deployments.</span></span> <span data-ttu-id="0ecf1-113">한 배포에서는 템플릿이 유효성 검사(**Validate**)에 실패했고 진행하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-113">In one deployment, the template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="0ecf1-114">다른 배포에서 템플릿은 유효성 검사를 통과했지만, 리소스를 만들 때(**Write Deployments**) 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-114">In the other deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span></span> 

![오류 코드 표시](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="0ecf1-116">유효성 검사 오류는 배포 전에 확인할 수 있는 시나리오에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="0ecf1-117">유효성 검사 오류에는 템플릿의 구문 오류나 구독 할당량을 초과하는 리소스를 배포하려는 구문 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-117">They include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="0ecf1-118">배포 오류는 배포 프로세스 중 발생하는 조건에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-118">Deployment errors arise from conditions that occur during the deployment process.</span></span> <span data-ttu-id="0ecf1-119">배포 오류에는 병렬로 배포 중인 리소스에 액세스하려는 시도가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-119">They include trying to access a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="0ecf1-120">두 가지 오류 유형에서 배포 문제를 해결하는 데 사용하는 오류 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-120">Both types of errors return an error code that you use to troubleshoot the deployment.</span></span> <span data-ttu-id="0ecf1-121">두 가지 오류 유형 모두 [활동 로그](resource-group-audit.md)에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-121">Both types of errors appear in the [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="0ecf1-122">하지만 배포가 시작된 것은 아니므로 유효성 검사 오류는 배포 기록에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-122">However, validation errors do not appear in your deployment history because the deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="0ecf1-123">오류 코드 확인</span><span class="sxs-lookup"><span data-stu-id="0ecf1-123">Determine error code</span></span>

<span data-ttu-id="0ecf1-124">오류 메시지 및 오류 코드를 살펴보면 오류에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-124">You can learn about an error by looking at the error message and the error code.</span></span> <span data-ttu-id="0ecf1-125">[Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md) 문서에는 오류 코드별로 해결 방법이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-125">The [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="0ecf1-126">이 항목에서는 Azure Portal을 사용하여 오류 코드를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-126">This topic shows how to use the Azure portal to discover the error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="0ecf1-127">유효성 검사 오류</span><span class="sxs-lookup"><span data-stu-id="0ecf1-127">Validation errors</span></span>

<span data-ttu-id="0ecf1-128">포털을 통해 배포할 때 값을 제출한 후 유효성 검사 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-128">When deploying through the portal, you see a validation error after submitting your values.</span></span>

![포털 유효성 검사 오류 표시](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="0ecf1-130">메시지를 선택하여 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-130">Select the message for more details.</span></span> <span data-ttu-id="0ecf1-131">다음 이미지에서 **InvalidTemplateDeployment** 오류와 정책에서 배포를 차단했음을 나타내는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-131">In the following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![유효성 검사 세부 정보 표시](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="0ecf1-133">배포 오류</span><span class="sxs-lookup"><span data-stu-id="0ecf1-133">Deployment errors</span></span>

<span data-ttu-id="0ecf1-134">작업이 유효성 검사를 통과했지만, 배포 중에 실패하는 경우 알림에 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-134">When the operation passes validation, but fails during deployment, you see the error in the notifications.</span></span> <span data-ttu-id="0ecf1-135">알림을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-135">Select the notification.</span></span>

![알림 오류](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="0ecf1-137">배포에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-137">You see more details about the deployment.</span></span> <span data-ttu-id="0ecf1-138">옵션을 선택하여 오류에 대한 자세한 정보를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-138">Select the option to find more information about the error.</span></span>

![배포 실패](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="0ecf1-140">오류 메시지 및 오류 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-140">You see the error message and error codes.</span></span> <span data-ttu-id="0ecf1-141">두 개의 오류 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-141">Notice there are two error codes.</span></span> <span data-ttu-id="0ecf1-142">첫 번째 오류 코드(**DeploymentFailed**)는 오류를 해결하는 데 필요한 세부 정보를 제공하지 않는 일반 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-142">The first error code (**DeploymentFailed**) is a general error that does not provide the details you need to solve the error.</span></span> <span data-ttu-id="0ecf1-143">두 번째 오류 코드(**StorageAccountNotFound**)는 필요한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-143">The second error code (**StorageAccountNotFound**) provides the details you need.</span></span> 

![오류 세부 정보](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="0ecf1-145">디버그 로깅 활성화</span><span class="sxs-lookup"><span data-stu-id="0ecf1-145">Enable debug logging</span></span>
<span data-ttu-id="0ecf1-146">무엇이 잘못되었는지 알려면 요청 및 응답에 대한 정보가 더 필요한 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-146">Sometimes you need more information about the request and response to discover what went wrong.</span></span> <span data-ttu-id="0ecf1-147">PowerShell 또는 Azure CLI를 사용하여, 배포 중에 추가 정보가 기록되도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="0ecf1-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ecf1-148">PowerShell</span></span>

   <span data-ttu-id="0ecf1-149">PowerShell에서 **DeploymentDebugLogLevel** 매개 변수를 All, ResponseContent 또는 RequestContent로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-149">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="0ecf1-150">요청 내용을 다음 cmdlet으로 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-150">Examine the request content with the following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="0ecf1-151">또는 응답 내용을 다음으로 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-151">Or, the response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="0ecf1-152">이 정보를 통해 템플릿의 값이 잘못 설정되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-152">This information can help you determine whether a value in the template is being incorrectly set.</span></span>

- <span data-ttu-id="0ecf1-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ecf1-153">Azure CLI</span></span>

   <span data-ttu-id="0ecf1-154">다음 명령을 사용하여 배포 작업을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-154">Examine the deployment operations with the following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="0ecf1-155">중첩된 템플릿</span><span class="sxs-lookup"><span data-stu-id="0ecf1-155">Nested template</span></span>

   <span data-ttu-id="0ecf1-156">중첩된 템플릿에 대한 디버그 정보를 기록하려면 **debugSetting** 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-156">To log debug information for a nested template, use the **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="0ecf1-157">문제 해결 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="0ecf1-157">Create a troubleshooting template</span></span>
<span data-ttu-id="0ecf1-158">경우에 따라 템플릿 문제를 해결하는 가장 쉬운 방법은 일부를 테스트해보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-158">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span></span> <span data-ttu-id="0ecf1-159">간소화된 템플릿을 만들어 오류를 일으키는 것으로 생각되는 부분에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-159">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span></span> <span data-ttu-id="0ecf1-160">예를 들어, 리소스를 참조할 때 오류가 발생한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="0ecf1-161">전체 템플릿을 처리하는 대신, 문제를 일으킬 수 있는 부분만 반환하는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-161">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span></span> <span data-ttu-id="0ecf1-162">이렇게 하면 템플릿 함수를 바르게 사용하여, 올바른 매개 변수를 전달하고 원하는 리소스를 가져오고 있는지 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-162">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="0ecf1-163">또는 종속성을 잘못 설정하는 것과 관련되었다고 생각되는 배포 오류가 발생한다고 가정해보세요.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-163">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span></span> <span data-ttu-id="0ecf1-164">간소화된 템플릿을 분리하여 템플릿을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="0ecf1-165">먼저 단일 리소스(예: SQL Server)를 배포하는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="0ecf1-166">리소스가 올바르게 정의된 것이 확실하면 종속되는 리소스(예: SQL Database)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="0ecf1-167">이러한 두 리소스가 올바르게 정의되어 있으면 다른 종속 리소스(예: 감사 정책)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="0ecf1-168">각 테스트 배포 사이에 리소스 그룹을 삭제하여 종속성을 적절히 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-168">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="0ecf1-169">배포 시퀀스 확인</span><span class="sxs-lookup"><span data-stu-id="0ecf1-169">Check deployment sequence</span></span>

<span data-ttu-id="0ecf1-170">대부분의 배포 오류는 예상치 않은 시퀀스로 리소스가 배포될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="0ecf1-171">이러한 오류는 종속성이 올바르게 설정되지 않은 경우 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="0ecf1-172">필요한 종속성이 없는 경우에는 한 리소스가 다른 리소스에 대한 값을 사용하려고 하는데 다른 리소스가 아직 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-172">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span></span> <span data-ttu-id="0ecf1-173">리소스를 찾을 수 없다는 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="0ecf1-174">각 리소스에 대한 배포 시간이 다를 수 있기 때문에 이러한 유형의 오류가 일시적으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-174">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span></span> <span data-ttu-id="0ecf1-175">예를 들어 리소스를 배포하려는 첫 번째 시도는 필요한 리소스가 시간 내에 임의로 완료되면 성공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-175">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="0ecf1-176">그러나 두 번째 시도는 필요한 리소스가 시간 내에 완료되지 않으면 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-176">However, your second attempt fails because the required resource did not complete in time.</span></span> 

<span data-ttu-id="0ecf1-177">하지만 필요하지 않은 종속성은 설정하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-177">But, you want to avoid setting dependencies that are not needed.</span></span> <span data-ttu-id="0ecf1-178">불필요한 종속성이 있으면 서로 종속되지 않은 리소스가 동시에 배포되는 것을 막기 때문에 배포 시간이 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-178">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="0ecf1-179">또한 배포를 방해하는 순환 종속성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-179">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="0ecf1-180">[reference](resource-group-template-functions-resource.md#reference) 함수는 리소스가 같은 템플릿에 배포되는 경우 참조되는 리소스에 대한 암시적 종속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-180">The [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on the referenced resource, when that resource is deployed in the same template.</span></span> <span data-ttu-id="0ecf1-181">따라서 **dependsOn** 속성에 지정된 종속성보다 많은 종속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-181">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="0ecf1-182">[resourceId](resource-group-template-functions-resource.md#resourceid) 함수는 암시적 종속성을 만들지 않거나 리소스가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-182">The [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span></span>

<span data-ttu-id="0ecf1-183">종속성 문제가 발생하는 경우 리소스 배포 순서를 간파할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-183">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="0ecf1-184">배포 작업의 순서를 보려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-184">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="0ecf1-185">리소스 그룹에 대한 배포 기록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-185">Select the deployment history for your resource group.</span></span>

   ![배포 기록 선택](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="0ecf1-187">기록에서 배포를 선택하고 **이벤트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-187">Select a deployment from the history, and select **Events**.</span></span>

   ![배포 이벤트 선택](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="0ecf1-189">각 리소스에 대한 이벤트의 시퀀스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-189">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="0ecf1-190">각 작업의 상태에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-190">Pay attention to the status of each operation.</span></span> <span data-ttu-id="0ecf1-191">예를 들어 다음 이미지는 병렬로 배포된 3개의 저장소 계정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-191">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="0ecf1-192">3개의 저장소 계정이 동시에 시작되었다는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-192">Notice that the three storage accounts are started at the same time.</span></span>

   ![병렬 배포](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="0ecf1-194">다음 이미지는 동시에 배포되지 않은 3개의 저장소 계정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-194">The next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="0ecf1-195">두 번째 저장소 계정은 첫 번째 저장소 계정에 종속되고 세 번째 저장소 계정은 두 번째 저장소 계정에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-195">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="0ecf1-196">따라서 다음 저장소 계정이 시작되기 전에 첫 번째 저장소 계정이 시작, 승인, 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-196">Therefore, the first storage account is started, accepted, and completed before the next is started.</span></span>

   ![순차 배포](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="0ecf1-198">더 복잡한 시나리오의 경우에도 같은 기법을 사용하여 각 리소스에 대해 배포가 시작되고 완료되는 시기를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-198">Even for more complicated scenarios, you can use the same technique to discover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="0ecf1-199">시퀀스가 예상한 것과 다른지 배포 이벤트를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-199">Look through your deployment events to see if the sequence is different than you would expect.</span></span> <span data-ttu-id="0ecf1-200">그런 경우 이 리소스에 대한 종속성을 다시 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-200">If so, reevaluate the dependencies for this resource.</span></span>

<span data-ttu-id="0ecf1-201">Resource Manager는 템플릿의 유효성을 검사하는 동안 순환적 종속성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="0ecf1-202">순환 종속성이 존재한다고 구체적으로 언급하는 오류 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="0ecf1-203">순환 종속성을 해결하려면:</span><span class="sxs-lookup"><span data-stu-id="0ecf1-203">To solve a circular dependency:</span></span>

1. <span data-ttu-id="0ecf1-204">템플릿에서 순환 종속성 내에 식별된 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-204">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="0ecf1-205">해당 리소스에 대해 **dependsOn** 속성 및 **reference** 함수가 사용되었는지 검토하여 어떤 리소스에 종속되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-205">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="0ecf1-206">해당 리소스를 검토하여 어떤 리소스에 종속되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-206">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="0ecf1-207">원래 리소스에 종속되는 리소스를 확인할 때까지 종속성을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-207">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="0ecf1-208">순환 종속성에 관련된 리소스의 경우 **dependsOn** 속성이 사용된 부분을 신중하게 모두 검토하여 필요하지 않은 종속성이 있는지 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-208">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="0ecf1-209">그러한 종속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-209">Remove those dependencies.</span></span> <span data-ttu-id="0ecf1-210">종속성이 필요한지 확신이 안되면 해당 종속성을 제거해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="0ecf1-211">템플릿을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-211">Redeploy the template.</span></span>

<span data-ttu-id="0ecf1-212">**dependsOn** 속성에서 값을 제거하면 템플릿을 배포할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-212">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="0ecf1-213">오류가 발생하면 해당 종속성을 템플릿에 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-213">If you encounter an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="0ecf1-214">이러한 방법으로 순환 종속성 문제가 해결되지 않으면 일부 배포 논리를 자식 리소스(예: 확장 또는 구성 설정)로 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-214">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="0ecf1-215">순환 종속성에 관련된 리소스를 배포한 후에 자식 리소스를 배포하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-215">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="0ecf1-216">예를 들어 두 개의 가상 컴퓨터를 배포하지만 각 컴퓨터에 서로를 참조하는 속성을 설정해야 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="0ecf1-217">이런 경우 다음과 같은 순서로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-217">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="0ecf1-218">vm1</span><span class="sxs-lookup"><span data-stu-id="0ecf1-218">vm1</span></span>
2. <span data-ttu-id="0ecf1-219">vm2</span><span class="sxs-lookup"><span data-stu-id="0ecf1-219">vm2</span></span>
3. <span data-ttu-id="0ecf1-220">vm1의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="0ecf1-221">이 확장은 vm2에서 얻은 값을 vm1에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-221">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="0ecf1-222">vm2의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="0ecf1-223">이 확장은 vm1에서 얻은 값을 vm2에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-223">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="0ecf1-224">동일한 방식이 App Service 앱에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-224">The same approach works for App Service apps.</span></span> <span data-ttu-id="0ecf1-225">구성 값을 앱 리소스의 자식 리소스로 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-225">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="0ecf1-226">두 개의 웹앱을 다음과 같은 순서로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-226">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="0ecf1-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="0ecf1-227">webapp1</span></span>
2. <span data-ttu-id="0ecf1-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="0ecf1-228">webapp2</span></span>
3. <span data-ttu-id="0ecf1-229">webapp1에 대한 구성이 webapp1 및 webapp2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="0ecf1-230">webapp2의 값을 사용하는 앱 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="0ecf1-231">webapp2에 대한 구성이 webapp1 및 webapp2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="0ecf1-232">webapp1의 값을 사용하는 앱 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0ecf1-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ecf1-233">Next steps</span></span>
* <span data-ttu-id="0ecf1-234">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-234">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="0ecf1-235">감사 작업에 대해 알아보려면 [리소스 관리자로 작업 감사](resource-group-audit.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-235">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="0ecf1-236">배포 중 오류를 확인하는 작업에 대해 알아보려면 [배포 작업 보기](resource-manager-deployment-operations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ecf1-236">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
