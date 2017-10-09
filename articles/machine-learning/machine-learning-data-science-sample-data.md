---
title: "Azure에서 aaaSample 데이터 blob 컨테이너, SQL Server 및 Hive 테이블 | Microsoft Docs"
description: "Tooexplore 데이터가 다양 한 Azure enviromnents에 저장 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Azure blob 컨테이너, SQL Server 및 Hive 테이블의 데이터 샘플링
이 문서에서 다루는 tootopics 연결 방법을 toosample 저장 된 데이터를 세 개의 서로 다른 Azure 위치 중 하나에:

* **Azure blob 컨테이너 데이터** 는 프로그래밍 방식으로 다운로드한 다음 샘플 Python 코드로 샘플링함으로써 샘플링됩니다.
* **SQL Server 데이터** SQL와 hello Python 프로그래밍 언어를 사용 하 여 샘플링 됩니다. 
* **Hive 테이블 데이터** 는 Hive 쿼리를 사용하여 샘플링됩니다.

hello 다음 **메뉴** toohello 항목 설명 하는 연결 방법을 각 Azure 저장소 환경에서 toosample 데이터입니다. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

이 샘플링 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.

**데이터를 샘플링하는 이유**

Tooanalyze 계획 hello 데이터 집합이 크면 경우 일반적으로 좋습니다 toodown 샘플 hello 데이터 tooreduce 것 tooa 있지만 대표 작고 더 관리 가능한 수치로 크기입니다. 그러면 데이터 이해, 탐색 및 기능 엔지니어링이 용이해집니다. Hello Cortana 분석 프로세스에서에서 해당 역할에는 데이터 처리 함수 hello 및 기계 학습 모델의 tooenable 빠르게 프로토타입을 만들입니다.

