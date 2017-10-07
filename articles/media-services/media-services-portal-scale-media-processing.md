---
title: "사용 하 여 처리 aaaScale 미디어 hello Azure 포털 | Microsoft Docs"
description: "이 자습서에서는 hello Azure 포털을 사용 하 여 처리 하는 크기 조정 미디어의 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Hello 예약 단위 형식 변경
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [포털](media-services-portal-scale-media-processing.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>개요

미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약 된 단위 유형과 연관 되어 있습니다. Hello 다음 중에서 선택할 수 예약 단위 형식: **S1**, **S2**, 또는 **S3**합니다. Hello를 사용할 때 동일한 인코딩 작업이 더 빠르게 실행 하는 hello 예를 들어 **S2** toohello 비교 하는 예약된 단위 형식 **S1** 유형입니다.

또한 toospecifying hello 예약 단위 형식, tooprovision를 사용 하 여 계정을 지정할 수 있습니다 **예약 단위** (RUs). 프로 비전 된 RUs hello 수 hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다.

>[!NOTE]
>RU는 Azure Media Indexer를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다. 그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.

> [!IMPORTANT]
> 있는지 tooreview hello 확인 [개요](media-services-scale-media-processing-overview.md) 항목 tooget 항목을 처리 하는 미디어 확장에 대 한 자세한 내용은 합니다.
> 
> 

## <a name="scale-media-processing"></a>미디어 처리 크기 조정
toochange hello 예약 단위 형식 및 hello 예약된 단위 수를 다음 hello지 않습니다.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. Hello에 **설정** 창에서 **미디어 예약 단위**합니다.
   
    예약된 단위 형식 너무 많이 선택 hello에 대 한 예약 단위 toochange hello 수, hello를 사용 하 여 **미디어 처리 단위** 슬라이더 합니다.
   
    toochange hello **예약 단위 형식**, S1, S2 또는 S3 키를 누릅니다.
   
    ![프로세서 페이지](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. 단추 toosave 변경 내용을 저장 하는 hello 키를 누릅니다.
   
    저장 단추를 누를 때 hello 새 예약된 단위 할당 됩니다.

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

