---
title: "aaaCreate 프로그램 첫 번째 Azure 가상 네트워크 | Microsoft Docs"
description: "Toocreate Azure 가상 네트워크 (VNet) 두 가상 컴퓨터 (VM) toohello VNet을 연결 하 고 toohello Vm을 연결 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>첫 가상 네트워크 만들기

Hello 다음 그림에에서 나와 있는 것 처럼 어떻게 toocreate 두 서브넷을 사용 하 여 가상 네트워크 (VNet) 두 가상 컴퓨터 (VM)를 만들고 연결 hello 서브넷의 각 VM tooone에 알아봅니다.

![가상 네트워크 다이어그램](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Azure 가상 네트워크 (VNet)는 hello 클라우드에서 사용자의 네트워크의 표현입니다. 사용자가 Azure 네트워크 설정을 제어하고 DHCP 주소 블록, DNS 설정, 보안 정책 및 라우팅을 정의할 수 있습니다. VNet 개념을 읽을 hello에 대 한 자세한 toolearn [가상 네트워크 개요](virtual-networks-overview.md) 문서. 다음 단계 toocreate hello 리소스 hello 그림에 표시 된 hello를 완료 합니다.

1. [두 개의 서브넷이 있는 VNet을 만듭니다](#create-vnet).
2. [네트워크 인터페이스 1 개 (NIC) 각각 두 개의 Vm을 만듭니다](#create-vms)를 네트워크 보안 그룹 (NSG) tooeach NIC 연결
3. [Tooand hello Vm에서 연결](#connect-to-from-vms)
4. [모든 리소스를 삭제합니다](#delete-resources). 이들 프로 비전 하는 동안이 연습에서 만든 hello 리소스 중 일부에 대 한 요금을 해야 합니다. toominimize hello 요금, hello 연습을 완료 한 후 toocomplete hello 만드는이 섹션 toodelete hello 리소스의 단계를 확인 해야 합니다.

기본적으로이 문서의 단계를 완료 하는 hello 후 VNet을 사용 하는 방법을 이해를 해야 합니다. 다음 단계 위해 제공 되는 방법에 대 한 자세히 알아볼 수 있습니다를 좀 더 깊게 Vnet toouse 합니다.

## <a name="create-vnet"></a>두 개의 서브넷이 있는 가상 네트워크 만들기

서브넷인은 단계를 완료 하는 hello 사용 하 여 가상 네트워크 toocreate 합니다. 서로 다른 서브넷은 일반적으로 toocontrol hello 서브넷 간의 트래픽 흐름을 사용 합니다.

1. Toohello 로그인 [Azure 포털](<https://portal.azure.com>)합니다. 아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free)을 등록할 수 있습니다. 
2. Hello에 **즐겨찾기** 창의 hello 포털의 클릭 **새로**합니다.
3. Hello에 **새로** 블레이드에서 클릭 **네트워킹**합니다. Hello에 **네트워킹** 블레이드에서 클릭 **가상 네트워크**hello 다음 그림에에서 나온 것 처럼:

    ![가상 네트워크 다이어그램](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  Hello에 **가상 네트워크** 블레이드에서 leave *리소스 관리자* hello 배포 모델 및 클릭으로 선택한 **만들기**합니다.
5.  Hello에 **만들기 가상 네트워크 블레이드** 나타나는 hello 다음 값을 입력 한 다음 클릭 **만들기**:

    |**설정**|**값**|**세부 정보**|
    |---|---|---|
    |**Name**|*MyVNet*|hello 이름은 hello 리소스 그룹 내에서 고유 해야 합니다.|
    |**주소 공간**|*10.0.0.0/16*|CIDR 표기법으로 원하는 주소 공간을 지정할 수 있습니다.|
    |**서브넷 이름**|*프런트 엔드*|hello 서브넷 이름이 hello 가상 네트워크 내에서 고유 해야 합니다.|
    |**서브넷 주소 범위**|*10.0.0.0/24*| 지정 된 hello 범위 hello 가상 네트워크에 대해 정의 된 hello 주소 공간 내에 있어야 합니다.|
    |**구독**|*[사용자의 구독]*|구독 toocreate hello VNet 선택에 있습니다. VNet은 단일 구독 내에 존재합니다.|
    |**리소스 그룹**|**새로 만들기:** *MyRG*|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) 개요 문서.|
    |**위치**:|*미국 서부*| 일반적으로 hello 위치와 가장 가까운 tooyour 실제 위치를 선택 합니다.|

    VNet은 몇 초 toocreate를 hello 합니다. Azure hello 참조을 만든 후 포털 대시보드에서.

6. Hello Azure 포털에서에서 만든 hello 가상 네트워크와 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **MyVNet** hello에서 가상 네트워크 **모든 리소스** 블레이드입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 *MyVNet* hello에 **이름별으로 필터링...** 상자 tooeasily 액세스 hello VNet입니다.
7. hello **MyVNet** 블레이드가 열리고 hello 다음 그림에에서 나와 있는 것 처럼 VNet hello에 대 한 정보를 표시 합니다.

    ![가상 네트워크 다이어그램](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. 클릭 하 여 hello 이전 그림에 나와 있는 것 처럼 **서브넷** toodisplay hello VNet 내의 hello 서브넷의 목록입니다. hello 존재 하는 서브넷에만 **프런트 엔드**, 5 단계에서 만든 서브넷 hello 합니다.
9. Hello MyVNet-서브넷 블레이드 클릭 **+ 서브넷** toocreate hello 사용 하 여 서브넷 정보 및 클릭 **확인** toocreate hello 서브넷:

    |**설정**|**값**|**세부 정보**|
    |---|---|---|
    |**Name**|*백 엔드*|hello 이름은 hello 가상 네트워크 내에서 고유 해야 합니다.|
    |**주소 범위**|*10.0.1.0/24*|지정 된 hello 범위 hello 가상 네트워크에 대해 정의 된 hello 주소 공간 내에 있어야 합니다.|
    |**네트워크 보안 그룹** 및 **경로 테이블**|*없음*(기본값)|네트워크 보안 그룹(NSG)은 이 문서의 뒷부분에서 다룹니다. hello 읽기 사용자 정의 경로 대 한 자세한 toolearn [사용자 정의 경로](virtual-networks-udr-overview.md) 문서.|

10. Hello를 닫을 수 hello 새 서브넷 toohello VNet를 추가한 후 **MyVNet – 서브넷** 블레이드에서 다음 닫기 hello **모든 리소스** 블레이드입니다.

## <a name="create-vms"></a>가상 컴퓨터 만들기

VNet hello와 서브넷을 만든 hello Vm을 만들 수 있습니다. 그러나이 연습에서는 hello Windows Server 운영 체제를 실행 하는 두 Vm에 대 한 여러 다른 Linux 배포판을 포함 하 여 Azure에서 지원 되는 운영 체제 실행할 수 있습니다.

### <a name="create-web-server-vm"></a>Hello 웹 서버 VM 만들기

toocreate hello 웹 서버 VM 단계를 수행 하는 전체 hello:

1. Hello Azure 포털 즐겨찾기 창에서 클릭 **새로**, **계산**, 다음 **Windows Server 2016 Datacenter**합니다.
2. Hello에 **Windows Server 2016 Datacenter** 블레이드에서 클릭 **만들기**합니다.
3. Hello에 **기본 사항** 나타나는 블레이드 입력 하거나 다음 값에는 hello 선택한 클릭 **확인**:

    |**설정**| **값**|**세부 정보**|
    |---|---|---|
    |**Name**|*MyWebServer*|이 VM은 인터넷 리소스가 연결되는 웹 서버 역할을 합니다.|
    |**VM 디스크 유형**|*SSD*|
    |**사용자 이름**|*사용자 선택*|
    |**암호 및 암호 확인**|*사용자 선택*|
    | **구독**|*<Your subscription>*|hello 구독 해야 hello의 5 단계에서 선택한 동일한 구독 hello [두 서브넷과 가상 네트워크 만들기](#create-vnet) 이 문서의 섹션. hello에 hello VM toomust 연결 VNet 존재 동일한 VM hello 구독 합니다.|
    |**리소스 그룹**|**기존 값 사용:** *MyRG* 선택|리소스 hello에 tooexist를 없는 경우에 동일한 리소스 그룹 VNet hello에 대 한 했던 것 처럼 hello hello에서는 동일한 리소스 그룹입니다.|
    |**위치**:|*미국 서부*|hello 위치 여야 hello의 5 단계에서 지정 된 동일한 위치 hello [두 서브넷과 가상 네트워크 만들기](#create-vnet) 이 문서의 섹션. Vm 및 hello toomust 연결할 Vnet에에서 있는 hello 동일 위치 합니다.|

4. Hello에 **크기를 선택** 블레이드에서 클릭 *DS1_V2 표준*, 클릭 **선택**합니다. 읽기 hello [Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure에서 지 원하는 모든 Windows VM 크기의 목록에 대 한 문서입니다.
5. Hello에 **설정** 블레이드를 입력 하거나 다음 값에는 hello 선택한 클릭 **확인**:

    |**설정**|**값**|**세부 정보**|
    |---|---|---|
    |**저장소: Managed Disks 사용**|*예*||
    |**가상 네트워크**| *MyVNet* 선택|동일한 hello에 존재 하는 모든 VNet을 선택할 수 있습니다 위치를 만드는 VM hello 합니다. Vnet 및 서브넷을 hello 읽기에 대 한 자세한 toolearn [가상 네트워크](virtual-networks-overview.md) 문서.|
    |**서브넷**|*프런트 엔드* 선택|Hello VNet 내에 있는 모든 서브넷을 선택할 수 있습니다.|
    |**공용 IP 주소**|Hello 기본값을 그대로|공용 IP 주소를 통해 있습니다 tooconnect toohello를 VM hello 인터넷에서에서 수 있습니다. hello를 읽고, 공용 IP 주소에 대 한 자세한 toolearn [IP 주소](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) 문서.|
    |**네트워크 보안 그룹(방화벽)**|Hello 기본값을 그대로|Hello 클릭 **(새) MyWebServer nsg** 기본 NSG hello 포털 설정을 tooview을 생성 합니다. Hello에 **네트워크 보안 그룹 만들기** 열리는 블레이드, 모든 원본 IP 주소에서의 TCP/3389 (RDP) 트래픽을 허용 하는 인바운드 규칙 하나에 있습니다.|
    |**다른 모든 값**|Hello 기본값을 적용|읽을 hello 설정을 남은 hello에 대 한 자세한 toolearn [Vm에 대 한](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.|

    네트워크 보안 그룹 NSG ()을 사용 하면 toocreate hello tooand hello VM에서에서 전달할 수 있는 네트워크 트래픽 종류에 대 한 인바운드/아웃 바운드 규칙입니다. 기본적으로 모든 인바운드 트래픽을 toohello VM 거부 되었습니다. 프로덕션 웹 서버에 대해 TCP/80(HTTP) 및 TCP/443(HTTPS)에 대한 추가 인바운드 규칙을 추가할 수 있습니다. 기본적으로 모든 아웃바운드 트래픽은 허용되기 때문에 아웃바운드 트래픽에 대한 규칙은 없습니다. 있습니다 수 추가/제거 규칙 toocontrol 트래픽 별 사용자 정책입니다. 읽기 hello [네트워크 보안 그룹](virtual-networks-nsg.md) Nsg에 대 한 자세한 문서 toolearn 합니다.

6.  Hello에 **요약** 블레이드에서 hello 설정을 검토 하 고 클릭 **확인** toocreate hello VM입니다. 상태 타일 VM 만듭니다 hello로 hello 포털 대시보드에 표시 됩니다. 몇 분 toocreate를 걸릴 수 있습니다. 않아도 toowait 것에 대 한 toocomplete 됩니다. Toohello hello VM이 생성 하는 동안 다음 단계를 계속할 수 있습니다.

### <a name="create-database-server-vm"></a>Hello 데이터베이스 서버 VM 만들기

toocreate hello 데이터베이스 서버 VM 단계를 수행 하는 전체 hello:

1.  Hello 즐겨찾기 창에서 클릭 **새로**, **계산**, 다음 **Windows Server 2016 Datacenter**합니다.
2.  Hello에 **Windows Server 2016 Datacenter** 블레이드에서 클릭 **만들기**합니다.
3.  Hello에 **기본 사항 블레이드에서**를 입력 하거나 다음 값을 hello를 선택한 다음 클릭 **확인**:

    |**설정**|**값**|**세부 정보**|
    |---|---|---|
    |**Name**|*MyDBServer*|이 VM hello 웹 서버에 연결 하지만 해당 hello 인터넷에 연결할 수 없는 데이터베이스 서버로 사용 됩니다.|
    |**VM 디스크 유형**|*SSD*||
    |**사용자 이름**|사용자 선택||
    |**암호 및 암호 확인**|사용자 선택||
    |**구독**|<Your subscription>|hello 구독 해야 hello의 5 단계에서에서 선택한 동일한 구독 hello [두 서브넷과 가상 네트워크 만들기](#create-vnet) 이 문서의 섹션.|
    |**리소스 그룹**|**기존 값 사용:** *MyRG* 선택|리소스 hello에 tooexist를 없는 경우에 동일한 리소스 그룹 VNet hello에 대 한 했던 것 처럼 hello hello에서는 동일한 리소스 그룹입니다.|
    |**위치**:|*미국 서부*|hello 위치 여야 hello의 5 단계에서 지정 된 동일한 위치 hello [두 서브넷과 가상 네트워크 만들기](#create-vnet) 이 문서의 섹션.|

4.  Hello에 **크기를 선택** 블레이드에서 클릭 *DS1_V2 표준*, 클릭 **선택**합니다.
5.  Hello에 **설정** 블레이드를 입력 하거나 다음 값에는 hello 선택한 클릭 **확인**:

    |**설정**|**값**|**세부 정보**|
    |----|----|---|
    |**저장소: Managed Disks 사용**|*예*||
    |**가상 네트워크**|*MyVNet* 선택|동일한 hello에 존재 하는 모든 VNet을 선택할 수 있습니다 위치를 만드는 VM hello 합니다.|
    |**서브넷**|선택 *백 엔드* hello를 클릭 하 여 **서브넷** 상자에서 다음을 선택 하면 **백 엔드** hello에서 **서브넷을 선택** 블레이드|Hello VNet 내에 있는 모든 서브넷을 선택할 수 있습니다.|
    |**공용 IP 주소**|None – hello 기본 주소를 차례로 클릭 **None** hello에서 **공용 IP 주소 선택** 블레이드|공용 IP 주소가 없으면만 연결할 수 toohello VM에서 다른 연결 된 VM toohello 동일한 VNet입니다. Hello 인터넷에서 직접 tooit를 연결할 수 없습니다.|
    |**네트워크 보안 그룹(방화벽)**|Hello 기본값을 그대로| 또한 hello MyWebServer VM이이 NSG에 대 한 작성 NSG hello 기본 hello 달리 동일 기본 인바운드 규칙입니다. 데이터베이스 서버에 대해 TCP/1433(MS SQL)에 대한 추가 인바운드 규칙을 추가할 수 있습니다. 기본적으로 모든 아웃바운드 트래픽은 허용되기 때문에 아웃바운드 트래픽에 대한 규칙은 없습니다. 있습니다 수 추가/제거 규칙 toocontrol 트래픽 별 사용자 정책입니다.|
    |**다른 모든 값**|Hello 기본값을 적용||

6.  Hello에 **요약** 블레이드에서 hello 설정을 검토 하 고 클릭 **확인** toocreate hello VM입니다. 상태 타일 VM 만듭니다 hello로 hello 포털 대시보드에 표시 됩니다. 몇 분 toocreate를 걸릴 수 있습니다. 않아도 toowait 것에 대 한 toocomplete 됩니다. Toohello hello VM이 생성 하는 동안 다음 단계를 계속할 수 있습니다.

## <a name="review"></a>리소스 검토

그러나 하나의 VNet과 두 개의 Vm hello hello MyRG 리소스 그룹에 사용자에 대 한 몇 가지 추가 리소스를 만들어 Azure 포털을 만들었습니다. Hello 다음 단계를 완료 하 여 hello MyRG 리소스 그룹의 hello 내용을 검토 합니다.

1. Hello에 **즐겨찾기** 창에서 클릭 **더 많은 서비스**합니다.
2. Hello에 **더 많은 서비스** 창, 형식 *리소스 그룹* hello 단어 hello 상자의 *필터* 에 있습니다. 클릭 **리소스 그룹** hello에 표시 될 때 필터링 된 목록입니다.
3. Hello에 **리소스 그룹** 창의 hello 클릭 *MyRG* 리소스 그룹입니다. 많은 기존 리소스 그룹을 구독에 있을 경우 입력할 수 있습니다 *MyRG* hello 텍스트를 포함 하는 hello 상자에서 *이름별으로 필터링...* tooquickly 액세스 hello MyRG 리소스 그룹입니다.
4.  Hello에 **MyRG** 블레이드에 표시 12 리소스를 포함 하는 해당 hello 리소스 그룹 hello 다음 그림에에서 나와 있는 것 처럼:

    ![리소스 그룹 콘텐츠](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

Vm, 디스크 및 저장소 계정, hello 읽기에 대 한 자세한 toolearn [가상 컴퓨터](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [디스크](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), 및 [저장소 계정](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 개요 문서입니다. Hello 두 개의 기본 Nsg hello 포털 생성을 볼 수 있습니다. Hello 포털이 만든 두 개의 네트워크 인터페이스 (NIC) 리소스를 볼 수 있습니다. NIC는 hello VNet 통해 VM tooconnect tooother 리소스 수 있습니다. 읽기 hello [NIC](virtual-network-network-interface.md) Nic에 대 한 자세한 문서 toolearn 합니다. hello 포털에도 공용 IP 주소 리소스가 만들어집니다. 공용 IP 주소는 공용 IP 주소 리소스에 대한 한 가지 설정입니다. hello를 읽고, 공용 IP 주소에 대 한 자세한 toolearn [IP 주소](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) 문서.

## <a name="connect-to-from-vms"></a>Toohello Vm 연결

VNet 및 만든 두 개의 Vm을 toohello Vm hello hello 다음 섹션에에서 나와 있는 단계를 완료 하 여 연결할 수 있습니다.

### <a name="connect-from-internet"></a>Hello 인터넷에서에서 toohello 웹 서버 VM 연결

tooconnect toohello 웹 서버 VM에서 인터넷을 단계를 수행 하는 전체 hello hello:

1. Hello 포털에서 열기 hello MyRG 리소스 그룹 hello를 완료 하 여 hello에서 단계 [리소스를 검토](#review) 이 문서의 섹션.
2. Hello에 **MyRG** 블레이드에서 hello 클릭 **MyWebServer** VM입니다.
3. Hello에 **MyWebServer** 블레이드에서 클릭 **연결**hello 다음 그림에에서 나온 것 처럼:

    ![Tooweb 서버 VM 연결](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. 브라우저 toodownload hello 허용 *MyWebServer.rdp* 파일을 다음 엽니다.
5. 클릭 하면 해당 hello 게시자의 hello 원격 연결을 확인할 수 없는 알리는 대화 상자가 표시 되 면 **연결**합니다.
6. 자격 증명을 입력할 때는 hello 사용자 이름 및 암호로 hello의 3 단계에서 지정한 로그인 확인 [만들기 hello 웹 서버 VM](#create-web-server-vm) 이 문서의 섹션. 경우 hello **Windows 보안** 나타나는 상자 hello 올바른 자격 증명을 나열 하지 않는, tooclick 할 수 있습니다 **추가 선택 사항을**, 다음 **다른 계정을 사용 하 여**할 수 있도록, hello 올바른 사용자 이름 및 암호 지정). 클릭 **확인** tooconnect toohello VM입니다.
7. 표시 되 면 한 **원격 데스크톱 연결** 클릭 하면 hello hello 원격 컴퓨터의 id를 확인할 수 없어서 상자 알리는 **예**합니다.
8. Hello 인터넷에서에서 연결 된 toohello MyWebServer VM가 나타납니다. Hello 다음 섹션의 hello 원격 데스크톱 연결 열기 toocomplete hello 단계를 둡니다.

hello 원격 연결은 toohello toohello 공용 IP 주소 리소스 hello 포털 hello의 5 단계에서 만든 할당 한 공용 IP 주소는 [두 서브넷과 가상 네트워크 만들기](#create-vnet) 이 문서의 섹션. hello 기본 규칙 hello에 만들어지므로 hello 연결이 허용 됩니다 **MyWebServer nsg** TCP/3389 (RDP) 허용 된 NSG 인바운드 toohello VM에서 모든 원본 IP 주소입니다. 다른 포트를 통해 tooconnect toohello VM에서 하면 hello 연결이 실패 하면 추가 인바운드 규칙 toohello NSG 허용 hello 추가 포트를 추가 하지 않는 한 합니다.

>[!NOTE]
>인바운드 규칙을 추가 toohello NSG를 추가 하는 경우 동일한 포트 hello Windows 방화벽에 열려 있는 또는 연결 실패 hello 해당 hello를 확인 합니다.
>

### <a name="connect-to-internet"></a>Hello 웹 서버 VM에서에서 toohello 인터넷 연결

tooconnect hello 웹 서버 VM 단계를 수행 하는 전체 hello에서에서 아웃 바운드 인터넷 toohello:

1. MyWebServerVM 열고 원격 연결 toohello 모를 경우 hello의 hello 단계를 완료 하 여 원격 연결 toohello VM을 만들 [hello 인터넷에서에서 연결 toohello 웹 서버 VM](#connect-from-internet) 이 문서의 섹션.
2. Hello Windows 바탕 화면에서 Internet Explorer를 엽니다. Hello에 **설치 Internet Explorer 11** 대화 상자를 클릭 **권장된 설정을 사용 하지 않는**, 클릭 **확인**합니다. 것이 권장된 tooaccept hello 권장 되는 프로덕션 서버에 대 한 설정 합니다.
3. Hello Internet Explorer 주소 표시줄에 입력 [bing.com](http:www.bing.com)합니다. Internet Explorer 대화 상자에 표시 되 면 클릭 **추가**, 다음 **추가** hello에 **신뢰할 수 있는 사이트** 대화 상자와 클릭 **닫기**합니다. 다른 Internet Explorer 대화 상자에 대해 이 과정을 반복합니다.
4. Hello Bing에서 검색 페이지, 입력 *whatsmyipaddress*, hello 돋보기 단추를 클릭 합니다. Bing은 hello 공용 IP 주소 할당 toohello 공용 IP 주소 리소스 hello VM을 만들 때 hello 포털에서 만든를 반환 합니다. Hello에 대 한 hello 설정을 검사 하는 경우 **MyWebServer ip** 참조 리소스를 뒤에 오는 hello 그림에 나와 있는 것 처럼 toohello 공용 IP 주소 리소스를 할당 하는 동일한 IP 주소를 hello 합니다. 그러나 hello IP 주소가 할당 tooyour VM이 다른 있습니다.

    ![Tooweb 서버 VM 연결](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Hello 다음 섹션의 hello 원격 데스크톱 연결 열기 toocomplete hello 단계를 둡니다.

있습니다 수 tooconnect toohello 인터넷 hello VM에서에서는 기본적으로 VM hello에서 모든 아웃 바운드 연결이 허용 됩니다. 추가 규칙 toohello 적용할 NSG toohello toohello 서브넷 hello NIC에, 연결 된 NIC를 추가 하 여 아웃 바운드 연결을 제한할 수 있습니다 또는 둘 다 합니다.

Hello VM에 보관 됩니다 hello 중지 (할당 취소) 상태 hello 포털을 사용 하 여 면 hello 공용 IP 주소를 변경할 수 있습니다. Hello 공용 IP 주소 변경이 하지 필요한 경우에 hello 동적 할당 방법 (즉, hello 기본값) 보다는 hello IP 주소에 대 한 hello 정적 할당 메서드를 사용할 수 있습니다. hello 읽기에 대해 더 알아봅니다 toolearn hello 할당 방법 간의 차이점이 [IP 주소 형식 및 할당 방법을](virtual-network-ip-addresses-overview-arm.md) 문서.

### <a name="webserver-to-dbserver"></a>Hello 웹 서버 VM에서에서 toohello 데이터베이스 서버 VM 연결

tooconnect toohello 데이터베이스 서버 VM VM 단계를 수행 하는 전체 hello hello 웹 서버에서:

1. 열 MyWebServer VM 원격 연결 toohello 모를 경우 hello의 hello 단계를 완료 하 여 원격 연결 toohello VM을 만들 [hello 인터넷에서에서 연결 toohello 웹 서버 VM](#connect-from-internet) 이 문서의 섹션.
2. Hello Windows 데스크톱의 hello 왼쪽 아래 모서리에 hello 시작 단추를 클릭 한 다음 입력을 시작 *원격 데스크톱*합니다. Hello 시작 메뉴 목록 표시 될 때 **원격 데스크톱 연결**를 클릭 합니다.
3. Hello에 **원격 데스크톱 연결** 대화 상자에 입력 *MyDBServer* hello 컴퓨터 이름과 클릭 **연결**합니다.
4. Hello 사용자 이름 및 hello의 3 단계에서 입력 한 암호가 입력 [만들기 hello 데이터베이스 서버 VM](#create-database-server-vm) 섹션이 문서의 클릭 **확인**합니다.
5. 클릭 하면 hello 원격 컴퓨터의 해당 hello id를 검증할 수 없다는 대화 상자에 표시 되 면 **예**합니다.
6. Hello 다음 섹션의 단계를 열고 toocomplete hello tooboth 서버 hello 원격 데스크톱 연결을 유지 합니다.

사용자는 hello 웹 서버에서 VM에 대해 다음 이유로 hello 수 toomake hello 연결 toohello 데이터베이스 서버 VM:

- Hello 기본 NSG hello의 5 단계에서 만든 모든 원본 IP에 대 한 TCP/3389 인바운드 연결이 설정 되어 [만들기 hello 데이터베이스 서버 VM](#create-database-server-vm) 이 문서의 섹션.
- Hello 웹 서버는 연결 된 toohello VM에서 hello 연결을 시작한 hello 데이터베이스 서버 VM으로 동일한 VNet입니다. tooconnect tooa에는 공용 IP 주소 할당 tooit 없는 VM에서에서 연결 해야 다른 연결 된 VM toohello 동일한 VNet hello VM이 다른 서브넷에 연결 된 tooa 경우에 합니다.
- Hello Vm은 연결 된 toodifferent 서브넷, 경우에 Azure 서브넷의 연결을 사용할 수 있는 기본 경로 만듭니다. 그러나 직접 만들어 hello 기본 경로 재정의할 수 있습니다. 읽기 hello [사용자 정의 경로](virtual-networks-udr-overview.md) Azure에서 라우팅에 대 한 자세한 문서 toolearn 합니다.

Hello에서와 같이 tooinitiate hello 인터넷에서에서 원격 연결 toohello 데이터베이스 서버 VM 시도 하면 [hello 인터넷에서에서 연결 toohello 웹 서버 VM](#connect-from-internet) 섹션 해당 hello 표시,이 문서의 **연결** 옵션은 회색입니다. 연결 되므로 hello 인터넷에서에서 인바운드 연결 tooit 가능 하지 않습니다. 없는 공용 IP 주소 할당 toohello VM에 있기 때문에 비활성화 되어 있습니다.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Hello 데이터베이스 서버 VM에서에서 toohello 인터넷 연결

Hello 다음 단계를 완료 하 여 hello 데이터베이스 서버 VM에서에서 인터넷 아웃 바운드 toohello를 연결 합니다.

1. Hello의 단계를 완료 hello hello MyWebServer VM에서에서 열 MyDBServer VM 원격 연결 toohello 모를 경우 [hello 웹 서버 VM에서에서 연결 toohello 데이터베이스 서버 VM](#webserver-to-dbserver) 이 문서의 섹션.
2. Hello MyDBServer VM에 hello Windows 바탕 화면에서 Internet Explorer를 열고 2 단계와 3의 hello에서에서와 같이 toohello 대화 상자를 응답 [hello 웹 서버 VM에서에서 toohello 인터넷 연결](#connect-to-internet) 이 문서의 섹션.
3. Hello 주소 표시줄에를 입력 [bing.com](http:www.bing.com)합니다.
4. 클릭 **추가** hello Internet Explorer 대화 상자가 표시 되 면 다음에 **추가**, 다음 **닫기** hello에 **신뢰할 수 있는** 사이트 대화 상자. 대화 상자가 추가로 표시되면 이러한 단계를 완료합니다.
5. Hello Bing에서 검색 페이지, 입력 *whatsmyipaddress*, hello 돋보기 단추를 클릭 합니다. Bing은 hello Azure 인프라 여 hello 공용 IP 주소를 현재 할당 된 toohello VM을 반환합니다. 6. Hello 원격 데스크톱 toohello MyDBServer VM hello MyWebServer VM에서에서 다음 hello 원격 연결 toohello MyWebServer VM을 닫습니다.

hello 아웃 바운드 연결 toohello 인터넷 공용 IP 주소 리소스 toohello MyDBServer VM 할당 되지 않은 경우에 기본적으로 모든 아웃 바운드 트래픽을 허용 하기 때문에 허용 됩니다. 기본적으로 모든 Vm 수 tooconnect 아웃 바운드 toohello 인터넷에 상관 없이 공용 IP 주소 할당 된 리소스 toohello VM 됩니다. 그러나 공용 IP 할당 하는 리소스 주소를 공용 IP가 있는 MyWebServer VM 수 toofor hello 있는 것과 hello 인터넷에서에서 주소 수 tooconnect toohello 되지는 않습니다.

## <a name="delete-resources"></a>모든 리소스 삭제

이 문서에서는 다음 단계 완료 hello에서에서 만든 모든 리소스를 toodelete:

1. 이 문서 전체에서 만든 tooview hello MyRG 리소스 그룹 단계 1-3에 hello [리소스를 검토](#review) 이 문서의 섹션. 다시 한 번 hello 리소스 그룹의 hello 리소스를 검토 합니다. 이전 단계에 따라 hello MyRG 리소스 그룹을 만든 경우 4 단계에서 hello 그림에 표시 된 hello 12 개의 리소스를 참조 합니다.
2. Hello MyRG 블레이드에서 hello 클릭 **삭제** 단추입니다.
3. hello 포털 해야 tootype hello 이름의 hello 리소스 그룹 tooconfirm toodelete 원하는 것입니다. 표시 되 면 리소스 이외의 hello의 4 단계에서 표시 된 hello 리소스 [리소스를 검토](#review) 섹션 클릭이 문서의 **취소**합니다. 이 문서의 일부로 만들어진 hello 12 리소스에만 표시 되 면 입력 *MyRG* hello 리소스 그룹 이름에 대 한 클릭 **삭제**합니다. 리소스 그룹을 삭제 hello 리소스 그룹 내에서 모든 리소스에 있으므로 항상 있는지 tooconfirm 리소스 그룹의 hello 내용을 삭제 하기 전에 합니다. hello 포털 hello 리소스 그룹 내에 포함 된 모든 리소스를 삭제 한 다음 자체 hello 리소스 그룹을 삭제 합니다. 이 프로세스는 몇 분 정도 걸립니다.

## <a name="next-steps"></a>다음 단계

이 연습에서 VNet 하나와 VM 둘을 만들었습니다. VM을 만드는 동안 사용자 지정 설정을 지정했고 몇 가지 기본 설정을 수락했습니다. Hello 기사, 프로덕션 Vnet 및 사용 가능한 모든 설정이 이해 tooensure Vm을 배포 하기 전에 다음을 확인 하는 것이 좋습니다.

- [가상 네트워크](virtual-networks-overview.md)
- [공용 IP 주소](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [네트워크 인터페이스](virtual-network-network-interface.md)
- [네트워크 보안 그룹](virtual-networks-nsg.md)
- [가상 컴퓨터](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
