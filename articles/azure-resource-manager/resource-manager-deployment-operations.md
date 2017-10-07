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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Azure Resource Manager를 사용한 배포 작업 보기


Hello Azure 포털을 통해 배포에 대 한 hello 작업을 볼 수 있습니다. 이 문서에서는 보기에 실패 한 작업 하므로 배포 하는 동안 오류가 발생를 받은 있을 경우 hello 작업 보기에 가장 관심이 수 있습니다. hello 포털 tooeasily 찾기 hello 오류 사용할 수 있는 인터페이스를 제공 하 고 잠재적 수정 사항을 결정 합니다.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>포털
toosee hello 배포 작업 단계를 수행 하는 hello를 사용 합니다.

1. Hello 배포와 관련 된 hello 리소스 그룹에 대 한 hello 마지막 배포의 hello 상태를 확인 합니다. 자세한 내용은이 상태 tooget를 선택할 수 있습니다.
   
    ![배포 상태](./media/resource-manager-deployment-operations/deployment-status.png)
2. Hello 최근 배포 기록을 표시 합니다. 실패 한 hello 배포를 선택 합니다.
   
    ![배포 상태](./media/resource-manager-deployment-operations/select-deployment.png)
3. Hello 링크 toosee 이유에 대 한 설명 hello 배포 실패를 선택 합니다. 아래 hello 이미지 hello DNS 레코드 고유 하지 않습니다.  
   
    ![실패한 배포 보기](./media/resource-manager-deployment-operations/view-error.png)
   
    이 오류 메시지는 하면 지원할 수 있어야 하며 toobegin 문제를 해결 합니다. 그러나 작업이 완료 된에 대 한 자세한 내용은 필요한 경우 단계를 수행 하는 hello와 같이 hello 작업 볼 수 있습니다.
4. Hello에서 모든 hello 배포 작업을 볼 수 있습니다 **배포** 블레이드입니다. 모든 작업 toosee 자세한 세부 정보를 선택 합니다.
   
    ![작업 보기](./media/resource-manager-deployment-operations/view-operations.png)
   
    이 경우 hello 저장소 계정, 가상 네트워크 및 가용성 집합 성공적으로 만들어졌는지 확인할 수 있습니다. hello 공용 IP 주소 실패 했으며, 기타 리소스를 시도 하지 않았습니다.
5. 선택 하 여 hello 배포에 대 한 이벤트를 볼 수 있습니다 **이벤트**합니다.
   
    ![이벤트 보기](./media/resource-manager-deployment-operations/view-events.png)
6. Hello 배포에 대 한 모든 hello 이벤트를 보고 자세한 내용을 보려면 하나를 선택 합니다. 상관 관계 Id를 너무 hello를 확인 합니다. 배포 기술 지원 tootroubleshoot 작업할 때이 값은 유용할 수 있습니다.
   
    ![이벤트 보기](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget hello를 사용 하 여 hello 배포의 전반적인 상태 **Get AzureRmResourceGroupDeployment** 명령입니다. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   또는 실패 한 배포에 대 한 hello 결과 필터링 할 수 있습니다.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. 각 배포에는 여러 작업이 포함되어 있습니다. 각 작업 hello 배포 프로세스의 단계를 나타냅니다. 배포와 무엇이 잘못 되었는지 toodiscover, 일반적으로 필요한 hello 배포 작업에 대 한 toosee 세부 정보입니다. Hello 작업과의 hello 상태를 확인할 수 **Get AzureRmResourceGroupDeploymentOperation**합니다.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    각 형식에 따라 hello에 여러 작업을 반환 합니다.

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget 실패 한 작업에 대 한 자세한 내용은 사용 하는 작업에 대 한 hello 속성 검색 **실패** 상태입니다.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    실패 한 작업 형식에 따라 hello 각 하나씩 hello 모두 반환 됩니다.

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

    Hello serviceRequestId 및 hello 작업에 대 한 hello trackingId note 합니다. hello serviceRequestId 배포 기술 지원 tootroubleshoot 작업할 때 유용할 수 있습니다. 특정 작업에 다음 단계 toofocus hello hello trackingId을 사용 합니다.
4. 특정 실패 한 작업에 다음 명령을 사용 하 여 hello의 tooget hello 상태 메시지:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    반환하는 내용은 다음과 같습니다.

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Azure의 모든 배포 작업에는 요청 및 응답 콘텐츠가 포함됩니다. 콘텐츠를 요청 하는 hello는 보낸 사항 tooAzure 배포 하는 동안 (예를 들어 VM을 만드는 OS 디스크 및 기타 리소스). hello 응답 콘텐츠 배포 요청에서 다시 전송 될 Azure는 합니다. 배포 하는 동안 사용할 수 있습니다 **DeploymentDebugLogLevel** hello 요청 및/또는 응답 매개 변수의 toospecify hello 로그에 유지 됩니다. 

  Hello 로그에서 해당 정보를 가져오고 hello 다음 PowerShell 명령을 사용 하 여 로컬로 저장 합니다.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Azure CLI

1. 가져오기 hello로 배포의 전반적인 상태를 hello **으로 azure 그룹 배포 쇼** 명령입니다.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  값을 반환 하는 hello 중 하나는 hello **correlationId**합니다. 이 값은 사용 tootrack 관련 이벤트, 하며 수 할 때 도움이 작동 기술 지원 tootroubleshoot으로 배포 합니다.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. 배포의 경우 toosee hello 작업을 사용 합니다.

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST (영문)

1. Hello로 배포 하는 방법에 대 한 정보를 가져올 [템플릿 배포에 대 한 정보를 가져올](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) 작업 합니다.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    Hello에 대 한 응답, 특히 눈여겨 hello **provisioningState**, **correlationId**, 및 **오류** 요소입니다. hello **correlationId** 사용 tootrack 관련 이벤트, 하며 수 할 때 도움이 작동 기술 지원 tootroubleshoot으로 배포 합니다.

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

2. Hello 사용 하 여 배포 작업에 대 한 정보를 가져올 [모든 템플릿 배포 작업 나열](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) 작업 합니다. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    hello에 지정 된 내용에 따라 요청 및/또는 응답 정보를 포함 하는 hello 응답 **debugSetting** 배포 중에 속성입니다.

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


## <a name="next-steps"></a>다음 단계
* 특정 배포 오류를 확인 하는 데 도움이 필요 하면 참조 [리소스 tooAzure Azure 리소스 관리자를 배포할 때 일반적인 오류를 해결](resource-manager-common-deployment-errors.md)합니다.
* toolearn hello 활동 사용에 대 한 로그 toomonitor 다른 유형의 작업에서 참조 [활동 보기 로그 toomanage Azure 리소스](resource-group-audit.md)합니다.
* toovalidate를 실행 하기 전에 배포 참조 [Azure 리소스 관리자 템플릿 사용 하 여 리소스 그룹 배포](resource-group-template-deploy.md)합니다.

