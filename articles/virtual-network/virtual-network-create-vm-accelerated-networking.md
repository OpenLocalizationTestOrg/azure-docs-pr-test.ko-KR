---
title: "aaaCreate 네트워킹이 Accelerated Azure 가상 컴퓨터 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 네트워킹이 가속화 됩니다. 가상 컴퓨터."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>가속화된 네트워킹을 사용하는 가상 컴퓨터 만들기

이 자습서에 설명 어떻게 toocreate 네트워킹이 Accelerated Azure 가상 컴퓨터 (VM). 가속화된 네트워킹은 Windows용 GA이고 특정 Linux 배포를 위한 공개 미리 보기로 제공됩니다. 가속된 네트워킹 단일 루트 I/O 가상화 (SR-IOV) tooa 네트워킹 성능을 크게 향상 VM을 사용 합니다. 이 성능 우선 경로 대기 시간, 지터, 및 지원 되는 VM 형식에 대 한 hello 가장 까다로운 네트워크 작업에 사용할 CPU 사용률 줄이기 hello 데이터 경로에서 호스트의 hello를 무시 합니다. hello와 가속된 네트워킹 없는 두 가상 컴퓨터 (VM) 간의 그림 표시 통신 다음:

![비교](./media/virtual-network-create-vm-accelerated-networking/image1.png)

가속된 네트워킹 없이 hello VM 내부 및 외부의 모든 네트워킹 트래픽 hello 호스트 및 가상 스위치 hello 트래버스해야 합니다. 예: 네트워크 보안 그룹으로 액세스 제어 목록, 격리 및 기타 가상화 된 네트워크 서비스 toonetwork 트래픽의 hello 가상 스위치 모든 정책 적용을 제공 합니다. 가상 스위치, hello 읽기에 대 한 자세한 toolearn [Hyper-v 네트워크 가상화 및 가상 스위치](https://technet.microsoft.com/library/jj945275.aspx) 문서.

가속 네트워킹 네트워크 트래픽을 hello VM의 네트워크 인터페이스 (NIC)에 도착 하 고 toohello VM 전달 됩니다. 가속된 네트워킹 오프 로드 되어 하드웨어에 적용 하지 않고 hello 가상 스위치는 모든 네트워크 정책에 적용 됩니다. 하드웨어 사용 hello NIC tooforward에 정책을 적용 네트워크 트래픽을 직접 toohello VM을 hello 호스트에 적용 되는 모든 hello 정책을 유지 하면서 hello 호스트 및 hello 가상 스위치를 무시 합니다.

hello 가속화 된 네트워킹의 이점만 적용 toohello VM에서 사용 하 합니다. 이상적인 tooenable hello 최상의 결과 두 개 이상의 Vm에서이 기능은 연결 toohello 동일한 Azure 가상 네트워크 (VNet). Vnet 또는 연결 온-프레미스에서 통신,이 기능에 영향을 최소화 toooverall 대기 시간에 있습니다.

> [!WARNING]
> 일반적 가용성 해제 된이 Linux 공개 미리 보기에는 동일한 수준의 가용성 및 안정성 기능으로 hello를 사용할 수 없습니다. hello 기능은 지원 되지 않습니다, 기능, 제한 있을 수 있습니다 및 모든 Azure 위치에서 사용할 수 없습니다. 가용성 및이 기능의 상태에 최신 알림 hello에 대 한 hello Azure 가상 네트워크 업데이트 페이지를 확인 합니다.

## <a name="benefits"></a>이점
* **대기 시간이 / 높은 패킷 / 초 (pps):** hello 데이터 경로에서 제거 하는 hello 가상 스위치 정책 처리에 대 한 hello 호스트에 패킷을 보내는 hello 시간과 제거 하 고 증가 hello hello VM 내에 처리할 수 있는 패킷 수입니다.
* **지터 감소:** 가상 스위치 처리 toobe 적용 해야 하는 정책의 hello 양과 hello 처리를 수행 하는 hello CPU의 hello 작업량에 따라 달라 집니다. Hello 정책 적용 toohello 하드웨어 오프 로드 toohello VM을 제거 하는 hello tooVM 통신을 호스트 하 고 모든 소프트웨어 인터럽트 및 컨텍스트 전환 직접 패킷을 전달 하 여 해당 가변성을 제거 합니다.
* **CPU 사용률 감소:** 무시 hello hello 호스트에서 가상 스위치에 네트워크 트래픽 처리에 대 한 CPU 사용률 tooless 잠재 고객 합니다.

## <a name="Limitations"></a>제한 사항
다음과 같은 제한을 hello이이 기능을 사용 하는 경우 존재 합니다.

* **네트워크 인터페이스 만들기:** 가속화된 네트워킹은 새 NIC에서만 사용할 수 있으며, 기존 NIC에서는 사용할 수 없습니다.
* **VM 만들기:** A 인 NIC와 가속된 네트워킹 사용 수만 때 hello 첨부 tooa VM 수 VM이 생성 됩니다. hello NIC VM을 기존 연결 된 tooan 일 수 없습니다.
* **지역:** 가속화된 네트워킹 기능을 갖춘 Windows VM은 대부분의 Azure 지역에서 제공됩니다. 가속화된 네트워킹 기능을 갖춘 Linux VM은 여러 지역에서 제공됩니다. hello 지역에서 사용할 수 있는이 기능을 확장 합니다. Hello 최신 정보에 대 한 아래 hello Azure 가상 네트워킹 업데이트가 블로그를 참조 하십시오.   
* **지원되는 운영 체제:** Windows: Microsoft Windows Server 2012 R2 Datacenter 및 Windows Server 2016. Linux: Ubuntu Server 16.04 LTS(커널 4.4.0-77 이상), SLES 12 SP2, RHEL 7.3 및 CentOS 7.3(“Rogue Wave Software”에 의해 게시됨).
* **VM 크기:** 8개 이상의 코어가 있는 범용 및 계산 용도로 최적화된 인스턴스 크기입니다. 자세한 내용은 참조 hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 및 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM의 문서 크기를 조정 합니다. hello 지원 되는 VM 인스턴스 크기 집합 확장 hello 앞에 있습니다.
* **ARM(Azure Resource Manager)을 통한 배포:** 가속화된 네트워킹은 ASM/RDFE를 통해 배포할 수 없습니다.

Hello를 통해 변경 내용을 toothese 제한 사항에 발표 됩니다 [업데이트 Azure 가상 네트워킹이](https://azure.microsoft.com/updates/accelerated-networking-in-preview) 페이지.

## <a name="create-a-windows-vm"></a>Windows VM 만들기
Hello Azure 포털 또는 Azure를 사용할 수 있습니다 [PowerShell](#windows-powershell) toocreate hello VM입니다.

### <a name="windows-portal"></a>포털

1. 인터넷 브라우저를 열고 Azure hello [포털](https://portal.azure.com) 및 Azure 사용 하 여 로그인 [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다. 아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.
2. Hello 포털에서 클릭 **+ 새로 만들기** > **계산** > **Windows Server 2016 Datacenter**합니다. 
3. Hello에 **Windows Server 2016 Datacenter** leave 나타나는 블레이드 *리소스 관리자* 아래에서 선택한 **배포 모델을 선택**를 클릭 하 고 **만들기** .
4. Hello에 **기본 사항** 나타나는 블레이드 hello 다음 값을 입력 hello 남아 있는 기본 옵션 또는 선택 하거나 사용자 고유의 값을 입력을 클릭 hello **확인** 단추:

    |설정|값|
    |---|---|
    |이름|MyVm|
    |리소스 그룹|**새로 만들기**를 선택한 채로 두고 *MyResourceGroup*을 입력합니다.|
    |위치|미국 서부 2|

    새 tooAzure 인 경우에 대해 자세히 알아보세요 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), 및 [위치](https://azure.microsoft.com/regions) (또한 않는 tooas 영역 함).
5. Hello에 **크기를 선택** 나타나는 블레이드 입력 *8* hello에 **최소 코어** 클릭 한 다음 상자 **모든 보기**합니다.
6. 클릭 **DS4_V2 표준**, 또는 지원 되는 모든 VM, 클릭 hello **선택** 단추입니다.
7. Hello에 **설정** 나타나는 블레이드 유지 된 모든 설정-클릭 제외 하 고는 **Enabled** 아래 **네트워킹 Accelerated**, hello 클릭 **확인** 단추입니다. **참고:** , 이전 단계에서 선택 하는 경우 VM 크기, 운영 체제 또는 위치에 대 한 hello에는 없지만 값 [제한](#Limitations) 이 문서의 섹션 **가속 네트워킹**표시 되지 않습니다.
8. Hello에 **요약** 블레이드를 놓고 클릭 hello **확인** 단추입니다. Azure는 hello VM 만들기를 시작 합니다. VM을 만드는 데 몇 분이 걸립니다.
9. Windows 네트워킹 드라이버 가속 tooinstall hello, hello에서 단계를 완료 하는 hello [Windows 구성](#configure-windows) 이 문서의 섹션.

### <a name="windows-powershell"></a>PowerShell
1. Hello 최신 버전의 hello Azure PowerShell 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 hello 읽을 [Azure PowerShell 개요](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.
2. Hello Windows 시작 단추를 클릭 하 여 PowerShell 세션을 시작 합니다. 입력 **powershell**를 클릭 한 다음 **PowerShell** hello 검색 결과에서 합니다.
3. PowerShell 창에 입력 hello `login-azurermaccount` Azure 사용 하 여 명령 toosign [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다. 아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.
4. 브라우저에서 다음 스크립트는 hello를 복사 합니다.
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. PowerShell 창에 toopaste hello 스크립트를 마우스 오른쪽 단추로 클릭 하 고 실행 되기 시작 합니다. 사용자 이름과 암호를 묻는 메시지가 나타납니다. Tooit hello 다음 단계에 연결할 때 이러한 자격 증명 toolog toohello VM에서에서 사용 합니다. Hello 스크립트 실패 실행 되기 전에 hello 스크립트의 값을 변경 하는 경우 VM 크기, 운영 체제에 사용 된 hello 값을 확인 하 고 hello 위치 같습니다 [제한](#Limitations) 이 문서의 섹션.
6. Windows 네트워킹 드라이버 가속 tooinstall hello, hello에서 단계를 완료 하는 hello [Windows 구성](#configure-windows) 이 문서의 섹션.

### <a name="configure-windows"></a>Windows 구성
Azure의 hello VM을 만든 후에 Windows 용 hello 가속된 네트워킹 드라이버를 설치 해야 합니다. Hello 다음 단계를 완료 하기 전에 만들었어야 Windows VM 중 하나가 hello를 사용 하 여 가속 네트워킹 [포털](#windows-portal) 또는 [PowerShell](#windows-powershell) 이 문서의 단계입니다. 

1. 인터넷 브라우저를 열고 Azure hello [포털](https://portal.azure.com) 및 Azure 사용 하 여 로그인 [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다. 아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *MyVm*합니다. 때 **MyVm** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **MyVm** 블레이드를 놓고 클릭 hello **연결** hello 왼쪽된 위 모서리의 hello 블레이드의 단추입니다. **참고:** 경우 **만들기** hello 아래에 표시 되 **연결** 단추, Azure가 아직 완료 되지 hello VM 만들기. 클릭 **연결** 더 이상 참조 한 후에 **만들기** hello에서 **연결** 단추입니다.
4. 브라우저 toodownload hello 허용 **MyVm.rdp** 파일입니다.  를 다운로드 한 후 클릭 hello 파일 tooopen 것입니다. 
5. Hello 클릭 **연결** hello 단추 **원격 데스크톱 연결** 상자가 표시 되 면 사용자에 게 알리는 hello 해당의 hello 원격 연결 게시자를 식별할 수 없습니다.
6. Hello에 **Windows 보안** 상자가 표시 되 면 클릭 **추가 선택 사항을**, 클릭 **다른 계정을 사용 하 여**합니다. Hello 사용자 이름 및 4 단계에서 입력 한 암호를 입력 한 다음 hello 클릭 **확인** 단추입니다.
7. Hello 클릭 **예** 단추 hello 원격 데스크톱 연결 나타나는 상자에서 사용자에 게 알리는 hello 원격 컴퓨터의 hello id를 확인할 수 없습니다.
8. Hello Windows 시작 단추를 마우스 오른쪽 단추로 클릭 하 고 클릭 **장치 관리자**합니다. Hello 확장 **네트워크 어댑터가** 노드. 해당 hello 확인 **함수 가상 이더넷 어댑터 Mellanox ConnectX 3** hello 다음 그림에에서 나와 있는 것 처럼 나타납니다.
   
    ![장치 관리자](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. 이제 가속화된 네트워킹을 VM에 사용할 수 있습니다.

## <a name="create-a-linux-vm"></a>Linux VM 만들기
Hello Azure 포털 또는 Azure를 사용할 수 있습니다 [PowerShell](#linux-powershell) toocreate Ubuntu 또는 SLES VM입니다. RHEL 및 CentOS VM의 경우 다른 워크플로가 있습니다.  아래의 hello 지침을 참조 하십시오.

### <a name="linux-portal"></a>포털
1. Hello의 1-5 단계를 완료 하 여 Linux 미리 보기에 대 한 네트워킹 accelerated hello에 대 한 레지스터 [PowerShell Linux VM-생성](#linux-powershell) 이 문서의 섹션.  Hello 포털에서 hello 미리 보기에 등록할 수 없습니다.
2. 에 hello 1-8 단계를 완료 [Windows VM-만듭니다 포털](#windows-portal) 이 문서의 섹션. 2단계에서 **Windows Server 2016 Datacenter** 대신 **Ubuntu Server 16.04 LTS**를 클릭합니다. 이 자습서에 대 한 선택 toouse SSH 키 대신 암호를 있지만 프로덕션 배포에 사용할 수 있습니다. 경우 **네트워킹 Accelerated** hello의 7 단계를 완료 하면 나타나지 않으면 [Windows VM-생성 포털](#windows-portal) 섹션이 문서의 될 hello 다음 이유 중 하나에 대해:
    - 사용자 등록 되지 않은 아직 hello 미리 보기에 대 한 합니다. 등록 상태 인지 확인 **등록 된**hello의 4 단계에서 설명한 것 처럼, [Powershell Linux VM-생성](#linux-powershell) 이 문서의 섹션. **참고:** 가속 hello에 참여 하는 경우 (해당 없음 긴 필요한 tooregister toouse Accelerated Windows Vm에 적합 한 네트워킹)를 Windows Vm 미리 보기에 대 한 네트워킹 하지 자동으로 등록 가속 hello에 대 한 네트워킹 Linux Vm의 경우 미리 보기입니다. Linux Vm에 tooparticipate 미리 보기에 대 한 hello 가속 네트워킹에 대 한 등록 해야 합니다.
    - VM 크기, 운영 체제 또는 hello에 나열 된 위치를 선택 하지 않은 [제한](#limitations) 이 문서의 섹션.
3. tooinstall hello Linux에 대 한 네트워킹 드라이버 accelerated, hello에서 단계를 완료 하는 hello [구성 Linux](#configure-linux) 이 문서의 섹션.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>가속 네트워킹 구독에서 Linux Vm을 만들고 다음 toocreate 가속화 된 네트워킹의 hello 사용 하 여 Windows VM을 시도 하는 경우 동일한 구독 hello Windows VM을 만들 실패할 수 있습니다. 이 미리 보기에서는 가속화된 네트워킹을 사용하는 Linux VM과 Windows VM을 별도의 구독에서 테스트하는 것이 좋습니다.
>

1. Hello 최신 버전의 hello Azure PowerShell 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 hello 읽을 [Azure PowerShell 개요](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.
2. Hello Windows 시작 단추를 클릭 하 여 PowerShell 세션을 시작 합니다. 입력 **powershell**를 클릭 한 다음 **PowerShell** hello 검색 결과에서 합니다.
3. PowerShell 창에 입력 hello `login-azurermaccount` Azure 사용 하 여 명령 toosign [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다. 아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.
4. Azure에 대 한 네트워킹 accelerated hello에 대 한 레지스터 hello 다음 단계를 완료 하 여 미리 보기:
    - 너무 전자 메일을 보내[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) 는 Azure 구독 ID로, 의도 된 용도입니다. Microsoft에서 보내는 구독 활성화에 대한 메일 확인을 기다려 주세요.
    - Hello 명령 tooconfirm hello 미리 보기에 등록 된 다음을 입력 합니다.
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        5 단계까지 진행 하지 마십시오 **등록 된** hello hello 이전 명령을 입력 한 후 출력에 나타납니다. 출력은 hello 다음 계속 하기 전에 출력 같이 표시 해야 합니다.
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >가속 hello에 참여 하는 경우 (해당 없음 긴 필요한 tooregister toouse Accelerated Windows Vm에 적합 한 네트워킹)를 Windows Vm 미리 보기에 대 한 네트워킹 하면 등록 되지 않은 자동으로 가속 hello에 대 한 Linux Vm의 경우 미리 보기에 대 한 네트워킹 합니다. Linux Vm에 tooparticipate 미리 보기에 대 한 hello 가속 네트워킹에 대 한 등록 해야 합니다.
      >
5. 브라우저에서 hello 다음 원하는 대로 Ubuntu 또는 SLES 대체 하 여 스크립트를 복사 합니다.  또한 Redhat 및 CentOS에는 아래에서 간략하게 설명되는 다른 워크플로가 있습니다.

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. PowerShell 창에 toopaste hello 스크립트를 마우스 오른쪽 단추로 클릭 하 고 실행 되기 시작 합니다. 사용자 이름과 암호를 묻는 메시지가 나타납니다. Tooit hello 다음 단계에 연결할 때 이러한 자격 증명 toolog toohello VM에서에서 사용 합니다. Hello 스크립트에 실패 하면 있는지 확인 합니다.
    - 4 단계에서 설명한 것 처럼 hello 미리 보기에 등록 된
    - VM 크기, 운영 체제 유형 또는 위치 값 hello 스크립트에서 실행 되기 전에 변경 하는 경우, hello 값 hello에 나열 됩니다 [제한](#Limitations) 이 문서의 섹션.
7. tooinstall hello Linux에 대 한 네트워킹 드라이버 accelerated, hello에서 단계를 완료 하는 hello [구성 Linux](#configure-linux) 이 문서의 섹션.

### <a name="configure-linux"></a>Linux 구성

Azure의 hello VM을 만든 후에 Linux 용 hello 가속된 네트워킹 드라이버를 설치 해야 합니다. Hello 다음 단계를 완료 하기 전에 만들었어야 Linux VM 중 하나가 hello를 사용 하 여 가속 네트워킹 [포털](#linux-portal) 또는 [PowerShell](#linux-powershell) 이 문서의 단계입니다. 

1. 인터넷 브라우저를 열고 Azure hello [포털](https://portal.azure.com) 및 Azure 사용 하 여 로그인 [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다. 아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.
2. Hello hello 포털 toohello 오른쪽의 hello 위쪽 *리소스 검색* 막대에서 클릭 hello **> _** 아이콘 toostart Bash 클라우드 셸 (미리 보기). hello Bash 클라우드 셸 창이 표시 하 고 몇 초 후 hello 포털의 hello 맨 아래에 표시 된  **username@Azure:~ $** 프롬프트입니다. Hello 클라우드 셸 대신 컴퓨터에서 SSH toohello VM 수 있지만이 자습서에서는 hello 지침 hello 클라우드 셸을 사용 하는 것을 가정 합니다.
3. Hello 포털의 hello 위쪽 hello 상자에 텍스트가 포함 된 hello *리소스 검색*, 형식 *MyVm*합니다. 때 **MyVm** 나타납니다 hello 검색 결과에를 클릭 합니다.
4. Hello에 **MyVm** 블레이드를 놓고 클릭 hello **연결** hello 왼쪽된 위 모서리의 hello 블레이드의 단추입니다. **참고:** 경우 **만들기** hello 아래에 표시 되 **연결** 단추, Azure가 아직 완료 되지 hello VM 만들기. 클릭 **연결** 더 이상 참조 한 후에 **만들기** hello에서 **연결** 단추입니다.
5. Azure tooenter hello 알려 상자를 엽니다. `ssh adminuser@<ipaddress>`합니다. 이 명령은 hello 클라우드 셸 (또는 복사에 4 단계에서 표시 된 hello 상자 고 toohello 클라우드 셸에서 붙여), Enter에는 다음 Enter를 누릅니다.
6. Enter **예** toocontinue 연결 하려는 경우 다음 Enter 키를 누르면 요청 toohello 질문 합니다.
7. Hello VM을 만들 때 입력 한 hello 암호를 입력 합니다. Toohello VM에에서 로그온 했습니다. 한 번 표시는 adminuser@MyVm:~ $ 프롬프트입니다. Hello 클라우드 셸 세션을 통해 VM toohello 이제 로그인 됩니다. **참고:** 클라우드 셸 세션을 10분 동안 사용하지 않으면 시간이 초과됩니다.

이 시점에서 hello 명령을 사용 하는 hello 배포에 따라 다릅니다. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. Hello 프롬프트에서 입력 `uname -r` hello 버전을 확인 합니다.

    * Ubuntu는 "4.4.0-77-generic" 이상임
    * SLES는 "4.4.59-92.20-default" 이상임

2. 다음에 나오는 실행 중인 hello 명령을 사용 하 여 hello 표준 네트워킹 vNIC 사이의 accelerated hello 네트워킹 vNIC 채권을 만듭니다. 네트워크 트래픽은 hello 채권 특정 구성 변경 내용은 간에 네트워킹 트래픽은 중단 되지 않도록 보장 하는 동안에 가속화 된 네트워킹 vNIC를 성능이 높은 hello를 사용 합니다.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Hello 스크립트를 실행 한 후 VM hello 60 초 일시 중지 한 후 다시 시작 됩니다.
4. 한 번 VM이 다시 시작 하는 hello tooit 다시 5-7 단계를 완료 하 여 다시 연결 합니다.
5. Hello 실행 `ifconfig` 명령 및 bond0가 들어온 고 hello 인터페이스 위쪽으로 표시 되었는지 확인 합니다. 
 
 >[!NOTE]
      >가속된 네트워킹을 사용 하 여 응용 프로그램 hello를 통해 통신 해야 *bond0* 되지 않은 인터페이스 *eth0*합니다.  가속된 네트워킹 일반 공급 전에 hello 인터페이스 이름이 변경 될 수 있습니다.

#### <a name="rhelcentos"></a>RHEL/CentOS

Red Hat Enterprise Linux 또는 CentOS 7.3 VM 만드는 몇 가지 추가 단계를 hello VF (가상 함수) hello 네트워크 카드 드라이버 및 SR-IOV에 필요한 tooload hello 최신 드라이버 필요 합니다. hello hello 지침의 첫 번째 단계는 이미지 준비 toomake 사용된 될 수 있는 hello 드라이버가 미리 로드 되어 하나 이상의 가상 컴퓨터.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>1단계: Red Hat Enterprise Linux 또는 CentOS 7.3 기본 이미지를 준비합니다. 

1.  Azure에서 비SRIOV CentOS 7.3 VM 프로비전

2.  LIS 4.2.2를 설치합니다.
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  구성 파일을 다운로드합니다.
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  이 VM의 프로비전 해제

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Azure 포털에서이 VM; 중지 및 "디스크" tooVM의, hello os 디스크 VHD URI를 캡처하십시오. 이 URI는 hello 기본 이미지의 VHD 이름 및 해당 저장소 계정을 포함합니다. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>2단계: Azure에서 새 VM 프로비전

1.  새 Vm 기반 새로 AzureRMVMConfig을 프로 비전 기본 이미지 AcceleratedNetworking hello vNIC에서 사용 하도록 설정 된, 1 단계에서 캡처된 VHD hello를 사용 하 여:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Vm 부팅 한 후 "lspci" 하 여 hello VF 장치를 확인 하 고 hello Mellanox 항목을 확인 합니다. 예를 들어 hello lspci 출력에서이 항목의 확인할:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Hello 결합 스크립트를 실행 합니다.

    ```bash
    sudo bondvf.sh
    ```

4.  다시 부팅 새 Vm hello:

    ```bash
    sudo reboot
    ```

hello VM bond0 구성 및 사용 하도록 설정 하는 네트워킹 Accelerated 경로 hello로 시작 해야 합니다.  실행 `ifconfig` tooconfirm 합니다.
