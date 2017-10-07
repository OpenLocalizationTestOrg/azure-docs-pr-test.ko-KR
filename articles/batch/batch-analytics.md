---
title: "일괄 처리 분석 aaaAzure | Microsoft Docs"
description: "Azure Batch 분석에 대한 참조입니다."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a>Batch 분석
일괄 처리 분석의 hello 항목 hello 이벤트 및 일괄 처리 서비스 리소스에 사용할 수 있는 경고에 대 한 참조 정보를 포함 합니다.

Batch 진단 로그를 활성화하고 사용하는 방법에 대한 자세한 내용은 [Azure Batch 진단 로깅](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)을 참조하세요.

## <a name="diagnostic-logs"></a>진단 로그

hello를 Azure 배치 서비스는 특정 일괄 처리 리소스의 hello 수명 동안 진단 로그 이벤트를 수행 하는 hello를 내보냅니다.

**서비스 로그 이벤트**
* [풀 만들기](batch-pool-create-event.md)
* [풀 삭제 시작](batch-pool-delete-start-event.md)
* [풀 삭제 완료](batch-pool-delete-complete-event.md)
* [풀 크기 조정 시작](batch-pool-resize-start-event.md)
* [풀 크기 조정 완료](batch-pool-resize-complete-event.md)
* [작업 시작](batch-task-start-event.md)
* [작업 완료](batch-task-complete-event.md)
* [작업 실패](batch-task-fail-event.md)