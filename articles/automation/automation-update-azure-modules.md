---
title: "aaaUpdate Azure의 Azure 자동화 모듈 | Microsoft Docs"
description: "이 문서에서는 Azure Automation에 기본적으로 제공되는 일반 Azure PowerShell 모듈을 즉시 업데이트하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>어떻게 Azure 자동화에서 tooupdate Azure PowerShell 모듈

hello 가장 일반적인 Azure PowerShell 모듈에서 각 자동화 계정은 기본적으로 제공 됩니다.  Azure 모듈 hello 자동화 계정에서에서 우리는 방법을 제공 tooupdate hello 모듈 hello 계정에 새 버전 hello 포털에서 사용할 수 없는 경우 하므로 정기적으로 hello hello Azure 팀 업데이트 합니다.  

모듈은 hello 제품 그룹에 의해 정기적으로 업데이트 하기 때문에 변경 내용을 변경 매개 변수 이름 바꾸기 또는 cmdlet을 완전히 사용 되지 않도록 지정 하는 등의 hello 형식에 따라 runbook에 부정적인 영향을 줄 수를 포함 하는 hello cmdlet과 함께 발생할 수 있습니다. runbook과 hello에 영향을 주지 tooavoid 자동화 프로세스, 테스트 하 고 계속 하기 전에 유효성을 검사 하는 좋습니다.  이 목적을 위한 전용된 자동화 계정이 없는 경우 hello hello를 업데이트 하는 등 추가 tooiterative 변경 내용에서 runbook 개발 하는 동안 다양 한 시나리오 및 순열을 테스트할 수 있도록 하나를 만들어 보십시오 PowerShell 모듈입니다.  Hello 결과 유효성을 검사 하 고 필요한 변경 내용을 적용 한 후 필요한 수정 하는 모든 runbook의 hello 마이그레이션 조정 계속 되 고 프로덕션 환경에서 아래 설명 된 대로 hello 업데이트를 수행 합니다.     

## <a name="updating-azure-modules"></a>Azure 모듈 업데이트

1. Hello 모듈의 자동화 계정 블레이드는 이라는 옵션이 **업데이트 Azure 모듈**합니다.  이 옵션은 항상 사용됩니다.<br><br> ![모듈 블레이드의 Azure 모듈 업데이트 옵션](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. 클릭 **업데이트 Azure 모듈** toocontinue 원하면 묻는 알림이 표시 됩니다.<br><br> ![Azure 모듈 업데이트 알림](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. 클릭 **예** hello 모듈 업데이트 프로세스가 시작 됩니다.  다음 모듈 15 20 분 tooupdate hello에 대 한 hello 업데이트 프로세스를 수행 합니다.

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Hello 모듈 toodate 위로 이므로 hello 프로세스는 몇 초 안에 완료 됩니다.  Hello 업데이트 프로세스가 완료 되 면 알려 줍니다.<br><br> ![Azure 모듈 업데이트 상태 업데이트](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Azure 자동화 새 예약 된 작업이 실행 될 때 자동화 계정에서 hello 최신 모듈을 사용 합니다.    

Cmdlet을 사용 하는 경우 프로그램 runbook toomanage Azure에서에서 이러한 Azure PowerShell 모듈에서 다음 리소스를 됩니다 tooperform이 업데이트 프로세스 매월 하거나 지금 적용 해야 tooassure hello 최신 모듈.

## <a name="next-steps"></a>다음 단계

* 통합 모듈 및 사용자 지정 모듈 toofurther toocreate 다른 시스템, 서비스 또는 솔루션을 자동화에 통합 하는 방법을 자세히 toolearn 참조 [통합 모듈](automation-integration-modules.md)합니다.

* 사용 하 여 소스 제어 통합 하는 것이 좋습니다. [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) 또는 [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally 관리 및 자동화 runbook 및 구성 포트폴리오 릴리스의 제어 합니다.  
