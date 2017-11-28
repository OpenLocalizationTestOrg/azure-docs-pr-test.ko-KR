---
title: "Azure 배포 오류 aaaUnderstand | Microsoft Docs"
description: "설명 방법을 toolearn Azure 배포 오류에 대 한 합니다."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "배포 오류를 azure 배포 tooazure 배포"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="816d5-104">Azure 배포 오류 이해</span><span class="sxs-lookup"><span data-stu-id="816d5-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="816d5-105">이 항목에서는 배포 오류 및 오류에 대한 자세한 정보를 검색하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="816d5-106">해상도 toocommon 배포 오류에 대 한 참조 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="816d5-107">두 가지 오류 유형</span><span class="sxs-lookup"><span data-stu-id="816d5-107">Two types of errors</span></span>
<span data-ttu-id="816d5-108">두 가지 유형의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="816d5-109">유효성 검사 오류</span><span class="sxs-lookup"><span data-stu-id="816d5-109">validation errors</span></span>
* <span data-ttu-id="816d5-110">배포 오류</span><span class="sxs-lookup"><span data-stu-id="816d5-110">deployment errors</span></span>

<span data-ttu-id="816d5-111">다음 이미지는 hello 구독에 대 한 hello 활동 로그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="816d5-112">또한 두 개의 배포를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-112">It represents two deployments.</span></span> <span data-ttu-id="816d5-113">한 가지 배포 hello 템플릿 유효성 검사를 실패 했습니다. (**유효성 검사**) 및을 계속할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="816d5-114">다른 배포 hello, hello 템플릿 유효성 검사를 통과 했지만 hello 리소스를 만들 때를 실패 했습니다 (**쓰기 배포**).</span><span class="sxs-lookup"><span data-stu-id="816d5-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![오류 코드 표시](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="816d5-116">유효성 검사 오류는 배포 전에 확인할 수 있는 시나리오에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="816d5-117">서식 파일 또는 구독 할당량을 초과 하는 동안 toodeploy 리소스에서 구문 오류가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="816d5-118">배포 오류 hello 배포 프로세스 중 발생 하는 조건에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="816d5-119">동시에 배포 되는 리소스 tooaccess 시도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="816d5-120">두 유형의 오류 tootroubleshoot hello 배포를 사용 하면 오류 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="816d5-121">Hello에 두 유형의 오류 표시 [활동 로그](resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="816d5-122">그러나 hello 배포를 시작 하지 때문에 유효성 검사 오류 배포 기록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="816d5-123">오류 코드 확인</span><span class="sxs-lookup"><span data-stu-id="816d5-123">Determine error code</span></span>

<span data-ttu-id="816d5-124">Hello 오류 메시지와 hello 오류 코드 보고는 오류에 대 한 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="816d5-125">hello [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md) 문서에서는 오류 코드에서 해결 방법을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="816d5-126">이 항목에서는 toouse Azure 포털 toodiscover hello 오류 코드를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="816d5-127">유효성 검사 오류</span><span class="sxs-lookup"><span data-stu-id="816d5-127">Validation errors</span></span>

<span data-ttu-id="816d5-128">Hello 포털을 통해 배포, 실제 값을 제출한 후 유효성 검사 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![포털 유효성 검사 오류 표시](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="816d5-130">자세한 내용은 hello 메시지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-130">Select hello message for more details.</span></span> <span data-ttu-id="816d5-131">표시 된 다음 이미지는 hello에서 프로그램 **InvalidTemplateDeployment** 오류 및 정책을 나타내는 메시지는 배포를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![유효성 검사 세부 정보 표시](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="816d5-133">배포 오류</span><span class="sxs-lookup"><span data-stu-id="816d5-133">Deployment errors</span></span>

<span data-ttu-id="816d5-134">Hello 작업이 유효성 검사에 성공 했지만 배포 중에 실패 하면, hello 오류 hello 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="816d5-135">Hello 알림을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-135">Select hello notification.</span></span>

![알림 오류](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="816d5-137">Hello 배포에 대 한 자세한 내용은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-137">You see more details about hello deployment.</span></span> <span data-ttu-id="816d5-138">Hello 옵션 toofind hello 오류에 대 한 자세한 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-138">Select hello option toofind more information about hello error.</span></span>

![배포 실패](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="816d5-140">Hello 오류 메시지 및 오류 코드를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-140">You see hello error message and error codes.</span></span> <span data-ttu-id="816d5-141">두 개의 오류 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-141">Notice there are two error codes.</span></span> <span data-ttu-id="816d5-142">첫 번째 오류 코드 hello (**DeploymentFailed**)은 hello 있습니다를 세부 정보를 제공 하지 않는 일반 오류가 필요한 toosolve hello 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="816d5-143">두 번째 오류 코드 hello (**StorageAccountNotFound**) 해야 하는 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![오류 세부 정보](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="816d5-145">디버그 로깅 활성화</span><span class="sxs-lookup"><span data-stu-id="816d5-145">Enable debug logging</span></span>
<span data-ttu-id="816d5-146">경우에 따라 필요한 요청 및 응답 toodiscover hello에 대 한 자세한 내용은 무엇이 잘못 되었는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="816d5-147">PowerShell 또는 Azure CLI를 사용하여, 배포 중에 추가 정보가 기록되도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="816d5-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="816d5-148">PowerShell</span></span>

   <span data-ttu-id="816d5-149">PowerShell에서 hello 설정 **DeploymentDebugLogLevel** 매개 변수 tooAll, ResponseContent, 또는 RequestContent 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="816d5-150">Cmdlet을 다음 hello로 콘텐츠를 요청 하는 hello 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="816d5-151">또는 응답 콘텐츠를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="816d5-152">이 정보를 사용 하 여부 hello 서식 파일의 값이 잘못 설정 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="816d5-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="816d5-153">Azure CLI</span></span>

   <span data-ttu-id="816d5-154">다음 명령을 hello로 hello 배포 작업을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="816d5-155">중첩된 템플릿</span><span class="sxs-lookup"><span data-stu-id="816d5-155">Nested template</span></span>

   <span data-ttu-id="816d5-156">중첩 된 템플릿 사용 하 여 hello에 대 한 디버그 정보 toolog **debugSetting** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="816d5-157">문제 해결 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="816d5-157">Create a troubleshooting template</span></span>
<span data-ttu-id="816d5-158">경우에 따라 가장 쉬운 방법은 tootroubleshoot hello 서식 파일에는 양식의 tootest 일부분입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="816d5-159">사용 하면 하는 간단한 템플릿을 toofocus hello 오류를 일으키는 확신 하는 hello 부분에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="816d5-160">예를 들어, 리소스를 참조할 때 오류가 발생한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="816d5-161">전체 서식 파일을 처리 하는 대신 문제를 일으킬 수 있는 hello 부분을 반환 하는 서식 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="816d5-162">인지를 결정에서 전달 하는 hello 오른쪽 매개 변수를 올바르게 템플릿 함수를 사용 하 여 원하는 hello 리소스를 가져오지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="816d5-163">또는 tooincorrectly 종속성을 설정 하 여 관련 확신 하는 배포 오류를 발생 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="816d5-164">간소화된 템플릿을 분리하여 템플릿을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="816d5-165">먼저 단일 리소스(예: SQL Server)를 배포하는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="816d5-166">리소스가 올바르게 정의된 것이 확실하면 종속되는 리소스(예: SQL Database)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="816d5-167">이러한 두 리소스가 올바르게 정의되어 있으면 다른 종속 리소스(예: 감사 정책)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="816d5-168">각 테스트 배포 사이 hello 리소스 그룹 toomake 있는지 하면 적절 하 게 테스트 hello 종속성을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="816d5-169">배포 시퀀스 확인</span><span class="sxs-lookup"><span data-stu-id="816d5-169">Check deployment sequence</span></span>

<span data-ttu-id="816d5-170">대부분의 배포 오류는 예상치 않은 시퀀스로 리소스가 배포될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="816d5-171">이러한 오류는 종속성이 올바르게 설정되지 않은 경우 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="816d5-172">필요한 종속성 누락 toouse hello 다른 있지만 다른 리소스에 대 한 값이 아직 존재 하지 않는 한 리소스 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="816d5-173">리소스를 찾을 수 없다는 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="816d5-174">이러한 종류의 오류를 일시적으로 발생할 수 있습니다 각 리소스에 대 한 hello 배포 시간이 다를 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="816d5-175">예를 들어 첫 번째 시도가 toodeploy 사용자 리소스 있으므로 성공 필요한 리소스는 임의로 시간 내에 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="816d5-176">그러나 두 번째 시도 hello 리소스 시간에 완료 되지 않았습니다 필요 하기 때문에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="816d5-177">하지만 원하는 필요 하지 않은 tooavoid 종속성 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="816d5-178">불필요 한 종속성이 있는를 병렬로 배포할 서로 종속 되지 않는 리소스를 방지 하 여 hello 배포 hello 기간을 연장 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="816d5-179">또한 hello 배포를 차단 하는 순환 종속성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="816d5-180">hello [참조](resource-group-template-functions-resource.md#reference) 함수 hello에 해당 리소스 배포 되 면 hello 참조 된 리소스에 대해 암시적 종속성을 만듭니다 같은 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="816d5-181">따라서 hello에 지정 된 hello 종속성 보다 더 많은 종속성을 할 수 **dependsOn** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="816d5-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) 함수 암시적 종속성이 생성 되지 않거나 hello 리소스 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="816d5-183">종속성 문제를 발생 하면 리소스 배포의 hello 순서 toogain 통찰력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="816d5-184">배포 작업의 tooview hello 순서:</span><span class="sxs-lookup"><span data-stu-id="816d5-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="816d5-185">리소스 그룹에 대 한 배포 기록을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-185">Select hello deployment history for your resource group.</span></span>

   ![배포 기록 선택](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="816d5-187">Hello 기록에서 배포를 선택 하 고 선택 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![배포 이벤트 선택](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="816d5-189">각 리소스에 대 한 이벤트의 hello 시퀀스를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="816d5-190">각 작업의 toohello 상태 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="816d5-191">예를 들어 hello 다음 이미지에서는 배포는 세 개의 저장소 계정을 동시에</span><span class="sxs-lookup"><span data-stu-id="816d5-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="816d5-192">Hello에 시작 되는 3 개의 저장소 계정이 hello는 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![병렬 배포](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="816d5-194">hello 다음 이미지에는 동시에 배포 되는 3 개의 저장소 계정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="816d5-195">두 번째 저장소 계정의 hello hello 첫 번째는 저장소 계정에 따라 달라 집니다 및 hello 세 번째 저장소 계정의 hello 두 번째 저장소 계정에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="816d5-196">따라서 hello 첫 저장소 계정은 시작 수락 있고, 다음 hello를 시작 하기 전에 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![순차 배포](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="816d5-198">더 복잡 한 시나리오에 대해서도 사용할 수 있습니다 배포 시작 되 고 각 리소스에 대해 완료 된 경우 동일한 기술을 toodiscover hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="816d5-199">Hello 시퀀스 예상과 다른 경우 배포 이벤트 toosee를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="816d5-200">이 경우에이 리소스에 대 한 hello 종속성 다시 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="816d5-201">Resource Manager는 템플릿의 유효성을 검사하는 동안 순환적 종속성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="816d5-202">순환 종속성이 존재한다고 구체적으로 언급하는 오류 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="816d5-203">toosolve 순환 종속성:</span><span class="sxs-lookup"><span data-stu-id="816d5-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="816d5-204">서식 파일에서 순환 종속성이 hello에서 식별 된 hello 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="816d5-205">해당 리소스에 대 한 검사 hello **dependsOn** 속성 및 hello의 사용이 **참조** toosee 리소스에 따라 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="816d5-206">이러한 리소스 toosee에 종속 리소스를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="816d5-207">Hello 원래 리소스에 의존 하는 리소스를 확인할 때까지 hello 종속성을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="816d5-208">순환 종속성이 hello에 관련 된 hello 리소스에 대 한 hello 사용 되는 모든 신중 하 게 검사 **dependsOn** 속성 tooidentify 필요 하지 않은 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="816d5-209">그러한 종속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-209">Remove those dependencies.</span></span> <span data-ttu-id="816d5-210">종속성이 필요한지 확신이 안되면 해당 종속성을 제거해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="816d5-211">Hello 템플릿을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-211">Redeploy hello template.</span></span>

<span data-ttu-id="816d5-212">Hello에서 값을 제거 **dependsOn** 속성 hello 서식 파일을 배포할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="816d5-213">오류가 발생 하는 경우 hello 템플릿으로 hello 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="816d5-214">이 방법 hello 순환 종속성을 해결 되지 않으면, 배포 논리의 일부로 자식 리소스 (예: 확장 또는 구성 설정)로 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="816d5-215">Hello 리소스 hello 순환 종속성에 관련 된 후 해당 자식 리소스 toodeploy를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="816d5-216">예를 들어, 두 가상 컴퓨터를 배포 하는 하지만 다른 toohello 참조 하는 각 항목에 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="816d5-217">순서에 따라 hello에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="816d5-218">vm1</span><span class="sxs-lookup"><span data-stu-id="816d5-218">vm1</span></span>
2. <span data-ttu-id="816d5-219">vm2</span><span class="sxs-lookup"><span data-stu-id="816d5-219">vm2</span></span>
3. <span data-ttu-id="816d5-220">vm1의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="816d5-221">hello 확장 v m 2에서 가져오는 v m 1의 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="816d5-222">vm2의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="816d5-223">hello 확장 v m 1에서 가져오는 v m 2에 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="816d5-224">앱 서비스 앱에 대 한 동일한 접근 방식은 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="816d5-225">구성 값 hello 응용 프로그램 리소스의 자식 리소스를 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="816d5-226">순서에 따라 hello에서 두 개의 웹 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="816d5-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="816d5-227">webapp1</span></span>
2. <span data-ttu-id="816d5-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="816d5-228">webapp2</span></span>
3. <span data-ttu-id="816d5-229">webapp1에 대한 구성이 webapp1 및 webapp2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="816d5-230">webapp2의 값을 사용하는 앱 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="816d5-231">webapp2에 대한 구성이 webapp1 및 webapp2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="816d5-232">webapp1의 값을 사용하는 앱 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="816d5-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="816d5-233">Next steps</span></span>
* <span data-ttu-id="816d5-234">해상도 toocommon 배포 오류에 대 한 참조 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="816d5-235">작업을 감사 하는 방법에 대 한 toolearn 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="816d5-236">배포 하는 동안 작업 toodetermine hello 오류에 대 한 toolearn 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="816d5-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
