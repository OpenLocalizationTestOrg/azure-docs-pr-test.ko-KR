---
title: "Azure 보안 센터에서 endpoint protection 상태 경고 aaaResolve | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 해결 Endpoint Protection 상태 경고 * *입니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Azure 보안 센터에서 Endpoint Protection 상태 경고 해결
Azure 보안 센터는 검색된 Endpoint Protection 상태 경고를 해결할 것을 권장합니다.  보안 센터 toosee를 끝점 보호 실패와 발생 한 오류 수는 가상 컴퓨터 (Vm)가 있습니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다. 단계별 가이드는 아닙니다.
> 
> 

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항 블레이드에서**선택, **해결 Endpoint Protection 상태 경고**합니다.
   ![Endpoint Protection 상태 경고 해결][1]
2. Hello 블레이드가 열립니다 **Endpoint Protection 오류** 각 VM에 대 한 실패 및 실패 hello 수와 Vm을 나열 하 합니다. Hello 목록에서 VM을 선택 합니다.
   ![Endpoint protection failure][2]
3. A **오류 목록** hello 실패 목록이 표시 하는 VM을 선택 하기 위해 블레이드에서 열립니다. 더 많은 hello 목록 toolearn에서 오류를 선택 합니다. Hello 선택 실패에 대 한 정보로는 블레이드가 열립니다.
   ![오류 목록][3]
   ![오류 이벤트][4]

## <a name="see-also"></a>참고 항목
보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)-자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)-- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)-toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)-자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
