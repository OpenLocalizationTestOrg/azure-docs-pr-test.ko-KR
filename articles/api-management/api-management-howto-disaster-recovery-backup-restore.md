---
title: "백업 및 복원 Azure API 관리에서 사용 하 여 aaaImplement 재해 복구 | Microsoft Docs"
description: "자세한 내용은 방법 toouse 백업 및 Azure API 관리에서 tooperform 재해 복구를 복원 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Tooimplement 재해 복구를 사용 하 여 백업 서비스 및 Azure API 관리에서 복원 방법
Toopublish를 선택 하 고 있는 toodesign, 구현 및 관리 해야 하는 많은 오류 내결함성 및 인프라 기능을 수행 하는 Azure API 관리를 통해 Api 관리 합니다. Azure 플랫폼 hello 늘어나 hello 비용의 일부분에 발생할 수 있는 오류를 완화합니다.

여기서 API 관리 서비스는 hello 지역에 영향을 주는 가용성 문제 로부터 toorecover 호스트 하면 언제 든 지 준비 tooreconstitute 다른 지역에 서비스 여야 합니다. 가용성 목표와 복구 시간 목표에 따라 수도 tooreserve 백업 서비스 하나 이상의 영역에 있으며 구성 및 콘텐츠 hello 활성 서비스와 동기화 toomaintain를 시도 하십시오. hello 서비스 백업 및 복원 기능은 재해 복구 전략을 구현 하기 위한 hello 필요한 문서 블록을 제공 합니다.

이 가이드에서는 Azure 리소스 관리자 tooauthenticate 요청 방법 등에 toobackup 및 API 관리 서비스 인스턴스를 복원 합니다.

> [!NOTE]
> API 관리 서비스 인스턴스를 준비 하는 등의 시나리오에 대 한 복제를 위한 백업 및 재해 복구에 대 한 API 관리 서비스 인스턴스 복원에 대 한 hello 프로세스를 사용할 수도 있습니다.
>
> 각 백업은 30일 후 만료되니 유의하세요. 와 hello 복원이 실패 합니다 hello 30 일 만료 기간이 만료 된 후 toorestore 백업을 시도 하면는 `Cannot restore: backup expired` 메시지입니다.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Azure 리소스 관리자 요청 인증
> [!IMPORTANT]
> hello REST API 백업 및 복원에 대 한 Azure 리소스 관리자를 사용 하 여 및에 서로 다른 인증 메커니즘이 API 관리 엔터티를 관리 하기 위한 REST Api를 hello 보다 합니다. 이 섹션의 단계 hello tooauthenticate Azure 리소스 관리자 요청 하는 방식에 대해 설명 합니다. 자세한 내용은 [Azure 리소스 관리자 요청 인증](http://msdn.microsoft.com/library/azure/dn790557.aspx)을 참조하세요.
>
>

모든 사용자가 hello Azure 리소스 관리자를 사용 하 여 리소스에서 수행 하는 hello 작업 단계를 수행 하는 hello를 사용 하 여 Azure Active Directory와 인증 되어야 합니다.

* 응용 프로그램 toohello Azure Active Directory 테 넌 트를 추가 합니다.
* 사용자가 추가한 hello 응용 프로그램에 대 한 권한을 설정 합니다.
* 리소스 관리자 요청 tooAzure를 인증 하기 위한 hello 토큰을 가져옵니다.

hello 첫 번째 단계는 toocreate Azure Active Directory 응용 프로그램입니다. Hello에 로그인 [Azure 클래식 포털](http://manage.windowsazure.com/) API 관리 서비스를 포함 하는 hello 구독을 사용 하 여 인스턴스 및 toohello 이동 **응용 프로그램** 기본 Azure Active Directory에 대 한 탭 합니다.

> [!NOTE]
> Hello Azure Active Directory 기본 디렉터리 표시 tooyour 계정이 아닌 경우 hello Azure 구독 toogrant hello의 연락처 hello 관리자 tooyour 계정 사용 권한 필요 합니다.

![Azure Active Directory 응용 프로그램 만들기][api-management-add-aad-application]

**추가**, **조직에서 개발 중인 응용 프로그램 추가**를 선택하고 **네이티브 클라이언트 응용 프로그램**을 선택합니다. 설명이 포함 된 이름을 입력 하 고 hello 다음 화살표를 클릭 합니다. 같은 자리 표시자 URL을 입력 `http://resources` hello에 대 한 **리디렉션 URI**처럼 필수 필드 이지만 hello 값은 나중에 사용 되지 않습니다. Hello 확인란 toosave hello 응용 프로그램을 클릭 합니다.

Hello 응용 프로그램을 저장 한 후 클릭 **구성**, toohello 아래로 스크롤하여 **tooother 응용 프로그램 사용 권한** 섹션을 클릭 하 여 **응용 프로그램을 추가**합니다.

![권한 추가][api-management-aad-permissions-add]

선택 **Windows** **Azure 서비스 관리 API** hello 확인란 tooadd hello 응용 프로그램을 클릭 합니다.

![권한 추가][api-management-aad-permissions]

클릭 **위임 된 권한** 새로 추가 된 hello 옆에 있는 **Windows** **Azure 서비스 관리 API** 응용 프로그램에 대 한 확인란 hello **Azure 액세스 서비스 관리 (미리 보기)**를 클릭 하 고 **저장**합니다.

![권한 추가][api-management-aad-delegated-permissions]

이전 tooinvoking hello를 생성 하는 Api hello 백업 및 복원에 필요한 tooget 토큰 합니다. hello 다음 예제에서는 hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget 패키지 tooretrieve hello 토큰입니다.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

대체 `{tentand id}`, `{application id}`, 및 `{redirect uri}` 지침을 진행 하는 hello를 사용 하 여 합니다.

대체 `{tenant id}` hello 방금 만든 Azure Active Directory 응용 프로그램의 hello 테 넌 트 id입니다. 클릭 하 여 hello id에 액세스할 수 있습니다 **끝점 보기**합니다.

![끝점][api-management-aad-default-directory]

![끝점][api-management-endpoint]

대체 `{application id}` 및 `{redirect uri}` hello를 사용 하 여 **클라이언트 Id** hello에서 URL을 hello 및 **리디렉션 Uri** 섹션에서 Azure Active Directory 응용 프로그램의 **구성**  탭 합니다.

![리소스][api-management-aad-resources]

Hello 값이 지정 되어 되 면 hello 코드 예제에서는 다음 예제에서는 토큰 비슷한 toohello를 반환 해야 합니다.

![위임][api-management-arm-token]

호출 hello 백업 및 복원 hello 다음 섹션에서에서 설명 하는 작업을 하기 전에 REST 호출에 대 한 hello 권한 부여 요청 헤더를 설정 합니다.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"> </a>API Management 서비스 백업
HTTP 요청을 수행 하는 API 관리 서비스 문제 hello tooback:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

설명:

* `subscriptionId`-toobackup 넣을 hello API 관리 서비스를 포함 하는 hello 구독의 id
* `resourceGroupName`-hello 'Api 기본-{서비스 영역을 (를)' 형태의 문자열로 여기서 `service-region` 예를 들어 hello Azure 지역 hello toobackup 고치려는 API 관리 서비스의 호스팅 위치를 식별`North-Central-US`
* `serviceName`-hello hello 해당 생성 시 지정 된 백업 하는 API 관리 서비스의 hello 이름
* `api-version` - `2014-02-14`(으)로 대체

Hello hello 요청 본문을 hello 대상 Azure 저장소 계정 이름, 액세스 키, blob 컨테이너 이름 및 백업 이름 지정:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Hello의 hello 값 설정 `Content-Type` 요청 헤더에 너무`application/json`합니다.

백업은 여러 분 toocomplete 걸리는 장기 실행 작업입니다.  Hello 요청이 성공 하 고 hello 백업 프로세스가 시작 된 경우 받을 수는 `202 Accepted` 와 응답 상태 코드는 `Location` 헤더입니다.  'GET' hello에 toohello URL을 요청 확인 `Location` 헤더 toofind hello 작업의 hello 상태 아웃 합니다. Hello 백업 진행 중인 동안 tooreceive 202 수락 상태 코드는 계속 합니다. 응답 코드가 `200 OK` hello 백업 작업이 성공적으로 완료를 표시 합니다.

백업 요청을 수행할 때는 제약 조건이 다음 hello를 note 하십시오.

* **컨테이너** hello 요청 본문에 지정 된 **있어야**합니다.
* 백업이 진행 중인 동안에는 SKU 업그레이드/다운그레이드, 도메인 이름 변경 등의 **서비스 관리 작업을 수행하면 안 됩니다** .
* 복원는 **30 일에 대해서만 백업 정해진** hello 순간 만들기 이후 합니다.
* **사용 현황 데이터** 분석 보고서를 만드는 데 사용 되는 **포함 되어 있지 않으면** hello 백업에서 합니다. 사용 하 여 [Azure API 관리 REST API] [ Azure API Management REST API] tooperiodically 보관을 위한 분석 보고서를 검색 합니다.
* hello 주파수 서비스 백업을 수행 된 복구 지점 목표에 영향을 줍니다. 것이 좋습니다 정기 백업 미 실시 구현으로 요청 시 백업 후 중요 한 toominimize tooyour API 관리 서비스를 변경 합니다.
* **변경 내용을** 만들어 놓은 toohello 서비스 구성 (예:: Api, 정책, 개발자 포털 모양) 백업 작업 동안 진행 중인 **hello 백업에 포함 될 수 있습니다 및 손실 될 됩니다**합니다.

## <a name="step2"> </a>API 관리 서비스 복원
toorestore 이전에 만든된 백업에서 API 관리 서비스는 hello 다음 HTTP 요청을 확인 합니다.

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

설명:

* `subscriptionId`-으로 백업을 복원 하는 hello API 관리 서비스를 포함 하는 hello 구독의 id
* `resourceGroupName`-hello 'Api 기본-{서비스 영역을 (를)' 형태의 문자열로 여기서 `service-region` 예를 들어 hello Azure 지역 hello에 백업을 복원 하는 API 관리 서비스의 호스팅 위치를 식별`North-Central-US`
* `serviceName`-hello hello 해당 생성 시에 복원 되 고 서비스를 지정 하는 API 관리의 hello 이름
* `api-version` - `2014-02-14`(으)로 대체

Hello hello 요청 본문을 Azure 저장소 계정 이름, 액세스 키, blob 컨테이너 이름 및 백업 이름, 즉 hello 백업 파일 위치를 지정 합니다.

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Hello의 hello 값 설정 `Content-Type` 요청 헤더에 너무`application/json`합니다.

복원은은 too30 또는 더 많은 분 toocomplete 차지 하는 장기 실행 작업입니다.  Hello 요청이 성공 하 고 hello 복원 프로세스가 시작 된 경우 받을 수는 `202 Accepted` 와 응답 상태 코드는 `Location` 헤더입니다.  'GET' hello에 toohello URL을 요청 확인 `Location` 헤더 toofind hello 작업의 hello 상태 아웃 합니다. Hello 복원이 진행 중인 동안 tooreceive '202 수락 됨' 상태 코드는 계속 합니다. 응답 코드가 `200 OK` hello 복원 작업이 성공적으로 완료를 표시 합니다.

> [!IMPORTANT]
> **hello SKU** hello 서비스를 복원 중인 **일치 해야** hello hello의 SKU가 복원 되는 서비스를 백업 합니다.
>
> **변경 내용을** 만들어 놓은 toohello 서비스 구성 (예:: Api, 정책, 개발자 포털 모양) 복원 작업 동안 진행 중인 **덮어쓰게**합니다.
>
>

## <a name="next-steps"></a>다음 단계
Microsoft 블로그 hello 백업/복원 프로세스의 서로 다른 두 연습에 대 한 다음 hello 확인해 보세요.

* [Azure API 관리 계정 복제](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * 그녀의 기여도 toothis 아티클의 tooGisela 감사 드립니다.
* [Azure API 관리: 백업 및 복원 구성](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * 자세한 Stuart 별로 hello 접근 방식을 hello 공식 지침에 맞지 않는 하지만 매우 흥미로운 쉽습니다.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
