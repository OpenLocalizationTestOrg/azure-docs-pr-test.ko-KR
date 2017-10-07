---
title: "Azure 미디어 서비스에서 Azure CDN 캐싱 정책 aaaManage | Microsoft Docs"
description: "자세한 내용은 방법 toomanage Azure 미디어 서비스에서 Azure CDN 캐싱 정책입니다."
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Azure Media Services에서 Azure CDN 캐싱 정책 관리
Azure 미디어 서비스는 HTTP 기반 적응 스트리밍 및 점진적 다운로드를 제공합니다. HTTP 기반 스트리밍은 클라이언트 쪽 캐싱뿐만 아니라 프록시 및 CDN 계층의 캐싱을 활용하므로 확장성이 뛰어납니다. 스트리밍 끝점은 일반적인 스트리밍 기능 및 HTTP 캐시 헤더에 대한 구성을 제공합니다. 스트리밍 끝점은 HTTP Cache-Control: max-age 및 Expires 헤더를 설정합니다. HTTP 캐시 헤더에 대한 자세한 내용은 [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html)에서 확인할 수 있습니다.

## <a name="default-caching-headers"></a>기본 캐싱 헤더
기본적으로 스트리밍 끝점은 주문형 스트리밍 데이터(실제 미디어 조각/청크) 및 매니페스트(재생 목록)에 대해 3일 캐시 헤더를 적용합니다. 라이브 스트리밍의 경우 스트리밍 끝점은 데이터(실제 미디어 조각/청크)에 대해 3일 캐시 헤드를 적용하고, 매니페스트(재생 목록) 요청에 대해 2초 캐시 헤더를 적용합니다. 라이브 프로그램 바뀌면 tooon 주문형 (라이브 보관) 주문형 스트리밍 캐시 헤더 적용 됩니다.

## <a name="azure-cdn-integration"></a>Azure CDN 통합
Azure 미디어 서비스는 스트리밍 끝점에 대한 [CDN 통합](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) 을 제공합니다. 캐시 제어 헤더에에서 적용 됩니다 hello 동일한 방식으로 스트리밍 끝점 tooCDN 사용 스트리밍 끝점입니다. 캐시 된 개체도이 값 tooset hello 배달 캐시 헤더를 사용 하는 내부적으로 구성 된 끝점 캐시 값 toodefine hello의 수명이 hello 스트리밍 azure CDN 사용 합니다. CDN 사용 스트리밍 끝점을 사용 하는 경우 tooset 작은 캐시 값을 권장 되지 않습니다. 작은 값을 설정 hello 성능이 저하 되 고 CDN의 hello 이점은 줄일 됩니다. CDN에 대 한 600 초 미만의 tooset 캐시 헤더 사용 스트리밍 끝점에서는 허용 되지 않습니다.

> [!IMPORTANT]
>Azure Media Services는 Azure CDN과 완전하게 통합됩니다. 한 번의 클릭으로 모든 hello 사용 가능한 Azure CDN 공급자 (Akamai 및 Verizon) tooyour 스트리밍 CDN 표준 및 프리미엄 제품을 포함 하 여 끝점을 통합할 수 있습니다. 자세한 내용은 이 [공지](https://azure.microsoft.com/blog/standardstreamingendpoint/)를 참조하세요.
> 
> 만 스트리밍 끝점 tooCDN에서 데이터 요금 hello CDN 사용 스트리밍 끝점 Api 또는 Azure 관리 포털의 스트리밍 끝점 섹션을 사용 하 여 위에 비활성화를 가져옵니다. 수동 통합 또는 CDN Api 또는 포털 섹션을 사용 하 여 CDN 끝점을 직접 만드는 hello 데이터 요금을 해제 하지 됩니다.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Azure 미디어 서비스를 사용하여 캐시 헤더 구성
Azure 관리 포털 또는 Azure 미디어 서비스 Api tooconfigure 캐시 헤더 값을 사용할 수 있습니다.

1. 관리를 사용 하 여 tooconfigure 캐시 헤더 포털 너무 참조 하십시오[어떻게 tooManage 스트리밍 끝점](../media-services/media-services-portal-manage-streaming-endpoints.md) 섹션 구성 hello 스트리밍 끝점입니다.
2. Azure 미디어 서비스 REST API, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl)
3. Azure 미디어 서비스 .NET SDK, [StreamingEndpointCacheControl 속성](http://go.microsoft.com/fwlink/?LinkId=615302)

## <a name="cache-configuration-precedence-order"></a>캐시 구성 우선 순위
1. Azure 미디어 서비스에서 구성된 캐시 값은 기본값을 재정의합니다.
2. 수동 구성이 없으면 기본값이 적용됩니다.
3. 기본적으로 캐시 헤더 toolive Azure 미디어 또는 Azure 저장소 구성에 관계 없이 manifest(playlist) 스트리밍 및이 값의 재정의 적용 하는 2 초 제공 되지 않습니다.

