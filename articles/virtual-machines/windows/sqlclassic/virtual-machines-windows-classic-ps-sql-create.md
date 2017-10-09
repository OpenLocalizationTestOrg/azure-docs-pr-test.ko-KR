---
title: "Azure PowerShell (클래식)에서 SQL Server 가상 컴퓨터 aaaCreate | Microsoft Docs"
description: "SQL Server 가상 컴퓨터 갤러리 이미지를 사용하여 Azure VM을 만드는 단계 및 PowerShell 스크립트를 제공합니다. 이 항목 hello 클래식 배포 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Azure PowerShell을 사용하여 SQL Server 가상 컴퓨터 프로비전(클래식)

이 문서는 어떻게 사용 하 여 Azure에서 SQL Server 가상 컴퓨터 toocreate hello PowerShell cmdlet에 대 한 단계를 제공 합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

이 항목의 hello 리소스 관리자 버전을 참조 하십시오. [Azure PowerShell 리소스 관리자를 사용 하 여 SQL Server 가상 컴퓨터를 프로 비전](../sql/virtual-machines-windows-ps-sql-create.md)합니다.

### <a name="install-and-configure-powershell"></a>PowerShell 설치 및 구성:
1. Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.
2. [다운로드 및 설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview)합니다.
3. Windows PowerShell을 시작 하 고 hello로 tooyour Azure 구독을 연결 **Add-azureaccount** 명령입니다.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>대상 Azure 지역 확인

SQL Server 가상 컴퓨터를 특정 Azure 지역에 있는 클라우드 서비스에서 호스트합니다. hello 다음 단계는 데 도움이 있습니다 toodetermine 지역, 저장소 계정 및 클라우드 서비스는 hello 자습서의 나머지 부분 hello에 사용 됩니다.

1. Hello 데이터 센터 되도록 toouse toohost SQL Server VM을 확인 합니다. 다음 PowerShell 명령을 hello 사용 가능한 지역 이름 목록을 표시 합니다.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. 사용자의 기본 위치를 식별 한 후 설정 이라는 변수에 **$dcLocation** toothat 영역입니다. 예를 들어 다음 명령을 집합 hello 지역 너무 hello "미국 동부":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>구독 및 저장소 계정 설정

1. Hello hello 새 가상 컴퓨터에 사용할 Azure 구독을 확인 합니다.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. 할당 대상 Azure 구독 toohello **$subscr** 변수입니다. 그런 다음 이를 현재 Azure 구독으로 설정합니다.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. 기존 저장소 계정을 확인합니다. hello 다음 스크립트를 표시 선택한 지역에 있는 모든 저장소 계정:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > 필요한 경우 새 저장소 계정, 모든 소문자 저장소 계정 이름을 먼저 hello 다음 예제와 같이 hello AzureStorageAccount 새로 만들기 명령을 사용 하 여 만듭니다.`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Hello 대상 저장소 계정 이름 toohello 할당 **$staccount**합니다. 다음 사용 하 여 **집합 AzureSubscription** tooset hello 구독 및 현재 저장소 계정입니다.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>SQL Server 가상 컴퓨터 이미지를 선택합니다.

1. Hello hello 갤러리에서 사용 가능한 SQL Server 가상 컴퓨터 이미지 목록을 확인할 수 있습니다. 이러한 모든 이미지에는 "SQL"로 시작하는 **ImageFamily** 속성이 있습니다. hello 다음 쿼리 표시 hello 이미지 패밀리 사용 가능한 tooyou SQL Server 사전 설치 되어 있습니다.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Hello 가상 컴퓨터 이미지 제품군을 찾을 때에이 제품군의 게시 된 이미지가 여러 개 나타날 수 있습니다. 사용 하 여 hello 다음 toofind hello 최신 게시 된 가상 컴퓨터 이미지 이름을 선택한 이미지 제품군에 대 한 스크립트 (예: **Windows Server 2012 r 2에서 SQL Server 2016 RTM Enterprise**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Hello 가상 컴퓨터 만들기

마지막으로, powershell hello 가상 컴퓨터를 만듭니다.

1. 클라우드 만들기 서비스 toohost hello 새 VM입니다. Note 수 있다는 것은 가능한 toouse 기존 클라우드 서비스 대신 합니다. 새 변수를 만듭니다 **$svcname** hello hello 클라우드 서비스의 짧은 이름을 사용 합니다.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Hello 가상 컴퓨터 이름 및 크기를 지정 합니다. 가상 컴퓨터 크기에 대한 자세한 내용은 [Azure에 대한 가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Hello 로컬 관리자 계정 및 암호를 지정 합니다.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Hello 스크립트 toocreate hello 가상 컴퓨터를 다음을 실행 합니다.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> 자세한 설명 및 구성 옵션에 대 한 참조 hello **명령 집합을 작성** 섹션 [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="example-powershell-script"></a>PowerShell 스크립트 예

hello 다음 스크립트의 예제를 제공을 만드는 전체 스크립트는 **Windows Server 2012 r 2에서 SQL Server 2016 RTM Enterprise** 가상 컴퓨터. 이 스크립트를 사용 하는 경우이 항목의 hello 이전 단계에 기반 하는 hello 초기 변수 사용자 지정 해야 합니다.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>원격 데스크톱을 사용하여 연결

1. 이러한 가상 컴퓨터 toocomplete 설치 hello 현재 사용자의 문서 폴더 toolaunch에 hello RDP 파일을 만듭니다.

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. Hello documents 디렉터리에 hello RDP 파일을 시작 합니다. 이전 제공한 hello 관리자 사용자 이름 및 암호를 사용 하 여 연결 (예를 들어 사용자 이름이 VMAdmin 되었으면 "\VMAdmin" hello 사용자로 지정 하 고 hello ¾ ï è).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Hello 원격 액세스를 위한 SQL Server 컴퓨터의 전체 hello 구성

원격 데스크톱을 사용 하 여 toohello 컴퓨터를 로그온 한 후의 hello 지침에 따라 SQL Server 구성 [Azure VM에서 SQL Server 연결을 구성 하기 위한 단계](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)합니다.

## <a name="next-steps"></a>다음 단계

Hello에서 PowerShell 사용한 가상 컴퓨터를 프로 비전 하기 위한 추가 지침을 찾을 수 [가상 컴퓨터 설명서](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

대부분의 경우에서 hello 다음 단계는 toomigrate 데이터베이스 toothis 새 SQL Server VM입니다. 데이터베이스 마이그레이션 지침 참조 [데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)합니다.

또한 hello Azure 포털 toocreate SQL 가상 컴퓨터를 사용 하 여에 관심이 있다면 참조 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](../sql/virtual-machines-windows-portal-sql-server-provision.md)합니다. PowerShell 여기에 사용 되는 hello 클래식 모델 보다는 권장 되는 리소스 관리자 모델 워크를 사용 하 여 Vm을 만듭니다 hello 포털을 통해 있습니다 hello는 해당 hello 자습서를 note 합니다.

또한 toothese 리소스 좋습니다 검토는 [toorunning Azure 가상 컴퓨터의 SQL Server과 관련 된 다른 항목](../sql/virtual-machines-windows-sql-server-iaas-overview.md)합니다.
