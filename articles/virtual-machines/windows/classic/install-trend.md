---
title: "VM에서 추세 Micro Deep Security aaaInstall | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooinstall 및 Azure의 hello 클래식 배포 모델을 사용 하 여 만든 VM에서 Trend Micro 보안을 구성 합니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>어떻게 tooinstall 및 서비스로 Windows VM에서 Trend Micro Deep Security 구성
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

이 문서에서는 어떻게 tooinstall 및 Trend Micro Deep Security를 서비스로 실행 하는 새로운 또는 기존 가상 컴퓨터 (VM) Windows Server에서 구성 합니다. Deep Security as a Service는 맬웨어 방지 보호, 방화벽, 침입 방지 시스템 및 무결성 모니터링을 포함합니다.

hello 클라이언트 hello VM 에이전트를 통해 보안 확장 프로그램으로 설치 됩니다. 새 가상 컴퓨터에 설치한 hello Deep Security Agent로 hello hello Azure 포털에서 VM 에이전트를 자동으로 생성 합니다.

Hello 클래식 포털, hello Azure CLI 또는 PowerShell을 사용 하 여 만든 기존 VM에 VM 에이전트가 없을 수도 있습니다. VM 에이전트 hello이 없는 기존 가상 컴퓨터에 대 한 toodownload 필요한 및 앱을 먼저 설치 합니다. 이 문서에서는 두 상황을 모두 다룹니다.

온-프레미스 솔루션에 대 한 Trend Micro에서 현재 구독을 보유 하는 경우 파일을 사용할 수 toohelp Azure 가상 컴퓨터를 보호 합니다. 아직 구독 고객이 아닌 경우에는 평가판 구독에 등록할 수 있습니다. 이 솔루션에 대 한 자세한 내용은 hello Trend Micro 블로그 게시물을 참조 하십시오. [Microsoft Azure VM 에이전트 확장에 대 한 전체 보안](http://go.microsoft.com/fwlink/p/?LinkId=403945)합니다.

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>새 VM에 hello Deep Security Agent를 설치 합니다.

hello [Azure 포털](http://portal.azure.com) hello에서 이미지를 사용 하는 경우 hello Trend Micro 보안 확장 프로그램을 설치 하면 **마켓플레이스** toocreate hello 가상 컴퓨터. 단일 가상 컴퓨터를 만드는 경우 hello 포털을 사용 하 여은 Trend Micro에서 쉽게 tooadd 보호 기능입니다.

Hello에서 항목을 사용 하 여 **마켓플레이스** hello 가상 컴퓨터를 설정 하는 데 도움이 되는 마법사를 엽니다. Hello를 사용 하 여 **설정을** 블레이드, hello hello 마법사, tooinstall hello Trend Micro 보안 확장 프로그램의 세 번째 패널입니다.  일반 지침은 [hello Azure 포털에서에서 Windows를 실행 중인 가상 컴퓨터를 만드는](tutorial.md)합니다.

Toohello를 가져올 때 **설정을** 블레이드 hello 마법사의 다음 단계 hello지 않습니다.

1. 클릭 **확장**, 클릭 **확장 추가** hello 다음 창에서.

   ![Hello 확장을 추가 하기 시작][1]

2. 선택 **Deep Security Agent** hello에 **새 리소스** 창. Hello Deep Security Agent 창에서 클릭 **만들기**합니다.

   ![Deep Security Agent 식별][2]

3. Hello 입력 **테 넌 트 식별자** 및 **테 넌 트 활성화 암호** hello 확장에 대 한 합니다. 선택적으로 **보안 정책 식별자**를 입력할 수도 있습니다. 클릭 **확인** tooadd hello 클라이언트입니다.

   ![확장 세부 정보 제공][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>기존 VM에 hello Deep Security Agent를 설치 합니다.
기존 VM에 tooinstall hello 에이전트, 다음 항목 hello가 필요 합니다.

* hello Azure PowerShell 모듈, 0.8.2 버전 또는 최신, 로컬 컴퓨터에 설치 합니다. Hello hello를 사용 하 여 설치 된 Azure PowerShell 버전을 확인할 수 있습니다 **Get-module azure | format-table 버전** 명령입니다. 지침 및 링크 toohello 최신 버전에 대 한 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 사용 하 여 Azure 구독 tooyour `Add-AzureAccount`합니다.
* hello VM 에이전트를 hello 대상 가상 컴퓨터에 설치 합니다.

첫째, VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다. Hello 클라우드 서비스 이름 및 가상 컴퓨터 이름을 입력 한 후 hello 다음 관리자 권한 Azure PowerShell 명령 프롬프트에서 명령을 실행 합니다. Hello < 및 > 문자를 포함 하 여 hello 인용 부호 있는 모든 항목을 대체 합니다.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Hello 클라우드 서비스 및 가상 컴퓨터 이름을 모르는 경우 실행 **Get-azurevm** hello 현재 구독에서 가상 컴퓨터를 모두에 대 한 정보는 toodisplay 합니다.

경우 hello **쓰기 호스트** 명령에서 반환 **True**, hello VM 에이전트가 설치 되어 있습니다. 반환 하는 경우 **False**, hello 지침 및 다운로드 hello Azure 블로그 게시물에서에서 링크 toohello 참조 [VM 에이전트 및 확장-2 부](http://go.microsoft.com/fwlink/p/?LinkId=403947)합니다.

Hello VM 에이전트가 설치 된 경우 다음이 명령을 실행 합니다.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>다음 단계
Hello 에이전트 toostart 설치 될 때 실행에 대 한 몇 가지 분 걸립니다. 그 후 전체 보안 관리자가 관리할 수 있도록 tooactivate Deep Security hello 가상 컴퓨터에 필요 합니다. 다음 추가 지침에 대 한 아티클을 hello 참조:

* 이 솔루션과 관련된 Trend 문서, [Microsoft Azure에 대한 즉시 재생 가능한 클라우드 보안](http://go.microsoft.com/fwlink/?LinkId=404101)
* A [샘플 Windows PowerShell 스크립트](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello 가상 컴퓨터
* [지침](http://go.microsoft.com/fwlink/?LinkId=404099) hello 샘플에 대 한

## <a name="additional-resources"></a>추가 리소스
[어떻게 toolog Windows Server를 실행 tooa 가상 컴퓨터]

[Azure VM 확장 및 기능]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[어떻게 toolog Windows Server를 실행 tooa 가상 컴퓨터]:connect-logon.md
[Azure VM 확장 및 기능]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
