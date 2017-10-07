---
title: "SQL 데이터 웨어하우스에 Azure Data Factory aaaUse | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Azure 데이터 팩터리(ADF) 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>SQL 데이터 웨어하우스와 함께 Azure 데이터 팩터리 사용
Azure 데이터 팩터리를 통해 완전히 관리 되는 데이터의 전송을 hello 및 SQL 데이터 웨어하우스에서 저장된 프로시저의 실행 오케스트레이션 합니다.  이렇게 하면 toomore 쉽게 설치 하 고 일정 복잡 한 변환 추출 및 로드 (ETL) 절차 SQL 데이터 웨어하우스에 합니다. Azure Data Factory의 자세한 개요를 참조 hello [Azure Data Factory 설명서][Azure Data Factory documentation]합니다.

## <a name="data-movement"></a>데이터 이동
Azure 데이터 팩터리는 온-프레미스 원본 및 다른 Azure 서비스 간의 데이터 이동을 설정할 수 있습니다.  Azure Data Factory와 전반적인, 현재 통합 hello 다음 위치에서에서 데이터 이동을 tooand를 지원 합니다.

* Azure Blob 저장소
* Azure SQL 데이터베이스
* 온-프레미스 SQL Server
* IaaS의 SQL Server

데이터를 tooset 활동을 복사 하는 방법에 대 한 내용은 [Azure 데이터 팩터리를 사용 하 여 데이터를 복사 합니다.][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>저장 프로시저
 Hello에 동일한 방식으로 수 tooschedule 데이터 전송, Azure Data Factory 수 있는 저장된 프로시저의 사용된 tooorchestrate hello 실행 될도 사용 합니다.  이 통해 만든 더 복잡 한 파이프라인 toobe 있으며 Azure Data Factory 기능 tooleverage hello의 계산 능력 SQL 데이터 웨어하우스를 확장 합니다.

## <a name="next-steps"></a>다음 단계
통합 개요는 [SQL Data Warehouse 통합 개요][SQL Data Warehouse integration overview]를 참조하세요.
더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

