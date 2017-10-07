---
title: "자동화 DSC 개요 aaaAzure | Microsoft Docs"
description: "Azure 자동화 DSC(필요한 상태 구성)의 개요, 용어 및 알려진 문제"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell DSC, 필요한 상태 구성, PowerShell DSC Azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Azure 자동화 DSC 개요

Azure 자동화 DSC는 toowrite 수 있는 Azure 서비스, 관리 및 PowerShell 필요한 상태 구성 (DSC) 컴파일 [구성을](https://msdn.microsoft.com/powershell/dsc/configurations), 가져오기 [DSC 리소스](https://msdn.microsoft.com/powershell/dsc/resources), 할당 hello 클라우드 모두에서 구성 tootarget 노드

## <a name="why-use-azure-automation-dsc"></a>Azure Automation DSC를 사용하는 이유

Azure Automation DSC는 Azure 외부에서 DSC를 사용하는 것보다 몇 가지 장점을 제공합니다.

### <a name="built-in-pull-server"></a>기본 제공 끌어오기 서버

Azure 자동화는 제공 하는 [DSC 끌어오기 서버](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) toohello 원하는 상태를 준수 및 하며 규정 준수에서 다시 보고할 대상 노드에 구성을 자동으로 받을 수 있도록 합니다.
Azure 자동화에서 hello 기본 제공 끌어오기 서버를 hello 필요 tooset 제거 및 사용자의 끌어오기 서버를 유지 관리 합니다.
Azure 자동화에는 가상 또는 실제 Windows 또는 Linux 컴퓨터 hello 클라우드 또는 온-프레미스에 지정할 수 있습니다.

### <a name="management-of-all-your-dsc-artifacts"></a>모든 DSC 아티팩트 관리

Azure 자동화 DSC에 제공 관리 계층을 동일한 너무 hello[PowerShell 필요한 상태 구성](https://msdn.microsoft.com/powershell/dsc/overview) PowerShell 스크립팅을 위해 Azure 자동화에서 제공 하는 대로 합니다.

Hello Azure 포털 또는 PowerShell에서 모든 DSC 구성, 리소스 및 대상 노드를 관리할 수 있습니다.

![Hello Azure 자동화 블레이드의 스크린 샷](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Log Analytics로 보고 데이터 가져오기

Azure 자동화 DSC를 사용 하 여 관리 노드가 자세한 보고 상태 데이터 toohello 기본 제공 된 끌어오기 서버에 보냅니다.
Azure 자동화 DSC toosend이 데이터 tooyour Microsoft Operations Management Suite (OMS) 로그 분석 작업 영역을 구성할 수 있습니다.
상태 데이터 tooyour toosend DSC 로그 분석 작업 영역을 확인 하려면 어떻게 해야 toolearn [데이터 tooOMS 로그 분석 보고 Azure 자동화 DSC 앞으로](automation-dsc-diagnostics.md)합니다.

## <a name="introduction-video"></a>소개 비디오

Tooreading를 감시 하는 것을 선호? 2015 년 5 월, Azure 자동화 DSC에 처음으로 발표에서 비디오를 따라 hello를 살펴본 합니다.

>[!NOTE]
>Hello 개념 및이 비디오에서 설명 하는 수명 주기는 올바른, Azure 자동화 DSC 진행을 너무 많이이 동영상이 녹화 된 이후입니다.
>이제 일반적으로 및 사용할 수, hello Azure 포털에서에서 훨씬 더 광범위 한 UI가 다양 한 추가 기능을 지원 합니다.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>다음 단계

* toolearn tooonboard 노드 toobe Azure 자동화 DSC를 사용 하 여 관리 하는 방법 참조 [Azure 자동화 DSC에 의해 관리에 대 한 온 보 딩 컴퓨터](automation-dsc-onboarding.md)
* Azure 자동화 DSC를 사용 하 여 시작 tooget 참조 [Azure 자동화 DSC 시작](automation-dsc-getting-started.md)
* toolearn tootarget 노드 할당할 수 있도록 DSC 구성을 작성에 대 한 참조 [Azure 자동화 dsc에서 구성 컴파일](automation-dsc-compile.md)
* Azure Automation DSC에 대한 PowerShell cmdlet 참조는 [Azure Automation DSC cmdlet ](/powershell/module/azurerm.automation/#automation)을 참조하세요.
* 가격 책정 정보는 [Azure Automation DSC 가격 책정](https://azure.microsoft.com/pricing/details/automation/)을 참조하세요.
* 연속 배포 파이프라인에서 Azure 자동화 DSC를 사용 하는 예제 toosee 참조 [연속 배포 tooIaaS Chocolatey 및 Vm 사용 하 여 Azure 자동화 DSC](automation-dsc-cd-chocolatey.md)
