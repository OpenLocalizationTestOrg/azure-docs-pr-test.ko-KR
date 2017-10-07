---
title: "모바일 앱 및 모바일 서비스에서 aaaClient 및 서버 SDK 버전 관리 | Microsoft Docs"
description: "모바일 서비스와 Azure 모바일 앱에 대한 클라이언트 SDK의 목록 및 서버 SDK 버전과 호환성"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>모바일 앱 및 모바일 서비스에서 클라이언트 및 서버 버전 관리
hello 최신 버전의 Azure 모바일 서비스는 hello **모바일 앱** Azure 앱 서비스 기능입니다.

모바일 응용 프로그램 클라이언트 hello 및 서버 Sdk는 모바일 서비스에서 항목에 따라 원래 되어도 없지만 *하지* 서로 호환 됩니다.
즉, *Mobile Apps* 서버 SDK 및 마찬가지로 *Mobile Services*를 사용하는 *Mobile Apps* 클라이언트 SDK를 사용해야 합니다. 이 계약은 hello 클라이언트와 서버 Sdk에서 사용 되는 특별 한 헤더 값을 통해 적용 `ZUMO-API-VERSION`합니다.

참고: 때마다이 문서는 참조 tooa *모바일 서비스* 백 엔드, 필요 하지 않습니다 반드시 toobe 모바일 서비스에서 호스트 합니다. Hello 서비스 여전히 사용 될 수 있지만 가능한 toomigrate 코드 변경 하지 않고 앱 서비스 모바일 서비스 toorun은 이제 *모바일 서비스* SDK 버전입니다.

에 대해 더 알아봅니다 toolearn hello 문서를 참조 tooApp 서비스 코드 변경 없이 마이그레이션할 [모바일 서비스 tooAzure 앱 서비스를 마이그레이션할]합니다.

## <a name="header-specification"></a>헤더 사양
hello 키 `ZUMO-API-VERSION` hello HTTP 헤더 또는 hello 쿼리 문자열에 지정할 수 있습니다. hello 값은 버전 문자열 hello 형태로 **x.y.z 형식이 며**합니다.

예:

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>버전 확인 건너뛰기
버전의 값을 설정 하 여 확인을 취소 수 **true** hello 응용 프로그램 설정에 대 한 **MS_SkipVersionCheck**합니다. Web.config 파일에 또는 hello hello Azure 포털의 응용 프로그램 설정 섹션에서에서이 지정 합니다.

> [!NOTE]
> 모바일 서비스와 특히 hello 오프 라인 동기화, 인증 및 푸시 알림 영역에서에서 모바일 응용 프로그램 간의 동작 변경의 여러 가지가 있습니다. 이러한 동작 변경 내용은 앱의 기능을 해제 되지 않도록 테스트 tooensure 완료 후 확인 버전만 취소 해야 합니다.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>모든 버전에 대한 호환성 요약
아래 hello 차트에서는 모든 클라이언트 및 서버 형식 간에 hello 호환성을 보여 줍니다. 백 엔드 어느 모바일으로 분류 됩니다 **서비스** 또는 모바일 **앱** hello 서버에서 사용 하는 SDK에 기반 합니다.

|  | **모바일 서비스** Node.js 또는 .NET | **모바일 앱** Node.js 또는 .NET |
| --- | --- | --- |
| [모바일 서비스 클라이언트] |확인 |오류\* |
| [모바일 앱 클라이언트] |오류\* |확인 |

\***MS_SkipVersionCheck**를 지정하여 제어될 수 있습니다.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>모바일 서비스 클라이언트 및 서버
hello 테이블 아래에 hello 클라이언트 Sdk와 호환 되는 **모바일 서비스**합니다.

참고: hello 모바일 서비스 클라이언트 Sdk *없는* 헤더 값에 대 한 보내기 `ZUMO-API-VERSION`합니다. 이 헤더 또는 쿼리 문자열 값인 hello 서비스에서 수신 하는 경우 위에 설명 된 대로 선택한 명시적으로 하지 않으면 오류가 반환 될 됩니다.

### <a name="MobileServicesClients"></a> 모바일 *서비스* 클라이언트 SDK
| 클라이언트 플랫폼 | 버전 | 버전 헤더 값 |
| --- | --- | --- |
| 관리된 클라이언트(Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |해당 없음 |
| iOS |[2.2.2](http://aka.ms/gc6fex) |해당 없음 |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |해당 없음 |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |해당 없음 |

### <a name="mobile-services-server-sdks"></a>모바일 *서비스* 서버 SDK
| 서버 플랫폼 | 버전 | 수락된 버전 헤더 |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* 버전 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |* * 버전 헤더가 * * |
| Node.js |(서비스 예정) |**버전 헤더 없음** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>모바일 서비스 백 엔드의 동작
| ZUMO-API-VERSION | MS_SkipVersionCheck의 값 | 응답 |
| --- | --- | --- |
| 지정되지 않음 |모두 |200 - 확인 |
| 어떤 값 |True |200 - 확인 |
| 어떤 값 |False/지정되지 않음 |400 - 잘못된 요청 |

## <a name="2.0.0"></a>Azure 모바일 앱 클라이언트 및 서버
### <a name="MobileAppsClients"></a> 모바일 *앱* 클라이언트 SDK
다음 버전의 hello 클라이언트 SDK hello로 시작 도입 된 버전을 확인에 대 한 **Azure 모바일 앱**:

| 클라이언트 플랫폼 | 버전 | 버전 헤더 값 |
| --- | --- | --- |
| 관리된 클라이언트(Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>모바일 *앱* 서버 SDK
버전 검사는 다음 서버 SDK 버전에 포함됩니다.

| 서버 플랫폼 | SDK) | 수락된 버전 헤더 |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>모바일 앱 백 엔드의 동작
| ZUMO-API-VERSION | MS_SkipVersionCheck의 값 | 응답 |
| --- | --- | --- |
| x.y.z 또는 Null |True |200 - 확인 |
| Null |False/지정되지 않음 |400 - 잘못된 요청 |
| 1.x.y |False/지정되지 않음 |400 - 잘못된 요청 |
| 2.0.0-2.x.y |False/지정되지 않음 |200 - 확인 |
| 3.0.0-3.x.y |False/지정되지 않음 |400 - 잘못된 요청 |

## <a name="next-steps"></a>다음 단계
* [모바일 서비스 tooAzure 앱 서비스를 마이그레이션할]

[모바일 서비스 클라이언트]: #MobileServicesClients
[모바일 앱 클라이언트]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[모바일 서비스 tooAzure 앱 서비스를 마이그레이션할]: app-service-mobile-migrating-from-mobile-services.md
