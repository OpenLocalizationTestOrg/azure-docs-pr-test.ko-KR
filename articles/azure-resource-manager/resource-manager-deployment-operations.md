---
title: "Azure 리소스 관리자와 aaaDeployment 작업 | Microsoft Docs"
description: "Tooview Azure 리소스 관리자 배포 작업과 hello 하는 방법을 설명 합니다. 포털, PowerShell, Azure CLI 및 REST API입니다."
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
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="81562-103">Azure Resource Manager를 사용한 배포 작업 보기</span><span class="sxs-lookup"><span data-stu-id="81562-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="81562-104">Hello Azure 포털을 통해 배포에 대 한 hello 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="81562-105">이 문서에서는 보기에 실패 한 작업 하므로 배포 하는 동안 오류가 발생를 받은 있을 경우 hello 작업 보기에 가장 관심이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="81562-106">hello 포털 tooeasily 찾기 hello 오류 사용할 수 있는 인터페이스를 제공 하 고 잠재적 수정 사항을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="81562-107">포털</span><span class="sxs-lookup"><span data-stu-id="81562-107">Portal</span></span>
<span data-ttu-id="81562-108">toosee hello 배포 작업 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="81562-109">Hello 배포와 관련 된 hello 리소스 그룹에 대 한 hello 마지막 배포의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="81562-110">자세한 내용은이 상태 tooget를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-110">You can select this status tooget more details.</span></span>
   
    ![배포 상태](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="81562-112">Hello 최근 배포 기록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-112">You see hello recent deployment history.</span></span> <span data-ttu-id="81562-113">실패 한 hello 배포를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-113">Select hello deployment that failed.</span></span>
   
    ![배포 상태](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="81562-115">Hello 링크 toosee 이유에 대 한 설명 hello 배포 실패를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="81562-116">아래 hello 이미지 hello DNS 레코드 고유 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![실패한 배포 보기](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="81562-118">이 오류 메시지는 하면 지원할 수 있어야 하며 toobegin 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="81562-119">그러나 작업이 완료 된에 대 한 자세한 내용은 필요한 경우 단계를 수행 하는 hello와 같이 hello 작업 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="81562-120">Hello에서 모든 hello 배포 작업을 볼 수 있습니다 **배포** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="81562-121">모든 작업 toosee 자세한 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-121">Select any operation toosee more details.</span></span>
   
    ![작업 보기](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="81562-123">이 경우 hello 저장소 계정, 가상 네트워크 및 가용성 집합 성공적으로 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="81562-124">hello 공용 IP 주소 실패 했으며, 기타 리소스를 시도 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="81562-125">선택 하 여 hello 배포에 대 한 이벤트를 볼 수 있습니다 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![이벤트 보기](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="81562-127">Hello 배포에 대 한 모든 hello 이벤트를 보고 자세한 내용을 보려면 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="81562-128">상관 관계 Id를 너무 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="81562-129">배포 기술 지원 tootroubleshoot 작업할 때이 값은 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![이벤트 보기](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="81562-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81562-131">PowerShell</span></span>
1. <span data-ttu-id="81562-132">tooget hello를 사용 하 여 hello 배포의 전반적인 상태 **Get AzureRmResourceGroupDeployment** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="81562-133">또는 실패 한 배포에 대 한 hello 결과 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="81562-134">각 배포에는 여러 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="81562-135">각 작업 hello 배포 프로세스의 단계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81562-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="81562-136">배포와 무엇이 잘못 되었는지 toodiscover, 일반적으로 필요한 hello 배포 작업에 대 한 toosee 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="81562-137">Hello 작업과의 hello 상태를 확인할 수 **Get AzureRmResourceGroupDeploymentOperation**합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="81562-138">각 형식에 따라 hello에 여러 작업을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="81562-139">tooget 실패 한 작업에 대 한 자세한 내용은 사용 하는 작업에 대 한 hello 속성 검색 **실패** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="81562-140">실패 한 작업 형식에 따라 hello 각 하나씩 hello 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81562-140">Which returns all hello failed operations with each one in hello following format:</span></span>

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

    <span data-ttu-id="81562-141">Hello serviceRequestId 및 hello 작업에 대 한 hello trackingId note 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="81562-142">hello serviceRequestId 배포 기술 지원 tootroubleshoot 작업할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="81562-143">특정 작업에 다음 단계 toofocus hello hello trackingId을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="81562-144">특정 실패 한 작업에 다음 명령을 사용 하 여 hello의 tooget hello 상태 메시지:</span><span class="sxs-lookup"><span data-stu-id="81562-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="81562-145">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81562-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="81562-146">Azure의 모든 배포 작업에는 요청 및 응답 콘텐츠가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81562-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="81562-147">콘텐츠를 요청 하는 hello는 보낸 사항 tooAzure 배포 하는 동안 (예를 들어 VM을 만드는 OS 디스크 및 기타 리소스).</span><span class="sxs-lookup"><span data-stu-id="81562-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="81562-148">hello 응답 콘텐츠 배포 요청에서 다시 전송 될 Azure는 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="81562-149">배포 하는 동안 사용할 수 있습니다 **DeploymentDebugLogLevel** hello 요청 및/또는 응답 매개 변수의 toospecify hello 로그에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81562-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="81562-150">Hello 로그에서 해당 정보를 가져오고 hello 다음 PowerShell 명령을 사용 하 여 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="81562-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="81562-151">Azure CLI</span></span>

1. <span data-ttu-id="81562-152">가져오기 hello로 배포의 전반적인 상태를 hello **으로 azure 그룹 배포 쇼** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="81562-153">값을 반환 하는 hello 중 하나는 hello **correlationId**합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="81562-154">이 값은 사용 tootrack 관련 이벤트, 하며 수 할 때 도움이 작동 기술 지원 tootroubleshoot으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="81562-155">배포의 경우 toosee hello 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="81562-156">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="81562-156">REST</span></span>

1. <span data-ttu-id="81562-157">Hello로 배포 하는 방법에 대 한 정보를 가져올 [템플릿 배포에 대 한 정보를 가져올](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="81562-158">Hello에 대 한 응답, 특히 눈여겨 hello **provisioningState**, **correlationId**, 및 **오류** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="81562-159">hello **correlationId** 사용 tootrack 관련 이벤트, 하며 수 할 때 도움이 작동 기술 지원 tootroubleshoot으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="81562-160">Hello 사용 하 여 배포 작업에 대 한 정보를 가져올 [모든 템플릿 배포 작업 나열](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="81562-161">hello에 지정 된 내용에 따라 요청 및/또는 응답 정보를 포함 하는 hello 응답 **debugSetting** 배포 중에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="81562-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="81562-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81562-162">Next steps</span></span>
* <span data-ttu-id="81562-163">특정 배포 오류를 확인 하는 데 도움이 필요 하면 참조 [리소스 tooAzure Azure 리소스 관리자를 배포할 때 일반적인 오류를 해결](resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="81562-164">toolearn hello 활동 사용에 대 한 로그 toomonitor 다른 유형의 작업에서 참조 [활동 보기 로그 toomanage Azure 리소스](resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="81562-165">toovalidate를 실행 하기 전에 배포 참조 [Azure 리소스 관리자 템플릿 사용 하 여 리소스 그룹 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81562-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

