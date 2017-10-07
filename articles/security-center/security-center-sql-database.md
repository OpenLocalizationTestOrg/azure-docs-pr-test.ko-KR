---
title: "보안 센터 및 Azure SQL 데이터베이스 서비스 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Security Center가 Azure SQL Database 서비스에서 데이터를 보호하는 데 어떻게 도움이 되는지 보여 줍니다."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Azure Security Center 및 Azure SQL Database 서비스
[Azure 보안 센터](https://azure.microsoft.com/documentation/services/security-center/) 하면 방지, 검색 및 toothreats 응답 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

이 문서에서는 Security Center가 Azure SQL Database 서비스에서 데이터를 보호하는 데 어떻게 도움이 되는지 보여 줍니다.

## <a name="why-use-security-center"></a>보안 센터를 사용해야 하는 이유
보안 센터를 사용 하면 모든 서버 및 데이터베이스의 보안을 hello에 대 한 가시성을 제공 하 여 SQL 데이터베이스의 데이터를 보호 합니다. 보안 센터를 사용하면 다음과 같은 작업을 수행할 수 있습니다.

* SQL Database 암호화 및 감사를 위한 정책을 정의합니다.
* 모든 구독에서 SQL 데이터베이스 리소스의 보안을 hello를 모니터링 합니다.
* 보안 문제를 신속하게 파악하고 해결합니다.
* [Azure SQL Database 위협 감지](../sql-database/sql-database-threat-detection.md)에 대한 경고를 통합합니다.

또한 toohelping SQL 데이터베이스 리소스를 보호, 보안 모니터링 및 관리 Azure 가상 컴퓨터, 클라우드 서비스, 응용 프로그램 서비스, 가상 네트워크 등에 대 한 보안 센터 제공 합니다. [여기](security-center-intro.md)에서 보안에 대해 자세히 알아보세요.

## <a name="prerequisites"></a>필수 조건
보안 센터와 시작 tooget, 구독 tooMicrosoft Azure 있어야 합니다. 보안 센터의 hello 무료 계층은 구독에 사용할 수 있습니다. 보안 센터의 무료 및 표준 계층에 대한 자세한 내용은 [보안 센터 가격 책정](https://azure.microsoft.com/pricing/details/security-center/)을 참조하세요.

보안 센터는 역할 기반 액세스를 지원합니다. Azure에서 역할 기반 액세스 제어 (RBAC)에 대해 자세히 toolearn 참조 [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다. hello 보안 센터 FAQ에 정보를 제공 [보안 센터 권한을 처리 되는 방법과](security-center-faq.md#permissions)합니다.

## <a name="access-security-center"></a>Security Center 액세스
보안 센터 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다. [Toohello 포털에 로그인](https://portal.azure.com/) 및 선택 hello **보안 센터 옵션**합니다.

![보안 센터 옵션][1]

hello **보안 센터** 블레이드를 엽니다.
![보안 센터 블레이드][2]

## <a name="set-security-policy"></a>보안 정책 설정
보안 정책 hello hello 지정된 구독 또는 리소스 그룹 내의 리소스에 대 한 권장 되는 컨트롤 집합을 정의 합니다. 보안 센터 구독 또는 tooyour 회사의 보안 요구 사항과 hello 응용 프로그램 종류 또는 hello 데이터 각 구독에서의 민감도 따라 리소스 그룹에 대 한 정책을 정의 합니다.

SQL 감사 및 SQL 투명 한 데이터 암호화 (TDE)에 대 한 정책 tooshow를 설정할 수 있습니다.

* 켜면 **SQL 감사 및 위협 감지**, 메시지도 표시 고급 검색 기능 및 조사 목적으로 규정 준수에 대 한 감사 액세스 tooAzure 데이터베이스는 사용할 수 있습니다.
* **SQL 투명한 데이터 암호화**를 켠 경우, Security Center에서는 Azure SQL Database, 연결된 백업 및 트랜잭션 로그 파일에 대해 휴지 상태의 암호화를 활성화하는 것이 좋습니다.

보안 정책 tooset 선택 hello **정책** hello 보안 센터 블레이드를 바둑판식으로 배열 합니다. Hello에 **보안 정책** 블레이드, tooenable hello 보안 정책을 원하는 선택 hello 구독 합니다. 선택 **방지 정책** 설정 **에** hello toouse이이 구독에서 지정 하는 보안 권장 사항입니다.
![보안 정책][3]

toolearn 더 참조 [보안 정책 설정](security-center-policies.md)합니다.

## <a name="manage-security-recommendation"></a>보안 권장 사항 관리
보안 센터 리소스를 Azure의 hello 보안 상태를 정기적으로 분석합니다. 보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다. hello 권장 사항이 필요한 hello 컨트롤 구성의 hello 프로세스를 안내 합니다.

보안 정책을 설정 하면 보안 센터 리소스 tooidentify 잠재적인 취약점의 hello 보안 상태를 분석 합니다. hello 권장 사항은 여기서 각 줄은 한 가지 특정 권장 하는 테이블 형식으로 표시 됩니다. 다음 표에 Azure SQL 데이터베이스와 어떤 각 권장 사항에 적용 하는 경우에 대 한 hello 사용할 수 있는 권장 사항을 이해 하는 참조 toohelp으로 hello를 사용 합니다. 권장 구성을 선택 하면 tooan 문서 tooimplement 보안 센터의 권장 조치를 hello 하는 방법을 설명 하는으로 이동 합니다.

| 권장 사항 | 설명 |
| --- | --- |
| [SQL Server에서 감사 및 위협 감지 사용](security-center-enable-auditing-on-sql-servers.md) |SQL Database 서버에 대한 감사 및 위협 감지를 켜는 것이 좋습니다. (SQL Database 서비스만 해당. 가상 컴퓨터에서 실행 중인 Microsoft SQL Server는 포함하지 않음) |
| [SQL 데이터베이스에서 감사 및 위협 감지 사용](security-center-enable-auditing-on-sql-databases.md) |SQL Database 데이터베이스에 대한 감사 및 위협 감지를 켜는 것이 좋습니다. (SQL Database 서비스만 해당. 가상 컴퓨터에서 실행 중인 Microsoft SQL Server는 포함하지 않음) |
| [투명한 데이터 암호화 사용](security-center-enable-transparent-data-encryption.md) |SQL Database에 대해 암호화를 활성화하는 것이 좋습니다. (SQL Database 서비스만 해당) |

Azure 리소스로 선택 hello에 대 한 권장 사항을 toosee **권장 사항을** hello 보안 센터 블레이드를 바둑판식으로 배열 합니다. Hello에 **권장 사항을** 블레이드에서 권장 toosee 세부 정보를 선택 합니다. 이 예제에서는 **SQL Server에서 감사 및 위협 감지 사용**을 선택하겠습니다.

![권장 사항][4]

SQL server 감사 및 위협 감지 설정 되어 있지 않습니다 hello 보안 센터에서는 아래 표시 된 대로 합니다. 감사를 설정한 후 위협 요소 탐지 설정을 구성할 수 있으며 전자 메일 보안 경고 설정을 tooreceive 수 있습니다. 위협 요소 탐지 잠재적 보안 위협을 toohello 데이터베이스를 나타내는 비정상 데이터베이스 작업 감지 되 면이 알려 줍니다. hello 경고가 hello 보안 센터 대시보드에 표시 됩니다.
![감사 및 위협 감지][5]

Hello 단계에 따라 [hello Azure 포털에서에서 SQL 데이터베이스 위협 검색](../sql-database/sql-database-threat-detection-portal.md) tooturn에 위협 요소 탐지와 tooconfigure hello 목록 검색 비정상적인 활동에 대해 보안 경고를 받을 전자 메일 주소 및 구성 합니다.

권장 사항에 대해 자세히 toolearn 참조 [보안 권장 사항 관리](security-center-recommendations.md)합니다.

## <a name="monitor-security-health"></a>보안 상태 모니터링
사용 하도록 설정한 후 [보안 정책](security-center-policies.md) 구독의 리소스에 대 한 보안 센터 hello 보안 리소스 tooidentify 잠재적인 취약점을 분석 합니다.  Hello에서 리소스의 hello 보안 상태를 볼 수 있습니다 **리소스 보안 상태** 바둑판식으로 배열입니다. 클릭할 때 **데이터** hello에 **리소스 보안 상태** 타일을 hello **데이터 리소스** 감사와 같은 및 투명 한 문제에 대 한 SQL 권장 사항 블레이드에서 열립니다 데이터 암호화를 사용할 수 없습니다. Hello 데이터베이스의 hello 일반 성능 상태에 대 한 권장 사항에 있습니다.
![리소스 보안 상태][6]

toolearn 더 참조 [보안 상태 모니터링](security-center-monitoring.md)합니다.

## <a name="manage-and-respond-toosecurity-alerts"></a>관리 및 toosecurity 경고에 응답
보안 센터 자동으로 수집, 분석 및 로그 데이터를 통합 [Azure SQL 위협 요소 탐지](../sql-database/sql-database-threat-detection.md), 변경과 같이 다른 Azure 리소스와 toodetect 실제 위협 및 거짓 긍정을 줄입니다. Hello와 함께 보안 센터에서 우선 순위가 지정 된 보안 경고의 목록이 표시 됩니다 hello 문제 및 방법에 대 한 권장 사항 tooquickly 필요한 정보를 조사 tooremediate 공격입니다.

toosee 경고를 선택 하는 hello **보안 경고** hello 보안 센터 블레이드를 바둑판식으로 배열 합니다. Hello에 **보안 경고** 블레이드를 hello 이벤트를 발생 시킨 hello 알림과 부분, any, 과정을 설명 하는 경우 대 한 자세한 정보는 경고 toolearn tootake tooremediate 공격 필요 합니다. 이 예제에서는 **잠재적인 SQL 삽입**을 선택하겠습니다.
![보안 경고][7]

보안 센터에 추가 세부 정보를 제공 하는 어떤 트리거된 hello 경고에 대 한 정보 hello 대상 리소스를 해당 hello 소스 IP 주소 및 방법에 대 한 권장 사항 제공 아래와 같이 tooremediate 합니다.
![잠재적인 SQL 삽입][8]

toolearn 더 참조 [관리 및 응답 toosecurity 경고](security-center-managing-and-responding-alerts.md)합니다.

## <a name="next-steps"></a>다음 단계
* [보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) -일련의 단계를 수행 하 고 작업 toooptimize 조직의 보안 요구 사항 및 클라우드 관리 모델에 따라 보안 센터의 사용 합니다.
* [Security Center 데이터 보안](security-center-data-security.md) – Security Center에서 구성 정보, 메타데이터, 이벤트 로그, 크래시 덤프 파일 등을 포함한 Azure 리소스에 대한 데이터를 수집하고 처리하는 방법을 알아봅니다.
* [보안 문제를 처리](security-center-incident.md) -toouse hello 보안에서 보안 센터 tooassist 기능을 경고 하는 방법을 알아보려면 보안 문제를 처리 하는에 있습니다.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
