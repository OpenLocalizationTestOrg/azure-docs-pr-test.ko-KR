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
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>리소스 관리자 템플릿과 리소스 관리자 REST API로 리소스 배포
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [포털](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

이 문서에서는 어떻게 toouse hello 리소스 관리자 REST API와 리소스 관리자 템플릿 toodeploy 리소스 tooAzure 설명 합니다.  

> [!TIP]
> 배포 중 발생하는 오류 디버깅에 대한 도움을 받으려면 다음을 참조하세요.
> 
> * [배포 작업을 보려면](resource-manager-deployment-operations.md) toolearn 하는 데 유용한 정보를 가져오는 방법에 대 한 오류 문제 해결
> * [Azure 리소스 관리자 리소스 tooAzure를 배포할 때 일반적인 오류 문제 해결](resource-manager-common-deployment-errors.md) toolearn 어떻게 tooresolve 일반적인 배포 오류
> 
> 

템플릿은 로컬 파일이거나 URI를 통해 사용 가능한 외부 파일일 수 있습니다. 서식 파일에는 저장소 계정에 있는 access toohello 서식 파일을 제한할 수 있으며 공유 액세스 서명 (SAS) 토큰을 배포 하는 동안 제공 수 있습니다.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Hello REST API를 사용 하 여 배포
1. 인증 토큰을 포함하여 [공통 매개 변수 및 헤더](https://docs.microsoft.com/rest/api/index)를 설정합니다.
2. 기본 리소스 그룹이 없는 경우 리소스 그룹을 만듭니다. 구독 ID, hello 이름 hello 새 리소스 그룹 및 솔루션에 필요한 위치를 제공 합니다. 자세한 내용은 [리소스 그룹 만들기](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate)를 참조하세요.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Hello를 실행 하 여 실행 하기 전에 배포 확인 [템플릿 배포의 유효성을 검사](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) 작업 합니다. Hello 배포를 테스트할 때는 하 듯 hello 배포 (hello 다음 단계에 표시)를 실행할 때 매개 변수를 제공 합니다.
4. 배포를 만듭니다. 구독 ID, hello 리소스 그룹의 이름을 hello, hello 배포의 hello 이름 및 링크 tooyour 템플릿을 제공 합니다. Hello 템플릿 파일에 대 한 정보를 참조 하십시오. [매개 변수 파일](#parameter-file)합니다. Hello REST API toocreate 리소스 그룹에 대 한 자세한 내용은 참조 [템플릿 배포를 만드는](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate)합니다. 공지 hello **모드** 너무 설정**증분**합니다. toorun 완전 한 배포 설정 **모드** 너무**완료**합니다. 서식 파일에 있지 않은 리소스를 실수로 삭제할 수 있습니다 때 hello 전체 모드를 사용 하는 경우 주의 해야 합니다.
   
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
   
      Toolog 응답 콘텐츠, 요청 콘텐츠 또는 둘 다를 원하는 경우 포함 **debugSetting** hello 요청에서 합니다.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      공유 액세스 서명 (SAS) 토큰을 저장소 계정 toouse를 설정할 수 있습니다. 자세한 내용은 [공유 액세스 서명을 사용하여 액세스 위임](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)을 참조하세요.
5. Hello 템플릿 배포의 hello 상태를 가져옵니다. 자세한 내용은 [템플릿 배포에 대한 정보 가져오기](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)를 참조하세요.
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>매개 변수 파일 

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>다음 단계
* 비동기 REST 작업을 처리 하는 방법에 대 한 toolearn 참조 [Azure 비동기 작업을 추적](resource-manager-async-operations.md)합니다.
* 리소스를 hello.NET 클라이언트 라이브러리를 통해 배포의 예제를 보려면 [.NET 라이브러리 및 서식 파일을 사용 하 여 리소스를 배포](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* 서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.
* 솔루션 toodifferent 환경 배포에 대 한 지침을 참조 하십시오. [Microsoft Azure에서 개발 및 테스트 환경](solution-dev-test-environments.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

