---
title: "Azure 가상 컴퓨터에서 네트워크 인터페이스 tooor aaaAdd 제거 | Microsoft Docs"
description: "네트워크 인터페이스 tooor tooadd 가상 컴퓨터에서 네트워크 인터페이스를 제거 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>가상 컴퓨터에서 제거 tooor 네트워크 인터페이스를 추가 합니다.

기존 네트워크 인터페이스 VM을 만들 때 또는에서 추가 하거나 제거할 네트워크 인터페이스 hello에 기존 VM tooadd (할당 취소) 상태를 중지 하는 방법에 대해 알아봅니다. 네트워크 인터페이스에는 인터넷, Azure, 온-프레미스 리소스와는 Azure 가상 컴퓨터 (VM) toocommunicate를 수 있습니다. 하나의 VM에 하나 이상의 네트워크 인터페이스가 있을 수 있습니다. 

변경 또는 제거 하는 네트워크 인터페이스에 대 한 IP 주소 tooadd 해야 할 경우 읽기 hello [네트워크 인터페이스 IP 주소 관리](virtual-network-network-interface-addresses.md) 문서. 변경 또는 삭제할 네트워크 인터페이스, toocreate 해야 할 경우 읽기 hello [네트워크 인터페이스 관리](virtual-network-network-interface.md) 문서.

## <a name="before"></a>시작하기 전에

이 문서의 섹션의 단계를 완료 하기 전에 작업을 수행 하는 hello를 완료 합니다.

- 네트워크 인터페이스 수에 대 한 hello를 검토 하 여 각 Linux 및 Windows VM 크기 지원 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM의 문서 크기를 조정 합니다.
- Toohello Azure에에서 로그인 [포털](https://portal.azure.com), Azure 명령줄 인터페이스 (CLI) 또는 Azure 계정으로 Azure PowerShell. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 이 문서에서는 toocomplete 작업 명령이 PowerShell을 사용 하는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전을 설치 하는 hello Azure PowerShell commandlet의 확인 합니다. 예제를 보려면으로 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- 이 문서에서는 toocomplete 작업 명령을 Azure CLI (명령줄 인터페이스)를 사용 하는 경우 [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com)합니다.

## <a name="about"></a>네트워크 인터페이스 및 VM 정보

추가할 수 있습니다 (연결)는 기존 네트워크 인터페이스 tooa hello 네트워크 인터페이스 현재 제공 hello VM을 만들 때 VM tooanother VM을 연결 합니다. 네트워크 인터페이스를를 추가 하거나 제거할 수 있습니다 (분리)는 네트워크 인터페이스 toofrom 기존의 VM에 VM hello hello에 중지 (할당 취소) 상태 제공 합니다. Hello Azure 포털을 사용 하 여 VM을 만들 hello 포털은 기본 설정을 사용 하 여 네트워크 인터페이스를 만듭니다. hello 포털을 허용 하지 않습니다.

- Hello VM을 만들 때 기존 네트워크 인터페이스 tooadd를 지정 합니다.
- 여러 네트워크 인터페이스를 사용하는 VM 만들기
- Hello 네트워크 인터페이스에 대 한 이름을 지정 (hello 포털 기본 이름으로 hello 네트워크 인터페이스를 생성 하는 데 사용)

Azure PowerShell 또는 CLI toocreate hello 네트워크 인터페이스 또는 VM에 대 한 hello 포털을 사용할 수 없는 모든 hello 이전 특성으로 사용할 수 있습니다. Hello 다음 섹션의에서 hello 태스크를 완료 하기 전에 hello 다음 사항을 고려 제약 조건 및 동작:

- 모든 VM 크기는 두 개 이상의 네트워크 인터페이스를 지원하지만, 일부 VM 크기는 세 개 이상의 네트워크 인터페이스를 지원합니다. 일부 VM 지나서 hello 크기만 하나의 네트워크 인터페이스 지원. toolearn 각 VM 크기를 지 원하는 네트워크 인터페이스를 개수 읽을 hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM의 문서 크기를 조정 합니다. 
- Hello 이전, 네트워크 인터페이스 지원 되는 여러 네트워크 인터페이스를 두 개 이상의 네트워크 인터페이스를 사용 하 여 만든 추가 tooVMs만 수 있습니다. Hello VM 크기가 지원 되는 여러 네트워크 인터페이스 하는 경우에 네트워크 인터페이스 tooa 하나의 네트워크 인터페이스를 사용 하 여 만든 VM을 추가 하지 못했습니다. 반대로, 세 개 이상의 네트워크 인터페이스를 사용 하 여 VM에서 네트워크 인터페이스 에서만 제거할 수 있습니다, 항상 두 개 이상의 네트워크 인터페이스를 사용 하 여 만든 Vm toohave 있기 때문에 둘 이상의 네트워크 인터페이스. 이러한 제약 조건은 더 이상 적용되지 않습니다. 있습니다 이제 VM 개수에 관계 없이 네트워크 인터페이스 (위쪽 hello v M 크기에서 지원 되는 toohello 개수)을 만들어 및 추가 하거나 제거할 수 (hello 중지 (할당 취소 됨) Vm 상태)에서 네트워크 인터페이스의 개수 hello VM은 항상 네트워크 인터페이스를 하나 이상 있으면 합니다.
- 기본적으로는 VM에서 첫 번째 네트워크 인터페이스 hello hello로 정의 *기본* 네트워크 인터페이스. Hello VM에서에서 다른 모든 네트워크 인터페이스는 *보조* 네트워크 인터페이스.
- Hello Azure DHCP 서버에서 기본 게이트웨이 할당 된 주 네트워크 인터페이스가 있지만 보조 네트워크 인터페이스가 없습니다. 보조 네트워크 인터페이스에는 기본 게이트웨이가 할당되지 않으므로 이 네트워크 인터페이스는 기본적으로 서브넷 외부의 리소스와 통신할 수 없습니다. 해당 서브넷 외부 리소스가 포함 된 Windows VM toocommunicate의 tooenable 보조 네트워크 인터페이스가 추가 hello를 사용 하 여 경로 toohello 운영 체제 `route add` Windows 명령줄에서 명령을 합니다. Linux Vm hello 기본 동작 라우팅, 취약 한 호스트를 사용 하므로 권장 보조 네트워크 인터페이스 tooa 단일 서브넷에 대 한 트래픽을 제한 됩니다. 보조 네트워크 인터페이스, 정책 기반 tooensure 해당 수신 라우팅 사용에 대 한 hello 서브넷 외부에서 연결을 필요 하 고 송신 트래픽에 hello를 사용 하 여 동일한 네트워크 인터페이스.
- 기본적으로 VM hello IP 주소를 전송 하는 hello에서 모든 아웃 바운드 트래픽을 hello 주 네트워크 인터페이스의 기본 IP 구성 toohello를 지정 합니다. Hello VM의 운영 체제 내에서 아웃 바운드 통신에 사용 되는 IP 주소를 제어 하지만 기본적으로 hello 주 네트워크 인터페이스를 통해.
- Hello 내에서 모든 Vm 지나서 hello 동일한 가용성 집합 필요한 toohave 단일 또는 여러 개의 네트워크 인터페이스 기능 이었습니다. 원하는 수의 네트워크 인터페이스에 이제 존재할 수 있는 Vm에 hello hello v M 크기에서 지원 되는 toohello 개수를 동일한 가용성 집합입니다. 그러나 만들어질 때 설정 하는 VM tooan 가용성만 추가할 수 있습니다. 가용성 집합을 읽을 hello에 대 한 자세한 toolearn [Azure에서 Vm의 가용성을 hello 관리](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) 문서.
- 네트워크 인터페이스 하는 동안 hello 동일한 VM 수 있으며 VNet 내에 연결 된 toodifferent 서브넷, hello 네트워크 인터페이스 될 연결 된 toohello 동일한 VNet입니다.
- 모든 기본 또는 보조 네트워크 인터페이스 tooan Azure 부하 분산 장치 백 엔드 풀의 모든 IP 구성에 대 한 모든 IP 주소를 추가할 수 있습니다. Hello 지난에서 hello 기본 IP 주소만 hello 주 네트워크 인터페이스에 대 한 tooa 백 엔드 풀을 추가할 수 없습니다. IP 주소 및 구성의 경우, hello 읽기에 대 한 자세한 toolearn [추가, 변경 또는 제거 IP 주소](virtual-network-network-interface-addresses.md) 문서.
- VM을 삭제 하는 hello 네트워크 인터페이스 연결된 tooit를 삭제 하지 않습니다. VM이 삭제 되 면 hello 네트워크 인터페이스 hello VM에서에서 분리 됩니다. Hello 네트워크 인터페이스 toodifferent Vm을 추가 하거나 삭제할 수 있습니다.
- 네트워크 인터페이스에는 개인 IPv6 주소 할당 tooit, hello VM을 만들 때이 tooa VM 연결할 수 있습니다. Hello VM을 만든 후에 할당 된 IPv6 주소 tooa VM 있는 네트워크 인터페이스를 연결할 수 없습니다. 가상 컴퓨터를 만들 때 할당된 된 개인 IPv6 주소가 있는 네트워크 인터페이스를 연결 하는 경우에 해당 네트워크 인터페이스 toohello 가상 컴퓨터, VM 크기가 hello 지원 개수 네트워크 인터페이스에 관계 없이 연결할 수 있습니다. 참조 [인터페이스 IP 주소 네트워크](virtual-network-network-interface-addresses.md) IP 할당에 대 한 더 toolearn toonetwork 인터페이스 주소입니다.

## <a name="vm-create"></a>기존 네트워크 인터페이스 tooa 추가 새 VM

Hello 포털을 통해 VM을 만들 hello 포털 기본 설정을 사용 하 여 네트워크 인터페이스를 만들고 toohello VM을 연결 합니다. 기존 네트워크 인터페이스 tooa를 추가할 수 없습니다 새 VM을 하거나 hello Azure 포털을 사용 하 여 여러 네트워크 인터페이스가 있는 VM을 만듭니다. 둘 다 할 수 있는 CLI 또는 PowerShell hello를 사용 하 여 합니다. VM 크기를 지 원하는 만드는지에 hello로 인터페이스 tooa VM 네트워크 여러으로 추가할 수 있습니다. 개수 네트워크에 대 한 자세한 toolearn 인터페이스 hello 읽을 각 VM 크기 지원 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM의 문서 크기를 조정 합니다. tooa VM을 추가 하는 hello 네트워크 인터페이스에 연결 된 tooanother VM 수 현재 없습니다. 네트워크 인터페이스, hello 읽을 만들기에 대 한 자세한 toolearn [네트워크 인터페이스를 관리](virtual-network-network-interface.md#create-a-network-interface) 문서.

> [!WARNING]
> 네트워크 인터페이스 tooit 할당 개인 IPv6 주소가 있으면 hello 가상 컴퓨터를 만들 때만 hello 네트워크 인터페이스 toohello 가상 컴퓨터를 추가할 수 있습니다. 연결할 수 없습니다 하나 이상의 네트워크 인터페이스 toohello 가상 컴퓨터 hello 가상 컴퓨터를 만들거나 hello 후 가상 컴퓨터를 만들 때으로 IPv6 주소 tooa 네트워크 연결 인터페이스 tooa 가상 컴퓨터에 할당 됩니다. 참조 [인터페이스 IP 주소 네트워크](virtual-network-network-interface-addresses.md) IP 할당에 대 한 더 toolearn toonetwork 인터페이스 주소입니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>기존 네트워크 인터페이스 tooan 기존 VM 추가

네트워크 인터페이스 toosupports를 추가 하는 VM 크기 hello로 인터페이스 tooa VM 네트워크 여러으로 추가할 수 있습니다. toolearn 각 VM 크기를 지 원하는 네트워크 인터페이스를 개수 읽을 hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM의 문서 크기를 조정 합니다. VM 네트워크 인터페이스 toomust 지원 tooadd을 중지 하는 hello에 있어야 네트워크 인터페이스의 hello 번호 tooadd 원하는 hello (할당 취소 됨) 상태입니다. 원하는 tooadd hello 네트워크 인터페이스에 연결 된 tooanother VM 수 현재 없습니다. 네트워크 인터페이스 tooan 기존 hello Azure 포털을 사용 하 여 VM을 추가할 수 없습니다. tooadd 네트워크 인터페이스 기존 VM tooan, hello CLI 또는 PowerShell을 사용 해야 합니다. 

> [!WARNING]
> 네트워크 인터페이스 tooit 할당 개인 IPv6 주소가 있으면 tooan 기존 가상 컴퓨터를 추가할 수 없습니다. 가상 컴퓨터를 만들 때에 할당 된 개인 IPv6 주소 tooa 가상 컴퓨터와 네트워크 인터페이스를 추가할 수 있습니다. 참조 [인터페이스 IP 주소 네트워크](virtual-network-network-interface-addresses.md) IP 할당에 대 한 더 toolearn toonetwork 인터페이스 주소입니다.

|도구|명령|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add)(참조) 또는 [세부 단계](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)(참조) 또는 [세부 단계](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a> VM에 대한 네트워크 인터페이스 보기

Hello IP 주소 할당 tooeach 네트워크 인터페이스 및 각 네트워크 인터페이스의 구성에 대 한 hello 네트워크 인터페이스 현재 연결 된 tooa VM toolearn 볼 수 있습니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 구독에 대 한 hello 소유자, 참가자 또는 네트워크 참가자 역할이 할당 된 계정으로 합니다. 역할 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *가상 컴퓨터*합니다. 때 **가상 컴퓨터** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **가상 컴퓨터** 나타나는 블레이드 hello tooview 네트워크 인터페이스에 대 한 VM의 hello 이름을 클릭 합니다.
4. Hello에 **설정** 섹션에 있는 VM 선택한 hello에 대 한 나타나는 hello 가상 컴퓨터 블레이드의 클릭 **네트워크 인터페이스**합니다. 네트워크 인터페이스 설정에 대 한 toolearn 방법과 toochange를 읽기 hello [네트워크 인터페이스를 관리](virtual-network-network-interface.md) 문서. 추가 대 한 toolearn, 변경 또는 tooa 네트워크 인터페이스에 할당 된 IP 주소를 제거 합니다. 참조 [관리 IP 주소](virtual-network-network-interface-addresses.md)합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>VM에서 네트워크 인터페이스 제거

hello VM tooremove 원하는 (또는 분리)에서 네트워크 인터페이스에 있어야 hello 중지 (할당 취소) 상태 및 현재 두 개 이상의 네트워크 인터페이스 연결 되어 있어야 tooit 합니다. 모든 네트워크 인터페이스를 제거할 수는 있지만 hello VM 하나 이상의 네트워크 인터페이스 연결 tooit 항상 있어야 합니다. 기본 네트워크 인터페이스를 제거 하면 Azure 연결된 toohello VM hello 가장 오래 된 hello 기본 특성 toohello 네트워크 인터페이스에 할당 합니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 구독에 대 한 hello 소유자, 참가자 또는 네트워크 참가자 역할이 할당 된 계정으로 합니다. 역할 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *가상 컴퓨터*합니다. 때 **가상 컴퓨터** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **가상 컴퓨터** 나타나는 블레이드 hello tooremove에 대 한 네트워크 인터페이스를 원하는 VM의 hello 이름을 클릭 합니다.
4. Hello에 **설정** 섹션에 있는 VM 선택한 hello에 대 한 나타나는 hello 가상 컴퓨터 블레이드의 클릭 **네트워크 인터페이스**합니다. 네트워크 인터페이스 설정에 대 한 toolearn 방법과 toochange를 읽기 hello [네트워크 인터페이스를 관리](virtual-network-network-interface.md) 문서. 추가 대 한 toolearn, 변경 또는 tooa 네트워크 인터페이스에 할당 된 IP 주소를 제거 합니다. 참조 [관리 IP 주소](virtual-network-network-interface-addresses.md)합니다.
5. 나타나는 hello 네트워크 인터페이스 블레이드에서 hello 클릭 **...**  toohello toodetach 원하는 hello 네트워크 인터페이스의 오른쪽입니다.
6. **분리**를 클릭합니다. 네트워크 연결 인터페이스 toohello 가상 컴퓨터 하나 뿐 이면 hello **분리** 옵션을 사용할 수 없습니다. 클릭 **예** 나타나는 hello 확인 상자에 있습니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove)(참조) 또는 [세부 단계](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)(참조) 또는 [세부 단계](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>다음 단계
toocreate 여러 네트워크 인터페이스가 있는 VM 또는 IP 주소, hello 다음 문서를 읽어 보십시오.

**명령**

|작업|도구|
|---|---|
|여러 NIC를 사용하여 VM 만들기|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|여러 IPv4 주소가 있는 단일 NIC VM 만들기|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Azure Load Balancer 뒤에 개인 IPv6 주소가 있는 단일 NIC VM 만들기|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager 템플릿](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
