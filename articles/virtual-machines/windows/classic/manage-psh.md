---
title: "aaaManage Azure PowerShell을 사용 하 여 가상 컴퓨터 | Microsoft Docs"
description: "가상 컴퓨터 관리의 tooautomate 작업을 사용할 수 있는 명령에 알아봅니다."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Azure PowerShell을 사용하여 가상 컴퓨터 관리
> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Hello 리소스 관리자 모델을 사용 하 여 일반적인 PowerShell 명령 참조 [여기](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

많은 작업을 수행할 일 toomanage 각 Vm에 Azure PowerShell cmdlet을 사용 하 여 자동화할 수 있습니다. 이 문서에서는 간단한 작업 및 링크 tooarticles 더 복잡 한 작업에 대 한 hello 명령을 보여 주는 예제 명령을 제공 합니다.

> [!NOTE]
> 아직 설치 하 고 Azure PowerShell을 구성 하지 않은 hello 문서의 지침을 가져올 수 있습니다 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
> 
> 

## <a name="how-toouse-hello-example-commands"></a>어떻게 toouse hello 명령 예입니다.
사용자 환경에 적합 한 텍스트로 명령을 hello hello 텍스트의 일부 tooreplace가 필요 합니다. hello < 및 > 기호 tooreplace 필요한 텍스트를 나타냅니다. Hello 텍스트를 대체 hello 기호를 제거 하지만 원위치에서 hello 인용 부호를 유지 합니다.

## <a name="get-a-vm"></a>VM 확인
자주 사용하게 될 기본 작업입니다. VM에 대 한 tooget 정보를 사용 하, vm에서 작업을 수행 하거나 변수에 출력 toostore를 가져옵니다.

VM hello에 대 한 정보 tooget hello < 및 > 문자를 포함 하 여 hello 따옴표로 모두 교체,이 명령을 실행 합니다.

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

$vm 변수에 출력 toostore hello 실행 합니다.

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Windows 기반 VM tooa 로그온
다음 명령을 실행합니다.

> [!NOTE]
> Hello hello 표시에서 hello 가상 컴퓨터 및 클라우드 서비스 이름을 얻을 수 **Get-azurevm** 명령입니다.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< 드라이브 및 폴더 위치 toostore hello 다운로드 한 RDP 파일, 예: c:\temp >" $localFile $localPath = + "\" + $vmname +".rdp"Get-azureremotedesktopfile- ServiceName $svcName-$vmName LocalPath $localFile 이름-시작
> 
> 

## <a name="stop-a-vm"></a>VM 중지
다음 명령을 실행합니다.

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> VIP (가상 IP) hello 클라우드 서비스는 경우이 매개 변수 tookeep hello를 사용 하 여 해당 클라우드 서비스에서 마지막 VM hello 합니다. <br><br> Hello StayProvisioned 매개 변수를 사용 하는 경우 VM hello에 대 한 청구 여전히 합니다.
> 
> 

## <a name="start-a-vm"></a>VM 시작
다음 명령을 실행합니다.

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>데이터 디스크 연결
이 작업에는 몇 단계가 필요합니다. 먼저, 사용 하 여 hello * * * 추가-AzureDataDisk * * * cmdlet tooadd hello 디스크 toohello $vm 개체입니다. 그런 다음 **Update-azurevm** hello VM의 cmdlet tooupdate hello 구성 합니다.

또한 해야 toodecide tooattach 새 디스크 또는 하나를 포함 하는지 여부를 데이터입니다. 새 디스크에 대 한 hello 명령 hello.vhd 파일을 만들어 연결 합니다.

새 디스크 tooattach이 명령을 실행 합니다.

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

기존의 데이터 디스크를 tooattach이 명령을 실행 합니다.

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach 데이터 디스크 blob 저장소에 기존.vhd 파일에서이 명령을 실행 합니다.

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Windows 기반 VM 만들기
새 Windows 기반 가상 컴퓨터를 azure에서의 지침을 사용 하 여 hello toocreate [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](create-powershell.md)합니다. 이 항목의 단계 hello 생성 된 Azure PowerShell 명령 집합을 통해을 만듭니다 Windows 기반 VM을 미리 구성할 수 있습니다.

* Active Directory 도메인 구성원 자격을 통해 만들기
* 추가 디스크를 통해 만들기
* 기존 부하 분산 집합의 구성원으로 만들기
* 고정 IP 주소로 만들기

