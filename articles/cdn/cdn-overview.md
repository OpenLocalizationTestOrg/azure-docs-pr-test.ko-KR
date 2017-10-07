---
title: "aaaAzure CDN 개요 | Microsoft Docs"
description: "Azure 콘텐츠 배달 네트워크 (CDN)은 어떤 hello에 알아봅니다 방법과 toouse 것 blob 및 정적 콘텐츠를 캐시 하 여 toodeliver 고대역폭 콘텐츠입니다."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Hello Azure 콘텐츠 배달 네트워크 (CDN)의 개요
> [!NOTE]
> 이 문서에서는 Azure 콘텐츠 배달 네트워크 (CDN)은 어떤 hello, 작동 방법 및 각 Azure CDN 제품의 hello 기능에 설명 합니다.  Tooskip이 정보를 표시할 경우 및 방법 대 직선 tooa 자습서 이동 toocreate CDN 끝점 참조 [Azure CDN을 사용 하 여](cdn-create-new-endpoint.md)합니다.  현재 CDN 노드 위치 목록을 toosee 참조 [Azure CDN POP 위치](cdn-pop-locations.md)합니다.
> 
> 

Azure 콘텐츠 배달 네트워크 (CDN) hello toousers 콘텐츠를 제공 하기 위한 전략적으로 배치 된 위치 tooprovide 최대 처리량에서 정적 웹 콘텐츠를 캐시 합니다.  CDN hello 개발자에 게 hello 전 세계 물리적 노드에서 hello 콘텐츠를 캐시 하 여 고대역폭 콘텐츠를 배달 하기 위한 글로벌 솔루션을 제공 합니다. 

hello CDN toocache 웹 사이트 자산을 사용 하 여 hello 이점은 다음과 같습니다.

* 더 나은 성능과 사용자 tooload 콘텐츠를 필요한 여러 번 왕복 있는 응용 프로그램을 사용 하는 경우에 특히 최종 사용자에 대 한 환경을 제공 합니다.
* 대형 배율 toobetter 제품의 hello 시작 될 때 시작 이벤트와 같은 일시적인 고 부하를 처리 합니다.
* 사용자 요청을 배포 하 고에 지 서버에서 콘텐츠 처리를 적게 트래픽이 toohello 원점을 전송 됩니다.

## <a name="how-it-works"></a>작동 방법
![CDN 개요](./media/cdn-overview/cdn-overview.png)

1. 사용자(Alice)가 특수 도메인 이름(예: `<endpointname>.azureedge.net`)으로 URL을 사용하여 파일(자산이라고도 함)을 요청합니다.  DNS는 hello 요청 toohello 가장 낮은 상태 지점 (POP) 위치를 라우팅합니다.  일반적으로이 hello POP 지리적으로 가장 가까운 toohello 사용자입니다.
2. Hello POP에에서 hello에 지 서버에서 캐시에에서 hello 파일이 수 없는 경우 hello에 지 서버 hello 원점에서 hello 파일을 요청 합니다.  Azure 웹 앱, Azure 클라우드 서비스, Azure 저장소 계정 또는 공개적으로 액세스할 수 있는 웹 서버 hello 원점 수 있습니다.
3. hello 원점 hello 파일 toohello 지 서버를 hello 파일의 시간 to Live (TTL)를 설명 하는 선택적 HTTP 헤더를 포함 하 여 반환 합니다.
4. hello에 지 서버 hello 파일을 캐시 하 고 hello 파일 toohello 원래 요청자 (Alice)를 반환 합니다.  hello 파일 hello TTL 만료 될 때까지 hello에 지 서버에 캐시 된 상태로 유지 됩니다.  Hello 원본 TTL을 지정 하지 않은 경우 hello 기본 TTL은 7 일입니다.
5. 추가 사용자가 요청 hello 동일한 URL을 사용 하 여 파일 동일 하 고 있을 수 있습니다 수 방향이 지정 된 toothat 수 있습니다. 동일한 POP 합니다.
6. Hello 파일에 대 한 hello TTL 만료 되지 않았는지 hello에 지 서버 hello 캐시에서 hello 파일을 반환 합니다.  이렇게 하면 보다 신속하고 응답성이 뛰어난 사용자 환경이 가능합니다.

## <a name="azure-cdn-features"></a>Azure CDN 기능
Azure CDN 제품은 **Akamai의 Azure CDN Standard**, **Verizon의 Azure CDN Standard**, **Verizon의 Azure CDN Premium**, 세 가지가 있습니다.  hello 다음 표에 hello 기능 각 제품을 사용할 수 있습니다.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __성능 기능과 최적화__ |
| [동적 사이트 가속](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[동적 사이트 가속 - 적응 이미지 압축](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[동적 사이트 가속 - 개체 프리페치](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [비디오 스트리밍 최적화](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [큰 파일 최적화](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [전역 서버 부하 분산(GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [빠른 삭제](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [자산 미리 로드](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [쿼리 문자열 캐싱](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| IPv4/IPv6 이중 스택 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTP/2 지원](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __보안__ |
| CDN 끝점에 HTTPS 지원 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [사용자 지정 도메인 HTTPS](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [사용자 지정 도메인 이름 지원](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [지역 필터링](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [토큰 인증](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [DDOS 보호](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __분석 및 보고__ |
| [핵심 분석](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [고급 HTTP 보고서](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [실시간 통계](cdn-real-time-stats.md) | | |**&#x2713;** |
| [실시간 경고](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __사용 편의성__ |
| [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md), [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md)와 같은 Azure와 간편하게 통합 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [REST API](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) 또는 [PowerShell](cdn-manage-powershell.md)을 통한 관리. |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [사용자 지정이 가능한 규칙 기반의 콘텐츠 배달 엔진](cdn-rules-engine.md) | | |**&#x2713;** |
| 캐시/헤더 설정( [규칙 엔진](cdn-rules-engine.md)사용) | | |**&#x2713;** |
| URL 리디렉션/다시 쓰기([규칙 엔진](cdn-rules-engine.md)사용) | | |**&#x2713;** |
| 모바일 장치 규칙( [규칙 엔진](cdn-rules-engine.md)사용) | | |**&#x2713;** |

\*Verizon은 일반 웹 배달을 통해 큰 파일 및 미디어를 직접 지원합니다.


> [!TIP]
> Azure CDN에서 toosee 원하는 기능 거기?  [피드백 보내기](https://feedback.azure.com/forums/169397-cdn) 
> 
> 

## <a name="next-steps"></a>다음 단계
CDN에서 시작 tooget 참조 [Azure CDN을 사용 하 여](cdn-create-new-endpoint.md)합니다.

기존 CDN 고객 인 경우 hello 통해 CDN 끝점 이제 관리할 수 있습니다 [Microsoft Azure 포털](https://portal.azure.com) 또는 [PowerShell](cdn-manage-powershell.md)합니다.

toosee 동작에서 CDN을 hello, 체크 아웃 hello [우리의 빌드 2016 세션의 비디오](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/)합니다.

자세한 내용은 방법 tooautomate Azure CDN와 [.NET](cdn-app-dev-net.md) 또는 [Node.js](cdn-app-dev-node.md)합니다.

가격 정보는 [CDN 가격 책정](https://azure.microsoft.com/pricing/details/cdn/)을 참조하세요.

