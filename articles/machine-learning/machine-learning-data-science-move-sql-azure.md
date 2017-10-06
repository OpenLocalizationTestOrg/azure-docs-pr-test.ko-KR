---
title: "Azure 기계 학습에 대 한 Azure SQL 데이터베이스 aaaMove 데이터 tooan | Microsoft Docs"
description: "SQL 테이블을 만들고 데이터 tooSQL 테이블 로드"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Azure 기계 학습에 대 한 데이터 tooan Azure SQL 데이터베이스를 이동
이 항목에서는 플랫 파일 (CSV 또는 TSV 형식) 또는 온-프레미스 SQL Server tooan Azure SQL 데이터베이스에 저장 된 데이터에서 데이터를 이동 하기 위한 hello 옵션을 설명 합니다. 이동 데이터가 toohello 클라우드에 대 한 이러한 작업은 일부 hello 팀 데이터 과학 프로세스입니다.

참조에 대 한 이동 데이터 tooan에 대 한 hello 옵션에 간략하게 설명 하는 항목을 온-프레미스 SQL Server에 대 한 기계 학습, [Azure 가상 컴퓨터에서 데이터 tooSQL 서버 이동](machine-learning-data-science-move-sql-server-virtual-machine.md)합니다.

hello 다음 **메뉴** tootopics hello 데이터 저장 끌어다 하는 동안 처리할 수 있는 대상 환경으로 데이터 tooingest 팀 데이터 과학 프로세스 (TDSP) hello 하는 방법을 설명 하는 링크입니다.

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

hello 다음 표에 요약 되어 이동 데이터 tooan Azure SQL 데이터베이스에 대 한 hello 옵션입니다.

| <b>원본</b> | <b>대상: Azure SQL 데이터베이스</b> |
| --- | --- |
| <b>플랫 파일(CSV 또는 TSV 형식)</b> |<a href="#bulk-insert-sql-query">대량 삽입 SQL 쿼리 |
| <b>온-프레미스 SQL Server</b> |1. <a href="#export-flat-file">TooFlat 파일 내보내기<br> 2. <a href="#insert-tables-bcp">SQL 데이터베이스 마이그레이션 마법사<br> 3. <a href="#db-migration">데이터베이스 백업 및 복원<br> 4. <a href="#adf">Azure 데이터 팩터리 |

## <a name="prereqs"></a>필수 조건
여기에 설명 된 절차에 hello 수 있어야 합니다.

* **Azure 구독**. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.
* **Azure 저장소 계정**. Azure 저장소 계정 '를 사용 하 여이 자습서에서 hello 데이터를 저장 합니다. Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서. Hello 저장소 계정을 만든 후 tooobtain hello 계정 키 tooaccess hello 저장소를 사용 해야 합니다. [저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)를 참조하세요.
* 액세스 tooan **Azure SQL 데이터베이스**합니다. Azure SQL 데이터베이스를 설정 해야 하는 경우 [Microsoft Azure SQL 데이터베이스 시작](../sql-database/sql-database-get-started.md) 방법에 대해 설명 tooprovision Azure SQL 데이터베이스의 새 인스턴스.
* 로컬로 설치 및 구성된 **Azure PowerShell** . 자세한 내용은 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

**데이터**: hello를 사용 하 여 hello 마이그레이션 프로세스는 나와 [NYC 택시 dataset](http://chriswhong.com/open-data/foil_nyc_taxi/)합니다. hello NYC 택시 데이터 집합 학습 데이터와 fairs에 대 한 정보 및 Azure blob 저장소에 있는: [NYC 택시 데이터](http://www.andresmh.com/nyctaxitrips/)합니다. 이러한 파일의 샘플 및 설명은 [NYC Taxi Trips 데이터 집합 설명](machine-learning-data-science-process-sql-walkthrough.md#dataset)에 제공됩니다.

자신만 데이터 집합이 프로시저 여기 설명 된 tooa hello를 조정 하거나 hello NYC 택시 데이터 집합을 사용 하 여 hello 단계에 따라 수 있습니다. tooupload hello를 온-프레미스 SQL Server 데이터베이스를 사용 하 여 NYC 택시 데이터 집합에 설명 된 hello 절차에 따라 [SQL Server 데이터베이스에 데이터 대량 가져오기](machine-learning-data-science-process-sql-walkthrough.md#dbload)합니다. 이러한 지침은 SQL Server에는 Azure 가상 컴퓨터를 위한 하지만 온-프레미스 SQL Server가 toohello 업로드 하기 위한 hello 프로시저 hello 동일 합니다.

## <a name="file-to-azure-sql-database"></a>플랫 파일 원본 tooan Azure SQL 데이터베이스에서 데이터 이동
플랫 파일 (CSV 또는 TSV 형식)에 있는 데이터에는 대량 삽입 SQL 쿼리를 사용 하 여 이동된 tooan Azure SQL 데이터베이스 수 있습니다.

### <a name="bulk-insert-sql-query"></a> 대량 삽입 SQL 쿼리
hello 대량 삽입 SQL 쿼리를 사용 하 여 hello 프로시저 hello 단계는 Azure VM에서 플랫 파일 원본 tooSQL 서버에서에서 데이터를 이동 하기 위한 hello 섹션에서 설명 하는 유사한 toothose 합니다. 자세한 내용은 [대량 삽입 SQL 쿼리](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery)를 참조하세요.

## <a name="sql-on-prem-to-sazure-sql-database"></a>온-프레미스 SQL Server tooan Azure SQL 데이터베이스에서 데이터 이동
Hello 원본 데이터는 온-프레미스 SQL Server에 저장 되어 경우 가지 이동 hello 데이터 tooan Azure SQL 데이터베이스에 대 한 다양 한 가능성이 있습니다.

1. [TooFlat 파일 내보내기](#export-flat-file)
2. [SQL 데이터베이스 마이그레이션 마법사](#insert-tables-bcp)
3. [데이터베이스 백업 및 복원](#db-migration)
4. [Azure 데이터 팩터리](#adf)

hello 처음 세 개의 hello에 대 한 단계는 매우 비슷한 toothose 섹션에서 [Azure 가상 컴퓨터에서 데이터 tooSQL 서버 이동](machine-learning-data-science-move-sql-server-virtual-machine.md) 이와 동일한 절차를 설명 하는 합니다. 해당 항목의 링크 toohello 적절 한 섹션 hello 다음 지침에에서 제공 됩니다.

### <a name="export-flat-file"></a>TooFlat 파일 내보내기
이 tooa 플랫 파일을 내보내는 hello 단계에서 설명 하는 유사한 toothose는 [tooFlat 파일 내보내기](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file)합니다.

### <a name="insert-tables-bcp"></a>SQL 데이터베이스 마이그레이션 마법사
hello 단계 hello SQL 데이터베이스 마이그레이션 마법사를 사용 하는 유사한 toothose에서 다루는 [SQL 데이터베이스 마이그레이션 마법사](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration)합니다.

### <a name="db-migration"></a>데이터베이스 백업 및 복원
데이터베이스를 사용 하 여 hello 단계를 백업 및 복원에서 설명 하는 유사한 toothose는 [데이터베이스 백업 및 복원](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup)합니다.

### <a name="adf"></a>Azure Data Factory
이동 데이터 tooan Azure SQL 데이터베이스와 Azure 데이터 팩터리 ADF ()에 대 한 hello 프로시저 hello 항목에 설명 된 [온-프레미스 SQL server tooSQL Azure 데이터 팩터리를 사용 하 여 Azure에서에서 데이터 이동](machine-learning-data-science-move-sql-azure-adf.md)합니다. 이 항목 ADF를 사용 하 여 Azure Blob 저장소를 통한 toomove 데이터를 온-프레미스 SQL Server 데이터베이스 tooan Azure SQL 데이터베이스 방법을 보여 줍니다.

데이터 요구 toobe 온-프레미스에 액세스 하는 하이브리드 시나리오에서 지속적으로 마이그레이션되면 ADF를 사용 하 여 및 클라우드 리소스를 하 고 hello 데이터의 트랜잭션 처리 하거나 필요 toobe 수정 하거나 비즈니스 논리 추가한 tooit 마이그레이션 중인 경우. ADF hello 일정 예약 및 hello 주기적으로 데이터 이동을 관리 하는 간단한 JSON 스크립트를 사용 하 여 작업에 대 한 모니터링을 허용 합니다. 또한 복잡한 작업을 지원하는 기타 기능도 포함하고 있습니다.
