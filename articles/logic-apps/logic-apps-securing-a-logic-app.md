---
title: "aaaSecure tooAzure 논리 앱에 액세스 | Microsoft Docs"
description: "보안 액세스 tootriggers, 입력 및 출력, 동작 매개 변수 및 Azure 논리 앱에서 워크플로로 사용 되는 서비스를 보호 하기 위한 추가 합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Tooyour 논리 앱 액세스 보안

많은 도구 사용 가능한 toohelp 논리 앱 보안 가지가 있습니다.

* 보안 액세스 tootrigger 논리 앱 (HTTP 요청 트리거)
* 보안 액세스 toomanage 편집 또는 논리 앱 읽기
* 입 / 출력 실행에 대 한 액세스 toocontents 보안 설정
* 워크플로에서 작업 내에서 매개 변수 또는 입력 보안
* 워크플로에서 요청을 수신 하는 액세스 tooservices 보안 설정

## <a name="secure-access-tootrigger"></a>보안 액세스 tootrigger

작업할 때 발생 하는 논리 앱은 HTTP 요청에 ([요청](../connectors/connectors-native-reqres.md) 또는 [Webhook](../connectors/connectors-native-webhook.md)), 권한 있는 클라이언트만 hello 논리 앱을 발생 시킬 수 있도록 액세스를 제한할 수 있습니다. 논리 앱에 대한 모든 요청은 SSL을 통해 암호화되고 보호됩니다.

### <a name="shared-access-signature"></a>공유 액세스 서명

논리 앱에 대 한 모든 요청 끝점 포함 한 [공유 액세스 서명 (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello URL의 일부분으로 합니다. 각 URL은 `sp`, `sv` 및 `sig` 쿼리 매개 변수를 포함합니다. 하 여 지정 된 사용 권한이 `sp`, tooHTTP 메서드 허용, 해당 `sv` hello 사용 되는 버전 toogenerate은 및 `sig` 사용된 tooauthenticate 액세스 tootrigger 됩니다. 모든 hello URL 경로 및 속성에 대 한 비밀 키와 hello SHA256 알고리즘을 사용 하 여 hello 서명을 생성 합니다. hello 비밀 키가 노출 및 게시 되지 hello 논리 앱의 일부로 저장 하 여 암호화 유지 됩니다. 논리 앱에만 트리거 hello 비밀 키를 사용 하 여 만든 유효한 서명을 포함 하는 권한을 부여 합니다.

#### <a name="regenerate-access-keys"></a>액세스 키 다시 생성

언제 든 지 hello REST API 또는 Azure 포털을 통해 새 보안 키를 다시 생성할 수 있습니다. Hello 이전 키를 사용 하 여 이전에 생성 된 모든 현재 Url에는 더 이상 권한이 부여 되었고 무효화 된 toofire hello 논리 앱 됩니다.

1. Hello Azure 포털에서에서 원하는 tooregenerate 키 hello 논리 앱을 열으십시오
1. Hello 클릭 **선택 키** 아래에서 메뉴 항목 **설정**
1. Hello 키 tooregenerate 및 전체 hello 프로세스를 선택 합니다.

다시 생성 한 후 검색 Url hello 새 액세스 키로 서명 됩니다.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>만료 날짜가 있는 콜백 URL 만들기

다른 상대방과 hello URL을 공유 하는 경우에 특정 키와 만료 날짜가 필요에 따라 Url을 생성할 수 있습니다. 있습니다 수 다음 원활 하 게 키를 롤백하거나 액세스 toofire 앱 확인 제한 tooa 특정 timespan이 됩니다. Hello 통해 URL에 대 한 만료 날짜를 지정할 수 있습니다 [논리 앱 REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Hello 본문에 포함 hello 속성 `NotAfter` hello 일까 지 유효만 하는 콜백 URL을 반환 하는 JSON 날짜 문자열로 `NotAfter` 날짜 및 시간입니다.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>기본 또는 보조 비밀 키로 URL 만들기

을 생성 하거나 요청 기반 트리거에 대 한 콜백 Url을 나열 하는 경우에 키 toouse toosign hello URL을 지정할 수 있습니다.  Hello 통해 특정 키로 서명 하는 URL을 생성할 수 [논리 앱 REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) 다음과 같습니다.

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Hello 본문에 포함 hello 속성 `KeyType` 하나로 `Primary` 또는 `Secondary`합니다.  지정 된 hello 보안 키로 서명 된 URL을 반환 합니다.

### <a name="restrict-incoming-ip-addresses"></a>받는 IP 주소 제한

또한 공유 액세스 서명을 toohello toorestrict 논리 앱을 특정 클라이언트의 호출을 지정할 수 있습니다.  예를 들어 Azure API 관리를 통해 끝점을 관리 하는 경우 제한할 수 있습니다 hello 논리 앱 tooonly hello API 관리 인스턴스 IP 주소에서에서 hello 요청한 경우 hello 요청을 수락 합니다.

Hello 논리 앱 설정 내에서이 설정을 구성할 수 있습니다.

1. Hello Azure 포털에서에서 IP 주소 제한을 tooadd 원하는 hello 논리 앱을 열으십시오
1. Hello 클릭 **액세스 제어 구성** 아래에서 메뉴 항목 **설정**
1. IP 주소 범위 toobe hello 트리거에 의해 수락 hello 목록 지정

올바른 IP 범위는 hello 형식 `192.168.1.1/255`합니다. 중첩 된 논리 앱으로 hello 논리 앱 tooonly 화재 hello를 선택 합니다 **다른 논리 앱** 옵션입니다. 이 옵션의 hello 전화만 서비스 자체 (부모 논리 앱) 화재 성공적으로 의미는 빈 배열을 toohello 리소스를 씁니다.

> [!NOTE]
> Hello REST API를 통해 요청 트리거 논리 앱을 계속 실행할 수 있습니다 / 관리 `/triggers/{triggerName}/run` IP에 관계 없이 합니다. 이 시나리오에서는 hello Azure REST API에 대 한 인증이 필요 하 고 hello Azure 감사 로그에에서 표시 되는 모든 이벤트. 그에 따라 액세스 제어 정책을 설정합니다.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>IP 범위 hello 리소스 정의에서 설정

사용 하는 경우는 [배포 템플릿을](logic-apps-create-deploy-template.md) tooautomate hello 리소스 템플릿 배포를 hello IP 범위 설정을 구성할 수 있습니다.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Azure Active Directory, OAuth 또는 기타 보안 추가

논리 앱 위에 프로토콜을 통해 더 많은 권한 부여 tooadd [Azure API 관리](https://azure.microsoft.com/services/api-management/) api 논리 앱 풍부한 모니터링, 보안, 정책 및 hello 기능 tooexpose 있는 모든 끝점에 대 한 설명서를 제공 합니다. Azure API 관리에는 Azure Active Directory, 인증서, OAuth, 또는 기타 보안 표준을 사용할 수 있는 hello 논리 앱에 대 한 공용 또는 개인 끝점을 노출할 수 있습니다. 요청을 받을 때 Azure API 관리 hello 요청 toohello 논리 앱 (모든 필요한 변환을 또는 진행 중인 제한 수행 중)를 전달 합니다. Hello 들어오는 IP 범위 hello 논리 앱 tooonly에서 설정을 허용 hello 논리 앱 toobe 트리거된 API 관리에서 사용할 수 있습니다.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>보안 액세스 논리 앱 toomanage 또는 편집

특정 사용자나 그룹은 수 tooperform hello 리소스에는 작업 수 있도록 논리 앱에서 액세스 toomanagement 작업을 제한할 수 있습니다. Azure hello를 사용 하 여 논리 앱 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md) 기능과 hello로 사용자 지정할 수 있습니다. 동일한 도구입니다.  몇 가지 기본 제공 역할이 구독 tooas의 멤버를 잘 할당할 수 있습니다.

* **논리 앱 참가자** -액세스 tooview, 편집 및 논리 앱 업데이트를 제공 합니다.  Hello 리소스를 제거 하거나 관리 작업을 수행할 수 없습니다.
* **논리 앱 연산자** -수 hello 논리 앱 및 실행된 기록 보기 및 설정/해제 합니다.  Hello 정의 업데이트 하거나 편집할 수 없습니다.

사용할 수도 있습니다 [Azure 리소스 잠금](../azure-resource-manager/resource-group-lock-resources.md) tooprevent 변경 또는 논리 앱을 삭제 합니다. 이 기능은 변경 또는 삭제가에서 중요 한 tooprevent 프로덕션 리소스에 설명 합니다.

## <a name="secure-access-toocontents-of-hello-run-history"></a>실행 기록 hello의 보안 액세스 toocontents

이전 실행 toospecific IP 주소 범위에서 입력 또는 출력의 toocontents 액세스를 제한할 수 있습니다.  

워크플로 실행 내에 있는 모든 데이터는 전송 중 그리고 미사용 시 암호화됩니다. 통화 toorun 기록 이루어지면 hello 서비스는 hello 요청을 인증 하 고 링크 toohello 요청 및 응답 입 / 출력을 제공 합니다. 이 링크는 지정 된 IP 주소 범위에서 tooview 콘텐츠 hello 콘텐츠를 반환 합니다. 보호 된 있도록 요청을 수 있습니다. 추가 액세스 제어를 위해 이 기능을 사용할 수 있습니다. 누구도 입/출력에 액세스할 수 없도록 `0.0.0.0`과 같이 IP 주소를 지정할 수도 있습니다. 관리자 권한을 가진 사용자만 이러한 제한을 '-just-in-time ' 액세스 tooworkflow 내용에 대 한 hello 가능성을 제공 하를 제거할 수 있습니다.

Hello Azure 포털의 hello 리소스 설정 내에서이 설정을 구성할 수 있습니다.

1. Hello Azure 포털에서에서 IP 주소 제한을 tooadd 원하는 hello 논리 앱을 열으십시오
1. Hello 클릭 **액세스 제어 구성** 아래에서 메뉴 항목 **설정**
1. Hello 목록이 액세스 toocontent에 대 한 IP 주소 범위를 지정 합니다.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>IP 범위 hello 리소스 정의에서 설정

사용 하는 경우는 [배포 템플릿을](logic-apps-create-deploy-template.md) tooautomate hello 리소스 템플릿 배포를 hello IP 범위 설정을 구성할 수 있습니다.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>워크플로 내에서 매개 변수 및 입력 보안

환경에 걸쳐 tooparameterize 배포에 대 한 워크플로 정의의 일부 측면을 할 수 있습니다. 일부 매개 변수에서와 같은 클라이언트 ID와 클라이언트 암호에 대 한 워크플로 편집할 때 tooappear 않을 보안 매개 변수가 될 수는 또한 [Azure Active Directory 인증](../connectors/connectors-native-http.md#authentication) HTTP 동작입니다.

### <a name="using-parameters-and-secure-parameters"></a>매개 변수 및 보안 매개 변수 사용

tooaccess hello 런타임에 리소스 매개 변수 값은 hello [워크플로 정의 언어](http://aka.ms/logicappsdocs) 제공는 `@parameters()` 작업 합니다. 또한 쉽게 [hello 리소스 배포 템플릿에 매개 변수를 지정](../azure-resource-manager/resource-group-authoring-templates.md#parameters)합니다. Hello 매개 변수 형식으로 지정 하지만 `securestring`, hello 매개 변수는 hello 리소스 정의의 hello 나머지와 함께 반환 될 없습니다 및 배포 후 hello 리소스를 확인 하 여 액세스할 수 없게 합니다.

> [!NOTE]
> Hello 머리글이 나 요청의 본문에 매개 변수는 사용 하는 경우 hello 매개 변수 볼 수 hello 실행 기록과 나가는 HTTP 요청에 액세스 합니다. 있는지 tooset 콘텐츠 액세스 정책의 적절 하 게 확인 합니다.
> 권한 부여 헤더는 입력 또는 출력을 통해 볼 수 없습니다. 따라서 hello 암호는 사용할 수 없습니다, hello 암호 검색 가능 되지 않습니다.

#### <a name="resource-deployment-template-with-secrets"></a>암호가 있는 리소스 배포 템플릿

hello 다음 보여 주는 예제는 배포의 보안 매개 변수를 참조 하는 `secret` 런타임에 합니다. Hello에 대 한 hello 환경 값을 지정할 수는 별도 매개 변수 파일에서 `secret`, 사용 또는 [Azure 리소스 관리자 KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve 비밀에 배포 시간입니다.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>워크플로에서 수신 요청 tooservices 액세스 보안

여러 방법으로 toohelp는 모든 끝점 hello 논리 앱에 필요한 tooaccess 안전 합니다.

### <a name="using-authentication-on-outbound-requests"></a>아웃바운드 요청에 대한 인증 사용

HTTP, HTTP + Swagger (개방형 API) 또는 Webhook 작업을 사용할 때 전송 되는 인증 toohello 요청을 추가할 수 있습니다. 추가할 수 있는 인증으로는 기본 인증, 인증서 인증 또는 Azure Active Directory 인증이 있습니다. 어떻게 tooconfigure이이 인증 있습니다에 대 한 내용은 [이 문서의](../connectors/connectors-native-http.md#authentication)합니다.

### <a name="restricting-access-toologic-app-ip-addresses"></a>Toologic 앱 IP 주소 액세스 제한

논리 앱의 모든 호출은 영역당 특정 IP 주소 집합에서 나옵니다. 추가 필터링을 추가할 수 있습니다 tooonly IP 주소를 지정 하는 것의 요청을 수락 합니다. 해당 IP 주소의 목록은 [논리 앱 제한 및 구성](logic-apps-limits-and-config.md#configuration)을 참조하세요.

### <a name="on-premises-connectivity"></a>온-프레미스 연결

논리 앱 안전 하 고 신뢰할 수 있는 여러 서비스 tooprovide와의 통합 온-프레미스 통신을 제공 합니다.

#### <a name="on-premises-data-gateway"></a>온-프레미스 데이터 게이트웨이

논리 앱에 대 한 많은 관리 되는 커넥터는 연결의 보안이 tooon 온-프레미스 시스템, 파일 시스템, SQL, SharePoint, DB2, 등을 제공 합니다. hello 게이트웨이 hello Azure 서비스 버스를 통해 암호화 된 채널에 온-프레미스 원본에서 데이터를 릴레이합니다. 모든 트래픽이 hello 게이트웨이 에이전트의 보안 아웃 바운드 트래픽이으로 시작 합니다. 에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](logic-apps-gateway-install.md#gateway-cloud-service)합니다.

#### <a name="azure-api-management"></a>Azure API Management

[Azure API 관리](https://azure.microsoft.com/services/api-management/) 온-프레미스 연결 옵션, 보안 된 프록시 및 통신 tooon 온-프레미스 시스템에 대 한 사이트 간 VPN 및 express 경로 통합 등이 있습니다. Hello 논리가 응용 프로그램 디자이너에서에서 tooon 온-프레미스 시스템 빠른 액세스를 제공 하는 워크플로 내에서 Azure API 관리에서 노출 하는 API를 신속 하 게 선택할 수 있습니다.

#### <a name="hybrid-connections-from-azure-app-service"></a>Azure App Services의 하이브리드 연결

Azure API 및 웹 앱 toocommunicate 온-프레미스에 대 한 hello 온-프레미스 하이브리드 연결 기능을 사용할 수 있습니다.  하이브리드 연결 및 tooconfigure 수 발견 하는 방법에 대 한 내용은 [이 문서의](../app-service-web/web-sites-hybrid-connection-get-started.md)합니다.

## <a name="next-steps"></a>다음 단계
[배포 템플릿 만들기](logic-apps-create-deploy-template.md)  
[예외 처리](logic-apps-exception-handling.md)  
[논리 앱 모니터링](logic-apps-monitor-your-logic-apps.md)  
[논리 앱 오류 진단 및 문제](logic-apps-diagnosing-failures.md)  
