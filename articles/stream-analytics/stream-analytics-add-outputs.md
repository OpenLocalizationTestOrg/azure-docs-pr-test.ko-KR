---
title: "스트림 분석 작업에 대 한 출력 aaaHow tooconfigure 데이터 | Microsoft Docs"
description: "Stream Analytics 작업에 대한 출력 구성 | 학습 경로 세그먼트."
keywords: "데이터 출력, 데이터 이동"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>스트림 분석 작업에 대 한 tooconfigure 데이터 출력 하는 방법

Azure 스트림 분석 작업이 연결 된 tooone 또는 연결 tooan 기존 데이터 싱크를 정의 하는 자세한 데이터 출력을 수 있습니다. 스트림 분석 작업을 처리 하 고 들어오는 데이터 변환으로 데이터 출력 이벤트 스트림의 tooyour 작업 출력을 기록 됩니다.

실시간 대시보드를 사용 하는 toosource 또는 경고, 트리거 데이터를 이동 하는 워크플로 또는 단순히 저장 된 데이터 일괄 처리는 나중에 처리에 대 한 스트림 분석 데이터 출력 될 수 있습니다. Stream Analytics은 여기에 자세히 문서화되어 있는 여러 Azure 서비스와 높은 수준으로 통합됩니다.

tooadd 출력 tooyour 스트림 분석 작업:

1. Hello에 [Azure 포털](https://portal.azure.com)작업 열고 클릭 **출력** 클릭 하 고 **추가** 나타나는 hello 출력 블레이드에서 합니다.
   
    ![출력 추가](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. 이 출력 hello에 대 한 이름을 제공 **출력 별칭** 상자입니다. 이 이름은 toorefer toohello 출력 나중에 작업의 쿼리에서 사용할 수 있습니다.  
   
    Hello 필요한 연결 속성 tooconnect tooyour 출력 hello 나머지를 입력 합니다.  이러한 필드는 출력 형식마다 다르며 여기서 자세히 정의됩니다.  
   
    ![데이터 이동 서비스 선택](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Hello 출력 종류에 따라 toospecify hello 데이터 serialize 되거나 포맷 어떻게 할 수 있습니다. 각 출력 형식에 대 한 특정 serialization 설정 hello 여기에 설명 되어 있습니다.
   
    Hello 필요한 연결 속성 tooconnect tooyour 데이터 원본 hello 나머지를 입력 합니다. 이러한 필드 입력 및 소스 형식의 형식에 따라 다르며 자세히 hello에 정의 되어 [작업 만들기 문서](stream-analytics-create-a-job.md)합니다.  

> [!Note]
>
> Hello 작업이 시작 되 고 이벤트 전송이 시작 모든 출력 요소 toohello 추가 된 작업을 종료 해야 합니다. 예를 들어 Blob 저장소를 사용 하 여 출력을 출력으로 hello 작업 자동으로 저장소 계정을 만들지 않습니다. Hello ASA 작업을 시작 하기 전에 hello 사용자가 만든 toobe가 필요 합니다.
> 
 

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

