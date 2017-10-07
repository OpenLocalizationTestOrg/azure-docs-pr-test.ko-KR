---
title: "자동화 DSC 연속 배포 Chocolatey와 aaaAzure | Microsoft Docs"
description: "Azure 자동화 DSC 및 Chocolatey패키지 관리자를 사용한 DevOps 연속 배포  전체 JSON ARM 템플릿 및 PowerShell 소스가 있는 예"
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>사용 예: 연속 배포 tooVirtual Chocolatey 및 자동화 DSC를 사용 하 여 컴퓨터
DevOps world hello 연속 통합 파이프라인에서 다양 한 요소와 함께 많은 도구 tooassist는 있습니다.  Azure 자동화 원하는 상태 구성 (DSC) DevOps 팀을 사용할 수 시작 새 추가 toohello 옵션입니다.  이 문서에서는 Windows 컴퓨터에 대 한 CD(연속 배포)를 보여줍니다.  쉽게 확장할 수 있습니다 hello 기술을 tooinclude hello 역할 (웹 사이트, 예:), 및에 없어 tooadditional에서 필요에 따라 많은 Windows 컴퓨터 역할에도 합니다.

![IaaS VM에 대한 연속 배포](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>높은 수준
이 단계는 상당 부분 진행 중이지만 다행스럽게도 두 가지 기본 프로세스로 나눌 수 있습니다. 

* 코드를 작성 및 테스트, 다음 만들기 및 hello 시스템의 주 버전과 부 버전에 대 한 설치 패키지를 게시 합니다. 
* 만들고 설치 하 고 hello 코드 hello 패키지를 실행 하는 Vm을 관리 합니다.  

위치에 있는 두 핵심 프로세스를 새 버전에서 생성 되 고 배포 하는 대로 모든 특정 VM에서 실행 되는 짧은 단계 tooautomatically 업데이트 hello 패키지입니다.

## <a name="component-overview"></a>구성 요소 개요
관리자와 같은 패키지 [apt get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) 는 hello Linux 하지만 하지 그것 들 hello Windows 환경에서에서 꽤 잘 알려진 합니다.  [Chocolatey](https://chocolatey.org/) 은 이러한 작업을 및 Scott Hanselman [블로그](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) hello 항목은 훌륭한 소개 합니다.  간단히 말해서 Chocolatey 있습니다 tooinstall 패키지를에서 패키지를 중앙 리포지토리에 hello 명령줄을 사용 하 여 Windows 시스템에.  자체 리포지토리를 만들어 관리할 수 있고 Chocolatey가 사용자가 지정한 수 만큼의 리포지토리에서 패키지를 설치할 수 있습니다.

DSC 필요한 상태 구성 () ([개요](https://technet.microsoft.com/library/dn249912.aspx))는 컴퓨터에 대해 원하는 toodeclare hello 구성을 허용 하는 PowerShell 도구입니다.  예를 들어, "Chocolatey와 IIS를 설치하고 포트 80을 개방하며 웹 사이트 설치의 1.0.0 버전을 원합니다."라고 말할 수 있습니다.  hello DSC 로컬 구성 관리자 (LCM)에 해당 구성을 구현합니다. DSC 풀 서버가 컴퓨터에 대한 구성 리포지토리를 담고 있습니다. 각 컴퓨터에 hello LCM 구성을 일치 hello 저장 된 구성 하는 경우 주기적으로 toosee를 확인 합니다. 상태를 보고 하거나 toobring hello 컴퓨터 부합 hello 저장 된 구성으로 다시 시도할 수 있습니다. Hello 저장 된 구성 hello 끌어오기 서버 toocause는 컴퓨터 또는 컴퓨터 toocome 집합이으로 변경 하는 hello 구성으로 편집할 수 있습니다.

Azure 자동화는 runbook, 노드, 자격 증명, 리소스 및 일정 및 전역 변수 등의 자산을 사용 하 여 다양 한 작업 tooautomate 수 있는 Microsoft Azure에서 관리 되는 서비스입니다. Azure 자동화 DSC이이 자동화 기능 tooinclude PowerShell DSC 도구를 확장합니다.  여기서 알맞은 [개요](automation-dsc-overview.md)를 제공합니다.

DSC 리소스는 네트워크 관리, Active Directory 또는 SQL Server 등과 같은 특정 기능을 갖는 코드 모듈입니다.  hello Chocolatey DSC 리소스 tooaccess (맺음) NuGet 서버 다운로드 패키지, 패키지를 설치 하 고 방법 등을 알고 있습니다.  Hello에도 다른 여러 DSC 리소스는 [PowerShell 갤러리](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title)합니다.  이러한 모듈은 사용자가 구성에서 사용할 수 있게 Azure 자동화 DSC 풀 서버에 설치됩니다.

리소스 관리자 템플릿은 네트워크, 서브넷, 네트워크 보안, 라우팅, 부하 분산 장치, NIC, VM 등의 인프라를 생성하는 선언적인 방법을 제공합니다.  다음은 프로그램 [문서](../azure-resource-manager/resource-manager-deployment-model.md) 비교 하 여 hello Azure 서비스 관리 (ASM, 또는 클래식)로 리소스 관리자 배포 모델 (선언적)를 hello 배포 (명령적), 모델 및 hello 핵심 리소스에 설명 공급자, 계산, 저장소 및 네트워크입니다.

리소스 관리자 템플릿 주요 기능 중 하나는 능력 tooinstall hello VM에 VM 확장은 프로 비전 됩니다.  VM 확장에는 사용자 지정 스크립트 실행, 바이러스 백신 소프트웨어 설치, DSC 구성 스크립트 실행 등과 같은 특정 기능이 있습니다.  VM 확장에는 여러 다른 형식이 있습니다.

## <a name="quick-trip-around-hello-diagram"></a>Hello 다이어그램 주변 빠른 여정
Hello 위쪽 starting, 코드를 작성 빌드 및 테스트, 다음 설치 패키지를 만듭니다.  Chocolatey는 MSI, MSU, ZIP 등과 같은 다양한 형태의 설치 패키지를 처리할 수 있습니다.  하며 tooit를 매우 Chocolatey의 기본 기능 하지 않은 경우 hello를 최대한 활용 PowerShell toodo hello 실제 설치 해야 합니다.  Hello 패키지를 했지만 위치 연결할 수 – 패키지 저장소에 넣습니다.  이 사용 예는 Auzre Blob 저장소 계정의 공용 폴더를 사용하지만 어디에나 있을 수 있습니다.  Chocolatey는 패키지 메타데이터의 관리를 위해 NuGet 서버 및 기타 제품과 기본적으로 연동됩니다.  [이 문서](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) hello 옵션에 설명 합니다.  이 사용 예는 NuGet을 사용합니다.  Nuspec은 패키지에 관한 메타데이터입니다.  hello Nuspec "컴파일될" NuPkg의 되며 NuGet 서버에 저장 됩니다.  구성 이름으로 패키지를 요청 하 고 NuGet 서버를 참조 하십시오 hello Chocolatey DSC 리소스 (이제 hello VM)에 가져와 hello 패키지를 설치 합니다.  특정 버전의 패키지를 요청할 수도 있습니다.

Hello hello 그림의 왼쪽된 부분을 아래쪽에서는 Azure 리소스 관리자 (ARM) 템플릿을 있습니다.  이 예에서 사용 hello VM 확장 노드로 hello VM hello Azure 자동화 DSC 끌어오기 서버 (즉, 끌어오기 서버)로 등록합니다.  hello 구성 hello 끌어오기 서버에 저장 됩니다.  사실 일반 텍스트로 1번, MOF 파일로 컴파일 1번 등(이에 대해 알고 있는 상황), 두 번 저장됩니다.  Hello 포털에서 hello MOF는 "노드 구성" (것과 반대로 toosimply "구성").  hello 아티팩트 hello 노드 구성을 알 수 있도록 노드를 연결 합니다.  아래 세부 정보 tooassign 노드 구성 toohello 노드 hello 하는 방법을 보여 줍니다.

아마도 hello 비트 hello 위쪽에, 또는 대부분의 이미 현재 수행 중인 합니다.  Hello nuspec 생성, 컴파일 및 NuGet 서버에 저장 하는 작은 변화 합니다.  이미 VM을 관리하고 있습니다.  다음 단계 toocontinuous 배포 hello 라인으로 전환 (한 번) hello 끌어오기 서버 설정, 노드 (한 번) 작성기를 등록 하 고 만들기 및 hello 구성 있습니다 (처음) 저장 필요 합니다.  Hello 구성 및 노드 구성 (필요에 따라 반복) hello 끌어오기 서버에서 새로 고침 대로 패키지를 업그레이드 하 고 toohello 저장소를 배포 합니다.

ARM 템플릿으로 시작하지 않아도 괜찮습니다.  PowerShell cmdlet toohelp hello 끌어오기 서버와 모든 hello 나머지 Vm에 등록 하면 있습니다. 자세한 내용은 다음 문서, [Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>1 단계: hello 끌어오기 서버와 자동화 계정 설정
인증 된 (추가 AzureRmAccount) PowerShell 명령줄에서: (수는 몇 분 정도 걸릴 hello 끌어오기 서버 설정 하는 동안)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Hello 영역 (즉, 위치) 다음 중 하나로 자동화 계정에 넣을 수 있습니다: 미국 동부 2, 미국 중남부, 미국 정부 기관용 버지니아, 서 부 유럽, 동남 아시아, 일본 동부, 중앙 인도 및 오스트레일리아 남동부, 캐나다 중앙 유럽 북부 합니다.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>2 단계: VM 확장 조정 toohello ARM 템플릿
VM 등록 (hello PowerShell DSC VM 확장 사용)이 제공에 대 한 세부 정보 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver)합니다.  이 단계는 hello DSC 노드 목록에서 hello 끌어오기 서버와 함께 새 VM을 등록합니다.  이러한 등록의 일부 hello 노드 구성 적용 toobe toohello 노드를 지정 하는 합니다.  이 노드 구성 없는 tooexist 아직 hello 끌어오기 서버에 있는 4 단계를 이렇게 hello에 대 한 처음으로 확인 되기 때문입니다.  하지만 여기 2 단계에서에서 필요 toohave 결정된 hello hello 노드의 이름과 이름 hello hello 구성 합니다.  이 예에서 사용 hello 노드는 'isvbox' 하며 hello 구성은 'ISVBoxConfig'.  따라서 hello 노드 구성 이름은 (toobe DeploymentTemplate.json에 지정 된)은 'ISVBoxConfig.isvbox'.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>3 단계: 필요한 DSC 리소스 toohello 끌어오기 서버를 추가합니다.
PowerShell 갤러리 hello Azure 자동화 계정에 계측 된 tooinstall DSC 리소스입니다.  원하는 고 hello "배포 tooAzure 자동화" 단추를 클릭 toohello 리소스를 이동 합니다.

![PowerShell 갤러리 예](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

또 다른 방법은 최근에 Azure 포털 toohello 있습니다 toopull 새 모듈 또는 업데이트 기존 모듈에 추가 했습니다. Hello 자동화 계정 리소스, hello 자산 타일 및 마지막으로 hello 모듈 타일을 클릭 합니다.  hello 찾아보기 갤러리 아이콘 toosee hello 목록이 hello 갤러리에 모듈을 사용 하면, 세부 정보로 드릴 다운 및 궁극적으로 자동화 계정으로 가져옵니다. 이 좋은 방법 tookeep 시간 tootime에서 toodate 모듈입니다. 고 hello 가져오기 기능은 다른 모듈 tooensure 아무 가져옵니다 동기화와 종속성을 확인 합니다.

또는 hello 수동 방법도 있습니다.  Windows 컴퓨터에 대 한 PowerShell 통합 모듈의 hello 폴더 구조는 hello Azure 자동화에 필요한 hello 폴더 구조와에서 약간 다릅니다.  여기에는 약간의 사용자 조정 작업이 필요합니다.  하지만, 없는 및 리소스 당 한 번만 수행 됩니다 (tooupgrade 사용 하려는 경우가 아니면 이후에.)  PowerShell 통합 모듈 제작에 대한 자세한 내용은 다음 문서를 참조하세요. [Azure Automation에 대한 통합 모듈 제작](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* 다음과 같이 워크스테이션에서 필요로 하는 hello 모듈을 설치 합니다.
  * [Windows Management Framework, v5](http://aka.ms/wmf5latest) 설치(Windows 10에는 필요 없음)
  * `Install-Module –Name MODULE-NAME`<-hello PowerShell 갤러리에서에서 모듈 hello grabs의 
* Hello 모듈 폴더에서 복사 `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa 임시 폴더 
* Hello 주 폴더에서 예제 및 설명서를 삭제 합니다. 
* Zip hello 주 폴더 hello 폴더와 같은 hello hello ZIP 파일을 정확 하 게 이름 지정 
* Hello ZIP 파일을 blob 저장소는 Azure 저장소 계정에 연결할 수 있는 HTTP 위치에 배치 합니다.
* 이 PowerShell 실행:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

포함 하는 hello 예제 cChoco 및 xNetworking에 대 한 다음이 단계를 수행합니다. Hello 참조 [노트](#notes) cChoco에 대 한 특수 처리를 위한 합니다.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>4 단계: hello 노드 구성 toohello 끌어오기 서버를 추가합니다.
Hello에 대 한 특별 한 일 처음 가져오는 경우 구성을 끌어오기 서버 hello 및 컴파일은 없습니다.  모든 후속 가져오기/컴파일하고 hello의 동일한 구성 형태로 정확 하 게 hello 동일 합니다.  패키지를 업데이트 하 고 toopush tooproduction 아웃 하면이 단계를 수행 hello 구성 파일을 확인 한 후 필요한 때마다 올바른지 – hello 패키지의 새 버전입니다.  Hello 구성 파일 및 PowerShell 다음과 같습니다.

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

새 노드 구성에서 이러한 단계 결과 라는 "ISVBoxConfig.isvbox" hello 끌어오기 서버에 배치 합니다.  hello 노드 구성 이름은 "configurationName.nodeName"로 작성 됩니다.

## <a name="step-5-creating-and-maintaining-package-metadata"></a>5단계: 패키지 메타데이터 만들기 및 유지 관리
Hello 패키지 리포지토리를 설정 하는 각 패키지에 대해 설명 하는 nuspec를 해야 합니다.  해당 nuspec은 NuGet 서버에서 컴파일 및 저장해야 합니다. 이 프로세스는 [여기](http://docs.nuget.org/create/creating-and-publishing-a-package)에서 설명합니다.  MyGet.org를 NuGet 서버로 사용할 수 있습니다.  이 서비스를 판매하고 있지만 스타터 SKU는 무료입니다.  NuGet.org에서 개인 패키지에 대 한 자체 NuGet 서버 설치 관련 지침을 찾을 수 있습니다.

## <a name="step-6-tying-it-all-together"></a>6단계: 모든 항목 요약
배포의 경우 버전 QA를 전달 하 고 승인 될 때마다 hello 패키지를 만들, nuspec nupkg 업데이트 되 고 toohello NuGet 서버를 배포 합니다.  또한 hello 구성 (4 단계 위의) hello 새 버전 번호로 업데이트 된 tooagree 이어야 합니다.  Toohello 끌어오기 서버를 전송 및 컴파일된 수 해야 합니다.  해당 지점에서 해당 구성 toopull hello 업데이트에 종속 하 고 설치 하는 toohello Vm가 있습니다.  이러한 각각의 업데이트는 하나 또는 두 줄의 PowerShell로 간단합니다.  Visual Studio Team Services의 hello 경우에서 그 중 일부를 빌드를 서로 연결 될 수 있는 빌드 작업에 캡슐화 됩니다.  이 [문서](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery)에 자세한 내용이 나와 있습니다.  이 [GitHub 리포지토리](https://github.com/Microsoft/vso-agent-tasks) 세부 정보 hello 다양 한 사용 가능한 빌드 작업입니다.

## <a name="notes"></a>참고 사항
사용 예제를 보려면이 hello Azure 갤러리에서에서 일반 Windows Server 2012 R2 이미지에서 VM으로 시작합니다.  저장된 된 이미지에서 시작할 수 있으며 다음 hello DSC 구성 사용 하 여 여기에서 수정할 수 있습니다.  그러나 이미지로 변환 되는 구성 변경는 DSC를 사용 하 여 hello 구성을 동적으로 업데이트 보다 훨씬 더 어렵습니다.

않아도 toouse ARM 템플릿 및 hello VM 확장 toouse이이 기술을 여 vm 됩니다.  및 Vm에 Azure toobe CD 관리 아래에 toobe 필요는 없습니다.  된 모든 것은 필요한 해당 Chocolatey 수 설치 되어 있고 hello LCM 구성 hello VM에 있는 hello 끌어오기 서버는 알 수 있도록 합니다.  

물론, 프로덕션 환경에 있는 VM에서 패키지를 업데이트 해야 tootake 순환 순서에서 해당 VM hello 업데이트가 설치 되는 동안 합니다.  이를 수행하는 방법은 크게 다릅니다.  예를 들어, Azure 부하 분산 장치 뒤에 있는 VM에서는 사용자 지정 프로브를 추가할 수 있습니다.  Hello VM을 업데이트 하는 동안는 400을 반환할 hello 프로브 끝점을 포함.  hello 미세 조정을 위해 필요한 toocause이이 변경 될 수 구성에 내부 조정한 tooswitch 다시 tooreturning 200 hello 업데이트 제거가 완료 되 면 hello 수 있습니다.

이 사용 예의 전체 원본은 GitHub의 [이 Visual Studio 프로젝트](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) 에 있습니다.

## <a name="related-articles"></a>관련 문서
* [Azure 자동화 DSC 개요](automation-dsc-overview.md)
* [Azure 자동화 DSC cmdlets](https://msdn.microsoft.com/library/mt244122.aspx)
* [Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)

