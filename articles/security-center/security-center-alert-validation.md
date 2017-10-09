---
title: "Azure 보안 센터에서 유효성 검사 aaaAlerts | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터에서 toovalidate hello 보안 경고 하면 있습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Azure Security Center에서 경고 유효성 검사
이 문서에서 이해할 수 있도록 도와 어떻게 tooverify Azure 보안 센터 경고에 대 한 시스템이 올바로 구성 합니다.

## <a name="what-are-security-alerts"></a>보안 경고란?
보안 센터 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 방화벽 및 endpoint protection 솔루션, toodetect 경고 있습니다 toothreats 같은 연결 된 파트너 솔루션에서 로그 데이터를 통합 합니다. 읽기 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) 보안 경고 보기 및 읽기에 대 한 자세한 내용은 [Azure 보안 센터에서 보안 경고 이해](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn 자세한 에 대 한 hello 다른 유형의 경고 합니다.

## <a name="alert-validation"></a>경고 유효성 검사
보안 센터 에이전트가 컴퓨터에 설치 된 후 다음과 같이 hello 아래 hello 컴퓨터에서 toobe 공격 hello 리소스 hello 경고의 원하는 위치.

1. 실행 파일 (예제 calc.exe) toohello 컴퓨터의 데스크톱 또는 사용자의 편의의 다른 디렉터리를 복사 합니다.
2. 이 파일을 너무 이름을**ASC_AlertTest_662jfi039N.exe**합니다.
3. Hello 명령 프롬프트를 열고 인수 (방금 가짜 인수 이름)으로이 파일을 같이 실행: *ASC_AlertTest_662jfi039N.exe foo*
4. 5 too10 분 기다린 보안 센터 경고를 엽니다. 있습니다 하나는 경고와 비슷한 toofollowing를 찾아야 합니다.

    ![경고 유효성 검사](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

이 경고를 검토할 때는 hello 필드 인수 감사가 설정 되어 완전 나타나는지 확인 합니다. False 나타나면 tooenable 명령줄 인수 감사 해야 합니다. 다음 명령줄 hello를 사용 하 여이 옵션을 설정할 수 있습니다.

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>참고 항목
이 문서는 toohello 경고 유효성 검사 프로세스를 도입 했습니다. 이 유효성 검사에 익숙하다면 했으므로 hello 문서 다음을 시도해 보십시오.

* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)합니다. 자세한 내용은 방법 toomanage 경고 및 보안 센터에서 toosecurity 인시던트 응답 합니다.
* [Azure Security Center에서 보안 상태 모니터링](security-center-monitoring.md). Toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure Security Center에서 보안 경고 이해](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Hello 다양 한 유형의 보안 경고에 알아봅니다.
* [Azure Security Center 문제 해결 가이드](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). 보안 센터에서 tootroubleshoot 공통 발급 하는 방법에 대해 알아봅니다. 
* [Azure Security Center FAQ](security-center-faq.md)로 설정합니다. Hello 서비스를 사용 하는 방법에 대 한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/). Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

