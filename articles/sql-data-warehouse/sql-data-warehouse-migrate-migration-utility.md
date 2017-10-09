---
title: "마이그레이션: 데이터 웨어하우스 마이그레이션 유틸리티 | Microsoft Docs"
description: "데이터 웨어하우스 tooSQL 마이그레이션하십시오."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>데이터 웨어하우스 마이그레이션 유틸리티(미리 보기)
> [!div class="op_single_selector"]
> * [마이그레이션 유틸리티 다운로드][Download Migration Utility]
> 
> 

데이터 웨어하우스 마이그레이션 유틸리티 hello 도구 설계 toomigrate 스키마 및 SQL 데이터 웨어하우스 tooAzure SQL Server 및 Azure SQL 데이터베이스의에서 데이터입니다. 스키마를 마이그레이션하는 동안 hello 도구 hello 소스 toodestination에서 해당 스키마를 자동으로 매핑합니다. Hello 스키마 마이그레이션한 후 hello 도구는 자동으로 생성 된 스크립트를 사용 하 여 hello 옵션 toomove 데이터를 제공 합니다.

또한이 도구에서는 방지 하는 hello 소스 및 대상 인스턴스 간의 비 호환성을 요약 하는 옵션 toogenerate 호환성 보고서를 hello tooschema 및 데이터 마이그레이션을 간소화 마이그레이션.

## <a name="get-started"></a>시작
설치에 대 한 필수 조건으로 hello BCP 명령줄 유틸리티 toorun 마이그레이션 스크립트 및 tooview hello 호환성 보고서를 Office 필요 합니다. Hello를 시작한 후 하면 다운로드 된 실행 파일 hello 도구가 설치 되기 전에 증명된 tooaccept 표준 EULA 됩니다.

또한 toorun hello 마이그레이션 Utiliy 있습니다 됩니다 필요 hello 하나 toomigrate 찾고 hello 데이터베이스에 다음 권한을: CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION입니다.

### <a name="launching-hello-tool-and-connecting"></a>Hello 도구를 시작 및 연결
Post 나타나는 hello 바탕 화면 아이콘을 클릭 하 여 시작 hello 도구를 설치 합니다. Hello 도구를 열 때 원본 및 대상 hello 마이그레이션 도구를 선택할 수 있는 초기 연결 페이지와 라는 메시지가 표시 됩니다. 현재는 원본으로 SQL Server 및 Azure SQL 데이터베이스를, 대상으로 SQL 데이터 웨어하우스를 지원합니다. 이 선택한 후 묻습니다 tooconnect tooyour 원본 서버의 서버 이름을 입력 하 고 인증 하 고 '연결'을 클릭 하 여 합니다.

를 인증 한 후 hello 도구에 연결 되어 있는 hello 서버에 있는 데이터베이스 목록이 표시 됩니다. Hello 마이그레이션 toomigrate을 '마이그레이션 선택'를 클릭 한 다음 원하는 데이터베이스를 선택 하 여 시작할 수 있습니다.

## <a name="migration-report"></a>마이그레이션 보고서
Hello 도구에서 데이터베이스 호환성 확인 '을 선택 하면 모든 개체 호환성 문제를 요약 하는 보고서를 생성 합니다 toomigrate hello 데이터베이스에서 요청한 합니다. 광범위 한 목록이 hello SQL 데이터 웨어하우스에 존재 하지 않는 SQL Server 기능 중 일부를 찾을 수 우리의 [마이그레이션 설명서][migration documentation]합니다. Hello 보고서가 생성 한 후 수 toosave 및 Excel에서 열기 hello 보고서 됩니다.

하십시오 note는 hello 마이그레이션 스키마의 해당 데이터의 순서 tooallow 즉시 마이그레이션 'Object' 조정 될 것으로 표시 되는 대부분의 문제를 생성할 때. 원하지 않는 toomake을 조절 hello 스키마를 적용 하기 전에 hello 변경 tooensure를 검토 하십시오.

## <a name="migrate-schema"></a>마이그레이션 스키마
에 연결한 후 마이그레이션 스키마 선택 hello 선택한 테이블에 대 한 스키마 마이그레이션 스크립트를 생성 합니다. 이 스크립트 포트 hello 구조 hello 테이블의 호환 되지 않는 데이터 형식 toomore 호환 forms, 매핑되고이 hello 마이그레이션 설정의 hello 사용자로 표시 하는 경우 보안 자격 증명 및 스키마를 만듭니다. 이 코드를 대상 hello SQL 데이터 웨어하우스 인스턴스에 대해 실행할 수, tooa 파일을 저장, tooyour 클립보드에 복사 또는 추가 작업이 이동 하기 전에 줄을 편집 합니다.  

마이그레이션 스키마 검토 hello 마이그레이션 해당 hello 변경 되는 경우 위에서 설명한 것 처럼 도구가 한 순서 tooensure를 완전히 이해 해야 하는 합니다.  

## <a name="migrate-data"></a>데이터 마이그레이션
Hello 데이터 마이그레이션 ' 옵션을 클릭 하 여 서버에서 첫 번째 tooflat 데이터 파일에 들어왔다 BCP 스크립트를 생성할 수 있습니다 및 SQL 데이터 웨어하우스에 직접 합니다. 이 프로세스 적은 양의 데이터를 다시 시도 횟수로 이동 하기 위한 기본 제공 되며 hello 네트워크 연결이 끊겼기 없을 경우 오류가 발생할 수 있습니다는 것이 좋습니다. 이 toorun 순서에, toohave hello BCP 명령줄 유틸리티 설치 해야 및 hello 데이터에 대 한 hello 스키마 이미 만들었다고 가정 합니다.

Hello 매개 변수 작성 한 후 위의 필요 tooclick를 실행 하면 마이그레이션 및 두 개의 패키지 집합이 생성 됩니다. tooyour 위치를 지정 합니다. 플랫 파일로 주문 tooexport 데이터에서 마이그레이션 원본에서 hello 내보내기 파일을 실행 하 고 hello 가져오기 파일에서에서 실행 순서 tooimport 데이터를 SQL 데이터 웨어하우스에 키를 누릅니다.

## <a name="next-steps"></a>다음 단계
일부 데이터를 마이그레이션한 했으므로 확인 방법에 대해 너무[개발][develop]합니다.

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
