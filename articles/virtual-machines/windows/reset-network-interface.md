---
title: "Windows Azure VM에 대 한 aaaHow tooreset 네트워크 인터페이스 | Microsoft Docs"
description: "Tooreset Azure Windows VM에 대 한 인터페이스에 네트워크 하는 방법을 보여 줍니다."
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Tooreset은 Azure Windows VM에 대 한 인터페이스에 네트워크 하는 방법 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello 기본 NIC (네트워크 인터페이스)를 사용 하지 않도록 설정한 후에 tooMicrosoft Azure Windows 가상 컴퓨터 (VM)를 연결할 수 없거나 수동으로 NIC. hello에 대 한 고정 IP 설정 이 문서에서는 tooreset hello 원격 연결 문제를 해결할 수 있는 Azure Windows VM에 대 한 네트워크 인터페이스에 hello 하는 방법을 보여 줍니다.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>네트워크 인터페이스 다시 설정

### <a name="for-classic-vms"></a>클래식 VM

tooreset 네트워크 인터페이스를 다음이 단계를 수행 합니다.

1.  Toohello 이동 [Azure 포털]( https://ms.portal.azure.com)합니다.
2.  **Virtual Machines(클래식)**를 선택합니다.
3.  가상 컴퓨터 선택 hello에 영향이 있습니다.
4.  **IP 주소**를 선택합니다.
5.  경우 hello **개인 IP 할당** 않습니다 **정적**도 변경**정적**합니다.
6.  변경 hello **IP 주소** hello 서브넷에서에서 사용할 수 있는 tooanother IP 주소입니다.
7.  [저장]을 선택합니다.
8.  가상 컴퓨터 hello tooinitialize hello 새 NIC toohello 시스템 다시 시작 됩니다.
9.  TooRDP tooyour 컴퓨터를 시도 하십시오. 성공 하면 원하는 경우 개인 IP 주소 다시 toohello 원래 hello를 변경할 수 있습니다. 그렇지 않은 경우 현재 상태를 유지할 수 있습니다. 

### <a name="for-vms-deployed-in-resource-group-model"></a>리소스 그룹 모델에서 배포된 VM의 경우

1.  Toohello 이동 [Azure 포털]( https://ms.portal.azure.com)합니다.
2.  가상 컴퓨터 선택 hello에 영향이 있습니다.
3.  **네트워크 인터페이스**를 선택합니다.
4.  Hello 컴퓨터와 연결 된 네트워크 인터페이스를 선택 합니다.
5.  **IP 구성**을 선택합니다.
6.  Hello IP를 선택 합니다. 
7.  경우 hello **개인 IP 할당** 않습니다 **정적**도 변경**정적**합니다.
8.  변경 hello **IP 주소** hello 서브넷에서에서 사용할 수 있는 tooanother IP 주소입니다.
9. 가상 컴퓨터 hello tooinitialize hello 새 NIC toohello 시스템 다시 시작 됩니다.
10. TooRDP tooyour 컴퓨터를 시도 하십시오. 성공 하면 원하는 경우 개인 IP 주소 다시 toohello 원래 hello를 변경할 수 있습니다. 그렇지 않은 경우 현재 상태를 유지할 수 있습니다. 

## <a name="delete-hello-unavailable-nics"></a>삭제 hello 사용할 수 없는 Nic
원격 데스크톱 toohello 컴퓨터 수 후에 hello 이전 Nic tooavoid hello 잠재적인 문제를 삭제 해야 합니다.

1.  장치 관리자를 엽니다.
2.  **보기** > **숨겨진 장치 표시**를 선택합니다.
3.  **네트워크 어댑터**를 선택합니다. 
4.  "Microsoft Hyper-v 네트워크 어댑터"로 지정 하는 hello 어댑터를 확인 합니다.
5.  사용할 수 없는 어댑터는 회색으로 표시된 것을 볼 수 있습니다. Hello 어댑터를 마우스 오른쪽 단추로 클릭 하 고 제거를 선택 합니다.

    ![hello NIC의 hello 이미지](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > 만 hello 이름이 "Microsoft Hyper-v 네트워크 어댑터" hello 사용할 수 없는 어댑터를 제거 합니다. Hello의 숨겨진된 그 밖의 어댑터를 제거 하는 경우 추가 문제를 일으킬 수 있습니다.
    >
    >

6.  이제 사용할 수 없는 모든 어댑터가 시스템에서 지워집니다.