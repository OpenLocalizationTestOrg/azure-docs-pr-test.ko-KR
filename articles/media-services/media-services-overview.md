---
title: "aaaAzure 미디어 서비스 개요 | Microsoft Docs"
description: "이 항목에서는 Azure Media Services에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Azure Media Services 개요 

Microsoft Azure 미디어 서비스는 개발자 toobuild 확장 가능한 미디어 관리 및 제공 응용 프로그램 수 있도록 하는 확장 가능한 클라우드 기반 플랫폼입니다. Toosecurely 업로드를 허용 하는 REST Api를 기반으로 하는 미디어 서비스, 저장, 인코딩 및 주문형 및 라이브 스트리밍 배달 toovarious 클라이언트 모두 (예를 들어, TV, PC 및 모바일 장치)에 대 한 비디오 또는 오디오 콘텐츠를 패키지 합니다.

전체 Media Services를 사용하여 종단 간 워크플로를 작성할 수 있습니다. 작업을 워크플로의 일부분에 대해 타사 구성 요소 toouse로 선택할 수도 있습니다. 예를 들어 타사 인코더를 사용하여 인코딩합니다. 그런 다음 Media Services를 사용하여 업로드, 보호, 패키징 및 배달합니다.

주문형으로 콘텐츠를 배달 하거나 toostream 라이브 콘텐츠를 선택할 수 있습니다. 또한 hello 항목 tooother 관련 항목을 안내합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
여기서 AMS 학습 경로를 볼 수 있습니다.

* [AMS 라이브 스트리밍 워크플로](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [AMS 주문형 스트리밍 워크플로](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>필수 조건

Azure 미디어 서비스를 사용 하 여 toostart hello 다음 있어야 합니다.

* Azure 계정. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com)을 참조하세요.
* Azure Media Services 계정. 자세한 내용은 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.
* (선택 사항) 개발 환경 설정. 개발 환경에 .NET 또는 REST API를 선택합니다. 자세한 내용은 [환경 설정](media-services-dotnet-how-to-use.md)을 참조하세요.

    또한, 너무 방법을 학습[tooAMS API를 프로그래밍 방식으로 연결](media-services-use-aad-auth-to-access-ams-api.md)합니다.
* 시작된 상태에 있는 표준 또는 프리미엄 스트리밍 끝점.  자세한 내용은 [스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)를 참조하세요.

## <a name="sdks-and-tools"></a>SDK 및 도구

toobuild 미디어 서비스 솔루션을 사용할 수 있습니다.

* [Media Services REST API](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Hello 사용 가능한 클라이언트 Sdk 중 하나입니다.
    * [.NET용 Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services),
    * [Java용 Azure SDK](https://github.com/Azure/azure-sdk-for-java),
    * [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),
    * [Node.js용 Azure Media Services](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Node.js SDK의 Microsoft가 아닌 타사 버전입니다. 커뮤니티에서 유지 관리 되 고 현재 없는 hello AMS Api의 100% 검사).
* 기존 도구:
    * [Azure Portal](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE(Azure Media Services 탐색기)는 Windows용 Winforms/C# 응용 프로그램임)

## <a name="concepts-and-overview"></a>개념 및 개요
Azure Media Services 개념은 [개념](media-services-concepts.md)을 참조하세요.

방법-tooseries tooall hello의 주요 구성 요소 Azure 미디어 서비스를 소개 하는, 참조 [Azure 미디어 서비스 단계별 자습서](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series)합니다. 이 시리즈 개념에 대 한 훌륭한 개괄적 개이고 hello AMSE 도구 toodemonstrate AMS 작업을 사용 합니다. AMSE 도구는 Windows 도구입니다. 이 도구는 대부분의 hello 작업을 프로그래밍 방식으로 작업을 수행할 수 지원 [AMS SDK for.NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), 또는 [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)합니다.

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>지원되는 시나리오 및 데이터 센터에서 Media Services의 사용 가용성

자세한 내용은 [AMS 시나리오 및 데이터 센터에서 기능 및 서비스의 사용 가용성](scenarios-and-availability.md)을 참조하세요.

## <a name="service-level-agreement-sla"></a>SLA(서비스 수준 계약)

* Media Services Encoding을 위해 REST API 트랜잭션의 99.9% 가용성을 보장합니다.
* 표준 또는 프리미엄 스트리밍 끝점을 구매하는 경우 스트리밍을 위해 기존 미디어 콘텐츠에 대해 99.9% 가용성을 보장하는 요청을 서비스합니다.
* 라이브 채널에 대 한 채널을 실행 해야는 외부 연결 hello 시간의 99.9% 이상의 하 게 됩니다.
* 콘텐츠 보호는 우리는 성공적으로 요청을 처리 해야 키 이상 hello 시간의 99.9% 보장 합니다.
* 에 대 한 인덱서에서는 요청을 처리 인덱서 작업 인코딩 예약을 사용 하 여 처리 hello 시간 단위 99.9%입니다.

자세한 내용은 [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/)를 참조하세요.

데이터 센터의 가용성에 대 한 정보를 참조 hello [Avaiability](scenarios-and-availability.md#availability) 섹션.

## <a name="support"></a>지원

[Azure 지원](https://azure.microsoft.com/support/options/) 에서는 Media Services를 포함하여 Azure에 대한 지원 옵션을 제공합니다.

## <a name="provide-feedback"></a>피드백 제공

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
