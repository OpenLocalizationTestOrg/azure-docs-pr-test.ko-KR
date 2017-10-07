---
title: "네트워크 보안 그룹-aaaTroubleshoot 포털 | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 hello Azure 리소스 관리자 배포에서 tootroubleshoot 네트워크 보안 그룹을 모델링 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>네트워크 보안 그룹 hello Azure 포털을 사용 하 여 문제 해결
> [!div class="op_single_selector"]
> * [Azure 포털](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

가상 컴퓨터 (VM)에 (Nsg) 네트워크 보안 그룹을 구성 하 고 VM 연결 문제가 발생 하는 경우이 문서에서는 Nsg toohelp 추가 문제 해결에 대 한 진단 기능에 대 한 개요를 제공 합니다.

Nsg를 사용 하면 toocontrol hello 유형의 트래픽 가상 컴퓨터 (Vm) 및 해당 흐름 있습니다. Nsg에는 Azure 가상 네트워크 (VNet), 네트워크 인터페이스 (NIC), 또는 둘 다에 적용 된 toosubnets 될 수 있습니다. hello 효과적인 규칙이 적용 되는 tooa NIC hello 적용할 Nsg tooa NIC 및 hello 서브넷에 연결 되어 있는 hello 규칙의 집계 됩니다. 때로는 이러한 NSG 간의 규칙이 서로 충돌하고 VM의 네트워크 연결에 영향을 줄 수 있습니다.  

VM의 Nic에 적용 될 때 프로그램 Nsg에서 모든 hello 효과적인 보안 규칙을 볼 수 있습니다. 이 문서에서는 tootroubleshoot VM 연결 문제에 이러한 규칙을 사용 하 여 Azure 리소스 관리자 배포 모델을 hello 하는 방법을 보여 줍니다. VNet과 NSG 개념에 잘 모르겠으면 읽을 hello [가상 네트워크](virtual-networks-overview.md) 및 [네트워크 보안 그룹](virtual-networks-nsg.md) 개요 문서입니다.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>효과적인 보안 규칙 tootroubleshoot VM 트래픽 흐름을 사용 하 여
다음에 나오는 hello 시나리오는 일반적인 연결 문제의 예:

VM *VM1*은 *WestUS-VNet1*이라는 VNet 내에 있는 *Subnet1* 서브넷의 일부입니다. 시도 tooconnect toohello RDP를 사용 하 여 TCP 포트 3389 통해 VM에 실패 합니다. 두 hello NIC에 Nsg 적용 *VM1 NIC1* 서브넷 hello 및 *Subnet1*합니다. 트래픽 tooTCP 포트 3389는 hello hello 네트워크 인터페이스와 연결 된 NSG에에서 사용할 수 있습니다. *VM1 NIC1*TCP 포트 3389 실패 tooVM1의 ping 있지만, 합니다.

이 예에서는 TCP 포트 3389를 사용 하는 동안 다음 단계 hello 모든 포트를 통해 사용 되는 toodetermine 인바운드 및 아웃 바운드 연결 오류가 발생할 수 있습니다.

### <a name="vm"></a>가상 컴퓨터에 대한 유효 보안 규칙 보기
Hello 단계 tootroubleshoot Nsg를 VM에 대해 다음을 완료 합니다.

Hello VM 자체에서 NIC에 hello 효과적인 보안 규칙의 전체 목록을 볼 수 있습니다. 추가 하 고 수정 하 고, 다음 권한을 tooperform 이러한 작업이 있는 hello 효과적인 규칙 블레이드에서 NIC와 서브넷 NSG 규칙 삭제 수도 있습니다.

1. Azure 포털 https://portal.azure.com toohello를 로그인 합니다.
2. 클릭 **더 많은 서비스**, 클릭 **가상 컴퓨터** 표시 되는 hello 목록에서입니다.
3. VM tootroubleshoot 나타나는 hello 목록에서 선택한 옵션과 함께 VM 블레이드를 표시 합니다.
4. **문제 진단 및 해결**을 클릭하고 일반적인 문제를 선택합니다. 예를 들어 **toomy Windows VM을 연결할 수 없습니다.** 을 선택 합니다. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. 단계는 hello 다음 그림에에서 나와 있는 것 처럼 hello 문제를 아래에 나타납니다. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    클릭 *효과적인 보안 그룹 규칙* hello 권장된 단계 목록에 있습니다.
6. hello **효과적인 보안 규칙을 가져올** hello 다음 그림에에서 나와 있는 것 처럼 블레이드 나타납니다.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Hello hello 그림의 다음 섹션을 참고 하세요.
   
   * **범위 지정:** 도*VM1*, 3 단계에서 선택한 VM hello 합니다.
   * **네트워크 인터페이스:** *VM1-NIC1* 이 선택됩니다. 하나의 VM에 여러 네트워크 인터페이스(NIC)가 있을 수 있습니다. 각 NIC에는 고유한 유효 보안 규칙이 있을 수 있습니다. 문제를 해결 하려면 각 NIC.에 대 한 tooview hello 효과적인 보안 규칙이 필요할 수 있습니다.
   * **연결 된 Nsg:** Nsg 적용된 tooboth hello NIC 및 hello 서브넷 hello NIC에 연결 될 수 있습니다. Hello 그림 NSG 적용된 tooboth hello NIC와 hello 서브넷에 연결 되어 되었습니다. 클릭할 수 있는 toodirectly hello NSG 이름에 hello Nsg의에서 규칙을 수정 합니다.
   * **VM1 nsg 탭:** hello hello 그림으로 표시 된 규칙의 목록은 다음과 같이 hello NSG toohello NIC. 적용 NSG가 만들어질 때마다 Azure에서 몇 가지 기본 규칙이 생성됩니다. Hello 기본 규칙을 제거할 수 없습니다 하지만 더 높은 우선 순위의 규칙을 재정의할 수 있습니다. 기본 규칙을 hello 읽기에 대 한 자세한 toolearn [NSG 개요](virtual-networks-nsg.md#default-rules) 문서.
   * **대상 열:** hello 규칙 중 일부는 텍스트 hello 열에 있고 다른 사용자는 주소 접두사입니다. hello 텍스트는 생성 된 기본 태그가 적용 toohello 보안 규칙의 hello 이름입니다. hello 태그는 여러 개의 접두사를 나타내는 시스템 제공 식별자입니다. 와 같은 태그를 사용 하는 규칙을 선택 하면 *AllowInternetOutBound*, hello에 hello 접두사를 나열 **주소 접두사** 블레이드입니다.
   * **다운로드:** hello 규칙 목록이 길게 지정할 수 있습니다. 클릭 하 여 오프 라인 분석을 위한 hello 규칙의.csv 파일을 다운로드할 수 있습니다 **다운로드** hello 파일을 저장 하 고 있습니다.
   * **AllowRDP** 인바운드 규칙:이 규칙은 VM의 RDP 연결 toohello 허용 합니다.
7. Hello 클릭 **Subnet1 NSG** hello 다음 그림에에서 나와 있는 것 처럼 탭 tooview hello hello NSG에서에서 효과적인 규칙 toohello 서브넷은 적용: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    공지 hello *denyRDP* **인바운드** 규칙입니다. Hello 서브넷에서 적용 하는 인바운드 규칙 hello 네트워크 인터페이스에 적용 하는 규칙 보다 먼저 평가 됩니다. Hello 거부 규칙이 적용 되는 hello 서브넷에 있으므로 hello 요청 tooconnect tooTCP 3389 실패할 hello 허용 규칙에 hello NIC 계산 되지 않습니다. 
   
    hello *denyRDP* 규칙은 hello RDP 연결 실패 하는 이유는 hello 이유입니다. 제거 hello 문제가 해결 됩니다.
   
   > [!NOTE]
   > Hello VM에 연결 된 hello로 NIC가 실행 중 상태 또는 Nsg에는 적용 된 toohello NIC 또는 서브넷 되지 않은, 규칙이 표시 됩니다.
   > 
   > 
8. tooedit NSG 규칙 클릭 *Subnet1 NSG* hello에 **연결 된 Nsg** 섹션.
   Hello 열립니다 **Subnet1 NSG** 블레이드입니다. 클릭 하 여 hello 규칙을 직접 편집할 수 있습니다 **인바운드 보안 규칙**합니다.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Hello를 제거한 후 *denyRDP* hello에 인바운드 규칙 **Subnet1 NSG** 추가 하 고는 *allowRDP* 규칙 hello 다음 그림 처럼 보이는 hello 효과적인 규칙 목록:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    TCP 포트 3389는 VM의 RDP 연결 toohello 열거나 hello PsPing 도구를 사용 하 여 열려 있는지 확인 하십시오. 읽는 hello 여 PsPing에 대 한 자세히 알아볼 수 있습니다 [PsPing 다운로드 페이지](https://technet.microsoft.com/sysinternals/psping.aspx)합니다.

### <a name="nic"></a>네트워크 인터페이스에 대한 유효 보안 규칙 보기
VM 트래픽 흐름 특정 NIC에 대 한 영향을 주지 경우 hello 다음 단계를 완료 하 여 hello hello 네트워크 인터페이스 컨텍스트에서 NIC hello에 대 한 효과적인 규칙의 전체 목록을 볼 수 있습니다.

1. Azure 포털 https://portal.azure.com toohello를 로그인 합니다.
2. 클릭 **더 많은 서비스**, 클릭 **네트워크 인터페이스** 표시 되는 hello 목록에서입니다.
3. 네트워크 인터페이스를 선택합니다. 다음 그림 hello, NIC 라는 *VM1 NIC1* 을 선택 합니다.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    해당 hello 확인 **범위** 선택 된 toohello 네트워크 인터페이스를 설정 합니다. hello의 6 단계를 읽고 toolearn에 대 한 자세한 정보 표시, 추가 정보 hello **Nsg를 VM에 대 한 문제를 해결** 이 문서의 섹션.
   
   > [!NOTE]
   > 네트워크 인터페이스에서 NSG 제거 되 면 hello 서브넷 NSG가 NIC. 제공 hello에 계속 적용 이 경우 hello 출력에서는 hello 서브넷 NSG의에서 규칙을 보여 줍니다. 규칙은 hello NIC는 VM tooa를 연결된 하는 경우에 표시 됩니다.
   > 
   > 
4. NIC 및 서브넷에 연결된 NSG에 대한 규칙만 직접 편집할 수 있습니다. toolearn hello의 8 단계를 읽는 방법, **가상 컴퓨터에 대 한 효과적인 보안 규칙 보기** 이 문서의 섹션.

## <a name="nsg"></a>NSG(네트워크 보안 그룹)에 대한 유효 보안 규칙 보기
NSG 규칙을 수정할 때는 특정 VM에 추가 되는 hello 규칙의 tooreview hello 영향을 수도 있습니다. 주어진된 NSG를에 적용 되는 Nic 모든 hello에 대 한 hello 효과적인 보안 규칙의 전체 목록을 볼 수 있습니다 NSG 블레이드를 제공 하는 hello tooswitch 컨텍스트가 필요 없이 합니다. tootroubleshoot NSG, 단계를 수행 하는 전체 hello 내에서 유효 규칙:

1. Azure 포털 https://portal.azure.com toohello를 로그인 합니다.
2. 클릭 **더 많은 서비스**, 클릭 **네트워크 보안 그룹** 표시 되는 hello 목록에서입니다.
3. NSG를 선택합니다. 다음 그림 hello에서 nsg v m 1 이라는 NSG 선택 되었습니다.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Hello hello 이전 그림의 다음 섹션을 참고 하세요.
   
   * **범위 지정:** toohello 선택한 NSG를 설정 합니다.
   * **가상 컴퓨터:** 때 NSG 적용된 tooa 서브넷, 적용 된 tooall 네트워크 인터페이스 연결 된 tooall Vm 연결 된 toohello 서브넷입니다. 이 목록은 이 NSG가 적용되는 모든 VM을 보여 줍니다. 모든 VM hello 목록에서 선택할 수 있습니다.
     
     > [!NOTE]
     > NSG가 적용 된 tooonly 빈 서브넷을 Vm 나열 되지 않습니다. NSG에 적용 된 tooa NIC는 VM과 연결 되지 않는 경우, 해당 Nic도 표시 되지 않습니다. 
     > 
     > 
   * **네트워크 인터페이스:** 하나의 VM에 여러 네트워크 인터페이스가 있을 수 있습니다. 네트워크 인터페이스를 선택할 수 있습니다 toohello 연결 된 VM을 선택 합니다.
   * **AssociatedNSGs:** tootwo를 만들 수는 NIC 언제 든 지 효과적인 Nsg toohello NIC를 적용 하 고 다른 toohello 서브넷 hello 하나 있습니다. Hello NIC에 NSG 효과적인 서브넷이 있는 경우 v m 1-nsg으로 hello 범위를 선택 하면 두 Nsg hello 출력에서 표시 됩니다.
4. NIC 또는 서브넷에 연결된 NSG에 대한 규칙만 직접 편집할 수 있습니다. toolearn hello의 8 단계를 읽는 방법, **가상 컴퓨터에 대 한 효과적인 보안 규칙 보기** 이 문서의 섹션.

hello의 6 단계를 읽고 toolearn에 대 한 자세한 정보 표시, 추가 정보 hello **가상 컴퓨터에 대 한 효과적인 보안 규칙 보기** 이 문서의 섹션.

> [!NOTE]
> 서브넷과 NIC를 설정할 수 있지만 각 NSG 적용 toothem 하나만, NSG 연결된 toomultiple Nic 및 다중 서브넷 될 수 있습니다.
> 
> 

## <a name="considerations"></a>고려 사항
연결 문제를 해결 하는 경우 지점 뒤에 hello를 고려 합니다.

* 기본 NSG 규칙 hello에서의 인바운드 액세스를 차단 합니다 인터넷 및 허용 VNet 인바운드 트래픽을 합니다. 규칙은 명시적으로 추가 되어야 tooallow 인바운드 필요에 따라 인터넷을 통해 액세스 합니다.
* VM의 네트워크 연결 toofail 일으키는 NSG 보안 규칙이 없으면로 인해 hello 문제 수 있습니다.
  * Hello VM의 운영 체제 내에서 실행 되는 방화벽 소프트웨어
  * 가상 어플라이언스 또는 온-프레미스 트래픽에 대해 경로가 구성되었습니다. 인터넷 트래픽을 통해 강제 터널링 리디렉션된 tooon 프레미스 될 수 있습니다. Hello 인터넷 tooyour VM에서에서 RDP/SSH 연결 hello 온-프레미스 네트워크 하드웨어가이 트래픽을 처리 하는 방법에 따라이 설정을 사용 하 여 작동 하지 않을 수 있습니다. 읽기 hello [경로 문제 해결](virtual-network-routes-troubleshoot-powershell.md) 문서 toolearn에 방해가 될 수 있는 toodiagnose 경로 문제 hello와 통신 흐름을 방법 hello VM입니다. 
* 기본적으로 Vnet을 살펴본 있는 hello VIRTUAL_NETWORK 태그 겹치기 Vnet에 대 한 tooinclude 접두사를 자동으로 확장 됩니다. Hello에 이러한 접두사를 볼 수 있습니다 **ExpandedAddressPrefix** 목록, tootroubleshoot 연결 피어 링 하는 문제 관련된 tooVNet 합니다. 
* 효과적인 보안 규칙은 NSG 또는 관련 된 hello VM NIC 및 서브넷 있는지에 표시 됩니다. 
* Hello NIC와 관련 된 없는 Nsg 또는 서브넷 있는 경우 tooyour VM에 할당 된 공용 IP 주소 이면 모든 포트 인바운드 및 아웃 바운드 액세스를 위해 열린 됩니다. Hello VM에 공용 IP 주소, 서브넷 또는 NIC에 Nsg toohello 적용이 좋습니다.

