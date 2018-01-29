---
title: "Azure Automation Hybrid Runbook Worker 제거 | Microsoft Docs"
description: "이 문서에서는 로컬 데이터 센터 또는 클라우드 환경의 컴퓨터에서 Runbook을 실행할 수 있도록 해주는 배포된 Azure Automation Hybrid Runbook Worker를 관리하는 방법에 대한 정보를 제공합니다."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: a897a97b9a1e259f5994a27b974eb5183fd1194b
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="remove-azure-automation-hybrid-runbook-workers"></a>Azure Automation Hybrid Runbook Worker 제거

이 문서의 설명에 따라 Azure Automation Hybrid Runbook Worker를 제거할 수 있습니다. 

## <a name="removing-hybrid-runbook-worker"></a>Hybrid Runbook Worker 제거

그룹에서 하나 이상의 Hybrid Runbook Worker를 제거하거나 요구 사항에 따라 그룹을 제거할 수 있습니다.  온-프레미스 컴퓨터에서 Hybrid Runbook Worker를 제거하려면 다음 단계를 수행합니다.

1. Azure Portal에서 Automation 계정으로 이동합니다.  
2. **설정** 블레이드에서 **키**를 선택하고 **URL** 및 **기본 액세스 키** 필드의 값을 확인합니다.  이 정보는 다음 단계에서 필요합니다.
3. 관리자 모드에서 PowerShell 세션을 열고 `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>` 명령을 실행합니다.  제거 과정에 대한 자세한 로그를 보려면 **-Verbose** 스위치를 사용합니다.

> [!NOTE]
> 컴퓨터의 Microsoft Monitoring Agent가 아닌 Hybrid Runbook Worker 역할의 기능 및 구성만을 제거합니다.  

## <a name="remove-hybrid-worker-groups"></a>Hybrid Worker 그룹 제거

그룹을 제거하려면 먼저 앞서 보았던 절차를 사용하여 그룹의 구성원인 모든 컴퓨터에서 Hybrid Runbook Worker를 제거한 후 다음 단계를 수행하여 그룹을 제거해야 합니다.  

1. Azure portal에서 Automation 계정을 엽니다.
1. **Hybrid Worker 그룹** 타일을 선택하고 **Hybrid Worker 그룹** 블레이드에서 삭제하려는 그룹을 선택합니다.  특정 그룹을 선택한 후 **Hybrid Worker 그룹** 속성 블레이드가 표시됩니다.<br> ![Hybrid Runbook Worker 그룹 블레이드](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
1. 선택한 그룹에 대한 속성 블레이드에서 **삭제**를 클릭합니다.  이 작업을 확인하라는 메시지가 표시되고 계속하려면 **예**를 선택합니다.<br> ![그룹 삭제 확인 대화 상자](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> 이 프로세스를 완료하려면 몇 초 정도가 소요되며 메뉴의 **알림**에서 진행 상황을 추적할 수 있습니다. 

## <a name="next-steps"></a>다음 단계

* [Hybrid Runbook Worker에서 Runbook 실행](automation-hrw-run-runbooks.md)을 검토하여 온-프레미스 데이터 센터 또는 다른 클라우드 환경의 프로세스를 자동화하도록 Runbook을 구성하는 방법을 알아봅니다.
* Windows Hybrid Runbook Worker를 설치하는 방법에 대한 자세한 내용은 [Azure Automation Windows Hybrid Runbook Worker](automation-windows-hrw-install.md)를 참조하세요.
* Linux Hybrid Runbook Worker를 설치하는 방법에 대한 자세한 내용은 [Azure Automation Linux Hybrid Runbook Worker](automation-linux-hrw-install.md)를 참조하세요.