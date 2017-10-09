---
title: "스트림 분석에 대 한 데이터 분석 처리 작업이 aaaHow toocreate | Microsoft Docs"
description: "Stream Analytics을 위한 데이터 분석 처리 작업 만들기 | 학습 경로 세그먼트."
keywords: "데이터 분석 처리"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>어떻게 toocreate 데이터 분석 처리는 스트림 분석에 대 한을 작업합니다
Azure 스트림 분석에서 hello 최상위 리소스는 스트림 분석 작업 합니다.  하나 이루어져 하거나 더 많은 데이터 원본과 데이터 변환 hello를 표현 하는 쿼리 결과에 기록 되며 하나 이상의 출력 대상을 입력 합니다. 스트리밍 데이터에 대 한 시나리오를 처리 하는 hello 사용자 tooperform 데이터 분석을 통해 이러한 있습니다.

스트림 분석을 사용 하 여 toostart 먼저 새 스트림 분석 작업을 만듭니다.  Note hello 작업이 시작 될 때까지이 작업에 요금이 청구 될 없습니다.

1. 온라인 hello에 로그인 [Azure 클래식 포털](http://manage.windowsazure.com) 또는 hello [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 포털에서: **새 클릭**, 클릭 **데이터 서비스** 또는 **데이터 분석** 포털을 클릭 한 다음에 따라 **Azure스트림분석** 또는 **Stream Analytics** 차례로 **빨리 만들기**합니다.
   
   ![데이터 분석 처리 작업 마법사](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![데이터 분석 처리 작업 만들기](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Hello 스트림 분석 작업에 대 한 hello 원하는 구성을 지정 합니다.
   
   * Hello에 **작업 이름을** 상자에 이름 tooidentify hello 스트림 분석 작업을 입력 합니다. Hello 때 **작업 이름을** 의 유효성이 확인 되 hello 작업 이름 상자에 녹색 확인 표시가 나타납니다. hello **작업 이름을** 영숫자 문자와 hello 포함 될 수 있습니다 '-' 문자, 있으며 3 ~ 63 자 사이 여야 합니다.
   * 사용 하 여 **지역** hello Azure 포털에서에서 또는 **위치** hello Azure에서에서 포털 toospecify hello toorun hello 작업 저장할 지리적 위치입니다.
   * Azure 포털을 hello를 사용 하 여, 선택 하거나 hello로 저장소 계정 toouse 만들 **지역별 모니터링 저장소 계정**합니다. 이 저장소 계정은이 영역에서 실행 중인 모든 스트림 분석 작업에 대 한 데이터를 모니터링 하는 사용 되는 toostore입니다.
   * Azure 포털을 hello를 사용 하 여, 지정 새 또는 기존 **리소스 그룹** toohold 관련 응용 프로그램에 대 한 리소스입니다.
4. 새 스트림 분석 작업 옵션 hello 구성 되 면 클릭 **스트림 분석 작업 만들기**합니다. 만든 hello 스트림 분석 작업 toobe 몇 분 정도 걸릴 수 있습니다. toocheck hello 상태 hello 알림 허브에서 hello 진행률을 모니터링할 수 있습니다.
   
   ![데이터 분석 처리 작업 알림 허브](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure Portal 데이터 분석 처리 작업 만들기](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. hello 새 작업의 상태가 표시 됩니다 **Created**합니다. 해당 hello 확인 **시작** 단추가 비활성화 됩니다. Hello 작업을 시작 하기 전에 hello 작업 입력, 쿼리 및 출력을 구성 합니다.
   
   ![데이터 분석 처리 작업 상태](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure Portal 데이터 분석 처리 작업 상태](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

