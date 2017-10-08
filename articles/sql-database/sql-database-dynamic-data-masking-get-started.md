---
title: "SQL 데이터베이스 동적 데이터 마스킹 aaaAzure | Microsoft docs"
description: "SQL 데이터베이스 동적 데이터 마스킹 toonon 권한이 사용자에 게 마스킹하 여 중요 한 데이터 노출을 제한합니다"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>SQL Database 동적 데이터 마스킹

SQL 데이터베이스 동적 데이터 마스킹 toonon 권한이 사용자에 게 마스킹하 여 중요 한 데이터 노출을 제한 합니다. 

동적 데이터 마스킹 고객 toodesignate를 사용 하 여 toosensitive 데이터를 무단된 액세스를 방지할 수 어느 정도의 hello 중요 한 데이터 tooreveal hello 응용 프로그램 계층에 미치는 영향을 최소화 합니다. hello 데이터베이스의 hello 데이터는 변경 되지 않으면 지정 된 데이터베이스 필드를 통해 hello hello 쿼리 결과 집합에서 중요 한 데이터를 숨기는 정책 기반 보안 기능.

예를 들어 콜 센터에서 서비스 담당자를 여은 신용 카드 번호의 여러 숫자로 발신자를 식별할 수 있지만 항목 완벽 하 게 되지 않아야 하는 이러한 데이터 toohello 서비스 담당자를 노출 합니다. Hello 제외 하 고 모두 마스킹 하도록 모든 쿼리의 hello 결과 집합에서 모든 신용 카드 번호의 네 자리 숫자 지속 되는 마스킹 규칙을 정의할 수 있습니다. 또 다른 예로, 개발자는 적합성 규정 준수 규칙을 위반 하지 않고 문제 해결을 위해 프로덕션 환경을 쿼리할 수 있도록 적절 한 데이터 마스크 정의 tooprotect 개인 식별이 가능한 정보 (PII) 데이터를 수 있습니다.

## <a name="sql-database-dynamic-data-masking-basics"></a>SQL Database 동적 데이터 마스킹 관련 기본 사항
설정한 동적 데이터 마스킹 정책 hello에 Azure 포털 hello 동적 데이터 마스킹 SQL 데이터베이스 구성 블레이드 또는 설정 블레이드에서에서 작업을 선택 하 여 합니다.

### <a name="dynamic-data-masking-permissions"></a>동적 데이터 마스킹 사용 권한
동적 데이터 마스킹 Azure 데이터베이스 admin 님 안녕하세요, 서버 관리자 또는 보안 책임자 역할에서 구성할 수 있습니다.

### <a name="dynamic-data-masking-policy"></a>동적 데이터 마스킹 정책
* **마스킹에서 제외 된 SQL 사용자** -A SQL 사용자 설정 또는 쿼리 결과 표시 SQL hello에 마스크 해제 된 데이터를 가져오기 하는 AAD id입니다. 관리자 권한이 있는 사용자는 항상, 마스킹에서 제외 됨 및 모든 마스크 없이 hello 원래 데이터를 참조 하십시오.
* **마스킹 규칙** -필드 toobe 마스크를 지정 하는 hello hello 마스킹 사용 되는 기능을 정의 하는 규칙 집합입니다. 데이터베이스 스키마 이름, 테이블 이름 및 열 이름을 사용 하 여 필드를 지정 하는 hello는 정의할 수 있습니다.
* **함수를 마스킹** -hello 노출이 다양 한 시나리오에 대 한 데이터를 제어 하는 메서드 집합이 있습니다.

| 마스킹 기능 | 마스킹 논리 |
| --- | --- |
| **기본값** |**Hello 유형의 toohello 데이터에 따라 전체 마스킹 필드 지정**<br/><br/>• 사용 XXXX 또는 미만의 x hello 필드의 hello 크기는 4 자 미만인 (nchar, ntext, nvarchar) 문자열 데이터 형식에 대 한 경우.<br/>• 숫자 데이터 형식(bigint, bit, decimal, int, money, numeric, smallint, smallmoney, tinyint, float, real)의 경우 0 값을 사용합니다.<br/>• 날짜/시간 데이터 형식(date, datetime2, datetime, datetimeoffset, smalldatetime, time)의 경우 01-01-1900을 사용합니다.<br/>• SQL variant 데이터 형식, hello 기본값인 hello 현재 형식에 대 한 사용 됩니다.<br/>XML hello 문서에 대 한 • <masked/> 사용 됩니다.<br/>• 특수 데이터 형식(타임스탬프 테이블, hierarchyid, GUID, 이진, 이미지, varbinary 공간 형식)의 경우 빈 값을 사용합니다. |
| **신용 카드** |**마스킹 hello를 노출 하는 방법의 마지막 4 자리 필드를 지정 하는 hello** 신용 카드의 hello 형태로 접두사로 상수 문자열을 추가 합니다.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **Email** |**마스킹 방법, hello 첫 글자를 노출 하 고 hello 도메인 XXX.com 교체** hello는 전자 메일 주소 형식에서 상수 문자열 접두사를 사용 하 여 합니다.<br/><br/>aXX@XXXX.com |
| **난수** |**난수를 생성 하는 방법을 마스킹** toohello에 따라 선택한 경계 및 실제 데이터 형식입니다. 경계를 지정 하는 hello 같으면 마스킹 함수가 hello 상수 숫자입니다.<br/><br/>![탐색 창](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **사용자 지정 텍스트** |**메서드를 노출 하는 먼저 hello 및 마지막 문자를 마스킹** hello 가운데에 사용자 지정 안쪽 여백 문자열을 추가 합니다. 원래 문자열 hello 노출 hello 접두사와 접미사 보다 짧은 경우 패딩 문자열 hello만 사용 됩니다. <br/>접두사[여백]접미사<br/><br/>![탐색 창](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>권장된 필드 toomask
hello DDM 권장 엔진 플래그를 지정 하면 데이터베이스에서 특정 필드 마스킹 하기에 적합 수 있는 잠재적으로 중요 한 필드입니다. 동적 데이터 마스킹 블레이드 hello 포털에서 hello 데이터베이스에 대 한 열을 권장 하는 hello를 나타납니다. Toodo 있으면 클릭 **마스크 추가** 하나 이상의 열에 대 한 다음 **저장** tooapply 이러한 필드에 대 한 마스크입니다.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>PowerShell cmdlet을 사용하여 데이터베이스에 대한 동적 데이터 마스킹 설정
[Azure SQL 데이터베이스 cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx)을 참조하세요.

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>REST API를 사용하여 데이터베이스에 대한 동적 데이터 마스킹 설정
[Azure SQL 데이터베이스에 대한 작업](https://msdn.microsoft.com/library/dn505719.aspx)을 참조하세요.

