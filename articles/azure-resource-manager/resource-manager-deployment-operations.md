---
title: "Azure Resource Manager를 사용한 배포 작업 | Microsoft Docs"
description: "포털, PowerShell, Azure CLI 및 REST API를 사용하여 Azure Resource Manager 배포 작업을 확인하는 방법을 설명합니다."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="523bf-103">Azure Resource Manager를 사용한 배포 작업 보기</span><span class="sxs-lookup"><span data-stu-id="523bf-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="523bf-104">Azure 포털을 통해 배포에 대한 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="523bf-105">배포 중에 오류가 나타날 때 작업을 보는 데 가장 많은 관심을 가질 수 있으므로 이 문서에서는 실패한 작업을 보는 것에 대해 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="523bf-106">포털은 쉽게 오류를 찾고 잠재적 해결 방법을 확인할 수 있는 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="523bf-107">포털</span><span class="sxs-lookup"><span data-stu-id="523bf-107">Portal</span></span>
<span data-ttu-id="523bf-108">배포 작업을 확인하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="523bf-109">배포에 관련된 리소스 그룹에 대해 마지막 배포의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="523bf-110">이 상태를 선택하여 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-110">You can select this status to get more details.</span></span>
   
    ![배포 상태](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="523bf-112">최근 배포 기록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-112">You see the recent deployment history.</span></span> <span data-ttu-id="523bf-113">실패한 배포를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-113">Select the deployment that failed.</span></span>
   
    ![배포 상태](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="523bf-115">배포에 실패한 이유에 대한 설명을 보려면 링크를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="523bf-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="523bf-116">아래 이미지에서 DNS 레코드는 고유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![실패한 배포 보기](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="523bf-118">이 오류 메시지는 문제 해결을 시작하는 데 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="523bf-119">그러나 어떤 작업이 완료되었는지에 대한 추가 정보가 필요한 경우 다음 단계에 표시된 대로 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="523bf-120">**배포** 블레이드에서 모든 배포 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="523bf-121">보다 자세한 정보를 확인하려면 원하는 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-121">Select any operation to see more details.</span></span>
   
    ![작업 보기](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="523bf-123">이 경우 저장소 계정, 가상 네트워크 및 가용성 집합이 성공적으로 만들어진 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="523bf-124">공용 IP 주소가 실패했고 다른 리소스를 시도하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="523bf-125">**이벤트**를 선택하여 배포에 대한 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![이벤트 보기](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="523bf-127">배포에 대한 모든 이벤트가 표시되면 하나 이상의 세부 정보를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="523bf-128">상관 관계 ID도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="523bf-129">이 값은 배포 문제를 해결하기 위해 기술 지원부와 협력할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![이벤트 보기](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="523bf-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="523bf-131">PowerShell</span></span>
1. <span data-ttu-id="523bf-132">배포의 전반적인 상태를 가져오려면 **Get-AzureRmResourceGroupDeployment** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="523bf-133">또는 실패한 배포에 대해서만 결과를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="523bf-134">각 배포에는 여러 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="523bf-135">각 작업은 배포 프로세스의 단계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="523bf-136">배포에서 무엇이 잘못 되었는지 검색하려면 일반적으로 배포 작업에 대한 세부 정보를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="523bf-137">**Get-AzureRmResourceGroupDeploymentOperation**을 사용하여 작업의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="523bf-138">여러 작업이 각각 다음과 같은 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="523bf-139">실패한 작업에 대한 자세한 정보를 얻으려면 상태가 **Failed** 인 작업에 대한 속성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="523bf-140">모든 실패한 작업이 각각 다음과 같은 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-140">Which returns all the failed operations with each one in the following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="523bf-141">작업의 serviceRequestId 및 trackingId를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="523bf-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="523bf-142">serviceRequestId는 기술 지원과 함께 배포 문제를 해결할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="523bf-143">특정 작업에 집중하기 위해 trackingId는 다음 단계에서 사용할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="523bf-144">특정 실패한 작업에 대한 상태 메시지를 얻으려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="523bf-145">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="523bf-146">Azure의 모든 배포 작업에는 요청 및 응답 콘텐츠가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="523bf-147">요청 콘텐츠는 배포하는 동안 Azure에 보낸 콘텐츠입니다(예: VM, OS 디스크 및 기타 리소스).</span><span class="sxs-lookup"><span data-stu-id="523bf-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="523bf-148">응답 콘텐츠는 Azure가 배포 요청에서 다시 보낸 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="523bf-149">배포하는 동안 **DeploymentDebugLogLevel** 매개 변수를 사용하여 요청 및/또는 응답을 로그에 보존하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="523bf-150">로그에서 해당 정보를 가져오고 다음 PowerShell 명령을 사용하여 로컬에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="523bf-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="523bf-151">Azure CLI</span></span>

1. <span data-ttu-id="523bf-152">**azure group deployment show** 명령을 사용하여 배포의 전반적인 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="523bf-153">반환되는 값 중 하나는 **correlationId**입니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="523bf-154">이 값은 관련 이벤트를 추적하는 데 사용되며 기술 지원과 함께 배포 문제를 해결할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="523bf-155">배포의 작업을 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="523bf-156">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="523bf-156">REST</span></span>

1. <span data-ttu-id="523bf-157">[템플릿 배포에 대한 정보 가져오기](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) 작업을 사용하여 배포에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="523bf-158">응답에서 **provisioningState** , **correlationId** 및 **error** 요소에 특히 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="523bf-159">**correlationId** 는 관련 이벤트를 추적하는 데 사용되며 기술 지원과 함께 배포 문제를 해결할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="523bf-160">[모든 템플릿 배포 작업 나열](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) 작업을 사용하여 배포 작업에 대한 정보를 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="523bf-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="523bf-161">응답에는 배포 중에 **debugSetting** 속성에 지정하는 설정을 기준으로 요청 및/또는 응답 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="523bf-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="523bf-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="523bf-162">Next steps</span></span>
* <span data-ttu-id="523bf-163">특정 배포 오류에 대한 도움말은 [Azure Resource Manager를 사용하여 Azure에 리소스를 배포할 때 발생한 일반적인 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523bf-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="523bf-164">활동 로그를 사용하여 다른 유형의 작업을 모니터링하는 방법에 대해 알아보려면 [활동 로그를 보고 Azure 리소스 관리](resource-group-audit.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523bf-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="523bf-165">실행하기 전에 배포의 유효성을 검사하려면 [Azure Resource Manager 템플릿을 사용하여 리소스 그룹 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523bf-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

