---
title: "aaaWhat Azure 자동화는 | Microsoft Docs"
description: "Azure 자동화를 제공 하는 어떤 값 알아보고를 시작할 수 있습니다를 만드는 runbook과 Azure 자동화 DSC를 사용 하 여 답변 toocommon 질문을 확인 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "자동화란, azure 자동화, azure 자동화 예"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Azure 자동화 개요
Microsoft Azure 자동화 방식으로 작업 하기 위한 제공 사용자 tooautomate hello 수동, 장기 실행, 오류가 발생 하기 쉽고 자주 반복 되는 클라우드 및 엔터프라이즈 환경에서 일반적으로 수행 되 합니다. 시간을 절약할 수 및 일반 관리 작업의 hello 안정성이 증가 하 고도 예약으로 toobe 자동으로 정기적으로 수행 합니다. Runbook을 사용하는 프로세스를 자동화하거나 원하는 상태 구성을 사용하여 구성 관리를 자동화할 수 있습니다. 이 문서에서는 Azure 자동화의 간단한 개요 및 일반적인 질문에 대한 답변을 제공합니다. Hello 서로 다른 항목에 대 한 자세한 내용을 보려면이 라이브러리의 문서를 tooother를 참조할 수 있습니다.

## <a name="automating-processes-with-runbooks"></a>Runbook을 사용하여 프로세스 자동화
Runbook은 Azure 자동화에서 일부 자동화 된 프로세스를 수행하는 작업의 집합입니다. 같은 가상 컴퓨터를 시작 하 고 로그 항목을 만드는 간단한 프로세스 중이거나 여러 리소스 또는 여러 클라우드 및 온-프레미스 환경에서 더 작은 다른 runbook tooperform 복잡 한 프로세스를 결합 하는 복잡 한 runbook 수 있습니다.  

예를 들어 toohello 데이터베이스를 연결 하는 연결 toohello 서버와 같은 여러 단계를 포함 하는 최대 크기에 도달 하는 경우 SQL 데이터베이스 자름에 대 한 프로세스, hello 데이터베이스의 현재 크기를 가져오려면, 확인 하는 경우에 기존 설명서를 할 수 있습니다. 임계값을 초과한 잘라 고 사용자에 게 알립니다. 이러한 각 단계를 수동으로 수행하는 대신 단일 프로세스로 이러한 작업을 모두 수행하는 runbook을 만들 수 있습니다. Hello runbook을 시작 하 고, hello SQL server 이름, 데이터베이스 이름 및 받는 사람 전자 메일 같은 hello 필요한 정보를 제공 하 고, hello 프로세스를 완료 하는 동안 다음 sit 게 됩니다. 

## <a name="what-can-runbooks-automate"></a>Runbook 자동화가 할 수 있는것은 무엇입니까?
Azure 자동화의 Runbook은 Windows PowerShell 또는 Windows PowerShell 워크플로를 기반으로 하기 때문에 PowerShell의 모든 기능을 수행할 수 있습니다. API가 있는 응용 프로그램이거나 서비스라면 runbook과 함께 작업할 수 있습니다. Hello 응용 프로그램에 대 한 PowerShell 모듈을 설정한 경우 Azure 자동화로 해당 모듈을 로드할 고 runbook에서 이러한 cmdlet이 포함 수 있습니다. Azure 자동화 runbook Azure 클라우드 hello에서 실행 되 고 모든 클라우드 리소스 또는 hello 클라우드에서 액세스할 수 있는 외부 리소스에 액세스할 수 있습니다. 사용 하 여 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), runbook 센터 toomanage 로컬 리소스 로컬 데이터에서 실행할 수 있습니다. 

## <a name="getting-runbooks-from-hello-community"></a>Hello 커뮤니티에서 runbook 가져오기
hello [Runbook 갤러리](automation-runbook-gallery.md#runbooks-in-runbook-gallery) 사용자 환경에서 변경 되지 않은 상태로 사용 하 여 설정할 수 있는 Microsoft 및 hello 커뮤니티에서 runbook을 포함 하거나 용도 대 한 사용자 지정 합니다. 값은 유용한 tooas 참조 toolearn 어떻게 toocreate 위한 고유한 runbook입니다. 다른 사용자에 게 유용할 수 생각 runbook toohello 갤러리를 직접 참가할 수 있습니다. 

## <a name="creating-runbooks-with-azure-automation"></a>Azure 자동화를 사용하여 Runbook 만들기
할 수 있습니다 [위한 고유한 runbook을 만들](automation-creating-importing-runbook.md) 에서 hello에서 runbook을 수정 하거나 스크래치 [Runbook 갤러리](http://msdn.microsoft.com/library/azure/dn781422.aspx) 고유한 요구 사항에 대 한 합니다. 요구 사항 및 PowerShell 환경에 따라 선택할 수 있는 네 가지 [Runbook 형식](automation-runbook-types.md)이 있습니다. Hello PowerShell 코드를 사용 하 여 직접 toowork를 원하는 경우 사용할 수 있습니다는 [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) 또는 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks) 오프 라인 상태 이거나 hello로 편집 하는 [텍스트편집기](http://msdn.microsoft.com/library/azure/dn879137.aspx) hello Azure 포털의에서. Tooedit 선호 하는 경우는 없지만 runbook toohello 기본 코드를 노출 한 다음 만들 수 있습니다는 [그래픽 runbook](automation-runbook-types.md#graphical-runbooks) hello를 사용 하 여 [그래픽 편집기](automation-graphical-authoring-intro.md) hello Azure 포털의에서. 

Tooreading를 감시 하는 것을 선호? Microsoft Ignite 2015 년 5 월에에서는 세션에서 비디오 아래 hello를 살펴본 합니다. 참고: hello 개념 및이 비디오에서 설명 하는 기능은 Azure 자동화 진행을 너무 많이이 동영상이 녹화 된 후 올바른, 이제 UI가 있는 더욱 광범위 한 hello Azure 포털 및 추가 기능을 지원 합니다.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>원하는 상태 구성을 사용하여 구성 관리 자동화
[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) toomanage, 수 있는 관리 플랫폼은 배포 및 물리적 호스트 및 선언적 PowerShell 구문을 사용 하 여 가상 컴퓨터에 대 한 구성을 적용 합니다. 대상 컴퓨터가 자동으로 검색하고 적용하는 중앙 DSC 끌어오기 서버에서 구성을 정의할 수 있습니다. DSC는 toomanage 구성 및 리소스를 사용할 수 있는 PowerShell cmdlet 집합을 제공 합니다.  

[Azure 자동화 DSC](automation-dsc-overview.md) 는 엔터프라이즈 환경에 필요한 서비스를 제공하는 PowerShell DSC에 대한 클라우드 기반 솔루션입니다.  Azure 자동화에서 DSC 리소스를 관리할 수 있으며 구성 toovirtual 또는 Azure 클라우드 hello에 DSC 끌어오기 서버에서이 검색 하는 물리적 컴퓨터를 적용할 수 있습니다.  또한 노드가 할당된 구성에서 파생되는 시기 및 새 구성이 적용되는 시기와 같은 중요한 이벤트를 알려주는 보고 서비스를 제공합니다. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Azure 자동화를 사용하여 고유한 DSC 구성 만들기
[DSC 구성](automation-dsc-overview.md) 노드의 hello 원하는 상태를 지정 합니다.  여러 노드에 적용할 수는 동일한 상태를 유지 모두 동일한 구성 tooassure hello 합니다.  로컬 컴퓨터에서 텍스트 편집기를 사용하여 구성을 만들고 컴파일하고 노드에 적용할 수 있는 Azure 자동화에 가져올 수 있습니다.

## <a name="getting-modules-and-configurations"></a>모듈 및 구성 가져오기
가져올 수 있습니다 [PowerShell 모듈](automation-runbook-gallery.md#modules-in-powershell-gallery) cmdlet에서 runbook 및 hello에서 DSC 구성을 사용할 수 있는 포함 된 [PowerShell 갤러리](http://www.powershellgallery.com/)합니다. Hello Azure 포털에서에서이 갤러리를 시작 하 고 Azure 자동화로 직접 모듈을 가져올 수 또는 다운로드 하 고 수동으로 가져올 수 있습니다. Hello Azure 포털에서 직접 hello 모듈을 설치할 수 없지만 다운로드할 수 있는 다른 모듈와 마찬가지로 설치 합니다. 

## <a name="example-practical-applications-of-azure-automation"></a>Azure 자동화의 실제 응용 프로그램 예제
다음은 무엇 인가요 hello 종류의 Azure 자동화에 대 한 자동화 시나리오는 몇 가지 예입니다. 

* 여러 Azure 구독에 가상 컴퓨터를 만들고 복사합니다. 
* 로컬 컴퓨터 tooan Azure Blob 저장소 컨테이너에서 파일을 복사합니다. 
* 서비스 공격이 거부된 것이 감지되면 클라이언트에서 요청 거부와 같은 보안 기능을 자동화합니다. 
* 구성된 보안 정책을 사용하여 지속적으로 컴퓨터를 정렬하도록 합니다.
* 클라우드 간 및 온-프레미스 인프라에 응용 프로그램 코드의 지속적인 배포를 관리합니다. 
* 랩 환경에 Azure의 Active Directory 포리스트를 빌드합니다. 
* DB가 최대 크기에 도달하면 SQL 데이터베이스의 테이블을 자릅니다. 
* Azure 웹 사이트의 환경 설정을 원격으로 업데이트합니다. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Azure 자동화 tooother 자동화 도구를 연결 하는 방법
[서비스 관리 자동화 (SMA)](http://technet.microsoft.com/library/dn469260.aspx) 는 의도 한 tooautomate hello 사설 클라우드에서 관리 작업입니다. [Microsoft Azure 팩](https://www.microsoft.com/en-us/server-cloud/)의 구성요소로 데이터 센터에 로컬로 설치됩니다. SMA과 Azure 자동화 hello를 사용 하 여 Windows PowerShell 및 Windows PowerShell 워크플로 기반으로 동일한 runbook 형식을 SMA에서 지원 되지 않는 [그래픽 runbook](automation-graphical-authoring-intro.md)합니다.  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) 는 온-프레미스 리소스의 자동화에 사용됩니다. Azure 자동화 및 서비스 관리 자동화 보다 다른 runbook 형식을 사용 하 고는 스크립팅을 수행 하지 않고 그래픽 인터페이스 toocreate runbook을 포함 합니다. 해당 runbook은 Ochestrator에 대해 구체적으로 적힌 통합 팩의 활동들로 구성됩니다. 

## <a name="where-can-i-get-more-information"></a>자세한 정보는 어디서 얻을 수 있습니까?
다양 한 리소스는 있습니다 toolearn Azure 자동화와 runbook을 직접 만드는 방법에 대 한 자세한에 사용할 수 있습니다. 

* **Azure 자동화 라이브러리** 입니다. 이 라이브러리의 hello 문서에 hello 구성 및 관리를 위한 고유한 runbook을 제작 하 고 Azure 자동화의 전체 설명서를 제공 합니다. 
* [Azure PowerShell cmdlet](http://msdn.microsoft.com/library/jj156055.aspx) 은 Windows PowerShell을 사용하여 Azure 작업을 자동화하는 방법에 대한 정보를 제공합니다. 이러한 cmdlet toowork를 사용 하 여 Azure 리소스와 Runbook입니다. 
* [관리 블로그](https://azure.microsoft.com/blog/tag/azure-automation/) microsoft에서 Azure 자동화 및 기타 관리 기술에 hello 최신 정보를 제공 합니다. Hello Azure 자동화 팀의 최신 hello로 toodate toothis 블로그 toostay를 가입 해야 합니다. 
* [자동화 포럼](http://go.microsoft.com/fwlink/p/?LinkId=390561) Microsoft 및 커뮤니티 자동화 hello로 주소를 지정 하는 Azure 자동화 toobe toopost 질문이 있습니다. 
* [Azure 자동화 cmdlet](https://msdn.microsoft.com/library/mt244122.aspx) 은 관리 작업을 자동화하는 방법에 대한 정보를 제공합니다. Cmdlet toomanage 자동화 계정, 자산, runbook, DSC 포함합니다.

## <a name="can-i-provide-feedback"></a>피드백을 제공할 수 있습니까?
**사용자 의견을 보내 주세요!** Azure 자동화 Runbook 솔루션 또는 통합 모듈을 찾고 있는 경우 스크립트 센터에 스크립트 요청을 게시하세요. Azure 자동화에 대한 의견이나 기능 요청이 있는 경우 [사용자 음성](http://feedback.windowsazure.com/forums/34192--general-feedback)에 게시하세요. 감사합니다. 

