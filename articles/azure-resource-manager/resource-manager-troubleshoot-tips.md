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
# <a name="understand-azure-deployment-errors"></a>Azure 배포 오류 이해
이 항목에서는 배포 오류 및 오류에 대한 자세한 정보를 검색하는 방법을 설명합니다. 해상도 toocommon 배포 오류에 대 한 참조 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.

## <a name="two-types-of-errors"></a>두 가지 오류 유형
두 가지 유형의 오류가 발생할 수 있습니다.

* 유효성 검사 오류
* 배포 오류

다음 이미지는 hello 구독에 대 한 hello 활동 로그를 보여 줍니다. 또한 두 개의 배포를 나타냅니다. 한 가지 배포 hello 템플릿 유효성 검사를 실패 했습니다. (**유효성 검사**) 및을 계속할 수 없습니다. 다른 배포 hello, hello 템플릿 유효성 검사를 통과 했지만 hello 리소스를 만들 때를 실패 했습니다 (**쓰기 배포**). 

![오류 코드 표시](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

유효성 검사 오류는 배포 전에 확인할 수 있는 시나리오에서 발생합니다. 서식 파일 또는 구독 할당량을 초과 하는 동안 toodeploy 리소스에서 구문 오류가 포함 됩니다. 배포 오류 hello 배포 프로세스 중 발생 하는 조건에서 발생 합니다. 동시에 배포 되는 리소스 tooaccess 시도 포함 됩니다.

두 유형의 오류 tootroubleshoot hello 배포를 사용 하면 오류 코드가 반환 됩니다. Hello에 두 유형의 오류 표시 [활동 로그](resource-group-audit.md)합니다. 그러나 hello 배포를 시작 하지 때문에 유효성 검사 오류 배포 기록에 표시 되지 않습니다.

## <a name="determine-error-code"></a>오류 코드 확인

Hello 오류 메시지와 hello 오류 코드 보고는 오류에 대 한 배울 수 있습니다. hello [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md) 문서에서는 오류 코드에서 해결 방법을 나열 합니다. 이 항목에서는 toouse Azure 포털 toodiscover hello 오류 코드를 hello 하는 방법을 보여 줍니다.

### <a name="validation-errors"></a>유효성 검사 오류

Hello 포털을 통해 배포, 실제 값을 제출한 후 유효성 검사 오류가 표시 됩니다.

![포털 유효성 검사 오류 표시](./media/resource-manager-troubleshoot-tips/validation-error.png)

자세한 내용은 hello 메시지를 선택 합니다. 표시 된 다음 이미지는 hello에서 프로그램 **InvalidTemplateDeployment** 오류 및 정책을 나타내는 메시지는 배포를 차단 합니다.

![유효성 검사 세부 정보 표시](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>배포 오류

Hello 작업이 유효성 검사에 성공 했지만 배포 중에 실패 하면, hello 오류 hello 알림이 표시 됩니다. Hello 알림을 선택 합니다.

![알림 오류](./media/resource-manager-troubleshoot-tips/notification.png)

Hello 배포에 대 한 자세한 내용은 참조 합니다. Hello 옵션 toofind hello 오류에 대 한 자세한 정보를 선택 합니다.

![배포 실패](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Hello 오류 메시지 및 오류 코드를 참조 합니다. 두 개의 오류 코드가 있습니다. 첫 번째 오류 코드 hello (**DeploymentFailed**)은 hello 있습니다를 세부 정보를 제공 하지 않는 일반 오류가 필요한 toosolve hello 오류입니다. 두 번째 오류 코드 hello (**StorageAccountNotFound**) 해야 하는 hello 세부 정보를 제공 합니다. 

![오류 세부 정보](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>디버그 로깅 활성화
경우에 따라 필요한 요청 및 응답 toodiscover hello에 대 한 자세한 내용은 무엇이 잘못 되었는지 합니다. PowerShell 또는 Azure CLI를 사용하여, 배포 중에 추가 정보가 기록되도록 요청할 수 있습니다.

- PowerShell

   PowerShell에서 hello 설정 **DeploymentDebugLogLevel** 매개 변수 tooAll, ResponseContent, 또는 RequestContent 합니다.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Cmdlet을 다음 hello로 콘텐츠를 요청 하는 hello 없는지 확인 합니다.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   또는 응답 콘텐츠를 환영 합니다.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   이 정보를 사용 하 여부 hello 서식 파일의 값이 잘못 설정 확인할 수 있습니다.

- Azure CLI

   다음 명령을 hello로 hello 배포 작업을 검토 합니다.

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- 중첩된 템플릿

   중첩 된 템플릿 사용 하 여 hello에 대 한 디버그 정보 toolog **debugSetting** 요소입니다.

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


## <a name="create-a-troubleshooting-template"></a>문제 해결 템플릿 만들기
경우에 따라 가장 쉬운 방법은 tootroubleshoot hello 서식 파일에는 양식의 tootest 일부분입니다. 사용 하면 하는 간단한 템플릿을 toofocus hello 오류를 일으키는 확신 하는 hello 부분에 만들 수 있습니다. 예를 들어, 리소스를 참조할 때 오류가 발생한다고 가정합니다. 전체 서식 파일을 처리 하는 대신 문제를 일으킬 수 있는 hello 부분을 반환 하는 서식 파일을 만듭니다. 인지를 결정에서 전달 하는 hello 오른쪽 매개 변수를 올바르게 템플릿 함수를 사용 하 여 원하는 hello 리소스를 가져오지 파악할 수 있습니다.

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

또는 tooincorrectly 종속성을 설정 하 여 관련 확신 하는 배포 오류를 발생 하는 가정 합니다. 간소화된 템플릿을 분리하여 템플릿을 테스트합니다. 먼저 단일 리소스(예: SQL Server)를 배포하는 템플릿을 만듭니다. 리소스가 올바르게 정의된 것이 확실하면 종속되는 리소스(예: SQL Database)를 추가합니다. 이러한 두 리소스가 올바르게 정의되어 있으면 다른 종속 리소스(예: 감사 정책)를 추가합니다. 각 테스트 배포 사이 hello 리소스 그룹 toomake 있는지 하면 적절 하 게 테스트 hello 종속성을 삭제 합니다. 

## <a name="check-deployment-sequence"></a>배포 시퀀스 확인

대부분의 배포 오류는 예상치 않은 시퀀스로 리소스가 배포될 때 발생합니다. 이러한 오류는 종속성이 올바르게 설정되지 않은 경우 발생합니다. 필요한 종속성 누락 toouse hello 다른 있지만 다른 리소스에 대 한 값이 아직 존재 하지 않는 한 리소스 시도 합니다. 리소스를 찾을 수 없다는 오류가 표시됩니다. 이러한 종류의 오류를 일시적으로 발생할 수 있습니다 각 리소스에 대 한 hello 배포 시간이 다를 수 있으므로 합니다. 예를 들어 첫 번째 시도가 toodeploy 사용자 리소스 있으므로 성공 필요한 리소스는 임의로 시간 내에 완료 합니다. 그러나 두 번째 시도 hello 리소스 시간에 완료 되지 않았습니다 필요 하기 때문에 실패 합니다. 

하지만 원하는 필요 하지 않은 tooavoid 종속성 설정 합니다. 불필요 한 종속성이 있는를 병렬로 배포할 서로 종속 되지 않는 리소스를 방지 하 여 hello 배포 hello 기간을 연장 합니다. 또한 hello 배포를 차단 하는 순환 종속성을 만들 수 있습니다. hello [참조](resource-group-template-functions-resource.md#reference) 함수 hello에 해당 리소스 배포 되 면 hello 참조 된 리소스에 대해 암시적 종속성을 만듭니다 같은 서식 파일입니다. 따라서 hello에 지정 된 hello 종속성 보다 더 많은 종속성을 할 수 **dependsOn** 속성입니다. hello [resourceId](resource-group-template-functions-resource.md#resourceid) 함수 암시적 종속성이 생성 되지 않거나 hello 리소스 있는지 확인 합니다.

종속성 문제를 발생 하면 리소스 배포의 hello 순서 toogain 통찰력이 필요 합니다. 배포 작업의 tooview hello 순서:

1. 리소스 그룹에 대 한 배포 기록을 hello를 선택 합니다.

   ![배포 기록 선택](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Hello 기록에서 배포를 선택 하 고 선택 **이벤트**합니다.

   ![배포 이벤트 선택](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. 각 리소스에 대 한 이벤트의 hello 시퀀스를 검사 합니다. 각 작업의 toohello 상태 주의 해야 합니다. 예를 들어 hello 다음 이미지에서는 배포는 세 개의 저장소 계정을 동시에 Hello에 시작 되는 3 개의 저장소 계정이 hello는 같은 시간입니다.

   ![병렬 배포](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   hello 다음 이미지에는 동시에 배포 되는 3 개의 저장소 계정을 보여 줍니다. 두 번째 저장소 계정의 hello hello 첫 번째는 저장소 계정에 따라 달라 집니다 및 hello 세 번째 저장소 계정의 hello 두 번째 저장소 계정에 따라 달라 집니다. 따라서 hello 첫 저장소 계정은 시작 수락 있고, 다음 hello를 시작 하기 전에 완료 되었습니다.

   ![순차 배포](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

더 복잡 한 시나리오에 대해서도 사용할 수 있습니다 배포 시작 되 고 각 리소스에 대해 완료 된 경우 동일한 기술을 toodiscover hello 합니다. Hello 시퀀스 예상과 다른 경우 배포 이벤트 toosee를 조사 합니다. 이 경우에이 리소스에 대 한 hello 종속성 다시 평가 합니다.

Resource Manager는 템플릿의 유효성을 검사하는 동안 순환적 종속성을 식별합니다. 순환 종속성이 존재한다고 구체적으로 언급하는 오류 메시지가 반환됩니다. toosolve 순환 종속성:

1. 서식 파일에서 순환 종속성이 hello에서 식별 된 hello 리소스를 찾습니다. 
2. 해당 리소스에 대 한 검사 hello **dependsOn** 속성 및 hello의 사용이 **참조** toosee 리소스에 따라 작동 합니다. 
3. 이러한 리소스 toosee에 종속 리소스를 검사 합니다. Hello 원래 리소스에 의존 하는 리소스를 확인할 때까지 hello 종속성을 따릅니다.
5. 순환 종속성이 hello에 관련 된 hello 리소스에 대 한 hello 사용 되는 모든 신중 하 게 검사 **dependsOn** 속성 tooidentify 필요 하지 않은 종속성입니다. 그러한 종속성을 제거합니다. 종속성이 필요한지 확신이 안되면 해당 종속성을 제거해 봅니다. 
6. Hello 템플릿을 다시 배포 합니다.

Hello에서 값을 제거 **dependsOn** 속성 hello 서식 파일을 배포할 때 오류가 발생할 수 있습니다. 오류가 발생 하는 경우 hello 템플릿으로 hello 종속성을 추가 합니다. 

이 방법 hello 순환 종속성을 해결 되지 않으면, 배포 논리의 일부로 자식 리소스 (예: 확장 또는 구성 설정)로 이동 하는 것이 좋습니다. Hello 리소스 hello 순환 종속성에 관련 된 후 해당 자식 리소스 toodeploy를 구성 합니다. 예를 들어, 두 가상 컴퓨터를 배포 하는 하지만 다른 toohello 참조 하는 각 항목에 속성을 설정 해야 합니다. 순서에 따라 hello에 배포할 수 있습니다.

1. vm1
2. vm2
3. vm1의 확장은 vm1 및 vm2에 종속됩니다. hello 확장 v m 2에서 가져오는 v m 1의 값을 설정 합니다.
4. vm2의 확장은 vm1 및 vm2에 종속됩니다. hello 확장 v m 1에서 가져오는 v m 2에 값을 설정 합니다.

앱 서비스 앱에 대 한 동일한 접근 방식은 번호입니다. 구성 값 hello 응용 프로그램 리소스의 자식 리소스를 이동 하는 것이 좋습니다. 순서에 따라 hello에서 두 개의 웹 앱을 배포할 수 있습니다.

1. webapp1
2. webapp2
3. webapp1에 대한 구성이 webapp1 및 webapp2에 종속됩니다. webapp2의 값을 사용하는 앱 설정이 포함됩니다.
4. webapp2에 대한 구성이 webapp1 및 webapp2에 종속됩니다. webapp1의 값을 사용하는 앱 설정이 포함됩니다.


## <a name="next-steps"></a>다음 단계
* 해상도 toocommon 배포 오류에 대 한 참조 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.
* 작업을 감사 하는 방법에 대 한 toolearn 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.
* 배포 하는 동안 작업 toodetermine hello 오류에 대 한 toolearn 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.
