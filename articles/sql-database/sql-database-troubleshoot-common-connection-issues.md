---
title: "aaaTroubleshoot 일반적인 연결 문제 tooAzure SQL 데이터베이스"
description: "단계 tooidentify 및 해결 일반적인 연결 오류 Azure SQL 데이터베이스에 대 한 합니다."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>연결 문제 tooAzure SQL 데이터베이스 문제 해결
수신 hello 연결 tooAzure SQL 데이터베이스에 실패 하면 [오류 메시지](sql-database-develop-error-messages.md)합니다. 이 문서는 Azure SQL Database 연결 문제를 해결하는 데 도움이 되는 중앙 집중식 항목입니다. 도입 [일반적인 원인은 hello](#cause) 연결 문제, 권장 [문제 해결 도구](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) identity hello 문제를 활용 하 고 문제 해결 단계 toosolve 제공 하는 [ 일시적인 오류](#troubleshoot-transient-errors) 및 [영구 또는 일시적이 지 않은 오류](#troubleshoot-persistent-errors)합니다. 

Hello 연결 문제가 발생 하면 시도 hello이이 문서에 설명 된 단계 문제를 해결 합니다.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>원인
연결 문제 hello 다음 중 하나로 인해 발생할 수 있습니다.

* 오류 tooapply 모범 사례 및 디자인 지침 hello 응용 프로그램 디자인 프로세스 중입니다.  참조 [SQL 데이터베이스 개발 개요](sql-database-develop-overview.md) tooget 시작 합니다.
* Azure SQL 데이터베이스 재구성
* 방화벽 설정
* 연결 제한 시간
* 잘못된 로그인 정보
* 일부 Azure SQL 데이터베이스 리소스에서 최대 한도 도달

일반적으로 SQL 데이터베이스 연결 문제 tooAzure 다음과 같이 분류할 수 있습니다.

* [일시적인 오류(단기 또는 일시적)](#troubleshoot-transient-errors)
* [영구적 또는 일시적이지 않은 오류(정기적으로 되풀이되는 오류)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Azure SQL 데이터베이스 연결 문제에 대 한 hello 문제 해결사
특정 연결 오류가 발생하면 문제를 빠르게 식별하고 해결하는 데 도움이 되는 [이 도구](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)를 사용해보세요.

## <a name="troubleshoot-transient-errors"></a>일시적인 오류 문제 해결

응용 프로그램 tooan Azure SQL 데이터베이스를 연결 하면 hello 다음과 같은 오류 메시지가 나타납니다.

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> 이 오류 메시지는 대개 일시적으로 나타납니다.
> 
> 

경우이 오류가 발생 hello Azure 데이터베이스가 되 고 이동 (또는 다시 구성)의 연결 toohello SQL 데이터베이스를 손실 하는 응용 프로그램 및입니다. SQL Database 재구성 이벤트는 계획된 이벤트(예: 소프트웨어 업그레이드) 또는 계획되지 않은 이벤트(예: 프로세스 충돌 또는 부하 분산) 때문에 발생합니다. 대부분의 다시 구성 이벤트는 보통 일시적으로 발생하며 최대 60초 이내에 완료됩니다. 그러나 이러한 이벤트는 큰 트랜잭션 실행 시간이 긴 복구를 다시 하는 경우와 같은 긴 toofinish를 걸릴 경우에 따라 수 있습니다.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>단계 tooresolve 일시적인 연결 문제

1. Hello 확인 [Microsoft Azure 서비스 대시보드](https://azure.microsoft.com/status) hello 응용 프로그램에서 오류가 보고는 hello 동안 hello 시간 중에 발생 한 모든 알려진 중단 합니다.
2. Azure SQL 데이터베이스 정기적으로 다시 구성 이벤트 및 구현 해야 같은 tooa 클라우드 서비스를 연결 하는 응용 프로그램 논리 toohandle이 방법으로 응용 프로그램 오류 toousers에서 표시가 하는 대신 이러한 오류를 다시 시도 합니다. 검토 hello [일시적인 오류](sql-database-connectivity-issues.md) 모범 사례 및 디자인 지침에 섹션 및 hello [SQL 데이터베이스 개발 개요](sql-database-develop-overview.md) 자세한 내용 및 일반 전략을 다시 시도 하십시오. 그런 다음 세부 사항은 [SQL Database 및 SQL Server에 대한 연결 라이브러리](sql-database-libraries.md) 에서 코드 샘플을 참조하세요.
3. 데이터베이스는 리소스 한계에 가까워지면 toobe 일시적인 연결 문제 것 처럼 보일 수 있습니다. [성능 문제 해결](sql-database-troubleshoot-performance.md)을 참조하세요.
4. 계속 해 서 연결 문제 또는 응용 프로그램을 hello 오류가 발생 하는 기간 60 초를 초과 하는 경우 hello 또는 hello 오류를 여러 번 지정된 된 날에 표시 되 면 Azure 지원 요청을 선택 하 여 파일 **지원가져오기** hello에 [Azure 지원](https://azure.microsoft.com/support/options) 사이트입니다.

## <a name="troubleshoot-persistent-errors"></a>영구 오류 문제 해결
Hello 응용 프로그램이 tooconnect tooAzure SQL 데이터베이스를 영구적으로 실패 하는 경우 일반적으로 문제를 hello 다음 중 하나를 나타냅니다.

* 방화벽 구성. SQL 데이터베이스 연결 tooAzure hello Azure SQL 데이터베이스 또는 클라이언트 쪽 방화벽 차단 합니다.
* Hello 클라이언트 쪽에서 재구성 네트워크: 예를 들어 새 IP 주소 또는 프록시 서버.
* 사용자 오류 발생: 예를 들어 hello hello 연결 문자열 서버 이름이 같은 연결 매개 변수를 잘못 입력 합니다.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>단계 tooresolve 영구 연결 문제
1. 설정 [방화벽 규칙](sql-database-configure-firewall-settings.md) tooallow hello 클라이언트 IP 주소입니다. 임시 테스트용으로 IP 주소 범위를 시작 및 종료 IP 주소 범위는 hello로 255.255.255.255를 사용 하 여 hello로 0.0.0.0를 사용 하 여 방화벽 규칙을 설정 합니다. Hello 서버 tooall IP 주소 열립니다. 이렇게 해서 연결 문제가 해결되면 이 규칙을 제거하고 적절하게 제한된 IP 주소 또는 주소 범위에 대해 방화벽 규칙을 만듭니다. 
2. 클라이언트 hello와 hello 인터넷 간의 모든 방화벽에서 포트 1433이 아웃 바운드 연결에 대해 열려 있는지 확인 합니다. 검토 [hello Windows 방화벽 tooAllow SQL Server 액세스를 구성](https://msdn.microsoft.com/library/cc646023.aspx) 및 [하이브리드 Identity 필요한 포트 및 프로토콜](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) tooopen에 대 한 필요 하지만 포인터는 tooadditional 포트 관련에 대 한 Azure Active Directory 인증 합니다.
3. 연결 문자열 및 기타 연결 설정을 확인합니다. 참조 hello hello에 대 한 연결 문자열 섹션 [연결 문제 항목](sql-database-connectivity-issues.md#connections-to-azure-sql-database)합니다.
4. Hello 대시보드에서 서비스 상태를 확인 합니다. 국가별 가동이 중지 생각 되 면 참조 [가동 중단에서 복구](sql-database-disaster-recovery.md) 단계 toorecover tooa 새 영역에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
* [Azure SQL 데이터베이스 성능 문제 해결](sql-database-troubleshoot-performance.md)
* [Microsoft Azure에서 검색 hello 설명서](http://azure.microsoft.com/search/documentation/)
* [보기 hello toohello Azure SQL 데이터베이스 서비스를 최신 업데이트](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>추가 리소스
* [SQL 데이터베이스 개발 개요](sql-database-develop-overview.md)
* [일반적인 일시적 오류 처리 지침](../best-practices-retry-general.md)
* [SQL 데이터베이스 및 SQL Server용 연결 라이브러리](sql-database-libraries.md)

