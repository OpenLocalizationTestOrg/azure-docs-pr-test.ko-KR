---
title: "Azure API 관리 제한 aaaAdvanced 요청"
description: "자세한 내용은 방법 toocreate 유연한 할당량 및 속도 제한 Azure API 관리를 사용 하 여 정책을 적용 합니다."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Azure API 관리로 고급 요청 제한
들어오는 요청 수 toothrottle Azure API 관리의 중요 한 역할입니다. API 관리를 통해 전송 하거나 요청 또는 hello 총 요청/데이터 hello 속도 제어 API 공급자 tooprotect 남용에서 해당 Api 다양 한 API 제품 계층에 대 한 값을 만듭니다.

## <a name="product-based-throttling"></a>제품 기반 제한
toodate, hello 속도 제한 기능 범위 제한 toobeing tooa 특정 제품 구독 (기본적으로 키) 되어 합니다 API 관리 게시자 포털 hello에 정의 되어 있어야 합니다. 그러나 Hello 개발자에 게 등록 한 toouse 자신의 API에 대 한 hello API 공급자 tooapply 제한에 유용 합니다, 도움이 되지는 않습니다, 예를 들어 hello API의 개별 최종 사용자를 제한 합니다. 가 응용 프로그램 tooconsume hello 개발자의 단일 사용자에 대해 전체 할당량을 hello 있으며 다음 못하도록 hello 개발자의 다른 고객 수 toouse hello 응용 프로그램입니다. 또한 많은 양의 요청을 생성할 수 있습니다는 여러 고객 액세스 toooccasional 사용자를 제한할 수 있습니다.

## <a name="custom-key-based-throttling"></a>사용자 지정 키 기반 제한
새 hello [키로 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [키로 할당량](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 정책은 훨씬 더 유연한 솔루션 tootraffic 컨트롤을 제공 합니다. 이러한 새 정책을 사용 하면 toodefine 식 tooidentify hello 키 사용된 tootrack 트래픽 사용 될 수 있습니다. 첫 번째 예이 작동 하는 hello 방법은 보여 줍니다 것이 가장 쉽습니다. 

## <a name="ip-address-throttling"></a>IP 주소 제한
hello 다음 정책을 제한할 단일 클라이언트 IP 주소 tooonly 10 1000000 호출 하 고 매달 대역폭의 10, 000 킬로바이트 단위는 총 1 분 마다를 호출 합니다. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Hello 인터넷에 있는 모든 클라이언트에 고유 IP 주소를 사용 하는 경우 사용자가 사용을 제한 하는 효과적인 방법을 수 있습니다. 그러나 여러 사용자가 toothem 액세스 hello 인터넷 NAT 장치를 통해 인해 단일 공용 IP 주소를 공유 한다는 가능성이 매우 높습니다. Hello 인증 되지 않은 액세스를 허용 하는 Api에 대 한 그럼에도 불구 하 고 `IpAddress` hello 최상의 옵션 일 수 있습니다.

## <a name="user-identity-throttling"></a>사용자 ID 제한
최종 사용자가 인증된 후 해당 사용자를 고유하게 식별하는 정보를 기반으로 제한 키를 생성할 수 있습니다.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

다음이 예제에서는 hello 권한 부여 헤더를 추출, 너무 변환`JWT` 개체 및 hello 토큰 tooidentify hello 사용자의 hello 제목을 사용 하 여 hello 속도 키 제한으로 사용 합니다. Hello 사용자 id hello에 저장 되어 있으면 `JWT` 하나 hello 다른 클레임으로 다음 그 자리에 값이 사용 될 수 있습니다.

## <a name="combined-policies"></a>결합된 정책
새로운 정책을 조절 하는 hello hello 제한 정책을 기존 보다 더 많은 제어를 제공 하지만 여전히 값이 두 기능을 결합 합니다. 제품 구독 키로 제한 ([구독에 의해 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [구독 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota))은 사용 수준에 따라 tooenable 충전 하 여 API의 monetizing 위한 훌륭한 방법입니다. hello 더 세밀 하 게 제어할 수 toothrottle 사용자가 되는 상호 보완적인 고 방지 한 사용자의 동작 다른 hello 경험을 저하 시 키 지 합니다. 

## <a name="client-driven-throttling"></a>클라이언트 기반 제한
키를 제한 하는 hello를 사용 하 여 정의 되는 [정책 식을](https://msdn.microsoft.com/library/azure/dn910913.aspx), hello 제한 범위 방법을 선택 하는 hello API 공급자는 합니다. 그러나 개발자는 경우가 평가 방법 toocontrol 자신의 고객을 제한 합니다. 이 사용자 지정 헤더 tooallow hello 개발자의 클라이언트 응용 프로그램 toocommunicate hello 키 toohello API를 도입 하 여 hello API 공급자가 설정할 수 수 있습니다.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

이렇게 하면 hello 개발자의 클라이언트 응용 프로그램 toochoose 보고자 toocreate hello 속도 키를 제한 합니다. 약간의 클라이언트 개발자 hello 키 용도 키 toousers의 집합을 할당 하 여 자신의 급여 계층을 만들 수 있습니다.

## <a name="summary"></a>요약
Azure API 관리 속도 및 따옴표 tooboth 제한 보호 하 고 추가 값 tooyour API 서비스를 제공 합니다. 새로운 사용자 지정 범위 지정 규칙을 사용 하 여 정책을 조절 하는 hello 더욱 세밀 하 게 하면 덜 세분화 된 해당 정책 tooenable 제어할 고객 toobuild 더 나은 응용 프로그램을 허용 합니다. 이 문서의 예제 hello 제조 속도 클라이언트 IP 주소, 사용자 id 및 클라이언트 생성 된 값과 함께 키를 제한 하 여 이러한 새 정책 사용 하 여를 hello를 보여 줍니다. 그러나 사용자 에이전트, URL 경로 부분, 메시지 크기와 같은 사용 될 수 있는 hello 메시지의 다른 많은 부분 있습니다.

## <a name="next-steps"></a>다음 단계
하십시오 의견을 보내 주십시오 hello Disqus 스레드에이 항목에 대 한 합니다. 시나리오에서 논리적인 선택 된 다른 잠재적인 키 값에 대 한 훌륭한 toohear 됩니다.

## <a name="watch-a-video-overview-of-these-policies"></a>이러한 정책에 대한 동영상 개요 시청
Hello에 대 한 자세한 내용은 [키로 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [키로 할당량](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 이 문서에서 다루는 정책을 hello 다음 비디오를 참조 하십시오.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

