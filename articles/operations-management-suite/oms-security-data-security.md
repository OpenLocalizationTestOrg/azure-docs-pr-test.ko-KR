---
title: "관리 도구 모음 보안 및 감사 솔루션 데이터 보안 aaaOperations | Microsoft Docs"
description: "이 문서에서는 데이터를 Operations Management Suite 보안 및 감사 솔루션에서 데이터를 관리하고 보호하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Operations Management Suite 보안 및 감사 솔루션 데이터 보안
toohelp 고객 방지 감지 하 고 toothreats, 응답 [Operations Management Suite (OMS) 보안 및 감사 솔루션](operations-management-suite-overview.md) 수집 하 고 포함 하는 리소스에 대 한 데이터를 처리 합니다.

* 보안 이벤트 로그
* Windows (ETW) 이벤트에 대한 이벤트 추적
* AppLocker 감사 이벤트
* Windows 방화벽 로그
* 고급 위협 분석 이벤트
* 기준 평가 결과
* 맬웨어 방지 평가 결과
* 업데이트/패치 평가 결과
* Hello 에이전트에 명시적으로 설정 되어 있는 Syslogs 스트림

강력한 약정 tooprotect hello 개인 정보 및이 데이터의 보안으로 만듭니다. Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다.
이 문서에서는 OMS 보안 및 감사 솔루션에서 데이터를 관리하고 보호하는 방법을 설명합니다.

## <a name="data-sources"></a>데이터 원본
OMS 보안 및 감사 솔루션에는 hello OMS 에이전트를 설치한 가상 컴퓨터와 물리적 컴퓨터에서 데이터를 분석 합니다. OMS 보안 및 감사 솔루션에서는 Windows 이벤트, 감사 로그, IIS 로그 및 syslog 메시지와 같은 보안 이벤트에 대한 구성 정보를 수집할 수 있습니다. 이러한 데이터의 예: 운영 체제 유형 및 버전, 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다.  

## <a name="data-protection"></a>데이터 보호
**데이터 분리**: 데이터 hello 서비스 전체에서 각 구성 요소에 논리적으로 별도로 유지 됩니다. 모든 데이터에는 조직별로 태그가 지정됩니다. 이 태그 hello 데이터 수명 주기 동안 유지 되며 hello 서비스의 각 계층에서 적용 됩니다. 

**데이터 액세스**: tooprovide 보안 권장 사항 및 보안 위협 조사, Microsoft 담당자 수집 또는 서비스에 의해 분석 정보에 액세스할 수 있습니다. Toohello 준수 우리 [Microsoft 온라인 서비스 약관](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) 및 [개인정보취급방침](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), Microsoft가 고객 데이터를 사용 하 여 만들어지거나 한 보급 또는 유사한에서 정보를 파생 되지 않습니다 상태 상업적 목적으로 합니다. tooprovide 보안 권장 사항 및 보안 위협 조사, Microsoft 담당자 수집 또는 서비스에 의해 분석 정보에 액세스할 수 있습니다. 만 고객 데이터를 사용 하 여 필요한 tooprovide 목적으로 서비스를 제공 호환 비롯 하 여 서비스는 Azure로 합니다. 모든 권한 tooyour 직접 데이터를 유지 합니다.

**데이터 사용**: 패턴을 사용 하 여 Microsoft 및 위협 인텔리전스 표시를 여러 테 넌 트에서 tooenhance 취급 예방 및 감지 기능;에 설명 된 hello 개인 정보 행에 따라 이렇게 우리의 [개인 정보 문](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)합니다.

> [!NOTE]
> 데이터 위치 hello 작업 영역을 만드는 동안 hello 초기 OMS 보안 및 감사 구성 프로세스의 일부인 hello OMS 작업 영역 수준에서 구성 됩니다.
> 
> 

## <a name="see-also"></a>참고 항목
이 문서에서는 OMS에서 데이터를 관리하고 보호하는 방법을 알아봅니다. OMS 보안 및 감사 솔루션에 대해 자세히 toolearn 참조:

* [OMS(Operations Management Suite) 개요](operations-management-suite-overview.md)
* [모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고](oms-security-responding-alerts.md)
* [Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링](oms-security-monitoring-resources.md)

