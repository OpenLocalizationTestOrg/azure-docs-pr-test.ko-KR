---
title: "Azure Automation 시작 | Microsoft Docs"
description: "이 문서에서는 Azure Marketplace에서 제공하는 제품을 등록하기 위한 준비 과정에서 설계 및 구현 세부 정보를 검토함으로써 Azure Automation 서비스에 대해 간략히 설명합니다."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/31/2017
ms.author: magoedte
ms.openlocfilehash: fad13053895c5d6e3c41835fea3cf0bdd3380cd4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="getting-started-with-azure-automation"></a>Azure Automation 시작

이 시작 가이드에서는 Azure Automation 배포와 관련된 핵심 개념을 소개합니다. Azure Automation을 처음 사용하거나 System Center Orchestrator와 같은 자동화 워크플로 소프트웨어를 사용해 보았으면 이 가이드를 통해 Automation을 준비하고 등록하는 방법을 이해할 수 있습니다.  그런 후에는 프로세스 자동화 요구 사항을 지원하기 위해 runbook을 개발할 준비가 됩니다. 


## <a name="automation-architecture-overview"></a>Automation 아키텍처 개요

![Azure Automation 개요](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Azure Automation은 Azure, 다른 클라우드 서비스 또는 온-프레미스에서 Runbook을 사용하여 프로세스를 자동화하고 DSC(필요한 상태 구성)를 사용하여 Windows 및 Linux 시스템의 구성 변경 사항을 관리하는 안정적이며 확장성이 있는 다중 테넌트 환경을 제공하는 SaaS(software as a service)입니다. Runbook, 자산, 실행 계정과 같은 Automation 계정 내에 포함된 엔터티는 사용자 구독 및 다른 구독 내의 다른 Automation 계정으로부터 격리됩니다.  

Azure에서 실행하는 Runbook은 Azure PaaS(platform as a service) 가상 컴퓨터에서 호스팅되는 Automation 샌드박스에서 실행됩니다.  Automation 샌드박스는 모듈, 저장소, 메모리, 네트워크 통신, 작업 스트림 등의 Runbook을 실행하는 모든 측면에서 테넌트를 격리합니다. 이 역할은 서비스에 의해 관리되고 사용자가 제어할 Azure 또는 Azure Automation 계정에서 액세스할 수 없습니다.         

로컬 데이터 센터 또는 다른 클라우드 서비스에서 리소스의 배포 및 관리를 자동화하려면 Automation 계정을 만든 후 하나 이상의 컴퓨터에서 [HRW(Hybrid Runbook Worker)](automation-hybrid-runbook-worker.md) 역할을 실행하도록 지정할 수 있습니다.  각 HRW에는 Log Analytics 작업 영역 및 Automation 계정에 연결된 Microsoft Management Agent가 필요합니다.  Log Analytics는 설치를 부트스트랩하고 Microsoft Management Agent를 유지 관리하며 HRW의 기능을 모니터링하는 데 사용됩니다.  Runbook 및 Runbook 실행 지침은 Azure Automation에 의해 전달됩니다.

여러 HRW를 배포하여 Runbook에 고가용성을 제공하고, Runbook 작업의 부하를 분산하고, 일부 경우에 특정 워크로드 또는 환경에 대한 전용으로 사용할 수 있습니다.  HRW에서 Microsoft Monitoring Agent는 TCP 포트 443을 통해 Automation 서비스와 통신을 시작하고 인바운드 방화벽 요구 사항은 없습니다.  Runbook이 환경 내의 HRW에서 실행 중이고 Runbook에서 다른 컴퓨터에 대한 관리 작업 또는 환경 내의 서비스를 수행하려는 경우 Runbook이 액세스해야 하는 다른 포트가 있을 수 있습니다.  IT 보안 정책이 네트워크에 있는 컴퓨터를 인터넷에 연결하지 않는 경우 [OMS 게이트웨이](../log-analytics/log-analytics-oms-gateway.md) 문서를 검토합니다. 해당 게이트웨이는 작업 상태를 수집하고 Automation 계정에서 구성 정보를 수신하는 HRW의 프록시 역할을 수행합니다.

HRW에서 실행되는 Runbook은 컴퓨터의 로컬 시스템 계정이라는 컨텍스트에서 실행되며 로컬 Windows 컴퓨터에서 관리 작업을 수행할 때 권장되는 보안 컨텍스트입니다. Runbook이 로컬 컴퓨터 외부에서 리소스에 대한 작업을 실행하려면 Runbook에서 액세스할 수 있는 Automation 계정에서 보안 자격 증명 자산을 정의하고 외부 리소스를 사용하여 인증하는 데 사용할 수도 있습니다. 이를 인증할 수 있도록 자격 증명을 지정할 수 있는 cmdlet과 함께 Runbook의 [자격 증명](automation-credentials.md), [인증서](automation-certificates.md) 및 [연결](automation-connections.md) 자산을 사용할 수 있습니다.

Azure Automation에 저장된 DSC 구성은 Azure 가상 컴퓨터에 직접 적용할 수 있습니다. 기타 물리적 및 가상 컴퓨터는 Azure Automation DSC 풀 서버에서 구성을 요청할 수 있습니다.  온-프레미스 물리적 또는 가상 Windows 및 Linux 시스템의 구성을 관리하려면 OMS 서비스에 TCP 포트 443을 통해 통신하기 때문에 Automation DSC에 의해 관리되는 각 시스템의 아웃바운드 인터넷 액세스인 Automation DSC 끌어오기 서버를 지원하는 인프라를 배포할 필요가 없습니다.   

## <a name="prerequisites"></a>필수 조건

### <a name="automation-dsc"></a>자동화 DSC
Azure 자동화 DSC를 다양한 컴퓨터의 관리에 사용할 수 있습니다.

* Windows 또는 Linux를 실행 중인 Azure 가상 컴퓨터(클래식)
* Windows 또는 Linux를 실행 중인 Azure 가상 컴퓨터
* Windows 또는 Linux를 실행 중인 AWS(Amazon Web Services) 가상 컴퓨터
* 온-프레미스 또는 Azure나 AWS 이외의 클라우드에 있는 Windows 실제/가상 컴퓨터
* 온-프레미스 또는 Azure나 AWS 이외의 클라우드에 있는 Linux 실제/가상 컴퓨터

Windows용 PowerShell DSC 에이전트가 Azure Automation과 통신하려면 최신 버전의 WMF 5가 설치되어 있어야 합니다. 최신 버전 [Linux용 PowerShell DSC 에이전트](https://www.microsoft.com/en-us/download/details.aspx?id=49150)가 Azure Automation과 통신하려면 Linux용으로 설치되어야 합니다.

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
하이브리드 Runbook 작업을 실행하는 컴퓨터를 지정할 때 이 컴퓨터에는 다음 항목이 있어야 합니다.

* Windows Server 2012 이상
* Windows PowerShell 4.0 이상  안정성 개선을 위해 컴퓨터에 Windows PowerShell 5.0을 설치하는 것이 좋습니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=50395)에서 새 버전을 다운로드할 수 있습니다.
* 최소 두 개의 코어
* 최소 4GB의 RAM

### <a name="permissions-required-to-create-automation-account"></a>Automation 계정을 만드는 데 필요한 권한
Automation 계정을 만들거나 업데이트하려면 이 항목을 완료하는 데 필요한 다음과 같은 특정 권한이 있어야 합니다.   
 
* Automation 계정을 만들려면 [Azure Automation에서 역할 기반 액세스 제어](automation-role-based-access-control.md) 문서에 설명된 대로 Microsoft.Automation 리소스에 대한 소유자 역할과 동일한 권한을 가진 역할에 AD 사용자 계정을 추가해야 합니다.  
* 앱 등록 설정이 **예**로 지정되어 있는 경우 Azure AD 테넌트의 관리자가 아닌 사용자는 [AD 응용 프로그램을 등록](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)할 수 있습니다.  앱 등록 설정이 **아니요**로 지정되어 있는 경우 이 작업을 수행하는 사용자는 Azure AD의 전역 관리자여야 합니다. 

구독의 전역 관리자/공동 관리자 역할에 추가되기 전에 구독 Active Directory 인스턴스의 멤버가 아닌 경우 Active Directory에 게스트로 추가됩니다. 이 상황에서는 “만들 수 있는 사용 권한이 없습니다…”라는 메시지를 받습니다. **Automation 계정 추가** 블레이드의 경고. 전역 관리자/공동 관리자 역할에 처음 추가된 사용자는 구독 Active Directory 인스턴스에서 제거한 다음 다시 추가하여 Active Directory의 완전한 사용자로 만들 수 있습니다. Azure Portal의 **Azure Active Directory** 창에서 이 상황을 확인하려면 **사용자 및 그룹**을 선택한 다음 **모든 사용자**를 선택하거나 특정 사용자를 선택한 후 **프로필**을 선택합니다. 사용자 프로필에서 **사용자 유형** 속성의 값은 **Guest**와 같지 않아야 합니다.

## <a name="authentication-planning"></a>인증 계획
Azure Automation을 사용하여 Azure, 온-프레미스 및 다른 클라우드 공급자의 리소스에 대해 작업을 자동화할 수 있습니다.  Runbook이 필요한 작업을 수행하려면 구독 내에서 최소의 권한으로 리소스에 안전하게 액세스할 수 있는 권한이 있어야 합니다.  

### <a name="what-is-an-automation-account"></a>Automation 계정이란? 
Azure Automation에서 Azure cmdlet을 사용하여 리소스에 대해 수행하는 모든 자동화 작업은 Azure Active Directory 조직 ID 자격 증명 기반 인증을 사용하여 Azure에 인증합니다.  Automation 계정을 포털에 로그인하는 데 사용한 계정과 분리하여 Azure 리소스를 구성하고 사용합니다.  계정에 포함된 Automation 리소스는 다음과 같습니다.

* **인증서** - runbook 또는 DSC 구성의 인증에 사용되는 인증서를 포함하거나 추가합니다.
* **연결** - runbook 또는 DSC 구성에서 외부 서비스 또는 응용 프로그램에 연결하는 데 필요한 인증 및 구성 정보를 포함합니다.
* **자격 증명** - runbook 또는 DSC 구성에서 인증하는 데 필요한 사용자 이름 및 암호와 같은 보안 자격 증명이 포함된 PSCredential 개체입니다.
* **통합 모듈** - runbook 및 DSC 구성 내에서 cmdlet을 사용할 수 있도록 Azure Automation 계정에 포함된 PowerShell 모듈입니다.
* **일정** - 반복되는 빈도를 포함하여 지정된 시간에 runbook을 시작하거나 중지하는 일정을 포함합니다.
* **변수** - runbook 또는 DSC 구성에서 사용할 수 있는 값을 포함합니다.
* **DSC 구성** - 운영 체제 기능을 구성하거나 Windows 또는 Linux 컴퓨터에 응용 프로그램을 설정하거나 설치하는 방법을 설명하는 PowerShell 스크립트입니다.  
* **Runbook** - Windows PowerShell을 기반으로 하는 Azure Automation에서 자동화된 프로세스 일부를 수행하는 일단의 작업입니다.    

각 Automation 계정의 Automation 리소스는 단일 Azure 지역과 연결되지만 Automation 계정은 구독 내 모든 리소스를 관리할 수 있습니다. 데이터 및 리소스를 특정 지역으로 격리해야 하는 정책이 있는 경우 여러 지역에서 Automation 계정을 만듭니다.

> [!NOTE]
> Azure Portal에서 작성된 Automation 계정 및 Automation 계정이 포함하는 리소스는 Azure 클래식 포털에서 액세스할 수 없습니다. 이러한 계정 또는 해당 리소스를 Windows PowerShell을 사용하여 관리하려는 경우 Azure 리소스 관리자 모듈을 사용해야 합니다.
> 

Azure Portal에서 Automation 계정을 만들 경우 두 개의 인증 엔터티를 자동으로 만듭니다.

* 실행 계정 이 계정은 Azure AD(Azure Active Directory)의 서비스 주체 및 인증서를 만듭니다. 또한 Runbook을 사용하여 Resource Manager 리소스를 관리하는 참가자 역할 기반 액세스 제어(RBAC)를 할당합니다.
* 클래식 실행 계정 이 계정은 Runbook을 사용하여 클래식 리소스를 관리하는 데 사용되는 관리 인증서를 업로드합니다.

Azure Resource Manager에서 역할 기반 액세스 제어를 사용하여 Azure AD 사용자 계정 및 실행 계정에 허용된 작업을 수락하고 서비스 주체를 인증할 수 있습니다.  Automation 사용 권한 관리 모델을 개발하는 방법에 대한 자세한 내용은 [Azure Automation에서 역할 기반 액세스 제어 문서](automation-role-based-access-control.md)를 참조하세요.  

#### <a name="authentication-methods"></a>인증 방법
다음 표에는 Azure Automation에서 지원하는 각 환경에 대한 다양한 인증 방법이 요약되어 있습니다.

| 메서드 | Environment 
| --- | --- | 
| Azure 실행 또는 클래식 실행 계정 |Azure Resource Manager 및 Azure 클래식 배포 |  
| Azure AD 사용자 계정 |Azure Resource Manager 및 Azure 클래식 배포 |  
| Windows 인증 |Hybrid Runbook Worker를 사용하는 로컬 데이터 센터 또는 다른 클라우드 공급자 |  
| AWS 자격 증명 |Amazon 웹 서비스 |  

**인증 및 보안 방법** 섹션에는 이러한 환경에 대해 기존 계정 또는 새 계정을 사용하여 해당 환경에 대한 인증을 구성하기 위한 개요 및 구현 단계를 제공하는 문서가 있습니다.  Azure 실행 계정 및 클래식 실행 계정과 관련하여 원래 실행 계정 또는 클래식 실행 계정으로 구성되지 않은 경우 [Automation 실행 계정 업데이트](automation-create-runas-account.md) 항목에서 포털 또는 PowerShell을 사용하여 기존 Automation 계정을 실행 계정으로 업데이트하는 방법을 설명합니다. 엔터프라이즈 CA(인증 기관)에서 발급한 인증서로 실행 계정 및 클래식 실행 계정을 만들려면 이 문서를 검토하여 이 구성을 사용하여 계정을 만드는 방법에 대해 알아봅니다.     
 
## <a name="network-planning"></a>네트워크 계획
Hybrid Runbook Worker를 사용하여 Microsoft Operations Management Suite(OMS)에 연결하고 등록하려면 아래 설명된 포트 번호 및 URL에 대한 액세스 권한이 있어야 합니다.  [Microsoft Monitoring Agent에 필요한 포트 및 URL](../log-analytics/log-analytics-windows-agents.md#network) 외에도 OMS에 연결합니다. 에이전트와 OMS 서비스 간의 통신에 프록시 서버를 사용하는 경우 적절한 리소스에 액세스할 수 있는지 확인해야 합니다. 방화벽을 사용하여 인터넷에 대한 액세스를 제한하는 경우 액세스를 허용하도록 방화벽을 구성해야 합니다.

아래 정보는 Hybrid Runbook Worker에서 Automation과 통신하는 데 필요한 포트 및 URL을 나열합니다.

* 포트: 아웃바운드 인터넷 액세스에는 TCP 443만 필요
* 글로벌 URL: *.azure-automation.net

특정 지역에 대해 정의된 Automation 계정이 있고 해당 지역의 데이터 센터와 통신을 제한하려는 경우 다음 표에서는 각 지역에 대한 DNS 레코드를 제공합니다.

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

이름 대신 IP 주소 목록을 보려면 Microsoft 다운로드 센터에서 [Azure 데이터 센터 IP 주소](https://www.microsoft.com/download/details.aspx?id=41653) xml 파일을 다운로드하여 검토하세요. 

> [!NOTE]
> 이 파일에는 Microsoft Azure 데이터 센터에서 사용되는 IP 주소 범위(Compute, SQL 및 Storage 범위 포함)가 포함되어 있습니다. 현재 배포된 범위와 향후 예정된 IP 범위 변경 내용을 반영하는 업데이트 파일이 매주 게시됩니다. 파일에 표시되는 새 범위는 적어도 1주일 동안 데이터 센터에서 사용되지 않습니다. Azure에서 실행되는 서비스를 정확하게 식별할 수 있도록 매주 새로운 xml 파일을 다운로드하고 사이트에서 필요한 변경 작업을 수행하세요. ExpressRoute 사용자는 각 달의 첫 번째 주에 Azure 공간의 BGP 광고를 업데이트하는 데 이 파일이 사용되는 것을 보게 될 수도 있습니다. 
> 

## <a name="creating-an-automation-account"></a>Automation 계정 만들기

여러 가지 방법으로 Azure Portal에서 Automation 계정을 만들 수 있습니다.  다음 표에서는 각 유형의 배포 환경 및 이들 간의 차이점을 소개합니다.  

|메서드 | 설명 |
|-------|-------------|
| Marketplace에서 Automation 및 컨트롤 선택 | 제품을 사용하여 동일한 리소스 그룹 및 지역에서 서로 연결된 Automation 계정 및 OMS 작업 영역을 모두 만듭니다.  OMS와 통합하면 Log Analytics를 사용하여 시간이 지남에 따라 Runbook 작업 상태 및 작업 스트림을 모니터링 및 분석하고 고급 기능을 활용하여 문제를 보고하거나 조사할 수 있는 이점이 있습니다. 또한 기본적으로 사용되는 변경 내용 추적 및 업데이트 관리 솔루션도 배포합니다. |
| Marketplace에서 Automation 선택 | OMS 작업 영역에 연결되지 않고 Automation 및 컨트롤 제품에서 사용 가능한 솔루션을 포함하지 않는 새로운 또는 기존 리소스 그룹에서 Automation 계정을 만듭니다. Automation를 소개하는 기본 구성이며 이를 통해 Runbook, DSC 구성을 작성하고 서비스의 기능을 사용하는 방법을 알아볼 수 있습니다. |
| 선택한 관리 솔루션 | 솔루션 – **[업데이트 관리](../operations-management-suite/oms-solution-update-management.md)**, **[몇 시간 동안 VM 시작/중지](automation-solution-vm-management.md)** 또는 **[변경 내용 추적](../log-analytics/log-analytics-change-tracking.md)**을 선택하는 경우 기존 Automation 및 OMS 작업 영역을 선택하라는 메시지가 표시되거나 구독에서 배포할 솔루션의 필요에 따라 모두 만드는 옵션을 제공합니다. |

이 항목에서는 Automation 및 컨트롤 제품을 등록하여 Automation 계정 및 OMS 작업 영역을 만드는 방법을 설명합니다.  테스트하기 위해 독립 실행형 Automation 계정을 만들거나 서비스를 미리 보려면 다음 [독립 실행형 Automation 계정 만들기](automation-create-standalone-account.md) 문서를 검토합니다.  

### <a name="create-automation-account-integrated-with-oms"></a>OMS와 통합된 Automation 계정 만들기
Automation을 등록하려면 Marketplace에서 Automation 및 컨트롤 제품을 선택하는 것이 좋습니다.  그러면 Automation 계정을 만들고 제품에 사용할 수 있는 관리 솔루션을 설 하는 옵션을 포함하는 OMS 작업 영역과 통합을 설정할 수 있습니다.  

1. 구독 관리자 역할의 멤버이자 구독의 공동 관리자인 계정으로 Azure Portal에 로그인합니다.

2. **새로 만들기**를 클릭합니다.<br><br> ![Azure Portal에서 새 옵션을 선택합니다.](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. **Automation**을 검색한 다음 검색 결과에서 **Automation 및 컨트롤***을 선택합니다.<br><br> ![Marketplace에서 Automation 및 컨트롤을 검색하고 선택합니다](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. 제품에 대한 설명을 읽은 후에 **만들기**를 클릭합니다.  

5. **Automation 및 컨트롤** 설정 블레이드에서 **OMS 작업 영역**을 선택합니다.  **OMS 작업 영역** 블레이드에서 Automation 계정이 있는 동일한 Azure 구독에 연결된 OMS 작업 영역을 선택하거나 OMS 작업 영역을 새로 만듭니다.  OMS 작업 영역이 없으면 **새 작업 영역 만들기**를 선택하고 **OMS 작업 영역** 블레이드에서 다음을 수행합니다. 
   - 새 **OMS 작업 영역**에 대한 이름을 지정합니다.
   - 기본으로 선택된 값이 적절하지 않으면 드롭다운 목록에서 선택하여 연결할 **구독**을 선택합니다.
   - **리소스 그룹**의 경우, 리소스 그룹을 만들거나 기존 리소스 그룹을 선택할 수 있습니다.  
   - **위치**를 선택합니다.  자세한 내용은 [Azure Automation을 사용할 수 있는 지역](https://azure.microsoft.com/regions/services/)을 참조하세요.  솔루션은 체험 계층 및 노드당(OMS) 계층이라는 두 가지 계층으로 제공됩니다.  무료 계층은 하루에 수집되는 데이터의 양, 보존 기간 및 Runbook 작업 런타임 시간(분)이 제한됩니다.  노드당(OMS) 계층은 하루에 수집할 수 있는 데이터의 양이 제한되지 않습니다.  
   - **Automation 계정**을 선택합니다.  OMS 작업 영역을 새로 만드는 경우, Azure 구독, 리소스 그룹 및 지역을 비롯하여 앞서 지정한 새 OMS 작업 영역과 연결되는 Automation 계정도 만들어야 합니다.  **Automation 계정 만들기**을 선택하고 **Automation 계정** 블레이드에서 다음을 제공합니다. 
  - **이름** 필드에서 Automation 계정의 이름을 입력합니다.

    다른 모든 옵션은 선택한 OMS 작업 영역을 기반으로 자동으로 채워지며 이러한 옵션은 수정할 수 없습니다.  Azure 실행 계정은 제품에 대한 기본 인증 방법입니다.  **확인**을 클릭하면 구성 옵션의 유효성이 검사되고 Automation 계정이 생성됩니다.  메뉴의 **알림**에서 진행 상황을 추적할 수 있습니다. 

    그렇지 않으면, 기존 Automation 실행 계정을 선택합니다.  선택한 계정은 다른 OMS 작업 영역에 미리 연결되어 있을 수 없습니다. 연결된 경우 알림 메시지가 블레이드에 표시됩니다.  이미 연결되어 있다면 다른 Automation 실행 계정을 선택하거나 계정을 만들어야 합니다.

    필요한 정보를 완료한 후에 **만들기**를 클릭합니다.  정보를 확인하고 Automation 계정 및 실행 계정을 만듭니다.  **OMS 작업 영역** 블레이드에 자동으로 돌아갑니다.  

6. **OMS 작업 영역** 블레이드에서 필요한 정보를 제공한 후에 **만들기**를 클릭합니다.  정보가 확인되고 작업 영역이 만들어지는 동안 메뉴의 **알림**에서 진행 상황을 추적할 수 있습니다.  **솔루션 추가** 블레이드가 다시 열립니다.  

7. **Automation 및 컨트롤** 설정 블레이드에서 권장된 미리 선택된 솔루션을 설치할 것인지 확인합니다. 선택을 취소한 경우 나중에 개별적으로 설치할 수 있습니다.  

8. **만들기**를 클릭하여 Automation 및 OMS 작업 영역 등록을 진행합니다. 모든 설정에 대한 유효성을 검사하면 구독 내에 제품을 배포하려고 합니다.  이 프로세스를 완료하려면 몇 초 정도가 소요되며 메뉴의 **알림**에서 진행 상황을 추적할 수 있습니다. 

제품이 등록된 후에는 runbook을 만들고, 사용하도록 설정된 관리 솔루션으로 작업하며, [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md) 역할을 배포할 수 있거나 [Log Analytics](https://docs.microsoft.com/azure/log-analytics)를 통해 클라우드 또는 온-프레미스 환경의 리소스에서 생성한 데이터를 수집할 수 있습니다.   

## <a name="next-steps"></a>다음 단계
* [Azure Automation 실행 계정 인증 테스트](automation-verify-runas-authentication.md)를 검토하여 새 Automation 계정이 Azure 리소스에 대해 인증할 수 있는지 확인할 수 있습니다.
* Runbook을 만들기 시작하려면 먼저 지원되는 [Automation runbook 형식](automation-runbook-types.md) 및 관련 고려 사항을 검토합니다.


