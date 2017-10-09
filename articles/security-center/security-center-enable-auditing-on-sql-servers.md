---
title: "Azure 보안 센터의 SQL server에 aaaEnable 감사 및 위협 감지 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * SQL 서버 * *에서 감사를 사용 하도록 설정 및 위협 검색 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Azure Security Center에서 SQL 서버에 대한 감사 및 위협 감지 사용
감사 및 위협 감지를 아직 사용하도록 설정하지 않은 경우 Azure SQL 서버의 모든 데이터베이스에 대한 감사를 켜는 것이 좋습니다. 감사 및 위협 감지는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.

감사를 설정한 후에 위협 요소 탐지 설정 및 전자 메일 tooreceive 보안 경고를 구성할 수 있습니다. 위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다. 이 toodetect 있으며 나타나는 순서 대로 toopotential 위협에 대응 합니다.

이 권장 사항은 적용 toohello Azure SQL 서비스에만 사용 합니다. Azure 인프라 서비스 (Azure IaaS)에서 가상 컴퓨터에서 실행 되는 SQL Server 포함 되지 않습니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  단계별 가이드는 아닙니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **SQL 서버에서 감사를 사용 하도록 설정 및 위협 검색**합니다.  Hello 열립니다 **SQL 서버에서 감사를 사용 하도록 설정 및 위협 검색** 블레이드입니다.

   ![SQL Server 감사 활성화][1]
2. 에 SQL server tooenable 감사 및 위협 검색을 선택 합니다. Hello 열립니다 **감사 및 위협 요소 탐지** 블레이드입니다.

3. Hello에 **감사 및 위협 요소 탐지** 블레이드를 **ON** 아래 **감사**합니다.

   ![감사 설정 켜기][2]
4. Hello 단계에 따라 [Azure 포털 hello에 SQL 데이터베이스 감사](../sql-database/sql-database-auditing-portal.md) 감사 로그를 저장할 tooconfigure 저장소입니다. hello 데이터 컬렉션에 대 한 구독의 저장소 계정 hello 기본 저장소 계정이입니다.
5. Hello 단계에 따라 [SQL 데이터베이스 위협 검색 시작](../sql-database/sql-database-threat-detection.md) tooturn에 위협 요소 탐지와 tooconfigure hello 목록 검색 비정상적인 활동에 대해 보안 경고를 받을 전자 메일 주소 및 구성 합니다.

## <a name="see-also"></a>참고 항목
이 문서에 설명 했습니다 ""감사를 사용 및 위협 SQL 서버에서 검색 합니다. 보안 센터 권장 tooimplement hello 하는 방법 SQL 데이터베이스를 보호에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [SQL 데이터베이스 보안 설정](../sql-database/sql-database-security-overview.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
