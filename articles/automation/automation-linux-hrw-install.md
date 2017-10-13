---
title: Azure Automation Linux Hybrid Runbook Worker | Microsoft Docs
description: "이 문서에서는 로컬 데이터 센터 또는 클라우드 환경의 Linux 기반 컴퓨터에서 Runbook을 실행할 수 있도록 해주는 Azure Automation Hybrid Runbook Worker를 설치하는 방법에 대한 정보를 제공합니다."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/07/2017
ms.author: magoedte
ms.openlocfilehash: 88c052c3a22611b796559d4dd62c763445aa6210
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-deploy-a-linux-hybrid-runbook-worker"></a>Linux Hybrid Runbook Worker를 배포하는 방법
Azure Automation의 Runbook은 Azure 클라우드에서 실행되므로 다른 클라우드 또는 온-프레미스 환경의 리소스에 액세스할 수 없습니다.  Azure Automation의 Hybrid Runbook Worker 기능을 사용하면 컴퓨터에 대해 직접 그리고 외부에서 환경의 리소스에 대해 Runbook을 실행하여 로컬 리소스를 관리할 수 있습니다. Runbook은 Azure Automation에 저장 및 관리된 후 하나 이상의 지정된 컴퓨터에 전달됩니다.  

이 기능은 다음 이미지에 나와 있습니다.<br>  

![Hybrid Runbook Worker 개요](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Hybrid Runbook Worker 역할의 기술적 개요는 [Automation 아키텍처 개요](automation-offering-get-started.md#automation-architecture-overview)를 참조하세요. Hybrid Runbook Worker 배포를 시작하기 전에 [하드웨어 및 소프트웨어 요구 사항](automation-offering-get-started.md#hybrid-runbook-worker) 및 [네트워크 준비를 위한 정보](automation-offering-get-started.md#network-planning)에 대한 다음 정보를 검토합니다.  Runbook Worker를 성공적으로 배포한 후에는 [Hybrid Runbook Worker에서 Runbook 실행](automation-hrw-run-runbooks.md)을 검토하여 온-프레미스 데이터 센터 또는 다른 클라우드 환경의 프로세스를 자동화하도록 Runbook을 구성하는 방법을 알아봅니다.     

## <a name="hybrid-runbook-worker-groups"></a>Hybrid Runbook Worker 그룹
각 Hybrid Runbook Worker는 에이전트를 설치할 때 지정한 Hybrid Runbook Worker 그룹의 구성원입니다.  그룹은 단일 에이전트를 포함할 수 있지만 고가용성을 위해 그룹에 여러 에이전트를 설치할 수 있습니다.

Hybrid Runbook Worker에서 Runbook을 시작할 경우 이를 실행할 그룹을 지정합니다.  그룹의 구성원에 따라 요청을 처리할 작업자가 결정됩니다.  특정 작업자를 지정할 수 없습니다.

## <a name="installing-linux-hybrid-runbook-worker"></a>Linux Hybrid Runbook Worker 설치
Linux 컴퓨터에서 Hybrid Runbook Worker를 설치 및 구성하려는 경우 매우 간단한 프로세스에 따라 역할을 수동으로 설치하고 구성하면 됩니다.   OMS 작업 공간에서 **Automation Hybrid Worker** 솔루션을 활성화한 다음 일련의 명령을 실행하여 컴퓨터를 작업자로 등록하고 새 또는 기존 그룹에 추가해야 합니다. 

계속 진행하기 전에 자동화 계정이 연결되어 있는 Log Analytics 작업 영역을 확인해야 하며 자동화 계정의 기본 키도 확인해야 합니다.  작업 영역과 기본 키는 모두 Portal에서 찾을 수 있습니다. 자동화 계정을 선택하고 **작업 영역**을 선택하면 작업 영역 ID를, **키**를 선택하면 기본 키를 확인할 수 있습니다.  

1.  OMS에서 “Automation Hybrid Worker”를 활성화합니다. 이렇게 하려면 다음 방법 중 하나를 사용합니다.

   1. [OMS 포털](https://mms.microsoft.com)의 솔루션 갤러리에서 **Automation Hybrid Worker** 솔루션 활성화
   2. 다음 cmdlet을 실행합니다.

        ```powershell
         $null = Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName  <ResourceGroupName> -WorkspaceName <WorkspaceName> -IntelligencePackName  "AzureAutomation" -Enabled $true
        ```

2.  Linux 컴퓨터에서 *-w* 및 *-k* 매개 변수의 값을 변경하여 다음 명령을 실행합니다.
    
    ```
    sudo python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/scripts/onboarding.py --register -w <OMSworkspaceId> -k <AutomationSharedKey> --groupname <hybridgroupname> -e <automationendpoint>
    ```
3. 명령이 완료되면 Azure Portal의 Hybrid Worker 그룹 블레이드에 새 그룹 및 멤버 수가 표시되고, 기존 그룹이 있으면 해당 멤버 수가 증가됩니다.  **Hybrid Worker 그룹** 블레이드의 목록에서 그룹을 선택하고 **Hybrid Worker** 타일을 선택합니다.  **Hybrid Worker** 블레이드에서 나열된 그룹의 각 멤버를 확인합니다.  

## <a name="next-steps"></a>다음 단계

* [Hybrid Runbook Worker에서 Runbook 실행](automation-hrw-run-runbooks.md)을 검토하여 온-프레미스 데이터 센터 또는 다른 클라우드 환경의 프로세스를 자동화하도록 Runbook을 구성하는 방법을 알아봅니다.
* Hybrid Runbook Worker를 제거하는 방법의 지침은 [Azure Automation Hybrid Runbook Worker 제거](automation-remove-hrw.md)를 참조하세요.