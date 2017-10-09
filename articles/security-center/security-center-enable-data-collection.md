---
title: "Azure 보안 센터에서 데이터 수집 aaaEnable | Microsoft Docs"
description: " 자세한 내용은 방법 Azure 보안 센터에서 tooenable 데이터 컬렉션입니다. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Azure 보안 센터에서 데이터 수집 활성화

> [!NOTE]
> 보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다. toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md)합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>
>

보안 센터에서에서 데이터를 수집한 가상 컴퓨터 (Vm) tooassess 자신의 보안 상태, 보안 권장 사항을 제공 하 고 있습니다 toothreats 경고 합니다. 보안 센터를 처음 사용할 때는 구독에서 모든 Vm에 대 한 hello 옵션 tooenable 데이터 수집을 수 있습니다. 데이터 수집을 사용 하지 않는 경우 해당 구독에 대 한 보안 정책 hello 데이터 수집을 켭니다 보안 센터 것이 좋습니다.

데이터 수집을 사용 하는 경우 Azure 가상 컴퓨터 및 만들어진 새로 프로 비전 hello Microsoft Monitoring Agent에 모든 기존 보안 센터 지원. Microsoft Monitoring Agent hello 다양 한 보안 관련 구성을 검색합니다. 또한 hello 운영 체제 이벤트 로그 이벤트를 발생 시킵니다. 이러한 데이터의 예: 운영 체제 유형 및 버전, 운영 체제 로그(Windows 이벤트 로그), 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다. Microsoft Monitoring Agent hello 이벤트 로그 항목 및 구성 읽고 분석용 hello 데이터 tooyour 작업 영역을 복사 합니다. 또한 Microsoft Monitoring Agent hello 크래시 덤프 파일 tooyour 작업 영역을 복사합니다.

보안 센터의 무료 계층 hello를 사용 하는 경우에 hello 보안 정책에서 데이터 수집을 해제 하 여 가상 컴퓨터에서 데이터 수집을 해제할 수 있습니다. 데이터 수집을 사용하지 않도록 설정하면 VM의 보안 평가가 제한됩니다. toolearn 더 참조 [데이터 수집을 사용 하지 않도록 설정](#disabling-data-collection)합니다. VM 디스크 스냅숏 및 아티팩트 컬렉션은 데이터 수집이 사용하지 않도록 설정된 경우에도 여전히 사용하도록 설정됩니다. 데이터 컬렉션 보안 센터의 hello 표준 계층에 구독이 필요 합니다.

> [!NOTE]
> Security Center의 무료 및 표준 계층에 대한 자세한 내용은 [가격 책정 계층](security-center-pricing.md)을 참조하세요.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다. 이 문서는 단계별 가이드가 아닙니다.
>
>

1. Hello에 **권장 사항을** 블레이드를 **구독에 대 한 데이터 컬렉션 활성화**합니다.  Hello 열립니다 **데이터 컬렉션 켜기** 블레이드입니다.
   ![권장 사항 블레이드][2]
2. Hello에 **데이터 컬렉션 켜기** 블레이드에서 구독을 선택 합니다. hello **보안 정책** 해당 구독에 대 한 블레이드를 엽니다.
3. Hello에 **보안 정책** 블레이드를 **에** 아래 **데이터 수집** tooautomatically 로그를 수집 합니다. 모든 현재와 새 데이터 컬렉션 프로 비전 hello 확장에 대 한 모니터링 설정 hello 구독에서는 Vm을 지원 합니다.
4. **저장**을 선택합니다.
5. **확인**을 선택합니다.

## <a name="disabling-data-collection"></a>데이터 수집 비활성화
보안 센터의 무료 계층 hello를 사용 하는 경우에 hello 보안 정책에서 데이터 수집을 해제 하 여 언제 든 지 가상 컴퓨터에서 데이터 수집을 해제할 수 있습니다. 데이터 컬렉션 보안 센터의 hello 표준 계층에 구독이 필요 합니다.

1. Toohello 반환 **보안 센터** 블레이드에 대 한 선택 hello **정책** 바둑판식으로 배열입니다. Hello 열립니다 **구독 당 정책 보안 정책-정의** 블레이드입니다.
   ![Hello 정책 타일을 선택 합니다.][5]
2. Hello에 **구독 당 정책 보안 정책-정의** 블레이드, 선택 hello 구독 toodisable 데이터 수집 한다고 합니다.
3. hello **보안 정책** 해당 구독에 대 한 블레이드를 엽니다.  데이터 컬렉션에서 **끄기** 를 선택합니다.
4. 선택 **저장** hello 위쪽 리본 메뉴에 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "사용 데이터 컬렉션입니다." 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)-toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)-자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
- [Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
