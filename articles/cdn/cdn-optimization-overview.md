---
title: "aaaOptimize 시나리오에 대 한 Azure 콘텐츠 배달"
description: "어떻게 특정 시나리오에 대 한 콘텐츠 toooptimize 배달"
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
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>시나리오에 대한 Azure 콘텐츠 배달 최적화

콘텐츠 tooa 큰 글로벌 고객을 배달 때 콘텐츠 중요 tooensure 액세스에 최적화 된 hello 배달 됩니다. hello Azure 콘텐츠 배달 네트워크에 있는 콘텐츠의 hello 형식을 기반으로 하는 hello 배달 환경을 최적화할 수 있습니다. 콘텐츠는 다운로드를 위한 웹 사이트, 라이브 스트림, 비디오 또는 대용량 파일일 수 있습니다. Hello에서 시나리오를 지정 하는 콘텐츠 배달 네트워크 (CDN) 끝점을 만들 때는 **에 대 한 액세스에 최적화 된** 옵션입니다. 최적화가 적용 된 toohello 콘텐츠 hello CDN 끝점에서 배달 결정 합니다.

최적화 선택 항목은 설계 된 toouse 모범 사례 동작 tooimprove 콘텐츠 배달 성능 및 더 나은 원점 오프 로드 합니다. 시나리오 선택 사항이 부분 캐싱, 개체 청크 및 hello 원본 실패 다시 시도 정책에 대 한 구성을 수정 하 여 성능을 적용 합니다. 

이 문서에서는 다양한 최적화 기능과 사용 시기에 대해 간략하게 설명합니다. 기능 및 제한 사항에 대 한 자세한 내용은 각 개별 최적화 유형에 대해 hello 해당 문서를 참조 하십시오.

> [!NOTE]
> 프로그램 **에 대 한 액세스에 최적화 된** 옵션을 선택 하는 hello 공급자에 따라 달라질 수 있습니다. CDN 공급자 hello 시나리오에 따라 다양 한 방법으로 향상 된 기능을 적용 합니다. 

## <a name="provider-options"></a>공급자 옵션

hello Akamai에서 Azure 콘텐츠 배달 네트워크를 지원합니다.

* 일반 웹 배달 

* 일반 미디어 스트리밍

* 주문형 비디오 미디어 스트리밍

* 대용량 파일 다운로드

* 동적 사이트 가속 

hello Verizon에서 Azure 콘텐츠 배달 네트워크에는 일반 웹으로 전송만 지원합니다. 주문형 비디오 및 대용량 파일 다운로드에 사용할 수 있습니다. Tooselect 있는 최적화 형식을 않아도 됩니다.

배송에 대 한 다양 한 공급자 tooselect hello 최적의 공급자 간의 성능 차이 테스트 하는 것이 좋습니다.

## <a name="select-and-configure-optimization-types"></a>최적화 형식 선택 및 구성

toocreate 새 끝점의 경우 hello 시나리오에 가장 잘 맞는 있는 최적화 형식 및 콘텐츠 끝점 toodeliver hello 원하는 형식을 선택 합니다. **일반 웹 배달** 프로그램이 hello 기본으로 선택 합니다. 언제 든 지 모든 기존 Akamai 끝점에 대해 hello 최적화 옵션을 업데이트할 수 있습니다. 이 변경 hello CDN에서에서 배달을 중단 하지 않습니다. 

1. 표준 Akamai 프로필 내에서 끝점을 선택합니다.

    ![끝점 선택 ](./media/cdn-optimization-overview/01_Akamai.png)

2. **설정** 아래에서 **최적화**를 선택합니다. 다음 hello에서 형식을 선택 **에 대 한 액세스에 최적화 된** 드롭 다운 목록입니다.

    ![최적화 및 형식 선택](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>특정 시나리오에 대한 최적화

Hello 다음 시나리오 중 하나에 대 한 hello CDN 끝점을 최적화할 수 있습니다. 

### <a name="general-web-delivery"></a>일반 웹 배달

일반 웹 배달은 hello 가장 일반적인 최적화 옵션입니다. 웹 페이지 및 웹 응용 프로그램과 같은 일반 웹 콘텐츠 최적화를 위해 설계되었습니다. 이 최적화는 파일 및 비디오 다운로드에도 사용할 수 있습니다.

일반적인 웹 사이트에는 정적 및 동적 콘텐츠가 포함되어 있습니다. 정적 콘텐츠는 이미지, JavaScript 라이브러리 및 캐시 하 고 toodifferent 사용자가 배달할 수 있는 스타일 시트에 포함 됩니다. 동적 콘텐츠 뉴스 항목을 조정할 tooa 사용자 프로필와 같은 개별 사용자에 대해 개인화 된 합니다. 동적 콘텐츠는 쇼핑 카트 내용을 같은 고유 tooeach 사용자 되었기 때문에 캐시 되지 않습니다. 일반 웹 배달은 전체 웹 사이트를 최적화할 수 있습니다. 

> [!NOTE]
> Hello Akamai에서 Azure 콘텐츠 배달 네트워크를 사용 하는 경우 toouse이이 최적화 평균 파일 크기가 10 MB 보다 작은 경우. 평균 파일 크기를 10MB 보다 큰 경우 선택 **큰 파일을 다운로드** hello에서 **에 대 한 액세스에 최적화 된** 드롭 다운 목록입니다.

### <a name="general-media-streaming"></a>일반 미디어 스트리밍

라이브 스트리밍 및 주문형 비디오 스트리밍에 대 한 toouse hello 끝점을 해야 할 경우 일반 미디어를 스트리밍 최적화 좋습니다.

미디어 스트리밍는 시간적, 패킷 hello 클라이언트에 늦게 도착 하는 등의 비디오 콘텐츠 자주 버퍼링 된 성능이 저하 된 뷰를 제공 될 수 있기 때문입니다. 미디어 스트리밍 최적화 미디어 콘텐츠 전송의 hello 대기 시간이 줄어들고 사용자 부드러운 스트리밍 환경을 제공 합니다. 

이 시나리오는 Azure Media Service 고객에게 일반적입니다. Azure Media Services를 사용하면 하나의 스트리밍 끝점을 라이브 스트리밍과 주문형 스트리밍 둘 다에 사용할 수 있습니다. 이 시나리오에서 고객 라이브 tooon 주문형 스트리밍에서 변경 될 때 tooswitch tooanother 끝점이 필요 하지 않습니다. 일반 미디어 스트리밍 최적화는 이 유형의 시나리오를 지원합니다.

hello Verizon에서 Azure 콘텐츠 배달 네트워크 hello 일반 웹 배달 최적화 유형 toodeliver 스트리밍 미디어 콘텐츠를 사용합니다.

미디어 스트리밍 최적화에 대해 자세히 toolearn 참조 [미디어 스트리밍 최적화](cdn-media-streaming-optimization.md)합니다.

### <a name="video-on-demand-media-streaming"></a>주문형 비디오 미디어 스트리밍

주문형 비디오 미디어 스트리밍 최적화는 주문형 비디오 스트리밍 콘텐츠를 향상시킵니다. 주문형 비디오 스트리밍에 대 한 끝점을 사용 하는 경우이 옵션에 toouse 할 수 있습니다.

hello Verizon에서 Azure 콘텐츠 배달 네트워크 hello 일반 웹 배달 최적화 유형 toodeliver 스트리밍 미디어 콘텐츠를 사용합니다.

미디어 스트리밍 최적화에 대해 자세히 toolearn 참조 [미디어 스트리밍 최적화](cdn-media-streaming-optimization.md)합니다.

> [!NOTE]
> Hello 끝점 주문형 비디오 콘텐츠를 주로 담당 하는 경우 이와 같은 최적화를 사용 합니다. 이 최적화 및 hello 일반 미디어 스트리밍 최적화 사이의 hello 주요 차이점에는 hello 연결 다시 시도 제한 시간입니다. hello 제한 시간은 훨씬 더 짧은 toowork 라이브 스트리밍 시나리오입니다.

### <a name="large-file-download"></a>대용량 파일 다운로드

Hello Akamai에서 Azure 콘텐츠 배달 네트워크를 사용 하는 경우에 큰 파일 다운로드 toodeliver 파일 1.8 g B 보다 큰 사용 해야 합니다. Azure 콘텐츠 배달 네트워크에서 Verizon hello 다운로드 크기의 일반 웹 배달 최적화에서 파일에 대 한 제한이 없는 것입니다.

Hello Akamai에서 Azure 콘텐츠 배달 네트워크를 사용 하는 경우 큰 파일 다운로드 10 MB 보다 큰 콘텐츠에 대 한 최적화 됩니다. 평균 파일의 크기를 10 MB 보다 작은 경우 toouse 일반 웹 배달을 할 수 있습니다. 평균 파일 크기를 일관 되 게 10 MB 보다 큰 경우에 보다 효율적인 toocreate 큰 파일에 대 한 별도 끝점 수 있습니다. 예를 들어 펌웨어 또는 소프트웨어 업데이트는 일반적으로 대용량 파일입니다.

hello Verizon에서 Azure 콘텐츠 배달 네트워크 hello 일반 웹 배달 최적화 유형 toodeliver 스트리밍 미디어 콘텐츠를 사용합니다.

더 큰 파일을 최적화에 대 한 toolearn 참조 [큰 파일을 최적화](cdn-large-file-optimization.md)합니다.

### <a name="dynamic-site-acceleration"></a>동적 사이트 가속

 동적 사이트 가속은 Akamai 및 Verizon Content Delivery Network 프로필에서 모두 사용할 수 있습니다. 이 최적화는 추가 요금 toouse를 포함 됩니다. 자세한 내용은 hello 가격 책정 페이지를 참조 하세요.

동적 사이트 가속 hello 대기 시간 및 동적 콘텐츠의 성능을 활용 하는 다양 한 기술을 포함 합니다. 경로 및 네트워크 최적화, TCP 최적화 등이 이러한 기술에 포함됩니다. 

이 최적화 tooaccelerate 캐시할 수 없는 다양 한 응답을 포함 하는 웹 앱을 사용할 수 있습니다. 예를 들어 검색 결과, 체크 아웃 트랜잭션 또는 실시간 데이터가 있습니다. 정적 데이터에 대 한 toouse 핵심 CDN 캐싱 기능을 계속할 수 있습니다. 



