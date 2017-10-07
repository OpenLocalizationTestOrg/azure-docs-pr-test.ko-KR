---
title: "aaaConfigure DevTest Labs Azure에서에서 가상 네트워크 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 기존 가상 네트워크 및 서브넷에 Azure DevTest Labs를 사용 하 여 VM에서 사용 하 고"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Azure DevTest Labs에서 가상 네트워크 구성
Hello 문서에 설명 된 대로 [tooa 랩 아티팩트를 사용 하 여 VM을 추가할](devtest-lab-add-vm-with-artifacts.md)랩에 VM을 만들 때, 구성 된 가상 네트워크를 지정할 수 있습니다. 이 작업을 수행 하는 시나리오 중 하나를 사용 하 여 Vm에서 회사 네트워크 리소스를 사이트 간 VPN 또는 express 경로도로 구성 된 가상 네트워크 hello tooaccess 해야 할 경우입니다. hello 다음 섹션에서는 설명 방법을 tooadd 한다는 Vm을 만들 때 사용할 수 있는 toochoose은 랩의 가상 네트워크 설정으로 기존 가상 네트워크가 됩니다.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 랩에 대 한 가상 네트워크 구성
hello 다음 단계에 관한 hello에 VM을 만들 때 사용할 수 있도록 기존 가상 네트워크 (및 서브넷) tooa 랩을 추가 동일한 랩입니다. 

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다. 
4. Hello 랩 블레이드에서 선택 **구성**합니다.
5. Hello 랩에 **구성** 블레이드를 **가상 네트워크**합니다.
6. Hello에 **가상 네트워크** 블레이드에 hello 현재 랩 뿐만 아니라 랩에 대해 만들어진 hello 기본 가상 네트워크에 대 한 구성 된 가상 네트워크의 목록을 표시 합니다. 
7. **+추가**를 선택합니다.
   
    ![기존 가상 네트워크 tooyour 랩을 추가합니다](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. Hello에 **가상 네트워크** 블레이드를 **[가상 네트워크 선택]**합니다.
   
    ![기존 가상 네트워크 선택](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. Hello에 **가상 네트워크 선택** 블레이드, 선택 hello 원하는 가상 네트워크입니다. hello 블레이드 표시 되는 모든 hello 가상 네트워크는 아래 hello 동일 지역 hello 랩 hello 구독에 있습니다.  
10. 가상 네트워크를 선택한 후 toohello 반환될지 **가상 네트워크** hello hello 블레이드 맨 아래에 hello 목록의 hello 서브넷을 클릭 합니다.

    ![서브넷 목록](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    hello 랩 서브넷 블레이드가 표시 됩니다.

    ![랩 서브넷 블레이드](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. **랩 서브넷 이름**을 지정합니다.
12. VM 만들기 랩에서 사용 되는 서브넷 toobe tooallow 선택 **가상 컴퓨터 생성에 사용 하 여**합니다.
13. tooenable는 [공용 IP 주소를 공유](devtest-lab-shared-ip.md)선택, **공용 IP를 공유 하는 활성화**합니다.
14. tooallow 공용 IP 주소는 서브넷에서 선택 **공용 IP를 만들 수 있도록**합니다.
15. Hello에 **사용자 당 최대 가상 컴퓨터** 필드에서 지정 각 서브넷에 대 한 사용자 당 최대 Vm hello 합니다. VM 수에 제한을 두지 않으려면 이 필드는 공백으로 둡니다.
16. 선택 **확인** tooclose hello 랩 서브넷 블레이드입니다.
17. 선택 **저장** tooclose hello 가상 네트워크 블레이드입니다.
18. Hello 가상 네트워크는 구성 했으므로 VM을 만들 때 선택할 수 있습니다. 
    toosee 어떻게 toocreate VM 가상 네트워크를 지정 하 고 toohello 문서를 참조 하십시오 [tooa 랩 아티팩트를 사용 하 여 VM을 추가할](devtest-lab-add-vm-with-artifacts.md)합니다. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>다음 단계
Hello 원하는 tooyour 랩 가상 네트워크를 추가 하면 hello에는 너무[추가 VM tooyour 랩](devtest-lab-add-vm-with-artifacts.md)합니다.

