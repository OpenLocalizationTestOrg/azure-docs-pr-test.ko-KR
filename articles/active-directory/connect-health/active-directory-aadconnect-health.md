---
title: "aaaMonitor hello에 온-프레미스 id 인프라에 클라우드입니다."
description: "이 무엇 인지 설명 하는 hello Azure AD Connect Health 페이지 및 사용 하는 이유입니다."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>프로그램 hello 클라우드에서 온-프레미스 id 인프라 및 동기화 서비스를 모니터링 합니다.
Azure (Azure AD) Active Directory Connect Health를 사용 하 여 모니터링 하 고 온-프레미스 id 인프라 및 hello 동기화 서비스 파악할 수 있습니다. 하면 toomaintain 안정적인 연결 tooOffice 365 및 Microsoft 온라인 서비스 (Azure AD Connect 서버가 Active Directory Federation Services (AD FS) 서버와 같은 주요 id 구성 요소에 대 한 모니터링 기능을 제공 하 여 동기화 엔진의 경우)으로 Active Directory 도메인 컨트롤러, 등입니다. 하기가 이러한 구성 요소에 대 한 중요 한 데이터 요소 hello 쉽게 사용을 얻을 수 있도록 액세스 및 기타 중요 한 insights toomake 정보를 결정 합니다.

hello로 hello 정보를 제공 [Azure AD Connect Health 포털](https://aka.ms/aadconnecthealth)합니다. Hello Azure AD Connect Health 포털에서 경고, 성능 모니터링, 사용 현황 분석 및 기타 정보를 볼 수 있습니다. Azure AD Connect Health hello 한 곳에서 키 id 구성 요소에 대 한 상태의 단일 렌즈를 수 있습니다.

![Azure AD Connect Health 정의](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Azure AD Connect Health의 hello 기능 커질수록 hello 포털 id의 hello 렌즈를 통해 단일 대시보드를 제공 합니다. 해당 기능 tooget 작업을 수행 훨씬 더 강력 하 고 정상, 통합 된 환경을 사용자 tooincrease를 가져옵니다.

## <a name="why-use-azure-ad-connect-health"></a>Azure AD Connect Health를 사용하는 이유
Azure AD와 온-프레미스 디렉터리를 통합 한 일반 id tooaccess 모두 클라우드 및 온-프레미스 리소스에 있기 때문에 사용자에 게 생산성을 높일 됩니다. 그러나이 통합의 모든 장치에서 사용자가 온-프레미스와 hello 두 클라우드 리소스를 안전 하 게 액세스할 수 있도록이 환경이 정상 인지 확인 해야 hello 챌린지를 만듭니다. Azure AD Connect Health를 사용 하면 모니터링 하 고 사용 되는 tooaccess Office 365 또는 다른 Azure AD 응용 프로그램에 온-프레미스 id 인프라에 대 한 정보를 얻을 수 있습니다. 각 온-프레미스 ID 서버에 에이전트를 설치하는 것만큼 간단합니다.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[AD FS에 대한 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
AD FS용 Azure AD Connect Health는 Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 R2에서 AD FS 2.0을 지원합니다. 또한 모니터링 hello AD FS 프록시를 지원 하거나 인증을 제공 하는 웹 응용 프로그램 프록시 서버가 엑스트라넷 액세스에 대 한 지원 합니다. Hello Health Agent의 쉽고 저렴 한 비용 설치에서는 AD FS에 대 한 Azure AD Connect Health의 주요 기능 집합을 추적 하는 hello를 제공 합니다.

* AD FS 및 AD FS 프록시 서버 정상 상태가 아닌 경우 경고 tooknow를 사용 하 여 모니터링
* 중요한 경고에 대한 전자 메일 알림
* AD FS의 용량 계획에 유용한 성능 데이터의 동향
* AD FS를 사용 하기 유용한 toounderstand 요소인 피벗 (앱, 사용자, 네트워크 위치 등)를 사용 하 여 AD FS 로그인 기능에 대 한 사용 현황 분석
* 잘못된 사용자 이름/암호를 시도한 상위 50명의 사용자와 그들의 최신 IP 주소와 같은 AD FS에 대한 보고서

hello 다음 비디오에서는 Azure AD Connect Health에 대해 간략하게 AD FS에 대 한 합니다.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[동기화에 대한 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)
동기화에 대 한 azure AD Connect Health를 모니터링 하 고 hello 동기화 하면 온-프레미스 Active Directory와 Azure AD 간에 발생 하는 방법에 대 한 정보를 제공 합니다. 동기화에 대 한 azure AD Connect Health의 주요 기능 집합을 추적 하는 hello를 제공 합니다.

* 경고 tooknow 때 Azure AD Connect 서버를 사용 하 여 모니터링, 라고도 hello 동기화 엔진이 정상이 아님
* 중요한 경고에 대한 전자 메일 알림
* 다른 작업에 대한 대기 시간 차트, 동기화 작업(추가, 업데이트, 삭제 등)의 동향을 비롯한 동기화 작업 통찰력
* 성공적인 눈에 보는 정보 동기화 속성에 대 한 및 마지막 tooAzure AD 내보내기
* 개체 수준 동기화 오류에 대한 보고서는 \(Azure AD Premium이 필요 없음\)

hello 다음 비디오에서는 Azure AD Connect Health에 대해 간략하게 동기화 합니다.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[AD DS용 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
AD DS(Active Directory Domain Services)용 Azure AD Connect Health는 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016에 설치된 도메인 컨트롤러에 대한 모니터링을 제공합니다. hello Health Agent 설치 수 있도록 하면 toomonitor 온-프레미스 AD DS 환경을 hello 클라우드에서 합니다. AD DS에 대 한 azure AD Connect Health의 주요 기능 집합을 추적 하는 hello를 제공 합니다.

* 도메인 컨트롤러는 정상 상태가 아닌 및 위험 경고에 대 한 알림을 전자 메일로 보낼 때 경고 toodetect 모니터링
* 빠른 hello 상태 보기 및 도메인 컨트롤러의 작업 상태를 제공 하는 hello 도메인 컨트롤러 대시보드
* hello 최신 복제 정보 않으며 오류가 감지 되 면 tootroubleshooting 안내선을 연결 하는 hello 복제 상태 대시보드
* 빠른 어느 곳에서 나 인기 있는 성능 카운터 문제 해결 및 모니터링을 위해 필요한 tooperformance 데이터 그래프

hello 다음 비디오에서는 Azure AD Connect Health에 대해 간략하게 AD DS에 대 한 합니다.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Azure AD Connect Health 시작
Azure AD Connect Health를 사용 하 여 hello 단계 tooget 시작:

1. [Azure AD Premium을 다운로드](../active-directory-get-started-premium.md)하거나 [평가판을 시작](https://azure.microsoft.com/trial/get-started-active-directory/)합니다.
2. [Azure AD Connect Health 에이전트](#download-and-install-azure-ad-connect-health-agent)를 다운로드하여 ID 서버에 설치합니다.
3. 보기 hello Azure AD Connect Health 대시보드 [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth)합니다.

> [!NOTE]
> Azure AD Connect Health 대시보드에 데이터를 볼 대상된 서버에 Azure AD Connect Health Agent tooinstall hello를 필요가 있다는 기억 하세요.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Azure AD Connect Health 에이전트 다운로드 및 설치
* 다음 사항을 확인 하면 [hello 요구 사항을 충족](active-directory-aadconnect-health-agent-install.md#requirements) Azure AD Connect Health에 대 한 합니다.
* AD FS용 Azure AD Connect Health 사용 시작
    * [AD FS용 Azure AD Connect Health Agent 다운로드.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Hello 설치 지침을 참조](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs)합니다.
* 동기화용 Azure AD Connect Health 사용 시작
    * [Hello 최신 버전의 Azure AD Connect 다운로드 및 설치](http://go.microsoft.com/fwlink/?linkid=615771)합니다. 동기화에 대 한 Health Agent hello hello Azure AD Connect 설치의 일부로 설치 됩니다 (1.0.9125.0 버전 이상)입니다.
* AD DS용 Azure AD Connect Health 사용 시작
    * [AD DS용 Azure AD Connect Health 에이전트 다운로드](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Hello 설치 지침을 참조](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds)합니다.

## <a name="azure-ad-connect-health-portal"></a>Azure AD Connect Health 포털
경고, 모니터링, 성능 및 사용 현황 분석의 뷰를 표시 하는 hello Azure AD Connect Health 포털 됩니다. hello https://aka.ms/aadconnecthealth URL에서는 Azure AD Connect Health의 주 블레이드에서 toohello 합니다. 블레이드를 창으로 생각할 수 있습니다. 참조 hello 주 블레이드에서 **빠른 시작**, Azure AD Connect Health, 및의 추가 구성 옵션의 서비스에 합니다. Hello 참조 스크린 샷 및 hello 스크린 샷 다음에 나오는 간략하게 설명 합니다. Hello 에이전트를 배포한 후 hello 상태 관리 서비스는 자동으로 Azure AD Connect Health가 모니터링 하는 hello 서비스를 식별 합니다.

> [!NOTE]
> 라이선스 정보에 대 한 참조 hello [Azure AD 연결 FAQ](active-directory-aadconnect-health-faq.md) 또는 hello [Azure AD 가격 책정 페이지](https://aka.ms/aadpricing)합니다.
    
![Azure AD Connect Health 포털](./media/active-directory-aadconnect-health/portal4.png)

* **빠른 시작**:이 옵션을 선택 하는 경우 hello **빠른 시작** 블레이드를 엽니다. 선택 하 여 hello Azure AD Connect Health Agent를 다운로드할 수 있습니다 **도구 가져오기를**합니다. 설명서에 액세스하고 피드백을 제공할 수도 있습니다.
* **Active Directory Federation Services**:이 옵션을 Azure AD Connect Health는 현재 모니터링 hello AD FS 서비스를 모두 표시 합니다. 인스턴스를 선택 하면 hello 블레이드를 엽니다 해당 서비스 인스턴스에 대 한 정보를 표시 합니다. 개요, 속성, 경고, 모니터링 및 사용 현황 분석이 이러한 정보에 포함됩니다. Hello 기능에 대 한 자세한 설명 [AD FS와 함께 사용 하 여 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)합니다.
* **Azure Active Directory Connect(동기화)**: 이 옵션은 Azure AD Connect Health에서 현재 모니터링하는 Azure AD Connect 서버를 표시합니다. Hello 항목을 선택 하는 경우 hello 블레이드를 엽니다 Azure AD Connect 서버에 대 한 정보를 표시 합니다. Hello 기능에 대 한 자세한 설명 [동기화를 사용 하 여 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)합니다.
* **Active Directory 도메인 서비스**:이 옵션을 Azure AD Connect Health는 현재 모니터링 hello AD DS 포리스트를 모두 표시 합니다. 포리스트를 선택 하면 hello 블레이드를 엽니다 해당 포리스트에 대 한 정보를 표시 합니다. 이 정보는 중요 한 정보, hello 도메인 컨트롤러 대시보드, hello 복제 상태 대시보드에서, 경고 및 모니터링에 대 한 개요를 포함 합니다. Hello 기능에 대 한 자세한 설명 [AD DS와 함께 사용 하 여 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)합니다.
* **구성**:이 섹션에서는 옵션 tooturn hello 다음 설정 하거나 해제 합니다.

  - 자동 업데이트 tooautomatically update hello Azure AD Connect Health 에이전트 toohello 최신 버전: 사용할 수 있는 경우 자동으로 업데이트 된 toohello hello Azure AD Connect Health Agent의 최신 버전이 됩니다. 이 옵션은 기본적으로 사용하도록 설정되어 있습니다.
  - Microsoft access tooyour Azure AD 디렉터리의 상태 데이터 문제 해결을 위해서만 허용:이 사용 하는 경우 Microsoft가 확인할 수 hello 동일한 데이터를 표시 합니다. 이 정보는 문제 해결 및 지원에 도움이 될 수 있습니다. 이 옵션은 기본적으로 사용하지 않도록 설정되어 있습니다.

## <a name="related-links"></a>관련 링크
* [Azure AD Connect Health 에이전트 설치](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 작업](active-directory-aadconnect-health-operations.md)
* [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)
* [동기화에 대한 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)
* [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)
