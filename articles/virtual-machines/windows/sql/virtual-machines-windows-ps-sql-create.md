---
title: "Azure PowerShell (리소스 관리자)에서 SQL Server 가상 컴퓨터 aaaCreate | Microsoft Docs"
description: "SQL Server 가상 컴퓨터 갤러리 이미지를 사용하여 Azure VM을 만드는 단계 및 PowerShell 스크립트를 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Azure PowerShell(리소스 관리자)을 사용하여 SQL Server 가상 컴퓨터 프로비전
> [!div class="op_single_selector"]
> * [포털](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>개요
이 자습서에서는 방법을 사용 하 여 Azure 가상 컴퓨터를 단일 toocreate hello **Azure 리소스 관리자** Azure PowerShell cmdlet을 사용 하 여 배포 모델입니다. 이 자습서에서는 hello SQL 갤러리에서에서 이미지에서 단일 디스크 드라이브를 사용 하 여 단일 가상 컴퓨터를 만듭니다. Hello 저장소, 네트워크 및 hello 가상 컴퓨터에서 사용할 수 있는 계산 리소스에 대 한 새 공급자를 만듭니다. 이러한 리소스에 대한 기존 공급자가 있는 경우 대신 이러한 공급자를 사용할 수 있습니다.

이 항목의 클래식 버전 hello 필요, 참조 [Azure PowerShell 클래식을 사용 하 여 SQL Server 가상 컴퓨터를 프로 비전](../classic/ps-sql-create.md)합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서에는 다음이 필요합니다.

* 시작하기 전에 Azure 계정 및 구독. 없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.
* [Azure PowerShell](/powershell/azure/overview), 최소 버전 1.4.0 이상(이 자습서는 1.5.0 버전을 사용하여 작성)
  * tooretrieve 버전, 형식 **Azure Get-module-ListAvailable**합니다.

## <a name="configure-your-subscription"></a>구독 구성
Windows PowerShell을 열고 Azure 계정 액세스 tooyour hello 다음 cmdlet을 실행 하 여 설정 합니다. 나타납니다 화면 tooenter 로그인과 자격 증명입니다. 사용 하 여 hello 동일한 전자 메일 및 toosign toohello Azure 포털에서에서 사용 하는 암호입니다.

    Add-AzureRmAccount

성공적으로 로그인 한 후에 로그인 하는 hello 구독 Id를 포함 하는 화면에 일부 정보가 나타납니다. 이 자습서에 대 한 hello 리소스 생성 시 사용할 tooa 다른 구독을 변경 하지 않는 한 hello 구독입니다. 여러 SubscriptionIds를 설정한 경우 모든 사용자 SubscriptionIds의 목록을 hello cmdlet tooreturn 다음 실행 합니다.

    Get-AzureRmSubscription

toochange tooanother SubscriptionID, hello 뒤에 원하는 구독 Id 사용 하 여 cmdlet을 실행 합니다.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>이미지 변수 정의
toosimplify 유용성 및 이해가이 자습서를 완료 하는 hello 스크립트의 여러 가지 변수를 정의 하 여 시작 하겠습니다. 나타나며, 하지만 제공 된 hello 값을 수정 하는 경우에는 명명 제한 관련된 tooname 길이 및 특수 문자에 유의 hello 매개 변수 값을 변경 합니다.

### <a name="location-and-resource-group"></a>위치 및 리소스 그룹
두 개의 변수 toodefine hello 데이터 영역과 hello 리소스 그룹을 만들게 됩니다 hello hello 가상 컴퓨터에 대 한 기타 리소스를 사용 합니다.

원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>저장소 속성
다음 변수 toodefine hello 저장소 계정 및 hello 유형의 저장소 toobe hello 가상 컴퓨터에서 사용 하는 hello를 사용 합니다.

원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다. 이 예제에서는 프로덕션 워크로드에 권장되는 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다. 이 참고 자료 및 기타 권장 사항에 대한 세부 정보는 [Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>네트워크 속성
Hello 다음 변수 toodefine hello 네트워크 인터페이스, hello TCP/IP 할당 방법, hello 가상 네트워크 이름, hello 가상 서브넷 이름, hello 가상 네트워크에 대 한 hello 범위의 IP 주소, 서브넷 hello 및 hello에 대 한 hello 범위의 IP 주소를 사용 하 여 공용 도메인 이름 레이블 toobe hello 가상 컴퓨터의 hello 네트워크에서 사용 합니다.

원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>가상 컴퓨터 속성
다음 변수 toodefine hello 가상 컴퓨터 이름 "," hello 컴퓨터 이름 "," hello 가상 컴퓨터 크기 "및" hello 가상 컴퓨터에 대 한 hello 운영 체제 디스크 이름을 hello를 사용 합니다.

원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>이미지 속성
다음 변수 toodefine hello 이미지 toouse hello 가상 컴퓨터에 대 한 hello를 사용 합니다. 이 예제에서는 hello SQL Server 2016 Enterprise 이미지가 사용 됩니다.

원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Note hello Get AzureRmVMImageOffer 명령 사용 하 여 SQL Server 이미지 제품의 전체 목록을 가져올 수 있습니다.

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

및 hello hello Get AzureRmVMImageSku 명령 사용 하 여 제공에 대 한 사용 가능한 Sku를 확인할 수 있습니다. hello 다음 명령을 표시 hello에 사용할 수 있는 모든 Sku **SQL2014SP1 WS2012R2** 제공 합니다.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>리소스 그룹 만들기
Hello 리소스 관리자 배포 모델을 만드는 첫 번째 개체를 hello은 hello 리소스 그룹입니다. Hello 사용 하 여 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate Azure 리소스 그룹 및 hello 리소스를 사용 하 여 해당 리소스 그룹 이름 및 이전에 초기화 hello 변수에 의해 정의 된 위치입니다.

다음 cmdlet toocreate hello 새 리소스 그룹을 실행 합니다.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>저장소 계정 만들기
hello 가상 컴퓨터는 hello 운영 체제 디스크 및 hello SQL Server 데이터 및 로그 파일에 대 한 저장소 리소스를 필요합니다. 간단히 하기 위해 둘 다에 대한 단일 디스크를 만듭니다. Hello를 사용 하 여 나중에 추가 디스크를 연결 하면 [추가 Azure 디스크](/powershell/module/azure/add-azuredisk) cmdlet에 주문 tooplace SQL Server 데이터 및 로그 파일은 전용된 디스크에 있습니다. Hello 사용 하 여 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate 표준 저장소 계정을 hello 저장소 계정 이름, 저장소 Sku 이름 및 hello 변수를 사용 하 여 정의 된 위치와 새 리소스 그룹 이전에 초기화 합니다.

새 저장소 계정의 hello cmdlet toocreate 다음을 실행 합니다.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>네트워크 리소스 만들기
hello 가상 컴퓨터는 네트워크 연결을 위한 다양 한 네트워크 리소스를 필요합니다.

* 각 가상 컴퓨터에 가상 네트워크가 필요합니다.
* 가상 네트워크에는 하나 이상의 서브넷이 정의되어 있어야 합니다.
* 네트워크 인터페이스가 공용 또는 개인 IP 주소 중 하나로 정의되어야 합니다.

### <a name="create-a-virtual-network-subnet-configuration"></a>가상 네트워크 서브넷 구성 만들기
가상 네트워크에 대한 서브넷 구성을 만들어 시작합니다. 이 자습서에 대 한 hello를 사용 하 여 기본 서브넷 만듭니다 [새로 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet. 이 가상 네트워크 서브넷 configuration hello 서브넷 이름 및 주소 접두사는 이전에 초기화 hello 변수를 사용 하 여 정의를 만듭니다.

> [!NOTE]
> 이 cmdlet을 사용 하 여 hello 가상 네트워크 서브넷 구성의 추가 속성을 정의할 수 있지만이 자습서의 hello 범위를 벗어납니다.
>
>

가상 서브넷 configuration hello cmdlet toocreate 다음을 실행 합니다.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>가상 네트워크 만들기
다음으로 hello를 사용 하는 가상 네트워크를 만들겠습니다 [새로 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet. 주소 접두사 정의 이전에 초기화 된 hello 변수를 사용 하 고 hello 이전 단계에서 정의 된 hello 서브넷 configuration을 사용 하 여 hello 이름, 위치와 새 리소스 그룹에는 가상 네트워크를 만듭니다.

가상 네트워크가 hello cmdlet toocreate 다음을 실행 합니다.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Hello 공용 IP 주소 만들기
이제는 가상 네트워크를 정의 했으므로 연결 toohello 가상 컴퓨터에 대 한 tooconfigure IP 주소가 필요 합니다. 이 자습서에서는 toosupport 인터넷 연결 주소를 지정 하는 동적 IP를 사용 하 여 공용 IP 주소를 만듭니다. Hello 사용 하 여 [새로 AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello 공용 IP 주소 hello 리소스 그룹을 만들었습니다 prevously 고 hello 이름, 위치, 할당 방법 및 hello를 사용 하 여 정의 하는 DNS 도메인 이름 레이블 이전에 초기화는 변수입니다.

> [!NOTE]
> 추가 속성을이 cmdlet을 사용 하 여 hello 공용 IP 주소를 정의할 수 있지만 초기이 자습서의 hello 범위를 벗어납니다. 고정 주소를 갖는 개인 주소 또는 주소를 만들 수도 수 있지만이 자습서의 hello 범위를 벗어나 그것도입니다.
>
>

공용 IP 주소가 hello cmdlet toocreate 다음을 실행 합니다.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Hello 네트워크 인터페이스 만들기
가상 컴퓨터에서 사용할 준비 toocreate hello 네트워크 인터페이스는 이제입니다. Hello 사용 하 여 [새로 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate hello 이름, 위치, 서브넷 및 공용 IP 주소 앞에서 만든 hello 리소스 그룹에이 네트워크 인터페이스는 이전에 정의 합니다.

다음 cmdlet toocreate hello 해당 네트워크 인터페이스를 실행 합니다.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>VM 개체 구성
이제 저장소 및 네트워크 리소스를 정의 했으므로 hello 가상 컴퓨터에 대 한 준비 toodefine 계산 리소스는 합니다. 이 자습서에 대 한 hello 가상 컴퓨터 크기와 다양 한 운영 체제 속성 지정, 이전에 만든 hello 네트워크 인터페이스 지정, blob 저장소를 정의 하 고 합니다 hello 운영 체제 디스크를 지정 합니다.

### <a name="create-hello-vm-object"></a>Hello VM 개체 만들기
Hello 가상 컴퓨터 크기를 지정 하 여 시작 하겠습니다. 이 자습서의 경우 DS13을 지정합니다. Hello 사용 하 여 [새로 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate 구성 가능한 가상 컴퓨터 개체에 hello 이름 및 크기를 이전에 초기화 하는 hello 변수를 사용 하 여 정의 합니다.

Hello cmdlet toocreate hello 가상 컴퓨터 개체를 다음을 실행 합니다.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>자격 증명 개체 toohold hello 이름 및 암호 hello 로컬 관리자 자격 증명 만들기
Hello 가상 컴퓨터에 대 한 hello 운영 체제 속성을 설정할 수 있습니다, 전에 toosupply hello 자격 증명이 필요 hello 로컬 관리자 계정에 대 한 보안 문자열로 합니다. tooaccomplish이 hello 사용 하 여 [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

Hello 다음 cmdlet을 실행 하 고 hello Windows PowerShell 자격 증명 요청 창에서 이름 및 암호 toouse hello Windows 가상 컴퓨터에서 로컬 관리자 계정 hello에 대 한 hello를 입력 합니다.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Hello 가상 컴퓨터에 대 한 hello 운영 체제 속성 설정
이제는 준비 tooset hello 가상 컴퓨터의 운영 체제 속성입니다. Hello 사용 하 여 [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello Windows 운영 체제 유형을 hello [가상 컴퓨터 에이전트](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 설치 toobe 해당 hello cmdlet을 사용 하면 자동 지정 업데이트 하 고 hello 가상 컴퓨터 이름, hello 컴퓨터 이름 및 이전에 초기화 하는 hello 변수를 사용 하 여 hello 자격 증명을 설정 합니다.

다음과 같은 가상 컴퓨터에 대 한 cmdlet tooset hello 운영 체제 속성 hello를 실행 합니다.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Hello 네트워크 인터페이스 toohello 가상 컴퓨터 추가
다음으로 hello 네트워크 인터페이스는 앞서 만든 toohello 가상 컴퓨터를 추가 합니다. Hello 사용 하 여 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) 앞에서 정의한 hello 네트워크 인터페이스 변수를 사용 하 여 cmdlet tooadd hello 네트워크 인터페이스.

가상 컴퓨터에 대 한 cmdlet tooset hello 네트워크 인터페이스를 수행 하는 hello를 실행 합니다.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Hello 디스크 toobe hello 가상 컴퓨터에서 사용에 대 한 hello blob 저장소 위치 설정
다음으로, 앞에서 정의한 hello 변수를 사용 하 여 hello 가상 컴퓨터에서 사용 하는 hello 디스크 toobe에 대 한 hello blob 저장소 위치를 설정 해 드립니다.

Hello 수정할 수 있는 cmdlet tooset hello blob 저장소 위치를 실행 합니다.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Hello 운영 체제 디스크 속성 hello 가상 컴퓨터에 대 한 설정
다음으로 설정 해 드립니다 hello 운영 체제 디스크 속성 hello 가상 컴퓨터에 대 한 합니다. Hello를 사용 합니다 [집합 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) hello 가상 컴퓨터용 운영 체제 hello cmdlet toospecify 이미지로 tooset tooread만 캐시에서 제공 됩니다 (hello에 SQL Server를 설치 하기 때문에 동일한 디스크) 및 정의 hello 가상 컴퓨터 이름과 hello 운영 체제 디스크는 앞에서 정의한 hello 변수를 사용 하 여 정의 합니다.

다음과 같은 가상 컴퓨터에 대 한 cmdlet tooset hello 운영 체제 디스크 속성 hello를 실행 합니다.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Hello 가상 컴퓨터에 대 한 hello 플랫폼 이미지를 지정 합니다.
수행할 마지막 구성 단계는 가상 컴퓨터에 대 한 toospecify hello 플랫폼 이미지입니다. 이 자습서에 대 한 hello 최신 SQL Server 2016 CTP 이미지를 사용 합니다. Hello 사용 하 여 [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse 앞에서 정의한 hello 변수에 의해 정의 된 대로이 이미지입니다.

가상 컴퓨터에 대 한 cmdlet toospecify hello 플랫폼 이미지를 수행 하는 hello를 실행 합니다.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Hello SQL VM 만들기
이제 hello 구성 단계를 완료 했으면 준비 toocreate hello 가상 컴퓨터는 합니다. Hello 사용 하 여 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 정의한 hello 변수를 사용 하 여 cmdlet toocreate hello 가상 컴퓨터.

다음 cmdlet toocreate hello 가상 컴퓨터를 실행 합니다.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

hello 가상 컴퓨터가 만들어집니다. 공지 hello hello 가상 컴퓨터의 디스크에 대 한 저장소 계정을 지정 하기 때문에 부팅 진단에 대 한 표준 저장소 계정이 만들어졌는지 프리미엄 저장소 계정입니다.

이제 hello Azure 포털 toosee에서이 컴퓨터를 볼 수 있습니다 [공용 IP 주소 및 정규화 된 도메인 이름](virtual-machines-windows-portal-sql-server-provision.md)합니다.

## <a name="example-script"></a>예제 스크립트
hello 다음 스크립트 hello 전체 PowerShell 스크립트를 포함이 자습서에 대 한 합니다. 이 있다고 가정 이미 hello로 설치 hello Azure 구독 toouse **추가 AzureRmAccount** 및 **선택 AzureRmSubscription** 명령입니다.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>다음 단계
Hello 가상 컴퓨터를 만든 후에 설치 프로그램 및 RDP 연결을 사용 하 여 준비 tooconnect toohello 가상 컴퓨터는. 자세한 내용은 참조 [tooa (리소스 관리자) Azure에서 SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.

