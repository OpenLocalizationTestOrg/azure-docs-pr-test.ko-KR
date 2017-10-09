---
title: "서비스 패브릭 aaaAzure API 관리 개요 | Microsoft Docs"
description: "이 문서는 소개 toousing Azure API 관리 게이트웨이 tooyour 서비스 패브릭 응용 프로그램으로 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Service Fabric 및 API Management 개요

클라우드 응용 프로그램은 일반적으로 사용자, 장치 또는 다른 응용 프로그램에 대 한 프런트 엔드 게이트웨이 tooprovide 수신 단일 지점이 필요 합니다. Service Fabric에서 게이트웨이는 [ASP.NET Core 응용 프로그램](service-fabric-reliable-services-communication-aspnetcore.md), 트래픽 수신을 위해 설계된 기타 서비스(예: [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/), [Azure API Management](https://docs.microsoft.com/azure/api-management/))와 같은 상태 비저장 서비스일 수 있습니다.

이 문서는 소개 toousing Azure API 관리 게이트웨이 tooyour 서비스 패브릭 응용 프로그램으로 합니다. API 관리 서비스 패브릭에서 라우팅 규칙 tooyour 백 엔드 서비스 패브릭 서비스의 풍부한 Api toopublish 있도록와 직접 통합 됩니다. 

## <a name="architecture"></a>아키텍처
공통 서비스 패브릭 아키텍처 tooback 엔드 서비스 HTTP Api를 노출 하는 HTTP 호출에 수행 하는 단일 페이지 웹 응용 프로그램을 사용 합니다. hello [getting started 샘플 응용 프로그램 서비스 패브릭](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) 이 아키텍처의 예가 나와 있습니다.

이 시나리오에서는 상태 비저장 웹 서비스는 hello 서비스 패브릭 응용 프로그램에 hello 게이트웨이로 사용 됩니다. 이 접근 방식에서는 hello 다음 다이어그램에에서 나와 있는 것 처럼 toowrite HTTP 프록시를 수행할 수 있는 웹 서비스 요청 tooback 엔드 서비스:

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-web-app-stateless-gateway]

응용 프로그램 복잡성에서 성장 함에 따라 여러 가지 백 엔드 서비스 앞에 API를 제공 해야 하는 게이트웨이 hello 수행 하므로 합니다. Azure API 관리는 디자인 된 toohandle 라우팅 규칙을 사용 하 여 복잡 한 Api 액세스 제어, 속도 제한, 모니터링, 이벤트 로깅 및 응답을 위해 별도의 최소한의 노력으로 캐시 합니다. 상태 비저장 API 게이트웨이 toowrite 필요 없이 복제본 선택 toointelligently 경로 요청 직접 tooback 서비스 패브릭에서 서비스 및 azure API 관리 서비스 패브릭 서비스 검색, 파티션 확인을 지원 합니다. 

이 시나리오에서는 hello 웹 UI HTTP API를 호출 하는 동안에 웹 서비스를 통해 제공 되는 관리 하 고 hello 다음 다이어그램에에서 나와 있는 것 처럼 Azure API 관리를 통해 라우팅될:

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-web-app]

## <a name="application-scenarios"></a>응용 프로그램 시나리오

Service Fabric의 서비스는 상태 비저장 또는 상태 저장일 수 있으며 단일 항목, int-64 범위 및 이름 지정(named)의 3가지 체계 중 하나를 사용하여 분할될 수 있습니다. 서비스 끝점 확인을 사용하려면 특정 서비스 인스턴스의 특정 파티션을 식별해야 합니다. 서비스 인스턴스 이름을 hello 모두 서비스의 끝점, 확인 하는 경우 (예를 들어 `fabric:/myapp/myservice`) 단일 파티션의 hello 경우를 제외 하 고 뿐만 아니라 hello hello 서비스의 특정 파티션을 지정 해야 합니다.

상태 비저장 서비스, 상태 저장 서비스 및 모든 파티션 체계를 조합하여 Azure API Management를 사용할 수 있습니다.

## <a name="send-traffic-tooa-stateless-service"></a>트래픽 tooa 상태 비저장 서비스에 보내기

가장 간단한 경우 hello 트래픽이 tooa 상태 비저장 서비스 인스턴스를 전달 됩니다. tooachieve,이 API 관리 작업에는 인바운드 처리 정책을 사용 하면 서비스 패브릭 백 엔드 hello 서비스 패브릭 백 엔드의 tooa 특정 상태 비저장 서비스 인스턴스에 매핑하는 포함 되어 있습니다. Toothat 서비스에 전송 된 요청 hello 상태 비저장 서비스 인스턴스의 tooa 임의의 복제본에 전송 됩니다.

#### <a name="example"></a>예제
시나리오를 따르는 hello, 서비스 패브릭 응용 프로그램에는 상태 비저장 서비스 명명 된 `fabric:/app/fooservice`을 내부 HTTP API를 노출 합니다. hello 서비스 인스턴스 잘 알려져 이름과 hello 인바운드 처리 API 관리 정책에 직접 하드 코드 될 수 있습니다. 

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Tooa 상태 저장 서비스의 트래픽 보내기

비슷한 toohello 상태 비저장 서비스 시나리오 트래픽은 tooa 상태 저장 서비스 인스턴스에 전달할 수 있습니다. 이 경우에 API 관리 작업 포함 하면 서비스 패브릭 백 엔드 특정 요청 tooa 특정 파티션에 매핑하는 인바운드 처리 정책은 *stateful* 서비스 인스턴스가 있습니다. hello 파티션 toomap hello 들어오는 HTTP 요청 으로부터 hello URL 경로에 있는 값과 같은 일부 입력을 사용 하 여 람다 메서드를 통해 각 요청 toois 계산 합니다. 구성 된 toosend 요청 toohello 주 복제본만 또는 tooa 임의의 복제본 읽기 작업에 대 한 hello 정책 수 있습니다.

#### <a name="example"></a>예제

서비스 패브릭 응용 프로그램에서 시나리오를 따르는 hello, 라는 분할 된 상태 저장 서비스를 포함 `fabric:/app/userservice` 을 내부 HTTP API를 노출 합니다. hello 서비스 인스턴스 잘 알려져 이름과 hello 인바운드 처리 API 관리 정책에 직접 하드 코드 될 수 있습니다.  

hello 서비스가 분할 된 두 개의 파티션으로 hello Int64 파티션 구성표와 모두 포함 된 키 범위를 사용 하 여 `Int64.MinValue` 너무`Int64.MaxValue`합니다. hello를 변환 하 여 해당 범위 내에 파티션 키를 계산 하는 hello 백 엔드 정책 `id` 모든 알고리즘에서 사용 되는 여기서 toocompute hello 파티션 키를 사용할 수 있지만 hello URL 요청 경로 tooa 64 비트 정수에 제공 된 값입니다. 

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>상태 비저장 서비스 toomultiple 트래픽 보내기

보다 고급 시나리오에서는 지도 하나의 서비스 인스턴스와 toomore를 요청 하는 API 관리 작업을 정의할 수 있습니다. 이 경우 각 작업 포함 tooa 특정 서비스 인스턴스 hello 서비스 인스턴스 내에서 파티션 hello 들어오는 HTTP 요청에서 상태 저장 서비스의 대/소문자 hello 및 같은 hello URL 경로 또는 쿼리 문자열 값에 따라 요청을 매핑하는 정책 . 

tooachieve이 작업을 사용 하면 서비스 패브릭 백 엔드 hello 들어오는 HTTP 요청에서 검색 된 값에 따라 hello 서비스 패브릭 백 엔드의 tooa 상태 비저장 서비스 인스턴스에 매핑하는 인바운드 처리 정책을 포함 하는 API 관리 합니다. 요청 tooa 서비스 인스턴스 hello 서비스 인스턴스의 tooa 임의의 복제본에 전송 됩니다.

#### <a name="example"></a>예제

이 예제에서는 새 상태 비저장 서비스 인스턴스가 만들어집니다 응용 프로그램의 각 사용자에 대해 다음 수식을 hello를 사용 하 여 동적으로 생성 된 이름을 가진:
 
 - `fabric:/app/users/<username>`

 각 서비스에는 고유한 이름이 있지만 hello 이름을 알 수 없는 사전 hello 서비스 응답 toouser에 만들어집니다. 또는 관리자 입력 및 따라서 커야 APIM 정책 또는 라우팅 규칙에 하드 코딩 합니다. 대신, hello 서비스 toowhich toosend 요청의 hello 이름 hello에서 hello 백 엔드 정책 정의에 생성 됩니다 `name` hello URL 요청 경로에 제공 된 값입니다. 예:

  - A 너무 요청`/api/users/foo` 라우트된 tooservice 인스턴스가`fabric:/app/users/foo`
  - A 너무 요청`/api/users/bar` 라우트된 tooservice 인스턴스가`fabric:/app/users/bar`

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>상태 저장 서비스 toomultiple 트래픽 보내기

비슷한 toohello 상태 비저장 서비스 예제에서는 작업에 매핑할 수는 API 관리 요청 1 보다 toomore **stateful** 서비스 인스턴스, 상태 저장 서비스의 각 tooperform 파티션 확인 할 수 있습니다도 경우 인스턴스입니다.

tooachieve이 작업을 사용 하면 서비스 패브릭 백 엔드 hello 들어오는 HTTP 요청에서 검색 된 값에 따라 hello 서비스 패브릭 백 엔드의 tooa 상태 저장 서비스 인스턴스에 매핑하는 인바운드 처리 정책을 포함 하는 API 관리 합니다. 또한 매핑된 tooa hello 서비스 인스턴스 및 필요에 따라 tooeither hello 주 복제본 내에서 특정 파티션 또는 hello 파티션 내에서 임의 보조 복제본에서 요청 toospecific 서비스 인스턴스를 hello 요청 toomapping 될 수도 있습니다.

#### <a name="example"></a>예제

이 예제에서는 새 상태 저장 서비스 인스턴스가 만들어집니다 hello 응용 프로그램의 각 사용자에 대해 다음 수식을 hello를 사용 하 여 동적으로 생성 된 이름을 가진:
 
 - `fabric:/app/users/<username>`

 각 서비스에는 고유한 이름이 있지만 hello 이름을 알 수 없는 사전 hello 서비스 응답 toouser에 만들어집니다. 또는 관리자 입력 및 따라서 커야 APIM 정책 또는 라우팅 규칙에 하드 코딩 합니다. 대신, hello 서비스 toowhich toosend 요청의 hello 이름 hello에서 hello 백 엔드 정책 정의에 생성 됩니다 `name` 제공 된 값 hello URL 요청 경로입니다. 예:

  - A 너무 요청`/api/users/foo` 라우트된 tooservice 인스턴스가`fabric:/app/users/foo`
  - A 너무 요청`/api/users/bar` 라우트된 tooservice 인스턴스가`fabric:/app/users/bar`

각 서비스 인스턴스는 분할 된 두 개의 파티션으로 hello Int64 파티션 구성표와 모두 포함 된 키 범위를 사용 하 여 `Int64.MinValue` 너무`Int64.MaxValue`합니다. hello를 변환 하 여 해당 범위 내에 파티션 키를 계산 하는 hello 백 엔드 정책 `id` 모든 알고리즘에서 사용 되는 여기서 toocompute hello 파티션 키를 사용할 수 있지만 hello URL 요청 경로 tooa 64 비트 정수에 제공 된 값입니다. 

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>다음 단계

Hello에 따라 [빠른 시작 가이드](service-fabric-api-management-quick-start.md) tooset를 프로그램 첫 번째 서비스 패브릭 클러스터 tooyour 서비스 관리 API를 통해 API 관리 및 흐름 요청으로 합니다.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png