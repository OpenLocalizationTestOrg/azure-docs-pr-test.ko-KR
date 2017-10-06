---
title: "관리 도구 모음 (OMS) 아키텍처 aaaOperations | Microsoft Docs"
description: "OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.  이 문서는 OMS에 포함 하는 hello 다른 서비스를 식별 하 고 링크를 제공 tootheir 콘텐츠를 자세히 설명 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>OMS 아키텍처
[OMS(Operations Management Suite)](https://azure.microsoft.com/documentation/services/operations-management-suite/)는 온-프레미스 및 클라우드 환경을 관리하기 위한 클라우드 기반 서비스의 모음입니다.  이 문서에서는 hello 다른 온-프레미스 및 클라우드 OMS와 해당 고급 아키텍처 구성 요소를 설명 합니다.  자세한 내용은 각 서비스에 대 한 toohello 설명서를 참조할 수 있습니다.

## <a name="log-analytics"></a>Log Analytics
모든 데이터를 수집 [로그 분석](https://azure.microsoft.com/documentation/services/log-analytics/) Azure에서 호스팅되는 hello OMS 리포지토리에 저장 됩니다.  연결 된 원본 hello OMS 리포지토리에 수집 된 데이터를 생성 합니다.  현재는 세 가지 유형의 연결된 원본이 지원됩니다.

* 에 설치 된 에이전트는 [Windows](../log-analytics/log-analytics-windows-agents.md) 또는 [Linux](../log-analytics/log-analytics-linux-agents.md) 컴퓨터 tooOMS 직접 연결 합니다.
* System Center Operations Manager (SCOM) 관리 그룹 [tooLog 분석 연결](../log-analytics/log-analytics-om-agents.md) 합니다.  SCOM 에이전트 toocommunicate 이벤트 및 성능 데이터 분석 tooLog 전달 하는 관리 서버와 계속 합니다.
* Azure의 작업자 역할, 웹 역할 또는 가상 컴퓨터에서 [Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 데이터를 수집하는 [Azure Storage 계정](../log-analytics/log-analytics-azure-storage.md).

로그 분석 이벤트 로그 및 성능 카운터를 포함 하 여 연결 된 원본에서 수집 하는 hello 데이터를 정의 하는 데이터 원본.  솔루션 기능 tooOMS를 추가 하 고 hello에서 쉽게 tooyour 작업 영역을 추가할 수 있습니다 [OMS 솔루션 갤러리](../log-analytics/log-analytics-add-solutions.md)합니다.  일부 솔루션도 있을 수 있습니다 설치 하는 추가 에이전트가 toobe SCOM 에이전트에서 직접 연결 tooLog 분석 필요할 수 있습니다.

로그 분석에는 웹 기반 포털 수 toomanage OMS 리소스를 사용 하 여, 추가 및 구성 OMS 솔루션 및 확인 하 여 hello OMS 리포지토리에 데이터를 분석 합니다.

![Log Analytics의 개략적 아키텍처](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure Automation
[Azure 자동화 runbook](http://azure.microsoft.com/documentation/services/automation) hello Azure 클라우드에에서 실행 되 고 다른 클라우드 서비스에서 Azure 또는에서 액세스할 수 있는 리소스에 액세스할 수 공용 인터넷 hello 합니다.  또한 Runbook이 로컬 리소스에 액세스할 수 있도록 [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md)를 사용하여 로컬 데이터 센터에 온-프레미스 컴퓨터를 지정할 수 있습니다.

[DSC 구성](../automation/automation-dsc-overview.md) Azure 자동화에 저장 된 가상 컴퓨터를 직접 적용 된 tooAzure 될 수 있습니다.  다른 실제 및 가상 컴퓨터는 hello Azure 자동화 DSC 끌어오기 서버에서 구성을 요청할 수 있습니다.

Azure 자동화에 toolaunch hello Azure 포털 모든 작업에 대 한 통계를 표시 하는 OMS 솔루션이 있습니다.

![Azure 자동화의 개략적 아키텍처](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure 백업
[Azure 백업](http://azure.microsoft.com/documentation/services/backup) 의 보호된 데이터는 특정 지리적 지역에 있는 백업 저장소에 저장됩니다.  hello 데이터가 복제 내 동일한 지역 hello 하 고, 자격 증명 모음에 hello 유형에 따라 추가 중복성을 위해 복제 tooanother 영역을 될 수도 있습니다.

Azure Backup에는 세 가지 기본 시나리오가 있습니다.

* Azure 백업 에이전트가 있는 Windows 컴퓨터.  이렇게 하면 모든 Windows 서버 또는 클라이언트에서 toobackup 파일 및 폴더 직접 tooyour Azure 백업 자격 증명 모음입니다.  
* System Center DPM(Data Protection Manager) 또는 Microsoft Azure 백업 서버. 이렇게 하면 있습니다 tooleverage DPM 또는 Microsoft Azure 백업 서버 toobackup 파일과 폴더 뿐만 아니라 SQL 및 SharePoint toolocal 저장 및 복제 후 tooyour Azure 백업 자격 증명 모음 같은 tooapplication 워크 로드 합니다.
* Azure 가상 컴퓨터 확장.  이렇게 하면 Azure 백업 자격 증명 모음 toobackup Azure 가상 컴퓨터 tooyour 있습니다.

Azure 백업에 모든 작업에 대 한 Azure 포털 toolaunch hello 통계를 표시 하는 OMS 솔루션이 있습니다.

![Azure 백업의 개략적 아키텍처](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) 는 가상 컴퓨터 및 물리적 서버의 복제, 장애 조치(failover), 장애 복구(failback)를 처리합니다. Hello 데이터 센터와 Azure 저장소 또는 Hyper-v 호스트, VMware 하이퍼바이저, 및 실제 서버에 기본 및 보조 데이터 센터 간에 복제 데이터가 교환 됩니다.  Site Recovery는 특정 지역의 Azure 지역에 위치한 저장소에 메타데이터를 저장합니다. Hello Site Recovery 서비스에서 저장 되는 복제 된 데이터가 있습니다.

Azure Site Recovery에는 세 가지 기본 복제 시나리오가 있습니다.

**Hyper-V 가상 컴퓨터 복제**

* VMM 클라우드에서 Hyper-v 가상 컴퓨터를 관리 하는 경우 보조 데이터 센터 또는 tooAzure 저장소 tooa 복제할 수 있습니다.  복제 tooAzure 보안 인터넷 연결입니다.  복제 tooa 보조 데이터 센터 hello LAN 끝났습니다.
* Hyper-v 가상 컴퓨터에 VMM에서 관리 되지 않을 경우 tooAzure 저장에만 복제할 수 있습니다.  복제 tooAzure 보안 인터넷 연결입니다.

**VMware 가상 컴퓨터 복제**

* VMware 가상 컴퓨터 tooa 실행 보조 데이터 센터 VMware 또는 tooAzure 저장소를 복제할 수 있습니다.  사이트 간 VPN 이나 Azure express 경로 또는 보안 인터넷 연결을 통해 복제 tooAzure 발생할 수 있습니다. 복제 tooa 보조 데이터 센터 hello InMage Scout 데이터 채널을 통해 발생 합니다.

**물리적 Windows 또는 Linux 서버 복제** 

* 물리적 서버 tooa 보조 데이터 센터 또는 tooAzure 저장소를 복제할 수 있습니다. 사이트 간 VPN 이나 Azure express 경로 또는 보안 인터넷 연결을 통해 복제 tooAzure 발생할 수 있습니다. 복제 tooa 보조 데이터 센터 hello InMage Scout 데이터 채널을 통해 발생 합니다.  Azure 사이트 복구에 몇 가지 통계를 표시 하는 OMS 솔루션이 있지만 임의 작업을 위해 hello Azure 포털을 사용 해야 합니다.

![Azure Site Recovery의 개략적 아키텍처](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>다음 단계
* [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)에 대해 알아보기
* [Azure Automation](https://azure.microsoft.com/documentation/services/automation)에 대해 알아보기
* [Azure Backup](http://azure.microsoft.com/documentation/services/backup)에 대해 알아보기
* [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)에 대해 알아보기

