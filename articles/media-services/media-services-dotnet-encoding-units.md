---
title: "Azure-는 인코딩 단위를 추가 하 여 처리 aaaScale 미디어 |  Microsoft Docs"
description: "자세한 내용은 방법.net toohow tooadd 인코딩 단위"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>어떻게 tooscale.NET SDK와 인코딩
> [!div class="op_single_selector"]
> * [포털](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>개요
> [!IMPORTANT]
> 있는지 tooreview hello 확인 [개요](media-services-scale-media-processing-overview.md) 항목 tooget 항목을 처리 하는 미디어 확장에 대 한 자세한 내용은 합니다.
> 
> 

toochange hello 예약 단위 형식 및 hello 수가 인코딩 예약된 단위.NET SDK를 사용 하 여 다음 hello지 않습니다.

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>지원 티켓 열기
기본적으로 모든 미디어 서비스 계정은 tooup too25 확장할 수 인코딩 및 5 주문형 스트리밍 예약 단위입니다. 지원 티켓을 열어 더 높은 한도를 요청할 수 있습니다.

### <a name="open-a-support-ticket"></a>지원 티켓 열기
지원 티켓 tooopen 다음 hello지 않습니다.

1. [지원 받기](https://manage.windowsazure.com/?getsupport=true)를 클릭합니다. 로그인 하지 않은 경우 자격 증명 프롬프트 tooenter 수 있습니다.
2. 사용 중인 구독을 선택합니다.
3. 지원 유형으로 "기술적"을 선택합니다.
4. "티켓 만들기"를 클릭합니다.
5. "Azure 미디어 서비스" hello 제품 목록에서 hello 다음 페이지에 표시를 선택 합니다.
6. 사용자의 문제에 적절한 "문제 유형"을 선택합니다.
7. 계속을 클릭합니다.
8. 다음 페이지의 지시에 따라 문제에 대한 세부 정보를 입력합니다.
9. 클릭은 tooopen hello 티켓을 제출 합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

