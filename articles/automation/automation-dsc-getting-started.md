---
title: "Azure 자동화 DSC aaaGetting 시작 | Microsoft Docs"
description: "설명 및 예제는 hello 가장 일반적인 작업의 Azure 자동화 DSC 필요한 상태 구성)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Azure 자동화 DSC 시작하기
이 항목에서는 방법을 toodo hello와 Azure 자동화 DSC 필요한 상태 구성 (), 만들기, 가져오기 및 구성, 너무 컴퓨터를 관리 하는 온 보 딩 컴파일 및 보고서를 보는 등의 가장 일반적인 작업을 설명 합니다. Azure 자동화 DSC가 무엇인지의 개요는 [Azure 자동화 DSC 개요](automation-dsc-overview.md)를 참조하세요. DSC 설명서는 [Windows PowerShell 필요한 상태 구성 개요](https://msdn.microsoft.com/PowerShell/dsc/overview)를 참조하세요.

이 항목에서는 단계별 가이드 toousing Azure 자동화 DSC를 제공 합니다. 이 항목에서 설명 하는 hello 단계를 수행 하지 않고 이미 설정 하는 샘플 환경을 원하는 경우 사용할 수 있습니다 [hello ARM 템플릿을 다음](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup)합니다. 이 템플릿은 Azure 자동화 DSC에 의해 관리되는 Azure VM을 포함하는 완료된 Azure 자동화 DSC 환경을 설정합니다.

## <a name="prerequisites"></a>필수 조건
이 항목의 toocomplete hello 예제, hello 다음이 필요 합니다.

* Azure 자동화 계정. Azure 자동화 실행 계정 만들기에 대한 지침은 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)을 참조하세요.
* Windows Server 2008 R2 이상을 실행하는 Azure Resource Manager VM(클래식 아님). VM을 만드는 방법에 지침은 [hello Azure 포털에서에서 첫 번째 Windows 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>DSC 구성 만들기
간단한 만듭니다 [DSC 구성을](https://msdn.microsoft.com/powershell/dsc/configurations) 중 hello의 유무 hello 검색이 설정 **웹 서버** Windows 기능 (IIS), 노드를 할당 하는 방법에 따라 합니다.

1. Windows PowerShell ISE hello (또는 다른 텍스트 편집기)를 시작 합니다.
2. Hello 텍스트 다음을 입력 합니다.
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Hello 파일으로 저장 `TestConfig.ps1`합니다.

이 구성은 호출 자원을 하나씩 각 노드 블록에 hello [WindowsFeature 리소스](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), 검색이 설정 중 하나 hello의 유무 hello **웹 서버** 기능입니다.

## <a name="importing-a-configuration-into-azure-automation"></a>Azure 자동화로 구성 가져오기
다음으로 hello 자동화 계정에 hello 구성을 가져옵니다 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성을**합니다.
4. Hello에 **DSC 구성을** 블레이드에서 클릭 **구성을 추가**합니다.
5. Hello에 **구성 가져오기** 블레이드, 찾아보기 toohello `TestConfig.ps1` 파일을 컴퓨터에 있습니다.
   
    ![Hello 스크린샷 * * 가져오기 구성 * * 블레이드](./media/automation-dsc-getting-started/AddConfig.png)
6. **확인**을 클릭합니다.

## <a name="viewing-a-configuration-in-azure-automation"></a>Azure 자동화에서 구성 보기
구성을 가져온 후에 hello Azure 포털에서에서 볼 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성**
4. Hello에 **DSC 구성을** 블레이드에서 클릭 **TestConfig** (hello 이전 절차에서이 가져온 hello 구성의 hello 이름).
5. Hello에 **TestConfig 구성** 블레이드에서 클릭 **구성 소스 보기**합니다.
   
    ![Hello TestConfig 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    A **TestConfig 구성 소스** 블레이드가 열리고 hello 구성에 대 한 hello PowerShell 코드를 표시 합니다.

## <a name="compiling-a-configuration-in-azure-automation"></a>Azure 자동화에서 구성 컴파일
원하는 상태 tooa 노드를 적용 하려면 먼저 해당 상태를 정의 하는 DSC 구성은 하나 이상의 노드 구성 (MOF 문서)으로 컴파일됩니다 고 hello 자동화 DSC 끌어오기 서버에 배치 해야 합니다. Azure 자동화 DSC에서 구성 컴파일의 자세한 설명은 [Azure 자동화 DSC에서 구성을 컴파일](automation-dsc-compile.md)을 참조하세요. 구성 컴파일에 대한 자세한 내용은 [DSC 구성](https://msdn.microsoft.com/PowerShell/DSC/configurations)을 참조하세요.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성**
4. Hello에 **DSC 구성을** 블레이드에서 클릭 **TestConfig** (hello hello의 이전에 가져온 이름 구성).
5. Hello에 **TestConfig 구성** 블레이드에서 클릭 **컴파일**, 클릭 하 고 **예**합니다. 컴파일 작업이 시작됩니다.
   
    ![컴파일 단추를 강조 표시는 hello TestConfig 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Azure 자동화에서 구성을 컴파일할 때 자동으로 모든 만든된 노드 구성 Mof toohello 끌어오기 서버를 배포 합니다.
> 
> 

## <a name="viewing-a-compilation-job"></a>컴파일 작업 보기
컴파일을 시작 하 고 나면 hello에서 볼 수 있습니다 **컴파일 작업** hello에 바둑판식으로 배열 **구성** 블레이드입니다. hello **컴파일 작업** 타일 표시 현재 실행 되 고 완료 하 고 실패 한 작업을 합니다. 컴파일 작업 블레이드를 여는 경우 오류 또는 경고가 발생 한를 포함 하 여 해당 작업에 대 한 정보를 표시, 입력된 매개 변수 로그 hello 구성 및 컴파일에서 사용 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성을**합니다.
4. Hello에 **DSC 구성을** 블레이드에서 클릭 **TestConfig** (hello hello의 이전에 가져온 이름 구성).
5. Hello에 **컴파일 작업** 타일의 hello **TestConfig 구성** 블레이드를 나열 하는 hello 작업 중 하나를 클릭 합니다. A **컴파일 작업** 시작 된 컴파일 작업 hello hello 날짜도 레이블이 지정 된이 블레이드에서 열립니다.
   
    ![Hello 컴파일 작업 블레이드의 스크린샷](./media/automation-dsc-getting-started/CompilationJob.png)
6. Hello에서 모든 타일에서 클릭 **컴파일 작업** hello 작업에 대 한 세부 정보 블레이드에서 toosee 추가 합니다.

## <a name="viewing-node-configurations"></a>노드 구성 보기
컴파일 작업을 성공적으로 완료하면 하나 이상의 새 노드 구성을 만듭니다. 노드 구성에 배포 된 toohello 끌어오기 서버와 준비 toobe 가져오고 하나 이상의 노드에 적용 MOF 문서입니다. Hello에 자동화 계정에서 hello 노드 구성을 볼 수 있습니다 **DSC 노드 구성을** 블레이드입니다. 노드 구성 이름이 hello 양식으로 *ConfigurationName*. *NodeName*합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드 구성을**합니다.
   
    ![Hello DSC 노드 구성을 블레이드의 스크린샷](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Azure 자동화 DSC를 통한 관리를 위한 Azure VM 온보드
Azure 자동화 DSC toomanage Azure Vm (리소스 관리자 및 기본), 온-프레미스 Vm, Linux 컴퓨터, AWS Vm 및 온-프레미스 물리적 컴퓨터를 사용할 수 있습니다. 이 항목에서는 다룹니다 어떻게 tooonboard Azure 리소스 관리자 Vm만 합니다. 다른 유형의 컴퓨터 온보드에 대한 정보는 [Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요.

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>Azure 자동화 DSC에 의해 관리에 대 한 Azure 리소스 관리자 VM tooonboard
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.
4. Hello에 **DSC 노드** 블레이드에서 클릭 **Azure VM 추가**합니다.
   
    ![Hello Azure VM 추가 단추를 강조 표시는 hello DSC 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/OnboardVM.png)
5. Hello에 **Azure Vm 추가** 블레이드에서 클릭 **tooonboard 가상 컴퓨터를 선택**합니다.
6. Hello에 **선택 Vm** 블레이드를 누르고 tooonboard, 원하는 VM 선택 hello **확인**합니다.
   
   > [!IMPORTANT]
   > Windows Server 2008 R2 이상을 실행하는 Azure Resource Manager VM이어야 합니다.
   > 
   > 
7. Hello에 **Azure Vm 추가** 블레이드에서 클릭 **등록 데이터를 구성**합니다.
8. Hello에 **등록** 블레이드에서 hello 이름을 입력 hello에 대 한 VM tooapply toohello hello 노드 구성의 원하는 **노드 구성 이름은** 상자입니다. Hello hello 자동화 계정에서에서 노드 구성 이름이 일치 해야 합니다. 이 시점에서 이름을 제공하는 것은 선택 사항입니다. 온 보 딩 hello 노드 할당 hello 노드 구성을 변경할 수 있습니다.
   **필요한 경우 노드 다시 부팅**을 선택한 다음 **확인**을 클릭합니다.
   
    ![Hello 등록 블레이드의 스크린샷](./media/automation-dsc-getting-started/RegisterVM.png)
   
    지정한 hello 노드 구성을 hello 하 여 지정 된 간격에 적용 된 toohello VM 수 **구성 모드 빈도가**, hello VM은 업데이트 toohello 노드 구성 hello 하여지정된간격에있는지확인하고 **새로 고침 빈도**합니다. 이러한 값은 사용 하는 방법에 대 한 자세한 내용은 참조 [hello 구성 로컬 구성 관리자](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)합니다.
9. Hello에 **Azure Vm 추가** 블레이드에서 클릭 **만들기**합니다.

Azure의 온 보 딩 hello VM hello 프로세스를 시작 됩니다. 완료 되 면 hello VM에에서 나타납니다 hello **DSC 노드** 블레이드 hello 자동화 계정에에서 있습니다.

## <a name="viewing-hello-list-of-dsc-nodes"></a>DSC 노드 hello 목록 보기
관리 hello의 자동화 계정에 대 한 등록 된 모든 컴퓨터의 hello 목록을 볼 수 있습니다 **DSC 노드** 블레이드입니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.

## <a name="viewing-reports-for-dsc-nodes"></a>DSC 노드에 대한 보고서 보기
관리 되는 노드에 대 한 일관성 확인을 수행 하는 Azure 자동화 DSC 때마다 hello 노드 상태 보고서 백 toohello 끌어오기 서버를 보냅니다. 해당 노드에 대 한 hello 블레이드에서 이러한 보고서를 볼 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.
4. Hello에 **보고서** 타일 hello 목록의 hello 보고서 중 하나를 클릭 하십시오.
   
    ![Hello 보고서 블레이드의 스크린샷](./media/automation-dsc-getting-started/NodeReport.png)

개별 보고서에 대 한 hello 블레이드에서 확인 hello 다음 hello 해당 일관성에 대 한 상태 정보를 확인할 수 있습니다.

* 상태 보고 hello-hello 노드는 hello 구성 "Failed", "준수" 여부 hello 노드는 "호환 되지 않는" (hello 노드 중인 **applyandmonitor** 모드와 hello 컴퓨터가 hello 원하는 상태에 있지 않은).
* hello hello 일관성 확인에 대 한 시작 시간입니다.
* hello 일관성에 대 한 총 런타임을 hello 확인 합니다.
* hello 유형의 일관성 확인 합니다.
* Hello 오류 코드 및 오류 메시지를 포함 하 여 모든 오류. 
* (여부 hello 노드는 해당 리소스에 대 한 원하는 hello 상태)의 각 리소스의 hello 상태 및 hello 구성에 사용 되는 모든 DSC 리소스-클릭할 수 있는 자세한 정보를 해당 리소스에 대 한 각 리소스 tooget에 있습니다.
* hello 이름, IP 주소 및 hello 노드의 구성 모드 중에서 선택 합니다.

클릭할 수도 있습니다 **원시 보고서를 볼** toosee hello 실제 데이터는 노드 hello toohello 서버 보냅니다. 해당 데이터 사용에 대한 자세한 내용은 [DSC 보고서 서버 사용](https://msdn.microsoft.com/powershell/dsc/reportserver)을 참조하세요.

Hello 첫 번째 보고서를 사용할 수 전에 노드는 등록 된 후에 다소 시간이 걸릴 수 있습니다. 할 수 있습니다 too30 분을 toowait hello 첫 번째 보고서에 대 한 후 등록 노드.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>다시 할당 하는 노드 tooa 다른 노드 구성
Hello 초기 할당 보다 다른 노드 구성 노드 toouse을 할당할 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.
4. Hello에 **DSC 노드** hello 이름 클릭 블레이드에서 원하는 tooreassign hello 노드의 합니다.
5. 해당 노드에 대 한 hello 블레이드에서 클릭 **할당 노드**합니다.
   
    ![Hello 노드 할당 단추를 강조 표시는 hello 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/AssignNode.png)
6. Hello에 **노드 구성을 할당** 블레이드, 선택 hello 노드 구성 toowhich tooassign hello 노드를 선택 하 고 클릭 **확인**합니다.
   
    ![Hello 노드 구성을 할당 블레이드의 스크린샷](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>노드 등록 취소
Azure 자동화 DSC에 의해 관리 되는 노드 toobe를 더 이상 사용 하지 않으려면 하는 경우 등록 취소할 수 없습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.
3. Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.
4. Hello에 **DSC 노드** hello 이름 클릭 블레이드에서 원하는 toounregister hello 노드의 합니다.
5. 해당 노드에 대 한 hello 블레이드에서 클릭 **등록 취소**합니다.
   
    ![Hello 등록 취소 단추를 강조 표시는 hello 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>관련 문서
* [Azure 자동화 DSC 개요](automation-dsc-overview.md)
* [Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)
* [Windows PowerShell 필요한 상태 구성 개요](https://msdn.microsoft.com/powershell/dsc/overview)
* [Azure 자동화 DSC cmdlets](/powershell/module/azurerm.automation/#automation)
* [Azure 자동화 DSC 가격 책정](https://azure.microsoft.com/pricing/details/automation/)

