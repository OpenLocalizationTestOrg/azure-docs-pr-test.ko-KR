---
title: "스트림 분석 이벤트 처리를 사용 하 여 처리 시간 aaaReal 이벤트 | Microsoft Docs"
description: "실시간 이벤트 처리 및 분석을 구현하기 위해 Azure 서비스가 어떻게 상호 운용되는지 알아보세요."
keywords: "실시간 처리, 이벤트 처리, 참조 아키텍처"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>참조 아키텍처: Microsoft Azure Stream Analytics으로 실시간 이벤트 처리
Azure 스트림 분석을 사용 하 여 처리 하는 실시간 이벤트에 대 한 hello 참조 아키텍처에는 의도 한 tooprovide 실시간 플랫폼으로 Microsoft Azure 서비스 (PaaS) 스트림 처리 솔루션으로 배포 하기 위한 일반 청사진입니다.

## <a name="summary"></a>요약
일반적으로 분석 솔루션 토대로 데이터 웨어하우징, ETL (extract, transform, load) 등의 기능 데이터를 이전 tooanalysis 저장된 합니다. 이 기존 모델 toohello 제한을 강제로 신속 하 게 도착 더 많은 데이터를 포함 하 여 변경 요구 사항입니다. hello 기능 tooanalyze 데이터 이동, 이전 toostorage 스트림 내에서 하나의 솔루션 이며 새로운 기능으로는 없지만 hello 접근 방식에 널리 채택 되지는 모든 업계 직종에서. 

Microsoft Azure는 여러 솔루션 시나리오 및 요구 사항을 지원할 수 있는 광범위한 분석 기술 카탈로그를 제공합니다. Azure 서비스 toodeploy 종단 간 솔루션에 대 한 제품의 hello 너비 이와 수를 선택 합니다. 이 백서는 디자인 된 toodescribe hello 기능 및 간의 상호 운용을 hello 이벤트 스트리밍 솔루션을 지 원하는 다양 한 Azure 서비스입니다. 또한이 유형의 방법에서 고객 혜택 수 있는 hello 시나리오 중 일부를 설명 합니다.

## <a name="contents"></a>목차
* 요약
* 소개 tooReal 시간 분석
* Azure에서 실시간 데이터의 가치 제안
* 실시간 분석의 일반적인 시나리오
* 아키텍처 및 구성 요소
  * 데이터 원본
  * 데이터 통합 계층
  * 실시간 분석 계층
  * 데이터 저장소 계층
  * 프레젠테이션/소비 계층
* 결론

**작성자:** Charles Feddersen - Microsoft Corporation, Data Insights Center of Excellence, 솔루션 설계자

**게시:** 2015년 1월

**수정 버전:** 1.0

**다운로드:** [Microsoft Azure Stream Analytics과 실시간 이벤트 처리](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

