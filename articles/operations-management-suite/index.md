---
title: "Operations Management Suite (OMS) 설명서-자습서 aaaAzure | Microsoft Docs"
description: "OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. 이 문서는 OMS에 포함 하는 hello 다른 서비스를 식별 하 고 링크를 제공 tootheir 콘텐츠를 자세히 설명 합니다."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>OMS(Operations Management Suite)란?
OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.  OMS는 클라우드 기반 서비스로 구현되므로 인프라 서비스에 대한 최소한의 투자로 빠르게 실행할 수 있습니다.  새로운 기능이 자동으로 제공되므로 지속적 유지 관리 및 업그레이드 비용을 절감할 수 있습니다.

또한 tooproviding 자체적으로 OMS에서 중요 한 서비스에 통합할 수 System Center Operations Manager tooextend 같은 System Center 구성 요소와 되어 기존 관리 투자 hello 클라우드.  System Center 및 OMS 수 협력 전체 하이브리드 관리 환경을 tooprovide 합니다.

hello 다음 섹션에서는 OMS 및 oms가 hello 구현 하는 서비스의 다른 값 영역 hello 자세히 설명 합니다.  각각에 대 한 설명서를 자세히 검토 hello 전에 hello 다양 한 OMS 구성 요소에 대 한 개요 tooOMS 아키텍처를 참조할 수 있습니다.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Insight and Analytics](media/operations-management-suite-overview/icon-insight-analytics.png) Insight and Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)을 통해 운영 체제 및 응용 프로그램에서 생성하는 로그 및 성능 데이터를 수집하고 상관 관계를 분석하고 검색하며 조치를 취할 수 있습니다. 통합된 검색을 사용 하 여 실시간 운영 정보 제공 하 고 사용자 지정 대시보드 tooreadily 모든 작업 및 서버의 물리적 위치에 관계 없이 수백만 개의 레코드를 분석 합니다.

솔루션 tooLog 분석 논리를 hello 및 수집 된 데이터 toobe를 정의 하는 분석을 쉽게 추가할 수 있습니다.  솔루션에는 최소한의 코드만 tooagents 또는 구성 작업 없이 자동으로 전달 되는 추가 기능이 포함 될 수 있습니다.  또한 toousing 분석 도구 제공 개별 솔루션을 통해 시스템 및 응용 프로그램 간의 순서 toocorrelate 데이터의 hello 전체 데이터 집합에서 사용자 지정 검색을 수행할 수 있습니다.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automation and Control](media/operations-management-suite-overview/icon-automation-control.png) Automation and Control
으로 관리 프로세스를 자동화 하는 azure 자동화 [runbook](../automation/automation-runbook-types.md) PowerShell을 기반으로 되 고 Azure 클라우드 hello에서를 실행 합니다.  Runbook은 AWS(Amazon Web Services)와 같은 다른 클라우드의 리소스를 포함하여 PowerShell로 관리할 수 있는 제품 또는 서비스에 액세스할 수 있습니다.  Runbook의 서버 로컬 데이터 센터 toomanage 로컬 리소스에도 실행할 수 있습니다.

Azure Automation은 [PowerShell DSC](../automation/automation-dsc-overview.md)를 사용하여 구성 관리를 제공합니다.  수 및 Azure에서 호스트 되는 DSC 리소스를 관리 하 고 toocloud 및 온-프레미스 시스템 toodefine 적용할 만들고 해당 구성을 자동으로 적용 합니다.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![보호 및 복구](media/operations-management-suite-overview/icon-protection-recovery.png) 보호 및 재해 복구
[Azure Backup](http://azure.microsoft.com/documentation/services/backup)은 자본 투자 없이 최소한의 운영 비용으로 응용 프로그램 데이터를 보호하고 수년 간 보존하며  SQL Server 및 SharePoint와 같은 추가 tooapplication 작업의 실제 및 가상 Windows 서버에서 데이터를 백업할 수 있습니다.  또한 사용할 수 있습니다 System Center Data Protection Manager (DPM) 보호 된 tooreplicate 데이터 tooAzure에서 중복성 및 장기 저장에 대 한 합니다.

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) 복제, 장애 조치 및 온-프레미스 Hyper-v 가상 컴퓨터, VMware 가상 컴퓨터 및 물리적 Windows의 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략 기여 / Linux 서버입니다. 컴퓨터 tooa 보조 데이터 센터 하거나 tooAzure를 복제 하 여 데이터 센터를 확장할 수 있습니다. Site Recovery는 또한 워크로드에 대해 간단한 장애 조치(Failover) 및 복구를 제공합니다. SQL Server AlwaysOn과 같은 재해 복구 메커니즘과 통합되며 여러 컴퓨터에서 계층화되는 워크로드의 간단한 장애 조치(Faiover)에 대한 복구 계획을 제공합니다.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![OMS 보안 및 규정 준수](media/operations-management-suite-overview/icon-security-compliance.png) 보안 및 규정 준수
보안 및 규정 준수 식별, 평가, 및 tooyour 인프라 보안 위험을 완화 하는 데 도움이 됩니다.  OMS의 이러한 기능은 에이전트 시스템 tooassist의 로그 데이터 및 구성을 분석 하는 로그 분석에서 여러 솔루션을 통해 구현 되어 사용자 환경의 hello 지속적인 보안 강화에 있습니다.

* hello [보안 및 감사 솔루션](oms-security-getting-started.md) 수집 하 고 관리 되는 시스템 tooidentify 의심 스러운 활동에 보안 이벤트를 분석 합니다.
* hello [맬웨어 방지 솔루션](../log-analytics/log-analytics-malware.md) hello 관리 시스템에서 맬웨어 방지 보호 상태를 보고 합니다.  
* 시스템 업데이트 솔루션 hello hello 보안 업데이트의 분석을 수행 하 고 시스템을 쉽게 식별할 수 있도록 관리 되는 시스템에서 업데이트 하는 다른 패치가 필요한 합니다.

## <a name="next-steps"></a>다음 단계
* [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)에 대해 알아보기
* [Azure Automation](../automation/automation-intro.md)에 대해 알아보기
* [Azure Backup](http://azure.microsoft.com/documentation/services/backup)에 대해 알아보기
* [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)에 대해 알아보기

