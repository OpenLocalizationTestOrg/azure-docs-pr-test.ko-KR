---
title: "Azure Stream Analytics 작업과 관련한 서비스 중단 방지 | Microsoft Docs"
description: "Stream Analytics 작업 업그레이드의 복원력을 높이기 위한 지침."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>서비스 업데이트 도중 Stream Analytics 작업 안정성 보장

완전히 관리 되는 서비스의 일부에는 hello 기능 toointroduce 새로운 서비스 기능을 빠른 속도로 향상 된 기능입니다. 따라서 Stream Analytics는 매주(또는 더 자주) 서비스 업데이트 배포가 이루어질 수 있습니다. 얼마나 많은 테스트가 수행에 관계 없이 사업이 여전히 기존를 실행 하 고 작업을 바꾸어 벗어나지 버그 toohello 소개 인해 위험이 있습니다. 이러한 위험 중요 스트리밍 처리 작업을 실행 하는 고객에 대 한 피해 toobe가 필요 합니다. 메커니즘 고객 tooreduce צ ְ ײ이 위험을 Azure의  **[쌍을 이루는 지역](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  모델입니다. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Azure 지역 쌍은 이러한 문제를 어떻게 해결할까요?

Stream Analytics는 지역 쌍의 작업이 별도의 일괄 처리로 업데이트되도록 보장합니다. 결과적으로 tooidentify 잠재적 주요 버그 및이 수정할 hello 업데이트 간의 충분 한 시간 간격이 됩니다.

_중앙 인도 hello 제외_ (인 쌍을 이루는 지역, 남 인도에 현재 상태 스트림 분석) 쌍 이룬된 지역 집합이 시간이 hello 배포는 업데이트 tooStream 분석 hello에서 발생 하지 않습니다. 여러 지역에 배포 **hello에 동일한 그룹** 발생할 수 있습니다 **hello에 동시**합니다.

hello 문서  **[가용성과 쌍 이룬된 지역](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  지역 쌍 hello 최신 정보는 합니다.

고객은이 권장된 toodeploy 동일 작업 쌍을 이루는 tooboth 영역. 또한 tooStream 분석 내부 모니터링 기능을 고객도 있습니다 알리도록 toomonitor hello 작업 처럼 **둘 다** 프로덕션 작업이 있습니다. 식별 된 toobe hello 스트림 분석 서비스 업데이트의 결과 중단을 사용 하는 경우 적절 하 게 에스컬레이션 및 장애 조치 모든 다운스트림 소비자 toohello 정상 작업 출력 합니다. 에스컬레이션 toosupport hello 새 배포에 의해 영향을 주지 않도록 hello 쌍을 이루는 지역을 작업이 방지 되 고 hello 쌍이 작업의 hello 무결성을 유지 합니다.
