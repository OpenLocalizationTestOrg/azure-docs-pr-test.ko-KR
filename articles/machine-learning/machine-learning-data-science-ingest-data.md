---
title: "분석에 대 한 Azure 저장소 환경으로 데이터 aaaLoad | Microsoft Docs"
description: "Azure Blob 저장소에서 데이터 tooand 이동"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a>분석용 저장소 환경에 데이터 로드
hello 팀 데이터 과학 프로세스는 데이터 수집 된 것인지에 다양 한 다른 저장소 환경 toobe 처리 되거나 hello 프로세스의 각 단계에서 hello 가장 적합 한 방식에서으로 분석할 로드 필요 합니다. 처리하기 위해 일반적으로 사용하는 데이터 대상에는 Azure Blob 저장소, SQL Azure 데이터베이스, Azure VM의 SQL Server, HDInsight(Hadoop) 및 Azure 기계 학습이 포함됩니다. 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

이 **메뉴** tootopics tooingest 데이터를 이러한 환경 hello 데이터가 저장 되 고 처리를 대상 하는 방법을 설명 하는 링크입니다.

기술 및 비즈니스 요구 사항 뿐 아니라 hello 초기 위치를 포맷 하 고 데이터의 크기는 hello 대상 환경에는 hello이 필요한 데이터 분석의 수집 된 toobe tooachieve hello 목표를 결정 합니다. 여러 환경 tooachieve hello 다양 한 작업 필요한 tooconstruct 예측 모델 간에 이동 하는 시나리오 toorequire 데이터 toobe도 드물지 않습니다. 이 작업 시퀀스에는 데이터 탐색, 사전 처리, 정리, 다운 샘플링, 모델 학습 등이 포함될 수 있습니다.

