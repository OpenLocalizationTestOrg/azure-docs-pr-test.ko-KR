---
title: "Azure DevTest Labs에서 가상 네트워크 구성 | Microsoft 문서"
description: "기존 가상 네트워크 및 서브넷을 구성하고 Azure DevTest Labs를 통해 VM에서 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Azure DevTest Labs에서 가상 네트워크 구성
[아티팩트를 사용하여 랩에 VM 추가](devtest-lab-add-vm-with-artifacts.md)문서에 설명된 대로 랩에 VM을 만들 때 구성된 가상 네트워크를 지정할 수 있습니다. 이 작업을 수행하는 시나리오 중 하나는 Express 경로 또는 사이트 간 VPN으로 구성된 가상 네트워크를 사용하여 VM에서 회사 네트워크 리소스에 액세스해야 하는 경우입니다. 다음 섹션에서는 VM을 만들 때 선택할 수 있도록 랩의 가상 네트워크 설정으로 기존 가상 네트워크를 추가하는 방법을 보여 줍니다.

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a>Azure 포털을 사용하여 랩에 대한 가상 네트워크 구성
다음 단계에서는 동일한 랩에서 VM을 만들 때 사용할 수 있도록 랩에 기존 가상 네트워크(및 서브넷)를 추가하는 방법을 안내합니다. 

1. [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.
2. **추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.
3. 랩 목록에서 원하는 랩을 탭합니다. 
4. 랩의 블레이드에서 **구성**을 선택합니다.
5. 랩의 **구성** 블레이드에서 **가상 네트워크**를 선택합니다.
6. **가상 네트워크** 블레이드에서 현재 랩에 대해 구성한 가상 네트워크 및 랩에 대해 만들어진 기본 가상 네트워크의 목록이 표시됩니다. 
7. **+추가**를 선택합니다.
   
    ![랩에 기존 가상 네트워크 추가](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. **가상 네트워크** 블레이드에서 **[가상 네트워크 선택]**을 선택합니다.
   
    ![기존 가상 네트워크 선택](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. **가상 네트워크 선택** 블레이드에서 원하는 가상 네트워크를 선택합니다. 블레이드에는 구독의 동일 지역에 속하는 모든 가상 네트워크가 랩으로 표시됩니다.  
10. 가상 네트워크를 선택하면 **가상 네트워크**로 되돌아가며, 블레이드 하단에 있는 목록에서 서브넷을 클릭합니다.

    ![서브넷 목록](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    랩 서브넷 블레이드가 표시됩니다.

    ![랩 서브넷 블레이드](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. **랩 서브넷 이름**을 지정합니다.
12. 서브넷이 랩 VM 생성에 사용되도록 하려면 **가상 컴퓨터를 만들 때 사용**을 선택합니다.
13. [shared public IP address](devtest-lab-shared-ip.md)(공유 공용 IP 주소)를 사용하도록 설정하려면 **Enable shared public IP**(공유 공용 IP 사용)를 선택합니다.
14. 서브넷에서 공용 IP 주소를 허용하려면 **Allow public IP creation(공용 IP 생성 허용)**을 선택합니다.
15. **사용자당 최대 가상 컴퓨터** 필드에서 각 서브넷에 대한 사용자당 최대 VM을 지정합니다. VM 수에 제한을 두지 않으려면 이 필드는 공백으로 둡니다.
16. **확인**을 선택하여 랩 서브넷 블레이드를 닫습니다.
17. **저장**을 선택하여 가상 네트워크 블레이드를 닫습니다.
18. 이제 가상 네트워크를 구성했으므로 VM을 만들 때 선택할 수 있습니다. 
    VM을 만들고 가상 네트워크를 지정하는 방법을 확인하려면 [아티팩트를 사용하여 랩에 VM 추가](devtest-lab-add-vm-with-artifacts.md)문서를 참조하세요. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>다음 단계
랩에 원하는 가상 네트워크를 추가한 후에는 [랩에 VM을 추가](devtest-lab-add-vm-with-artifacts.md)해야 합니다.

