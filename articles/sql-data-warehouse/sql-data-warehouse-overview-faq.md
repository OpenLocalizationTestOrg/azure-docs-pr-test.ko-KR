---
title: "aaaAzure SQL 데이터 웨어하우스 질문과 대답 | Microsoft Docs"
description: "이 문서에는 고객 및 개발자를 위한 Azure SQL Data Warehouse 관련 질문과 대답이 나와 있습니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>SQL Data Warehouse에 대한 질문과 대답

## <a name="general"></a>일반

Q. SQL DW는 데이터 보안을 위해 어떤 기능을 제공하나요?

A. SQL DW는 TDE 및 감사와 같이 데이터를 보호하기 위한 몇 가지 솔루션을 제공합니다. 자세한 내용은 [보안]을 참조하세요.

Q. SQL DW와 호환되는 법적 또는 비즈니스 표준은 어디에서 확인할 수 있나요?

A. Hello 방문 [Microsoft 준수] SOC 및 ISO와 같은 제품에 의해 다양 한 규정 준수 기능에 대 한 페이지입니다. 먼저 규정 준수 제목으로 선택한 다음 확장 Azure의 hello 페이지 toosee hello 범위 내 Microsoft 클라우드 서비스 섹션 hello 오른쪽에 있는 Azure 서비스를 서비스는 규격입니다.

Q. PowerBI를 연결할 수 있나요?

A. 예! PowerBI는 SQL DW를 사용한 직접 쿼리를 지원하지만 많은 수의 사용자 또는 실시간 데이터용은 아닙니다. PowerBI를 프로덕션용으로 사용하는 경우 Azure Analysis Services 또는 Analysis Services IaaS에서 PowerBI를 사용하는 것이 좋습니다. 

Q. SQL Data Warehouse 용량 제한은 얼마인가요?

A. 현재 [용량 제한] 페이지를 참조하세요. 

Q. 크기 조정/일시 중지/계속 작업이 너무 오래 걸리는 이유는 무엇인가요?

A. 다양 한 요인 계산 관리 작업에 대 한 hello 시간에 영향을 줄 수 있습니다. 장기 실행 작업의 일반적인 경우는 트랜잭션 롤백입니다. 크기 조정 또는 일시 중지 작업이 시작되면 들어오는 모든 세션이 차단되고 쿼리가 해제됩니다. 안정 된 상태가 주문 tooleave hello 시스템에서 작업을 시작할 수 있습니다 되기 전에 트랜잭션은 롤백할 수 해야 합니다. 더 많은 hello 수 및 트랜잭션 hello 로그 크기를 더 큰 hello, hello 시스템 tooa 안정적인 상태를 복원할 hello 긴 hello 작업이 중단 됩니다.

## <a name="user-support"></a>사용자 지원

Q. 기능 요청이 있는 경우 어디에 제출하나요?

A. 기능 요청이 있는 경우 [UserVoice] 페이지에 제출하세요.

Q. 어떻게 하면 될까요?

A. SQL Data Warehouse를 사용하는 개발에 도움이 필요한 경우 [스택 오버플로] 페이지에서 질문할 수 있습니다. 

Q. 지원 티켓을 제출하려면 어떻게 해야 하나요?

A. [지원 티켓]은 Azure Portal을 통해 정리할 수 있습니다.

## <a name="sql-languagefeature-support"></a>SQL 언어/기능 지원 

Q. SQL Data Warehouse는 어떤 데이터 형식을 지원하나요?

A. SQL Data Warehouse [데이터 형식]을 참조하세요.

Q. 어떤 테이블 기능이 지원되나요?

A. SQL Data Warehouse는 많은 기능을 지원하지만 일부 지원되지 않는 기능은 [지원되지 않는 테이블 기능]에 나와 있습니다.

## <a name="tooling-and-administration"></a>도구 및 관리

Q. Visual Studio에서 데이터베이스 프로젝트가 지원되나요?

A. 현재 Visual Studio에서는 SQL Data Warehouse용 데이터베이스 프로젝트가 지원되지 않습니다. Toocast 원하는 경우 투표 tooget이 기능을 통해 사용자 의견을 방문 [데이터베이스 프로젝트 기능 요청]합니다.

Q. SQL Data Warehouse는 REST API를 지원하나요?

A. 예. SQL Database와 함께 사용할 수 있는 REST 기능 대부분을 SQL Data Warehouse에서도 사용할 수 있습니다. REST 설명서 페이지 또는 [MSDN]에서 이 API 정보를 찾을 수 있습니다.


## <a name="loading"></a>로드

Q. 어떤 클라이언트 드라이버가 지원되나요?

A. Hello에 DW에 대 한 드라이버 지원이 있습니다 [연결 문자열] 페이지

Q: SQL Data Warehouse를 사용하는 PolyBase는 어떤 파일 형식을 지원하나요?

A: Orc, RC, Parquet 및 일반 구분 텍스트

Q: 수 toofrom SQL DW PolyBase를 사용 하 여 연결 해야 합니까? 

A: [Azure Data Lake Store] 및 [Azure Storage Blob]

Q: 연결 하는 저장소 Blob 또는 ADLS tooAzure 때 가능한 계산 푸시 다운을 인가요? 

A: 아니요, SQL DW PolyBase는만 hello 저장소 구성 요소 상호 작용합니다. 

Q: tooHDI를 연결할 수 있습니까?

A: HDI ADLS 또는 WASB hello HDFS 계층 기호로 사용할 수 있습니다. 둘 중 하나를 HDFS 계층으로 사용하는 경우 해당 데이터를 SQL DW에 로드할 수 있습니다. 그러나 푸시 다운 계산 toohello HDI 인스턴스를 생성할 수 없습니다. 

## <a name="next-steps"></a>다음 단계
SQL Data Warehouse 전반에 대한 자세한 내용은 [개요] 페이지를 참조하세요.


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[연결 문자열]: ./sql-data-warehouse-connection-strings.md
[스택 오버플로]: http://stackoverflow.com/questions/tagged/azure-sqldw
[지원 티켓]: ./sql-data-warehouse-get-started-create-support-ticket.md
[보안]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft 준수]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[용량 제한]: ./sql-data-warehouse-service-capacity-limits.md
[데이터 형식]: ./sql-data-warehouse-tables-data-types.md
[지원되지 않는 테이블 기능]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blob]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[데이터베이스 프로젝트 기능 요청]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[개요]: ./sql-data-warehouse-overview-faq.md