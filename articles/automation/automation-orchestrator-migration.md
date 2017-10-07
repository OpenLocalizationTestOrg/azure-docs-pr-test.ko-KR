---
title: "Orchestrator tooAzure 자동화에서에서 aaaMigrating | Microsoft Docs"
description: "System Center Orchestrator tooAzure 자동화에서에서 toomigrate runbook 및 통합 팩 하는 방법을 설명 합니다."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Orchestrator tooAzure 자동화 (베타)에서 마이그레이션
[System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) 의 Runbook은 특별히 Orchestrator용으로 작성된 통합 팩의 활동을 기반으로 하는 반면, Azure Automation의 Runbook은 Windows PowerShell을 기반으로 합니다.  [그래픽 runbook](automation-runbook-types.md#graphical-runbooks) Azure 자동화에서와 비슷한 모양 tooOrchestrator runbook PowerShell cmdlet, 자식 runbook과 자산을 나타내는 해당 활동에 있어야 합니다.

hello [System Center Orchestrator 마이그레이션 도구 키트](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) 도구 tooassist 포함에서 Orchestrator tooAzure 자동화에서에서 runbook을 변환 합니다.  또한 자체 tooconverting hello runbook hello 통합 팩 hello runbook toointegration 모듈을 사용 하 여 Windows PowerShell cmdlet과 hello 활동을 변환할 수 있습니다.  

다음은 Orchestrator runbook tooAzure 자동화 변환 하기 위한 기본 프로세스 hello입니다.  이러한 각 단계는 hello 섹션 아래에서 자세히 설명 되어 있습니다.

1. Hello 다운로드 [System Center Orchestrator 마이그레이션 도구 키트](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) hello 도구와이 문서에서 설명 하는 모듈을 포함 하 합니다.
2. [Standard Activities Module](#standard-activities-module) 을 Azure Automation에 가져옵니다.  여기에는 변환된 Runbook에서 사용할 수 있는 변환된 버전의 표준 Orchestrator 활동이 들어 있습니다.
3. System Center에 액세스하는 Runbook에서 사용하는 통합 팩을 위해 [System Center Orchestrator Integration Modules](#system-center-orchestrator-integration-modules) 를 Azure Automation에 가져옵니다.
4. Hello를 사용 하 여 사용자 지정 및 제 3 자 통합 팩을 변환 [통합 팩 변환기](#integration-pack-converter) Azure 자동화로 가져옵니다.
5. Orchestrator runbook hello를 사용 하 여 변환 [Runbook 변환기](#runbook-converter) 하 고 Azure 자동화에서 설치 합니다.
6. 수동으로 hello Runbook 변환기 이러한 리소스를 변환 하지 않습니다 이후 Azure 자동화에서 필요한 조정자 자산을 만듭니다.
7. 구성 된 [Hybrid Runbook Worker](#hybrid-runbook-worker) 로컬 리소스에 액세스 하는 로컬 데이터 센터 변환 toorun runbook의 합니다.

## <a name="service-management-automation"></a>Service Management Automation
[서비스 관리 자동화](http://technet.microsoft.com/library/dn469260.aspx) SMA ()를 저장 하 고, Orchestrator와 같은 로컬 데이터 센터에서 runbook을 실행 하 고 hello를 사용 하 여 Azure 자동화로 동일한 통합 모듈입니다. hello [Runbook 변환기](#runbook-converter) Orchestrator runbook toographical runbook을 통해 변환 하 여 SMA에 지원 되지 않습니다.  Hello를 설치할 수 있습니다 [기본 활동 모듈](#standard-activities-module) 및 [System Center Orchestrator 통합 모듈](#system-center-orchestrator-integration-modules) , SMA로 수동으로 실행 해야 하지만 [runbook을 다시 작성](http://technet.microsoft.com/library/dn469262.aspx)합니다.

## <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker
Orchestrator의 Runbook은 데이터베이스 서버에 저장되고 Runbook 서버에서 실행됩니다(두 서버 모두 로컬 데이터 센터에 있음).  Azure 자동화의 Runbook은 Azure 클라우드 hello에 저장 되며 사용 하 여 로컬 데이터 센터에서 실행할 수는 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)합니다.  로컬 서버에서 설계 된 toorun 되므로 변환 Orchestrator에서 runbook 일반적으로 실행 되는 방식을입니다.

## <a name="integration-pack-converter"></a>Integration Pack Converter
통합 팩 변환기 hello hello를 사용 하 여 만든 통합 팩을 변환 [Orchestrator Integration Toolkit OIT ()](http://technet.microsoft.com/library/hh855853.aspx) Azure 자동화로 가져올 수 있는 Windows PowerShell을 기반으로 toointegration 모듈 또는 서비스 관리 자동화 합니다.  

Hello 통합 팩 변환기를 실행 하면 tooselect 통합 팩 (.oip) 파일을 사용할 수 있는 마법사와 함께 표시 됩니다.  hello 마법사 다음 해당 통합 팩에 포함 하는 hello 활동을 나열 하 고 tooselect 마이그레이션되고 있는 있습니다.  Hello 마법사를 완료 하면 용 hello hello 원래 통합 팩에는 활동의 각 해당 cmdlet이 포함 된 통합 모듈을 만듭니다.

### <a name="parameters"></a>매개 변수
Hello 통합 팩에는 활동의 모든 속성은 변환 된 tooparameters hello hello 통합 모듈에서 해당 cmdlet의 합니다.  Windows PowerShell cmdlet에는 모든 cmdlet에서 사용할 수 있는 [일반 매개 변수](http://technet.microsoft.com/library/hh847884.aspx) 집합이 있습니다.  예를 들어 hello-Verbose 매개 변수 사용 하면 cmdlet toooutput 해당 작업에 대 한 정보를 자세히 설명 합니다.  없음 cmdlet hello로 일반 매개 변수 이름과 같은 이름을 가진 매개 변수가 있을 수 있습니다.  활동 일반 매개 변수 이름이 hello 사용 하 여 속성을가지고 않으면 hello 매개 변수에 다른 이름을 hello 마법사 tooprovide 하면 표시 됩니다.

### <a name="monitor-activities"></a>모니터링 활동
로 시작 Orchestrator에서에서 runbook을 모니터링 한 [활동 모니터링](http://technet.microsoft.com/library/hh403827.aspx) 및 특정 이벤트에 의해 호출 되는 대기 중인 toobe 지속적으로 실행 합니다.  Azure 자동화 hello 통합 팩의 모든 모니터 활동이 변환 되지 않습니다 하므로 모니터 runbook을 지원 하지 않습니다.  대신, 자리 표시자 cmdlet 작업을 모니터링 하는 hello에 대 한 hello 통합 모듈에 만들어집니다.  이 cmdlet에는 기능이 없습니다 있지만 사용 하는 변환 된 모든 runbook toobe 설치 되어 있습니다.  이 runbook은 Azure 자동화에서 수 toorun 않지만 수정할 수 있도록 설치할 수 있습니다.

### <a name="integration-packs-that-cannot-be-converted"></a>변환할 수 없는 통합 팩
OIT 만들어지지 않은 통합 팩 hello 통합 팩 변환기로 변환할 수 없습니다. 또한 이 도구로 현재 변환할 수 없는 Microsoft에서 제공한 통합 팩이 있습니다.  이러한 변환된 버전의 통합 팩은 [다운로드를 위해 제공](#system-center-orchestrator-integration-modules) 되므로 Azure Automation 또는 Service Management Automation에 설치할 수 있습니다.

## <a name="standard-activities-module"></a>Standard Activities Module
Orchestrator에는 통합 팩에 없지만 많은 Runbook에서 사용하는 [표준 활동](http://technet.microsoft.com/library/hh403832.aspx) 집합이 들어 있습니다.  hello 표준 작업 모듈은 이러한 각 작업에 대 한 해당 cmdlet을 포함 된 통합 모듈입니다.  표준 활동을 사용하는 변환된 Runbook을 가져오기 전에 이 통합 모듈을 Azure Automation에 설치해야 합니다.

또한 toosupporting 변환 runbook, hello 표준 작업 모듈의 cmdlet hello Orchestrator toobuild Azure 자동화에서 새 runbook에 익숙한 사용자가 사용할 수 있습니다.  Hello 표준 작업의 모든 기능이 hello cmdlet으로 수행할 수, 하는 동안 다르게 작동할 수 있습니다.  hello cmdlet 변환 hello 표준 작업 모듈은 작동에 hello 동일 대로 해당 활동 및 사용 하 여 hello 동일한 매개 변수입니다.  이 해당 전환 tooAzure 자동화 runbook의에서 hello 기존 Orchestrator runbook 작성자를 수 있습니다.

## <a name="system-center-orchestrator-integration-modules"></a>System Center Orchestrator Integration Modules
Microsoft 제공 [통합 팩](http://technet.microsoft.com/library/hh295851.aspx) runbook tooautomate System Center 구성 요소 및 기타 제품을 구축 하기 위한 합니다.  이러한 통합 팩의 일부 현재 OIT 기반으로 하지만 알려진된 문제 때문에 변환 된 toointegration 모듈 현재 될 수 없습니다.  [System Center Orchestrator Integration Modules](https://www.microsoft.com/download/details.aspx?id=49555) 에는 Azure Automation 및 Service Management Automation으로 가져올 수 있는 변환된 버전의 통합 팩이 포함되어 있습니다.  

이 도구의 hello RTM 버전으로 통합 팩 변환기 게시 될 hello로 변환 될 수 있는 OIT 기반 hello 통합 팩의 버전 업데이트.  가이드는 OIT에 따라 runbook 활동 hello 통합 팩을 사용 하지 않으면 변환에서 tooassist도 제공 됩니다.

## <a name="runbook-converter"></a>Runbook Converter
hello Runbook 변환기에서 변환 Orchestrator runbook을 [그래픽 runbook](automation-runbook-types.md#graphical-runbooks) Azure 자동화로 가져올 수 있습니다.  

Runbook 변환기가 호출 하는 cmdlet과 PowerShell 모듈로 서 구현 **ConvertFrom SCORunbook** hello 변환을 수행 하는 합니다.  Hello 도구를 설치할 때 hello cmdlet을 로드 하는 바로 가기 tooa PowerShell 세션을 만들어집니다.   

다음은 hello 것이 기본적인 프로세스 tooconvert Orchestrator runbook을 Azure 자동화로 가져올 합니다.  hello 다음 섹션에서는 추가 정보를 제공을 hello 도구를 사용 하 고 변환 된 runbook을 사용 합니다.

1. Orchestrator에서 하나 이상의 runbook을 내보냅니다.
2. Hello runbook의 모든 활동에 대 한 통합 모듈을 가져옵니다.
3. Hello 내보낸된 파일에 hello Orchestrator runbook으로 변환 합니다.
4. 필요한 수동 작업 로그 toovalidate hello 변환과 toodetermine의 정보를 검토 합니다.
5. 변환된 runbook을 Azure Automation으로 가져옵니다.
6. Azure Automation에 필요한 자산을 만듭니다.
7. Hello runbook toomodify Azure 자동화에에서 필요한 모든 활동을 편집 합니다.

### <a name="using-runbook-converter"></a>Runbook Converter 사용
구문에 대 한 hello **ConvertFrom SCORunbook** 는 다음과 같습니다.

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath-toohello 내보내기 경로 포함 된 hello runbook tooconvert를 파일입니다.
* 모듈-쉼표로 구분한 목록 hello runbook에 활동을 포함 하는 통합 모듈입니다.
* OutputFolder-경로 toohello 폴더 toocreate 그래픽 runbook을 변환 합니다.

다음 예에서는 명령을 변환 hello 라는 내보내기 파일에는 runbook hello **MyRunbooks.ois_export**합니다.  이러한 runbook hello Active Directory 및 Data Protection Manager 통합 팩을 사용합니다.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>로그 파일
hello Runbook 변환기 hello 다음 hello에 로그 파일이 만들어집니다. hello와 동일한 위치 runbook을 변환 합니다.  Hello 파일이 이미 존재 하는 경우 hello 마지막 변환 작업의 정보로 덮어씁니다 됩니다.

| 파일 | 목차 |
|:--- |:--- |
| Runbook Converter - Progress.log |성공적으로 변환 된 각 활동에 대 한 정보 및 변환 되지 않고 각 활동에 대 한 경고를 포함 하 여 hello 변환의 자세한 단계입니다. |
| Runbook Converter - Summary.log |Hello 요약 마지막 모든 경고를 포함 하 여 변환 하 고 변환 하는 hello runbook에 필요한 변수를 만들 때 처럼 tooperform 해야 하는 작업을 따릅니다. |

### <a name="exporting-runbooks-from-orchestrator"></a>Orchestrator에서 runbooks 내보내기
hello Runbook 변환기에서 Orchestrator runbook을 하나 이상 포함 하는 내보내기 파일에서 작동 합니다.  각 Orchestrator runbook에 대 한 해당 Azure 자동화 runbook을 hello 내보내기 파일에 만들어집니다.  

Orchestrator에서 runbook이 tooexport hello runbook에 Runbook Designer의 hello 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **내보내기**합니다.  tooexport hello 이름 hello 폴더를 선택 하는 폴더에서 모든 runbook을 마우스 오른쪽 단추로 클릭 **내보내기**합니다.

### <a name="runbook-activities"></a>Runbook 활동
hello Runbook 변환기 hello Orchestrator runbook tooa Azure 자동화의 해당 활동의에서 각 활동으로 변환합니다.  변환할 수 없는 이러한 작업에 대 한 자리 표시자 활동 경고 텍스트를 사용 하 여 hello runbook에 만들어집니다.  Azure 자동화로 변환 하는 hello runbook을 가져온 후 hello 필요한 기능을 수행 하는 유효한 작업으로 이러한 활동 중 하나를 대체 해야 있습니다.

Hello의 모든 Orchestrator 활동이 [기본 활동 모듈](#standard-activities-module) 변환 됩니다.  이 모듈에 없지만 변환되지 않는 일부 표준 Orchestrator 작업이 있습니다.  예를 들어 **플랫폼 이벤트 보내기** hello 이벤트는 특정 tooOrchestrator 있으므로 해당 키 없음 Azure 자동화를 갖습니다.

[작업 모니터링](https://technet.microsoft.com/library/hh403827.aspx) Azure 자동화에서 없는 해당 toothem 없기 때문에 변환 되지 않습니다.  hello 예외를 모니터에서 활동 [통합 팩을 변환](#integration-pack-converter) 변환된 toohello 자리 표시자 활동 사용 됩니다.

모든 활동을 한 [통합 팩을 변환](#integration-pack-converter) hello로 hello 경로 toohello 통합 모듈을 제공 하는 경우 변환 **모듈** 매개 변수입니다.  System Center 통합 팩에 대 한 hello를 사용할 수 있습니다 [System Center Orchestrator 통합 모듈](#system-center-orchestrator-integration-modules)합니다.

### <a name="orchestrator-resources"></a>Orchestrator 리소스
hello Runbook 변환기에만 runbook, 카운터, 변수, 연결 등 기타 Orchestrator 리소스가 아닌으로 변환합니다.  카운터는 Azure Automation에서 지원되지 않습니다.  변수 및 연결은 지원되지만 수동으로 만들어야 합니다.  hello 로그 파일은 hello runbook에 이러한 리소스가 필요한 경우에 하 고 runbook toooperate를 제대로 변환 hello에 대 한 Azure 자동화에서 toocreate 해야 해당 리소스를 지정 합니다.

예를 들어 runbook 활동에서 변수 toopopulate 특정 값을 사용할 수 있습니다.  hello 변환 된 runbook hello 활동으로 변환 되며 hello Orchestrator 변수로 이름과 같은 이름을 hello로 Azure 자동화에서 변수 자산을 지정 합니다.  이 hello에 기록 됩니다 **Runbook 변환기-Summary.log** hello 변환 후에 만들어지는 파일입니다.  해야 toomanually hello runbook을 사용 하기 전에 Azure 자동화에서이 변수 자산을 만듭니다.

### <a name="input-parameters"></a>입력 매개 변수
Hello로 입력된 매개 변수를 허용 하는 Orchestrator에서 Runbook **데이터 초기화** 활동입니다.  변환 중인 hello runbook이이 활동을 포함 하는 경우 아니라면 [입력된 매개 변수](automation-graphical-authoring-intro.md#runbook-input-and-output) hello Azure 자동화에서에서 runbook을 만들 각 매개 변수에 대해 hello 활동에서 합니다.  A [워크플로 스크립트 컨트롤](automation-graphical-authoring-intro.md#activities) 검색 하 고 각 매개 변수를 반환 하는 변환 hello runbook에 활동을 만듭니다.  입력된 매개 변수를 사용 하는 hello runbook의 모든 활동이이 활동에서 toohello 출력을 참조 하십시오.

이 전략을 사용 하는 hello 이유는 hello Orchestrator runbook에서 toobest 미러 hello 기능입니다.  새 그래픽 runbook에 활동 tooinput 매개 변수는 Runbook의 입력된 데이터 원본을 사용 하 여 직접 참조 해야 합니다.

### <a name="invoke-runbook-activity"></a>Runbook 작업 호출
Orchestrator에서 Runbook hello로 다른 runbook을 시작할 **Runbook 호출** 활동입니다. 이 활동과 hello 환산 hello runbook에 포함 되어 있으면 **완료 될 때까지** 옵션이 설정 되어 다음 변환 hello runbook에서 runbook 작업의 생성 됩니다.  경우 hello **완료 될 때까지** 옵션을 설정 하지 않으면 다음 워크플로 스크립트 작업 사용 하는 만드는 **Start-azureautomationrunbook** toostart hello runbook입니다.  Azure 자동화로 변환 하는 hello runbook을 가져온 후 hello 활동에 지정 된 hello 정보로이 작업을 수정 해야 합니다.

## <a name="related-articles"></a>관련 문서
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx)
* [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)
* [Orchestrator Standard Activities](http://technet.microsoft.com/library/hh403832.aspx)
* [System Center Orchestrator Migration Toolkit 다운로드](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
