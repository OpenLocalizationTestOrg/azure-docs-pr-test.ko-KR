---
title: "Azure 자동화 aaa 시작 | Microsoft Docs"
description: "이 문서에서는 Azure Marketplace에서 제공 하는 준비 tooonboard hello hello 디자인 및 구현 세부 정보를 검토 하 여 Azure 자동화 서비스의 개요를 제공 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Azure Automation 시작

이 시작된 가이드에서는 Azure 자동화의 핵심 개념 관련된 toohello 배포를 소개합니다. 이 가이드에서는 이해 하는 데는 Azure에서 새 tooAutomation 하거나 System Center Orchestrator와 같은 자동화 워크플로 소프트웨어 사용한 경험이 있는 경우 어떻게 tooprepare 및 온보드 자동화 합니다.  이후에 있습니다 준비 될 toobegin 프로세스 자동화 요구를 지원 하기 위해 runbook을 개발 합니다. 


## <a name="automation-architecture-overview"></a>Automation 아키텍처 개요

![Azure 자동화 개요](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Azure 자동화는 확장성과 안정성을 다중 테 넌 트를 제공 하는 saas () 응용 프로그램으로는 소프트웨어 환경 tooautomate runbook으로 처리 하 고 구성 변경 내용 tooWindows 및 원하는 상태 구성을 사용 하 여 Linux 시스템 관리 (DSC) Azure, 다른 클라우드 서비스 또는 온-프레미스에 있습니다. Runbook, 자산, 실행 계정과 같은 Automation 계정 내에 포함된 엔터티는 사용자 구독 및 다른 구독 내의 다른 Automation 계정으로부터 격리됩니다.  

Azure에서 실행하는 Runbook은 Azure PaaS(platform as a service) 가상 컴퓨터에서 호스팅되는 Automation 샌드박스에서 실행됩니다.  Automation 샌드박스는 모듈, 저장소, 메모리, 네트워크 통신, 작업 스트림 등의 Runbook을 실행하는 모든 측면에서 테넌트를 격리합니다. 이 역할 hello 서비스에서 관리 되며 toocontrol 있습니다에 대 한 Azure 또는 Azure 자동화 계정에서 액세스할 수 없습니다.         

하나 이상의 컴퓨터 toorun hello tooautomate hello 배포 및 관리 로컬 데이터 센터 또는 다른 클라우드 서비스는 자동화 계정을 만든 후에 리소스를 지정할 수 있습니다 [하이브리드 Runbook 작업자 (HRW)](automation-hybrid-runbook-worker.md) 역할입니다.  각 HRW 연결 tooa 로그 분석 작업 영역 및 자동화 계정을 사용 하 여 Microsoft Management Agent hello가 필요합니다.  Hello Microsoft 관리 에이전트 유지 관리 로그 분석은 사용 되는 toobootstrap hello 설치 하 고 hello HRW의 hello 기능을 모니터링 합니다.  Azure 자동화에서 수행 하는 runbook 및 hello 명령 toorun의 hello 배달 합니다.

Runbook에 대 한 여러 HRW tooprovide 고가용성을 배포 하 고, 잔액 runbook 작업을 로드 하 고, 특정 작업 또는 환경에 대 한 전용 경우에 따라 수 있습니다.  hello HRW에 Microsoft Monitoring Agent hello TCP 포트 443 통해 hello 자동화 서비스와의 통신을 시작 하 고 인바운드 방화벽 요구 사항은 없습니다.  Hello 환경 내에서 HRW에서 실행 중인 runbook을 해야 하 고 다른 컴퓨터 또는 해당 환경 내에서 서비스에 대 한 hello tooperform 관리 작업을 runbook, 될 수 있습니다 수 hello 다른 포트 runbook에 액세스를 해야 합니다.  Hello 문서 검토 하는 경우 IT 보안 정책을 네트워크 tooconnect toohello 인터넷에서 컴퓨터를 허용 하지 않으므로, [OMS 게이트웨이](../log-analytics/log-analytics-oms-gateway.md), 어떤 HRW toocollect hello에 대 한 프록시의 역할 작업 상태 및 구성 정보를 수신 합니다. 자동화 계정입니다.

Hello hello hello 컴퓨터 로컬 시스템 계정 컨텍스트에서 실행 되는 HRW에서 실행 중인 Runbook은 hello 권장 됨 보안 컨텍스트 hello 로컬 Windows 컴퓨터 관리 작업을 수행할 때. Hello 로컬 컴퓨터 외부의 리소스에 대 한 hello runbook toorun 작업을 하려는 경우에 hello hello runbook에서 액세스 하 고 tooauthenticate hello 외부 리소스로 사용할 수 있는 자동화 계정에서에서 toodefine 보안 자격 증명 자산을 할 수 있습니다. 사용할 수 있습니다 [자격 증명](automation-credentials.md), [인증서](automation-certificates.md), 및 [연결](automation-connections.md) toospecify 자격 증명 허용을 인증할 수 있도록 하는 cmdlet이 포함 된 runbook의 자산입니다.

Azure 자동화에 저장 하는 DSC 구성에 직접 적용 된 tooAzure 가상 컴퓨터 수 있습니다. 다른 실제 및 가상 컴퓨터는 hello Azure 자동화 DSC 끌어오기 서버에서 구성을 요청할 수 있습니다.  온-프레미스 물리적 또는 가상 Windows 및 Linux 시스템의 구성, 관리 하기 위한 않아도 toodeploy 모든 인프라 toosupport hello 자동화 DSC 끌어오기 서버에서 자동화 DSC에 의해 관리 되는 각 시스템 toobe에서만 아웃 바운드 인터넷 액세스 TCP 포트 443 toohello OMS 서비스를 통해 통신 합니다.   

## <a name="prerequisites"></a>필수 조건

### <a name="automation-dsc"></a>자동화 DSC
Azure 자동화 DSC toomanage 사용 되는 다양 한 일 수 있습니다.

* Windows 또는 Linux를 실행 중인 Azure 가상 컴퓨터(클래식)
* Windows 또는 Linux를 실행 중인 Azure 가상 컴퓨터
* Windows 또는 Linux를 실행 중인 AWS(Amazon Web Services) 가상 컴퓨터
* 온-프레미스 또는 Azure나 AWS 이외의 클라우드에 있는 Windows 실제/가상 컴퓨터
* 온-프레미스 또는 Azure나 AWS 이외의 클라우드에 있는 Linux 실제/가상 컴퓨터

최신 버전의 WMF 5 hello hello PowerShell DSC에 대 한 에이전트 Windows toobe 수 toocommunicate Azure 자동화에 설치 되어야 합니다. 최신 버전의 hello hello [Linux 용 PowerShell DSC 에이전트](https://www.microsoft.com/en-us/download/details.aspx?id=49150) Linux toobe 수 toocommunicate Azure 자동화에 대 한 설치 해야 합니다.

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
컴퓨터 toorun 하이브리드 runbook 작업을 지정 하면,이 컴퓨터 hello 다음이 있어야 합니다.

* Windows Server 2012 이상
* Windows PowerShell 4.0 이상  신뢰성 향상된을 위해 hello 컴퓨터에 Windows PowerShell 5.0을 설치 하는 것이 좋습니다. Hello에서 hello 새 버전을 다운로드할 수 있습니다 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50395)
* 최소 두 개의 코어
* 최소 4GB의 RAM

### <a name="permissions-required-toocreate-automation-account"></a>필요한 toocreate 자동화 계정 권한
이 항목 toocomplete 필요한 사용 권한 및 다음 특정 권한을 hello toocreate 또는 자동화 계정 업데이트 해야 합니다.   
 
* 순서 toocreate 자동화 계정에에서 AD 사용자 계정의 사용 권한 해당 toohello 소유자 역할을 가진 toobe 추가 tooa 역할 Microsoft.Automation 리소스에 대 한 설명 된 대로 문서의 [Azure 자동화에서 역할 기반 액세스 제어 ](automation-role-based-access-control.md).  
* Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**예**, Azure AD 테 넌 트의 관리자가 아닌 사용자 수 [AD 응용 프로그램 등록](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)합니다.  Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**아니요**,이 작업을 수행 하는 hello 사용자는 Azure ad에서 전역 관리자 여야 합니다. 

가 아닌 hello 구독 Active Directory 인스턴스에서 소속 toohello 전역 관리자/공동 관리자의 역할 hello 구독을 추가 하기 전에 사용자 tooActive 디렉터리에 게스트로 추가 됩니다. 이 경우에는 "없는 사용 권한을 toocreate..." 표시 hello에 경고 **자동화 계정 추가** 블레이드입니다. 먼저 hello 구독 Active Directory 인스턴스에서 제거할 수도 있고 toomake 다시 추가 toohello 전역 관리자/공동 관리자 역할에 추가 된 사용자를 해당 Active Directory에서 전체 사용자입니다. tooverify hello에서 이러한 경우 **Azure Active Directory** hello Azure 포털의에서 창 **사용자 및 그룹**선택, **모든 사용자에 게** 및 hello를 선택한 후 특정 사용자 **프로필**합니다. 값의 hello hello **사용자 유형** hello 사용자 프로필 아래에 특성 같지 해야 **게스트**합니다.

## <a name="authentication-planning"></a>인증 계획
Azure 자동화 하면 tooautomate 작업 리소스에 대 한 다른 클라우드 공급자와 azure에서 온-프레미스에서.  Runbook tooperform 위해에서 필요한 작업을 있어야 hello 리소스에 액세스 권한을 toosecurely hello 구독 내에서 필요한 hello 최소의 권한을 가진 합니다.  

### <a name="what-is-an-automation-account"></a>Automation 계정이란? 
Hello Azure cmdlet을 사용 하 여 Azure 자동화에서 리소스에 대해 수행 하는 모든 hello 자동화 작업 tooAzure Azure Active Directory 조직 id 자격 증명 기반 인증을 사용 하 여 인증 합니다.  자동화 계정을 toosign toohello 포털 tooconfigure에서 사용 하 고 Azure 리소스를 사용 하 여 hello 계정와에서 분리 됩니다.  계정에 포함 된 자동화 리소스 hello 다음과 같습니다.

* **인증서** - runbook 또는 DSC 구성의 인증에 사용되는 인증서를 포함하거나 추가합니다.
* **연결** -인증 및 구성 필요한 정보 tooconnect tooan 외부 서비스 또는 응용 프로그램에서 runbook 또는 DSC 구성을 포함 합니다.
* **자격 증명** -사용자 이름 및 암호 필요 같은 보안 자격 증명을 포함 하는 PSCredential 개체 runbook 또는 DSC 구성에서 tooauthenticate 합니다.
* **통합 모듈** -는 runbook 및 DSC 구성 내에서 cmdlet의 Azure 자동화 계정 toomake 사용에 포함 된 PowerShell 모듈입니다.
* **일정** - 반복되는 빈도를 포함하여 지정된 시간에 runbook을 시작하거나 중지하는 일정을 포함합니다.
* **변수** - runbook 또는 DSC 구성에서 사용할 수 있는 값을 포함합니다.
* **DSC 구성** -PowerShell 스크립트를 설명 하는 방법을 tooconfigure 운영 체제 기능 또는 설정 또는 Windows 또는 Linux 컴퓨터에 응용 프로그램을 설치 합니다.  
* **Runbook** - Windows PowerShell을 기반으로 하는 Azure Automation에서 자동화된 프로세스 일부를 수행하는 일단의 작업입니다.    

각 자동화 계정의 자동화 리소스 hello 단일 Azure 지역과 연관 되어 있지만 자동화 계정은 구독에서 모든 hello 리소스를 관리할 수 있습니다. 데이터와 리소스 toobe 격리 tooa 특정 지역을 필요로 하는 정책이 있는 경우 자동화 계정을 다른 지역에 만듭니다.

> [!NOTE]
> 자동화 계정 및 hello 리소스를 포함 하는 hello Azure 포털에서에서 만들어진, hello Azure 클래식 포털에에서 액세스할 수 없습니다. 이러한 계정 또는 Windows PowerShell을 사용 하 여 해당 리소스 toomanage를 원하는 경우 hello Azure 리소스 관리자 모듈을 사용 해야 합니다.
> 

Hello Azure 포털에서에서 자동화 계정을 만들면 두 인증 엔터티에 자동으로 만듭니다.

* 실행 계정 이 계정은 Azure AD(Azure Active Directory)의 서비스 주체 및 인증서를 만듭니다. 또한 hello 참가자 역할 기반 액세스 제어 (RBAC) runbook을 사용 하 여 리소스 관리자 리소스를 관리 하는 할당 합니다.
* 클래식 실행 계정 이 계정에 runbook을 사용 하 여 사용 되는 toomanage 클래식 리소스는 관리 인증서를 업로드 합니다.

역할 기반 액세스 제어 작업 tooan Azure AD 사용자 계정 및 계정으로 실행을 허용 하는 Azure 리소스 관리자 toogrant은 사용할 수 있게 하 고 해당 서비스 보안 주체를 인증 합니다.  읽기 [Azure 자동화 문서에서 역할 기반 액세스 제어](automation-role-based-access-control.md) toohelp 자세한 정보에 대 한 자동화 권한 관리를 위한 모델을 개발 합니다.  

#### <a name="authentication-methods"></a>인증 방법
hello 다음 표에 요약 되어 Azure 자동화에서 지 원하는 각 환경에 대 한 hello 다른 인증 방법을 사용 합니다.

| 메서드 | Environment 
| --- | --- | 
| Azure 실행 또는 클래식 실행 계정 |Azure Resource Manager 및 Azure 클래식 배포 |  
| Azure AD 사용자 계정 |Azure Resource Manager 및 Azure 클래식 배포 |  
| Windows 인증 |로컬 데이터 센터 또는 hello Hybrid Runbook Worker를 사용 하 여 다른 클라우드 공급자 |  
| AWS 자격 증명 |Amazon 웹 서비스 |  

Hello에서 **어떻게 to\Authentication 및 보안** 섹션 tooconfigure 인증 된 기존 하거나 해당 환경에 대 한 개요 및 구현 단계를 제공 하는 문서를 지 원하는 하거나 새 계정을 해당 환경에 사용 되는 전용입니다.  Azure 계정으로 실행 하는 hello 및 기존 실행 계정에 대 한 항목을 hello [업데이트 자동화 실행 계정을](automation-create-runas-account.md) 방법을 tooupdate 기존 자동화 계정으로 실행 하는 hello로는 hello 포털 또는 되지 않은 경우 PowerShell을 사용 하 여을 계정 설명 원래 계정으로 실행 또는 클래식 계정으로 실행 계정으로 구성 합니다. Toocreate 실행 하 고 기본 실행 계정을 엔터프라이즈 인증 기관 (CA)에서 발급 한 인증서를 검토 toocreate hello를 사용 하 여 계정을 어떻게 문서 toolearn이이 구성 합니다.     
 
## <a name="network-planning"></a>네트워크 계획
Hello Hybrid Runbook Worker tooconnect tooand 레지스터와 Microsoft OMS Operations Management Suite ()에 대 한 액세스 toohello 포트 번호가 있어야 하 고 hello Url 아래에서 설명 합니다.  이 또한 toohello [포트 및에 필요한 Url hello Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS 합니다. Hello 에이전트와 hello OMS 서비스 간의 통신에 프록시 서버를 사용 하는 경우 hello 적절 한 리소스를 액세스할 수 있는 tooensure를 해야 합니다. 방화벽 toorestrict 액세스 toohello 인터넷을 사용 하는 경우 방화벽 toopermit 액세스 tooconfigure 해야 있습니다.

아래 목록 hello 포트 및 자동화 Hybrid Runbook Worker toocommunicate hello에 필요한 Url hello 정보입니다.

* 포트: 아웃바운드 인터넷 액세스에는 TCP 443만 필요
* 글로벌 URL: *.azure-automation.net

특정 지역에 대해 정의 된 자동화 계정이 있는 경우 해당 지역의 데이터 센터와 toorestrict 통신 hello 다음 표에서 hello DNS 레코드 각 지역에 대 한.

| **지역** | **DNS 레코드** |
| --- | --- |
| 미국 중남부 |scus-jobruntimedata-prod-su1.azure-automation.net |
| 미국 동부 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| 미국 중서부 | wcus-jobruntimedata-prod-su1.azure-automation.net |
| 서유럽 |we-jobruntimedata-prod-su1.azure-automation.net |
| 북유럽 |ne-jobruntimedata-prod-su1.azure-automation.net |
| 캐나다 중부 |cc-jobruntimedata-prod-su1.azure-automation.net |
| 동남아시아 |sea-jobruntimedata-prod-su1.azure-automation.net |
| 인도 중부 |cid-jobruntimedata-prod-su1.azure-automation.net |
| 일본 동부 |jpe-jobruntimedata-prod-su1.azure-automation.net |
| 오스트레일리아 동남부 |ase-jobruntimedata-prod-su1.azure-automation.net |
| 영국 남부 | uks-jobruntimedata-prod-su1.azure-automation.net |
| 미국 정부 버지니아 | usge-jobruntimedata-prod-su1.azure-automation.us |

목록이 이름 대신 IP 주소에 대 한 다운로드 하 여 검토 hello [Azure 데이터 센터 IP 주소](https://www.microsoft.com/download/details.aspx?id=41653) hello Microsoft 다운로드 센터에서에서 xml 파일입니다. 

> [!NOTE]
> 이 파일에는 hello IP 주소 범위 (계산, SQL 및 저장소 범위) hello Microsoft Azure 데이터 센터에서에서 사용 되는 포함 되어 있습니다. 현재 배포 된 hello 범위 및 모든 이후 변경 toohello IP 범위를 반영 하는 업데이트 된 파일 매주 게시 됩니다. 최소한 한 주에 대 한 hello 파일에 표시 되는 새 범위가 hello 데이터 센터에서 사용 되지 않습니다. 다운로드 hello 새 xml 파일 매주 하 고 사이트에 hello 필요한 변경을 수행 하십시오 toocorrectly Azure에서 실행 되는 서비스를 식별 합니다. Express 경로 사용자 tooupdate hello BGP 광고 hello Azure 공간의 각 월의 첫째 주를 사용 하는이 파일을 발견할 수 있습니다. 
> 

## <a name="creating-an-automation-account"></a>Automation 계정 만들기

여러 가지 방법으로 hello Azure 포털에서에서 자동화 계정을 만들 수 있습니다.  다음 표에서 hello 각 유형의 배포 환경 및 이들 간의 차이 소개 합니다.  

|메서드 | 설명 |
|-------|-------------|
| Hello Marketplace에서에서 자동화 및 제어를 선택 합니다. | 자동화 계정 및 OMS 작업 영역 만듭니다 되는 제품 연결 tooone 동일한 리소스 그룹 및 지역에서 다른 hello 합니다.  OMS와의 통합 또한 toomonitor 로그 분석을 사용 하는 hello 이점은 포함 및 시간에 따라 runbook 작업 상태 및 작업 스트림 분석 및 tooescalate 고급 기능을 활용 하거나 문제를 조사 합니다. 기본적으로 활성화 되 hello 변경 내용 추적 및 업데이트 관리 솔루션을 배포 hello도 제공 합니다. |
| Hello Marketplace에서에서 자동화를 선택 합니다. | OMS 작업 영역 연결된 tooan 아니며 hello 자동화 및 제어를에서 사용 가능한 솔루션을 포함 하지 않는 새로운 또는 기존 리소스 그룹의 자동화 계정을 만듭니다. TooAutomation 소개 하는 기본 구성을 이므로 toowrite runbook, DSC 구성 및 사용 하 여 hello hello 서비스의 기능에 어떻게 방법을 알 수 있습니다. |
| 선택한 관리 솔루션 | – 솔루션을 선택 하는 경우  **[업데이트 관리](../operations-management-suite/oms-solution-update-management.md)**,  **[업무 외 시간 동안 시작/중지 Vm](automation-solution-vm-management.md)**, 또는  **[ 변경 내용 추적을](../log-analytics/log-analytics-change-tracking.md)**  tooselect 기존 자동화 하 고 OMS 작업 영역에서 메시지를 표시 하거나 구독에 배포 된 hello 솔루션 toobe에 필요한 두 옵션 toocreate hello를 제안 하는 것입니다. |

이 항목에서는 온 보 딩 hello 자동화 및 제어를 제공 함으로써 자동화 계정 및 OMS 작업 영역을 만드는 과정을 안내 합니다.  독립 실행형 테스트 또는 toopreview hello 서비스 검토 hello 다음 문서에 대 한 자동화 계정 toocreate [독립 실행형 자동화 계정 만들기](automation-create-standalone-account.md)합니다.  

### <a name="create-automation-account-integrated-with-oms"></a>OMS와 통합된 Automation 계정 만들기
hello는 메서드 tooonboard를 자동화 hello Marketplace에서에서 hello 자동화 및 제어 제품을 선택 하 여는 것이 좋습니다.  자동화 계정을 만들고 hello 통합 솔루션을 비롯 한 hello 옵션 tooinstall hello 관리 hello 제품과 함께 제공 되는 OMS 작업 영역을 설정 합니다.  

1. Hello 구독 관리자 역할의 멤버 및 hello 구독의 공동 관리자 인 계정으로 Azure 포털 toohello에 로그인 합니다.

2. **새로 만들기**를 클릭합니다.<br><br> ![Azure Portal에서 새 옵션을 선택합니다.](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. 검색할 **자동화** 다음 hello에 검색 결과 선택 하 고 **자동화 및 제어*** 합니다.<br><br> ![Marketplace에서 Automation 및 컨트롤을 검색하고 선택합니다](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Hello 제공에 대 한 설명을 hello를 읽은 후 클릭 **만들기**합니다.  

5. Hello에 **자동화 및 제어** 설정 블레이드에서 **OMS 작업 영역**합니다.  Hello에 **OMS 작업 영역** 블레이드에서 hello 자동화 계정을 동일한 Azure 구독에이 OMS 작업 영역 연결 toohello를 선택 하거나 OMS 작업 영역을 만듭니다.  OMS 작업 영역 경우 선택 **새 작업 영역 만들기** hello에 **OMS 작업 영역** 블레이드 hello 다음을 수행 합니다. 
   - 새 hello에 대 한 이름을 지정 **OMS 작업 영역**합니다.
   - 선택 된 **구독** toolink hello 기본 선택 된 적절 하지 않은 경우 tooby hello 드롭 다운 목록에서 선택 합니다.
   - **리소스 그룹**의 경우, 리소스 그룹을 만들거나 기존 리소스 그룹을 선택할 수 있습니다.  
   - **위치**를 선택합니다.  현재는 사용할 수 있는 유일한 위치 hello **오스트레일리아 남동부**, **미국 동부**, **동남 아시아**, **중앙 미국 서 부**, 및  **서 부 유럽**합니다.
   - **가격 책정 계층**을 선택합니다.  두 계층에 hello 솔루션 프린터가: 해제 하 고 노드 (OMS) 당 계층입니다.  hello 무료 계층에서는 hello 매일, 보존 기간 및 runbook 작업 런타임 분 수집 된 데이터 양을 제한 합니다.  매일 수집 되는 데이터의 hello 금액에 hello 노드 (OMS) 당 계층 제한을 않아도 됩니다.  
   - **Automation 계정**을 선택합니다.  필요한 모르는 새로운 OMS 작업 영역을 만드는 경우 tooalso hello 새로운 OMS 작업 영역 이전에 지정한 Azure 구독, 리소스 그룹 및 영역을 포함 하 여와 연결 된 자동화 계정 만들기.  선택할 수 있습니다 **자동화 계정 만들기** hello에 **자동화 계정** 블레이드를 hello 다음을 제공 합니다. 
  - Hello에 **이름** 필드의 자동화 계정 hello hello 이름을 입력 합니다.

    다른 모든 옵션 hello OMS 작업 영역이 선택에 따라 자동으로 채워진 및 이러한 옵션을 수정할 수 없습니다.  Azure 계정으로 실행 계정은 hello 제공에 대 한 hello 기본 인증 방법입니다.  클릭 한 후 **확인**hello 구성 옵션은 유효성을 검사 하 고 hello 자동화 계정이 생성 됩니다.  진행률을 추적할 수 있습니다 **알림** hello 메뉴에서 합니다. 

    그렇지 않으면, 기존 Automation 실행 계정을 선택합니다.  선택한 hello 계정 연결된 tooanother OMS 작업 영역 일 수 없습니다, 그리고 hello 블레이드에서 알림 메시지가 표시 되는 그렇지 않은 경우.  이미 연결 되어 다른 자동화 계정으로 실행 계정을 tooselect 필요 하거나 만드십시오.

    필요한 hello 정보를 완료 한 후 클릭 **만들기**합니다.  hello 정보를 확인 하 고 hello 자동화 계정 및 실행 계정을 생성 됩니다.  Toohello 반환될지 **OMS 작업 영역** 블레이드 자동으로 합니다.  

6. Hello에 hello 필요한 정보를 제공한 후 **OMS 작업 영역** 블레이드에서 클릭 **만들기**합니다.  Hello 정보를 확인 하 고 hello 작업 영역이 만들어진, 아래에서 진행률을 추적할 수 있습니다 **알림** hello 메뉴에서 합니다.  Toohello 반환될지 **솔루션 추가** 블레이드입니다.  

7. Hello에 **자동화 및 제어** 설정 블레이드에서 tooinstall hello 권장 미리 선택 된 솔루션을 것인지 확인 합니다. 선택을 취소한 경우 나중에 개별적으로 설치할 수 있습니다.  

8. 클릭 **만들기** tooproceed 온 보 딩 자동화 및 OMS 작업 영역입니다. 모든 설정 유효성을 검사 하 고 구독에서 제공 하는 toodeploy hello를 시도 합니다.  이 프로세스는 몇 가지 걸릴 수 초 toocomplete 하 고 아래에서 해당 진행률을 추적할 수 **알림** hello 메뉴에서 합니다. 

Hello 제공 등록 된 후에 runbook, 작업 hello로 사용 하도록 설정한 관리 솔루션 만들기를 시작, 배포 수 있습니다는 [하이브리드 Runbook 작업자](automation-hybrid-runbook-worker.md) 역할 또는 작업 시작 [로그 분석](https://docs.microsoft.com/azure/log-analytics) 클라우드 또는 온-프레미스 환경에서 리소스에 의해 생성 된 toocollect 데이터입니다.   

## <a name="next-steps"></a>다음 단계
* [Azure Automation 실행 계정 인증 테스트](automation-verify-runas-authentication.md)를 검토하여 새 Automation 계정이 Azure 리소스에 대해 인증할 수 있는지 확인할 수 있습니다.
* runbook을 만드는 것부터 시작 tooget, hello를 먼저 검토 [자동화 runbook 형식](automation-runbook-types.md) 작성을 시작 하기 전에 지원 잠금과 고려 사항입니다.


