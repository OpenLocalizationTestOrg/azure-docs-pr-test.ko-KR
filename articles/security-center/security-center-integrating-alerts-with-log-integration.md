---
title: "Azure와 함께 Azure 보안 센터 알림을 aaaIntegrating 로그 통합 | Microsoft Docs"
description: "이 문서는 Azure 로그 통합에 보안 센터 알림을 통합하는 데 도움을 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Azure 로그 통합에 Azure Security Center 알림 통합
많은 보안 작업 및 사고 대응 팀은 시작 지점에 대 한 심사 및 보안 경고를 조사 하는 hello를 보안 정보 및 이벤트 관리 (SIEM) 솔루션으로 사용 합니다. Azure 로그 통합을 사용하여 Azure Security Center 알림을 SIEM 솔루션에 통합할 수 있습니다.

Azure 로그 통합은 현재 HP ArcSight, Splunk 및 IBM QRadar를 지원합니다.

## <a name="what-logs-can-i-integrate"></a>어떤 로그와 통합할 수 있나요?
Azure에서는 모든 서비스에 대해 광범위한 로깅을 생성합니다. 이러한 로그는 다음과 같이 분류됩니다.

* **컨트롤/관리 로그** hello에 대 한 가시성을 제공 하는 Azure 리소스 관리자 만들기, 업데이트 및 삭제 작업입니다. 이러한 제어 평면 이벤트 hello Azure 활동 로그에 표시
* **데이터 평면 로그** 하는 Azure 리소스를 사용 하는 경우 발생 하는 hello 이벤트에 대 한 가시성을 제공 합니다. 예를 들어 hello Windows 이벤트 로그에 있는 hello 이벤트 뷰어 보안 채널에서 보안 이벤트 정보를 얻을 수 있습니다. 데이터 평면 이벤트(가상 컴퓨터 또는 Azure 서비스에서 생성)는 Azure 진단 로그에 표시됩니다.

현재 azure 로그 통합의 hello 통합을 지원합니다.

* Azure VM 로그
* Azure 감사 로그
* Azure 보안 센터 경고

## <a name="install-azure-log-integration"></a>Azure 로그 통합 설치
[Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324)을 다운로드합니다.

hello Azure 로그 통합 서비스가 설치 되어 있는 hello 컴퓨터에서 원격 분석 데이터를 수집 합니다.  수집된 원격 분석 데이터는 다음과 같습니다.

* Azure 로그 통합 실행 중에 발생하는 예외
* 쿼리 및 처리 된 이벤트의 hello 수에 대 한 메트릭
* 어떤 Azlog.exe 명령줄 옵션이 사용되었는지에 대한 통계

> [!NOTE]
> 이 옵션을 선택 취소하여 원격 분석 데이터의 컬렉션을 해제할 수 있습니다.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Azure 감사 로그 및 보안 센터 경고 통합
1. 명령 프롬프트 열기 hello 및 **cd** 에 **c:\Program Files\Microsoft Azure 로그 통합**합니다.
2. Hello 실행 **azlog createazureid** 명령 toocreate는 [Azure Active Directory 서비스 사용자](../active-directory/active-directory-application-objects.md) hello Azure AD (Active Directory)에서 호스트 하는 테 넌 트 hello Azure 구독.

    Azure 로그인을 묻는 메시지가 표시됩니다.

   > [!NOTE]
   > Hello 구독 소유자 또는 hello 구독의 공동 관리자 여야 합니다.
   >
   >

    인증 tooAzure Azure AD를 통해 수행 됩니다.  Azure 로그 통합에 대 한 서비스 사용자를 만들면 액세스 tooread Azure 구독에서 지정 된 hello Azure AD id를 만들어집니다.
3. Hello 실행 **azlog 권한을 부여 <SubscriptionID>**  hello 구독 toohello 서비스 보안 주체에 2 단계에서 만든 tooassign 판독기 액세스 명령입니다. 지정 하지 않으면는 **SubscriptionID**, hello 서비스 사용자는 할당 된 hello 판독기 역할 tooall 구독 toowhich 액세스할 수 있습니다.

   > [!NOTE]
   > Hello를 실행 하는 경우 경고를 표시 될 수 있습니다 **권한을 부여** hello 직후 명령을 **createazureid** 명령입니다. Hello Azure AD 계정이 만들어질 때와 hello 계정에 사용 하기 위해 제공 된 경우 간에 약간의 대기 시간이 있습니다. Hello를 실행 한 후까지 10 초 정도 대기 하는 경우 **createazureid** 명령 toorun hello **권한을 부여** 명령, 다음 이러한 경고가 표시 되지 않습니다.
   >
   >
4. 감사 로그 JSON 파일 hello 폴더 tooconfirm 다음 hello 사항이 확인 합니다.

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. 보안 센터 알림을에 존재 하는 폴더 tooconfirm 다음 hello를 확인 합니다.

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Hello SIEM 파일 전달자 커넥터 toohello 적절 한 폴더를 구성 합니다. hello 프로시저를 사용 하는 SIEM hello에 따라 달라 집니다.

## <a name="next-steps"></a>다음 단계
Azure 활동 로그 및 속성 정의 대해 자세히 toolearn 참조:

* [리소스 관리자로 작업 감사](../azure-resource-manager/resource-group-audit.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.
