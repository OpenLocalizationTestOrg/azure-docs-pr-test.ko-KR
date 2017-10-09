---
title: "상태 구성에 대 한 Azure 개요 aaaDesired | Microsoft Docs"
description: "PowerShell 필요한 상태 구성에 대 한 hello Microsoft Azure 확장 처리기를 사용 하 여에 대 한 개요를 제공 합니다. 필수 구성 요소, 아키텍처, cmdlet...을 포함"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>소개 toohello Azure 필요한 상태 구성 확장 처리기
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

hello Azure VM 에이전트와 연결 된 확장은 hello Microsoft Azure 인프라 서비스의 일부입니다. VM 확장은 hello VM 기능을 확장 하 고 다양 한 VM 관리 작업을 단순화 하는 소프트웨어 구성 요소입니다. Hello VMAccess 확장 관리자의 암호를 사용 하는 tooreset 수 하거나 사용자 지정 스크립트 hello 수 예를 들어 확장명 사용된 tooexecute hello VM에 대 한 스크립트를 사용할 수 있습니다.

이 문서에서는 hello Azure PowerShell SDK의 일부분으로 Azure Vm에 대 한 hello PowerShell 필요한 상태 구성 (DSC) 확장을 소개 합니다. 새 cmdlet tooupload를 사용할 수 있으며 hello PowerShell DSC 확장을 사용 하도록 설정 하는 Azure VM에는 PowerShell DSC 구성을 적용할 수 있습니다. PowerShell DSC tooenact hello 하 여 hello PowerShell DSC 확장 호출 hello VM에서 DSC 구성을 받았습니다. 이 기능은 hello Azure 포털을 통해 사용할 수도 있습니다.

## <a name="prerequisites"></a>필수 조건
**로컬 컴퓨터** 와 toointeract hello Azure VM 확장, 필요한 toouse 어느 hello Azure 포털 또는 Azure PowerShell SDK를 환영 합니다. 

**게스트 에이전트** hello hello DSC 구성에 의해 구성 된 Azure VM 관리 프레임 워크 WMF (Windows) 4.0 또는 5.0 원하는 OS를 toobe 필요 합니다. hello에 지원 되는 운영 체제 버전의 전체 목록을 hello 있습니다 [DSC 확장 버전 기록](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/)합니다.

## <a name="terms-and-concepts"></a>용어 및 개념
이 가이드 hello 다음 개념에 익숙하다고를 가정 합니다.

구성 - DSC 구성 문서. 

노드 - DSC 구성에 대한 대상. 이 문서에 "노드" tooan Azure VM을 항상 참조합니다.

구성 데이터 - 구성에 대한 환경 데이터를 포함하는 .psd1 파일

## <a name="architectural-overview"></a>아키텍처 개요
hello Azure VM 에이전트 프레임 워크 toodeliver을 사용 하 여 hello Azure DSC 확장 하 고 시행 하 고, Azure Vm에서 실행 되는 DSC 구성을 보고 합니다. DSC 확장 hello 최소한 구성 문서를 포함 하는.zip 파일을 요구 하 고 매개 변수 집합이 제공 hello Azure PowerShell SDK 또는 hello를 통해 Azure 포털 키를 누릅니다.

처음으로 hello에 대 한 hello 확장을 호출할 때 설치 프로세스를 실행 됩니다. 이 프로세스 논리 hello를 사용 하 여 hello Windows Management Framework (WMF)의 버전을 설치 합니다.

1. Windows Server 2016 hello Azure VM OS 이면 아무 작업도 수행 합니다. Windows Server 2016 설치 된 powershell hello 최신 버전에 이미 있습니다.
2. 경우 hello `wmfVersion` 속성을 지정한 경우 해당 버전의 WMF hello hello VM의 OS와 호환 되지 않으면 설치 되어 있습니다.
3. 하지 않으면 `wmfVersion` 속성이 지정 되 면 hello 최신 해당 버전의 hello WMF 설치 되어 있습니다.

Hello WMF 설치 다시 부팅이 필요합니다. 다시 부팅 후 hello 확장 hello에 지정 된 hello.zip 파일을 다운로드 `modulesUrl` 속성입니다. SAS 토큰 hello에 지정할 수 있습니다이 위치가 Azure blob 저장소에 있으면 `sasToken` 속성 tooaccess hello 파일입니다. Hello.zip을 다운로드 하 여 압축을 푼 후에 정의 된 구성 함수 hello `configurationFunction` toogenerate hello MOF 파일을 실행 합니다. hello 확장 한 다음 실행 `Start-DscConfiguration -Force` on hello 생성 된 MOF 파일. hello 확장 출력 캡처하고 toohello Azure 상태 채널 다시 작성 합니다. Hello에이 지점에서 DSC LCM 모니터링 및 수정 정상적으로 처리합니다. 

## <a name="powershell-cmdlets"></a>PowerShell cmdlet
PowerShell cmdlet Azure 리소스 관리자와 함께 사용할 수 있습니다 또는 클래식 배포 모델 toopackage hello, 게시 및 DSC 확장 배포를 모니터링 합니다. hello 나열 된 다음 cmdlet hello 클래식 배포 모듈에 있더라도 "Azure"는 "AzureRm" toouse hello Azure 리소스 관리자 모델으로 바꿀 수 있습니다. 예를 들어 `Publish-AzureVMDscConfiguration` 사용 하 여 hello 클래식 배포 모델 여기서 `Publish-AzureRmVMDscConfiguration` Azure 리소스 관리자를 사용 합니다. 

`Publish-AzureVMDscConfiguration`구성 파일에서 걸리며 종속 DSC 리소스에 대 한 검색 hello 구성 및 DSC 리소스 필요한 tooenact hello 구성에 포함 된.zip 파일을 만듭니다. Hello를 사용 하 여 로컬로 hello 패키지를 만들 수도 수 `-ConfigurationArchivePath` 매개 변수입니다. 그렇지 않으면 hello.zip 파일 tooAzure blob 저장소를 게시 하 고 있는 SAS 토큰으로 보호 합니다.

이 cmdlet에서 만든 hello.zip 파일의 hello.ps1 구성 스크립트를 hello 보관 폴더의 hello 루트에 있습니다. 리소스는 hello 모듈 폴더 hello 보관 폴더에 배치 됩니다. 

`Set-AzureVMDscExtension`VM 구성 개체에 hello PowerShell DSC 확장에 필요한 hello 설정을 삽입 합니다. Hello 클래식 배포 모델에서 hello VM 변경 해야 합니다 적용된 tooan Azure VM으로 `Update-AzureVM`합니다. 

`Get-AzureVMDscExtension`특정 VM의 hello DSC 확장 상태를 검색합니다. 

`Get-AzureVMDscExtensionStatus`hello DSC 확장 처리기를 통해 시행 되 hello DSC 구성의 hello 상태를 검색 합니다. 이 작업을 단일 VM 또는 VM 그룹에 대해 수행할 수 있습니다.

`Remove-AzureVMDscExtension`지정된 된 가상 컴퓨터에서 hello 확장 처리기를 제거합니다. 이 cmdlet이 수행 **하지** hello 구성을 제거, hello WMF, 제거 또는 hello 가상 컴퓨터에 적용 하는 hello 설정을 변경 합니다. 만 hello 확장 처리기를 제거합니다. 

**ASM과 Azure Resource Manager cmdlets의 주요 차이점**

* Azure Resource Manager cmdlets는 동기입니다. ASM cmdlet은 비동기입니다.
* ResourceGroupName, VMName, ArchiveStorageAccountName, 버전, 위치는 Azure Resource Manager에서 모두 새 필수 매개 변수입니다.
* ArchiveResourceGroupName은 Azure Resource Manager에 대한 새로운 선택적 매개 변수입니다. 저장소 계정 하나 hello 보다 tooa 다른 리소스 그룹 hello 가상 컴퓨터를 만들 위치 속해 있는 경우이 매개 변수를 지정할 수 있습니다.
* ConfigurationArchive는 Azure Resource Manager에서 ArchiveBlobName이라고 합니다.
* ContainerName은 Azure Resource Manager에서 ArchiveContainerName이라고 합니다.
* StorageEndpointSuffix는 Azure Resource Manager에서 ArchiveStorageEndpointSuffix라고 합니다.
* 자동 업데이트 사용 가능 해지면 및 hello 확장 처리기 toohello 최신 버전으로의 리소스 관리자 tooenable tooAzure hello AutoUpdate 스위치 추가 되었습니다. 이 매개 변수는 hello 잠재적인 toocause 참고 hello 새 버전의 hello WMF 해제 될 때 VM에 다시 부팅 합니다. 

## <a name="azure-portal-functionality"></a>Azure 포털 기능
Tooa VM을 이동 합니다. 설정 -> 일반에서 "확장"을 클릭합니다. 새 창을 만듭니다. "추가"를 클릭하고 PowerShell DSC를 선택합니다.

hello 포털에 입력을 해야합니다.
**구성 모듈 또는 스크립트**: 이 필드는 필수 필드입니다. 구성 스크립트를 포함 하는.ps1 파일 또는 hello 루트에서.ps1 구성 스크립트 및 hello.zip 내의 모듈 폴더의 모든 종속 리소스와.zip 파일이 필요 합니다. Hello로 만들 수 있습니다 `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet hello Azure PowerShell SDK에에서 포함 합니다. hello.zip 파일이 SAS 토큰을 통해 보안이 유지 하 여 사용자 blob 저장소에 업로드 됩니다. 

**구성 데이터 PSD1 파일**: 이 필드는 선택적 필드입니다. 구성에 필요한.psd1에서 구성 데이터 파일을 사용 하 여이 필드 tooselect 것는 SAS 토큰에 의해 보호 tooyour 사용자 blob 저장소에 업로드 합니다. 

**구성의 모듈 정규화된 이름**: .ps1 파일에는 여러 개의 구성 함수가 있을 수 있습니다. Hello 구성.ps1 스크립트 뒤의 hello 이름을 입력 한 '\' hello 함수의 및 이름 hello 구성 합니다. 예를 들어.ps1 스크립트에서 hello 이름 "configuration.ps1" hello 구성은 "IisInstall"을 입력 합니다.`configuration.ps1\IisInstall`

**구성 인수**: hello 구성 함수는 인수를 사용 하는 경우 hello 형태로 표시 여기에 입력 한 `argumentName1=value1,argumentName2=value2`합니다. PowerShell cmdlet 또는 Resource Manager 템플릿을 통해 구성 인수를 수락하는 방법과는 다른 서식입니다. 

## <a name="getting-started"></a>시작
DSC 구성 문서에는 Azure Vm에서 해당을 시행 하는 hello Azure DSC 확장 합니다. 구성의 간단한 예제가 뒤따릅니다. "IisInstall.ps1"으로 다음과 같이 로컬로 저장합니다.

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

hello 단계 위치 hello IisInstall.ps1 스크립트에 나오는 hello에 VM을 지정 하 고 hello 구성, 실행 상태 다시 보고 합니다.
###<a name="classic-model"></a>클래식 모델
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Azure Resource Manager 모델

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>로깅
로그는 다음에 배치됩니다.

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]

## <a name="next-steps"></a>다음 단계
PowerShell DSC에 대 한 자세한 내용은 [hello PowerShell 설명서 센터를 방문](https://msdn.microsoft.com/powershell/dsc/overview)합니다. 

Hello 검사 [hello DSC 확장에 대 한 Azure Resource Manager 템플릿](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

PowerShell DSC로 관리할 수 있는 toofind 추가 기능 [hello PowerShell 갤러리 찾아보기](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) 자세한 DSC 리소스에 대 한 합니다.

구성으로 중요 한 매개 변수 전달에 대 한 세부 정보를 참조 하십시오. [hello DSC 확장 처리기와 안전 하 게 자격 증명 관리](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

