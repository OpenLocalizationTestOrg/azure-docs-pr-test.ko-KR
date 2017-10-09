---
title: "Azure CDN을 통해 사이트 가속 aaaDynamic"
description: "동적 사이트 가속 심층 분석"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Azure CDN을 통해 동적 사이트 가속

소셜 미디어, 전자 상거래 및 hello 하이퍼 개인 설정 웹 hello 폭발, 빠르게 증가 백분율로 hello 콘텐츠 tooend 사용자 제공은 실시간으로 생성 합니다. 사용자는 브라우저, 위치, 장치 또는 네트워크와 독립된 빠르고 안정적인 개인 설정 웹 환경을 기대합니다. 그러나 또한 참여 하므로 이러한 환경을 구성 하는 hello 매우 혁신적이 대 한 느린 페이지 다운로드 하 고 hello 소비자 환경의 hello 품질 위험에 노출 합니다. 

표준 CDN 기능 hello 기능 toocache 파일 자세히 tooend 사용자 toospeed 정적 파일 배달을 포함합니다. 그러나 동적 웹 응용 프로그램과 함께 가장자리 위치에서 해당 콘텐츠를 캐싱하 수는 없습니다 hello 서버 응답 toouser 동작이 hello 콘텐츠를 생성 하기 때문입니다. 이러한 콘텐츠의 hello 배달 속도 기존의 지 캐싱 보다 더 복잡 한 고 각 요소에서 초기 toodelivery hello 전체 데이터 경로 따라 정밀 하 게 조정 하는 종단 간 솔루션 필요 합니다. Azure CDN 동적 사이트 Acceleration (DSA)와 함께, 동적 콘텐츠가 포함 된 웹 페이지의 hello 성능은 눈에 띄게 향상 됩니다.

Akamai 및 Verizon에서 azure CDN은 hello 통해 DSA 최적화를 제공 **에 대 한 액세스에 최적화 된** 메뉴 끝점을 만드는 중입니다.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>CDN 끝점 tooaccelerate 배달을 동적 파일의 구성

Azure 포털을 통해 동적 파일의 CDN 끝점 toooptimize 배송 hello를 선택 하 여 구성할 수 있습니다 **동적 사이트 가속** hello 옵션 **에 대 한 액세스에 최적화 된** 하는 동안 속성 선택 hello 끝점을 만드는 합니다. 또한 REST Api를 사용할 수 있습니다 또는 동일한 작업을 프로그래밍 방식으로 hello hello 클라이언트 Sdk toodo 중 하나입니다. 

### <a name="probe-path"></a>프로브 경로
프로브 경로 사이트 가속 기능 특정 tooDynamic 되며 올바른 만들기 위해 필요 합니다. DSA 작은 사용 하 여 *프로브 경로* hello 원점 toooptimize 네트워크 라우팅 구성에 대해 CDN hello 파일 배치 합니다. 다운로드 하 고 우리의 샘플 파일 tooyour 사이트를 업로드 하거나 약 10KB hello 프로브 경로 대 한 대신가 있는 경우 hello 자산 원본에서 기존 자산을 사용할 수 있습니다.

> [!Note]
> DSA 사용 시 별도 요금이 발생합니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cdn/) 자세한 정보에 대 한 합니다.

다음 스크린 샷을 hello Azure 포털을 통해 hello 과정을 보여 줍니다.
 
![새 CDN 끝점 추가](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*그림 1: hello CDN 프로필에서에서 새 CDN 끝점 추가*
 
![DSA를 사용하여 새 CDN 끝점 만들기](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*그림 2: 동적 사이트 가속 최적화가 선택된 CDN 끝점 만들기*

Hello CDN 끝점을 만든 후에 특정 기준에 일치 하는 모든 파일에 대 한 hello DSA 최적화 적용 됩니다. 다음 단원을 hello DSA 최적화 자세히 설명 합니다.

## <a name="dsa-optimization-using-azure-cdn"></a>Azure CDN을 사용하여 DSA 최적화

Azure CDN에서 동적 사이트 가속 기술을 다음 hello를 사용 하 여 동적 자산의 배달 속도가 향상:

-   경로 최적화
-   TCP 최적화
-   개체 사전 인출(Akamai에만 해당)
-   모바일 이미지 압축(Akamai에만 해당)

### <a name="route-optimization"></a>경로 최적화

경로 최적화는 hello 인터넷 동적 출발점이, 여기서 트래픽 및 일시적으로 중단 지속적으로 변경 하는 hello 네트워크 토폴로지는 중요 합니다. hello 프로토콜 BGP (경계 게이트웨이)는 hello 인터넷의 hello 라우팅 프로토콜 있지만 중간 지점의 현재 상태 (PoP) 서버를 통해 더 빠른 경로 있을 수 있습니다. 

경로 최적화를 hello 최적의 경로 toohello 원본 사이트에서 계속 액세스할 수 있고 동적 콘텐츠를 배달 tooend가 가장 빠른 hello 및 가장 신뢰할 수 있는 경로 통해 선택 합니다. 

hello Akamai 네트워크 기술을 toocollect 실시간 데이터 사용 하 고 hello open 인터넷 toodetermine hello 빠른 라우팅을 hello 원점과 hello 간의 전체 hello 기본 BGP 경로 비롯 하 여 hello Akamai 서버에 다른 노드를 통해 다양 한 경로 비교 합니다. CDN 가장자리입니다. 이러한 기술은 인터넷 정체 지점과 긴 경로를 회피합니다. 

마찬가지로, 애니캐스트 DNS, 대용량의 조합을 지원, Pop 및 상태 검사 toodetermine hello 최상의 게이트웨이 toobest에서 경로 데이터 hello Verizon 네트워크에서 클라이언트 toohello 원점을 hello 합니다.
 
보다 빠르고 보다 안정적으로 완전히 동적이 고 트랜잭션 콘텐츠 전달 결과적으로, tooend 사용자가 캐시할 수 없는 경우에 합니다. 

### <a name="tcp-optimizations"></a>TCP 최적화

전송이 TCP (Control Protocol)의 hello 인터넷 프로토콜 모음 hello 표준을 사용 하는 IP 네트워크에서 응용 프로그램 간 toodeliver 정보입니다.  기본적으로 몇 백 하며 요청으로 TCP 연결의 경우이 인해 배율로 비효율성 제한 tooavoid 네트워크 congestions를 tooset를 필요한 하는 전달 합니다. Akamai의 Azure CDN은 3개의 영역을 최적화하여 이 문제를 다룹니다. 

 - 느린 시작 제거
 - 영구 연결 활용
 - TCP 패킷 매개 변수 조정(Akamai에만 해당)

#### <a name="eliminating-slow-start"></a>느린 시작 제거

*시작 속도가 느린* hello hello 네트워크를 통해 전송 되는 데이터 양을 제한 하 여 네트워크 혼잡을 방지 하는 hello TCP 프로토콜의 일부입니다. 시작 발신자와 수신자 사이의 작은 혼잡 한 창 크기와 최대 hello에 도달 하거나 패킷 손실이 검색 될 때까지 합니다.

Akamai 및 Verizon의 Azure CDN은 세 단계로 느린 시작을 제거합니다.

1.  Akamai와 Verizon의 네트워크 상태 및 toomeasure hello 대역폭 지 PoP 서버 간 연결을 모니터링 하는 대역폭을 사용 합니다.
2. 각 서버 hello 네트워크 상태를 인식 하며 서버 상태를 다른 Pop 주위의 hello 있도록 hello 메트릭 지 PoP 서버 간에 공유 됩니다.  
3. hello CDN에 지 서버 hello 최적의 창 크기의 근접에서 다른 CDN에 지 서버와 통신할 때 사용 해야 하는 등의 몇 가지 전송 매개 변수 수 toomake 가정 됩니다. 이 단계는 hello 상태 hello CDN에 지 서버 간의 hello 연결의 패킷 데이터 전송을 더 높은 수 있는 경우 hello 초기 혼잡 창 크기를 늘릴 수 있는지를 의미 합니다.  

#### <a name="leveraging-persistent-connections"></a>영구 연결 활용

CDN을 사용 하는 고유 컴퓨터 수가 적어집니다 tooyour 원점 직접 연결 하는 사용자와 직접 비교 tooyour 원본 서버를 연결 합니다. Akamai 및 Verizon에서 azure CDN 풀 사용자 요청 함께 tooestablish hello 원점와 더 적은 수의 연결 합니다.

앞서 언급 했 듯이 TCP 연결 몇 개의 요청 간에에 걸릴 핸드셰이크 tooestablish 새 연결. 영구 연결 라고도 "HTTP 연결 유지," 여러 HTTP 요청 toosave 라운드트립 시간에 대 한 기존 TCP 연결을 다시 사용 및 배달 속도입니다. 

또한 hello Verizon 네트워크 hello TCP 연결 tooprevent 닫히는에서 열려 있는 연결을 통해 정기적으로 연결 유지 패킷이 보냅니다.

#### <a name="tuning-tcp-packet-parameters"></a>TCP 패킷 매개 변수 조정

Akamai에서 azure CDN도 서버 간 연결을 제어 하는 hello 매개 변수를 튜닝 한 후 다음 기술을 hello를 사용 하 여 hello 사이트에 포함 된 round trips 필요한 tooretrieve 콘텐츠 장거리의 hello 양이 줄어듭니다.

1.  승인을 기다리지 않고 더 많은 패킷을 보내고 받을 수 있도록 hello 초기 정체 창을 증가 합니다.
2.  손실을 검색 하 고 재전송 더 빠르게 수행 되도록 hello 초기 재전송 시간 제한을 감소 합니다.
3.  감소 hello 최소 및 최대 재전송 시간 제한 tooreduce hello 대기 시간 패킷 전송 중에 손실 된 가정 하기 전에.

### <a name="object-prefetch-akamai-only"></a>개체 사전 인출(Akamai에만 해당)

대부분의 웹 사이트는 이미지 및 스크립트와 같은 다양한 리소스를 참조하는 HTML 페이지로 구성됩니다. 일반적으로 웹 페이지를 요청 하는 클라이언트 hello 브라우저를 먼저 다운로드 및 hello HTML 개체를 구문 분석 하 고 있도록 toolinked 자산을 필요한 toofully hello 페이지를 로드 하는 추가 요청 합니다. 

*프리페치* 은 기술 tooretrieve 이미지 및 스크립트에에서 포함 된 hello HTML 페이지 hello HTML 광고가 toohello 브라우저 및 hello 하기 전에 브라우저도에서는 이러한 개체 요청 하는 동안 합니다. 

Hello로 **프리페치** 옵션이 경우 CDN hello HTML 기본 페이지 toohello 클라이언트의 브라우저를 사용 하는 hello hello CDN hello 시 설정 되어 있으면 hello HTML 파일의 구문 분석 수행 연결된 된 리소스에 대 한 추가 요청 하 고 캐시에 저장 합니다. Hello 클라이언트에서는 hello 요청 hello 연결 된 자산에 대 한, hello CDN에 지 서버가 이미 요청 된 개체에 hello에 및 사용 될 수 있습니다 이러한 즉시 왕복 toohello 원점 하지 않고 있습니다. 이 최적화는 캐시할 수 있는 콘텐츠 및 캐시할 수 없는 콘텐츠에 모두 제공됩니다.

### <a name="adaptive-image-compression-akamai-only"></a>적응 이미지 압축(Akamai에만 해당)

일부 장치, 모바일 세션 특히 느린 네트워크 속도 시간 tootime에서 발생합니다. 이러한 시나리오에서 더는 것이 hello 사용자 tooreceive 해당 웹 페이지에 더 작은 이미지에 대 한 전체 고해상도 이미지에 대 한 오래 대기 하는 대신에 보다 신속 하 게 합니다.

이 기능은 자동으로 네트워크 품질을 모니터링 하 고 네트워크 속도가 느린 tooimprove 배달 시간 때 표준 JPEG 압축 메서드를 사용 합니다.

적응 이미지 압축 | 파일 확장명  
--- | ---  
JPEG 압축 | .jpg, .jpeg, .jpe, .jig, .jgig, .jgi

## <a name="caching"></a>구성

DSA와 캐싱 꺼져 hello CDN에서에 기본적으로 hello 원점 hello에 대 한 응답 제어/만료 캐시 머리글을 포함 하는 경우에 있습니다. DSA 고유 tooeach 클라이언트는 있으므로 캐시 하지 않아야 하는 동적 자산에 대 한 일반적으로 사용 되기 때문에이 기본값은 해제 하 고 기본적으로 캐시를 설정 하면이 동작 손상 될 수 있습니다.

정적 및 동적 자산을 조합 하 여 웹 사이트를 설정한 경우 최상의 tootake 하이브리드 방식 tooget hello 최상의 성능입니다. 

ADN Verizon premium을 사용 하는 경우 규칙 엔진 hello를 사용 하 여 특정 사례에 대 한 캐싱 다시 설정할 수 있습니다.  

CDN 끝점을 두 개의 toouse 것이 좋습니다. DSA toodeliver 동적 자산을 사용 하 여 및 정적 최적화와 함께 다른 끝점 형식, 예: 일반 웹 배달 toodelivery 캐시할 자산입니다. 이 대체 순서 tooaccomplish, toohello 자산에 hello toouse CDN 끝점을 직접 웹 페이지 Url toolink를 수정 합니다. 

예를 들어: `mydynamic.azureedge.net/index.html` 동적 페이지가 고 hello DSA 끝점에서 로드 됩니다.  hello html 페이지를 참조 JavaScript 라이브러리와 같은 여러 정적 자산 또는에서 로드 되는 이미지와 같은 정적 CDN 끝점을 hello `mystatic.azureedge.net/banner.jpg` 및 `mystatic.azureedge.net/scripts.js`합니다. 

예를 찾을 수 있습니다 [여기](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) 어떻게 toouse 컨트롤러에는 ASP.NET 웹 응용 프로그램 tooserve 콘텐츠 특정 CDN URL을 통해에 있습니다.




