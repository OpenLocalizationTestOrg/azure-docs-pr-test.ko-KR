---
title: "Azure DevTest Labs에서 aaaManage 랩 정책 | Microsoft Docs"
description: "자세한 내용은 VM과 같은 toodefine 랩 정책 크기, 사용자 당 최대 Vm 하는 방법 및 종료 자동화 합니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs에서 랩에 대한 모든 정책 관리

Azure DevTest Labs에서는 각 랩의 정책(설정)을 관리하여 랩에서 비용을 관리하고 낭비를 최소화할 수 있습니다. 이 문서에 대 한 단계별 자세히 설명 방법을 tooset 각 정책입니다.  

## <a name="set-allowed-virtual-machine-sizes"></a>허용된 가상 컴퓨터 크기를 설정합니다.
hello 설정 hello에 대 한 정책을 허용 toominimize 랩 toospecify hello 랩에는 VM 크기는 사용할 수 있도록 하 여 낭비 하는 VM 크기는 데 도움이 됩니다. 이 정책은 인증 된 경우이 목록에서 VM 크기만 사용된 toocreate Vm 수 있습니다.

1. Hello 랩에 **구성 및 정책** 블레이드를 **가상 컴퓨터 크기를 허용**합니다.
   
    ![허용된 가상 컴퓨터 크기](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. 선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.

1. 이 정책을 사용하도록 설정한 경우 랩에서 만들 수 있는 하나 이상의 VM 크기를 선택합니다.

1. **저장**을 선택합니다.

## <a name="set-virtual-machines-per-user"></a>사용자당 가상 컴퓨터를 설정합니다.
에 대 한 정책을 hello **사용자 당 가상 컴퓨터** toospecify hello 최대 개별 사용자가 만들 수 있는 Vm 수 있습니다. 경우 사용자가 toocreate 또는 클레임 VM hello 사용자도 충족 될 경우에 오류 메시지가 표시 되는 해당 hello VM 생성/을 요구할 수 없습니다. 

1. Hello 랩에 **구성 및 정책** 메뉴 선택 **사용자 당 가상 컴퓨터**합니다.
   
    ![사용자당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. 선택 **예** Vm 사용자 당 toolimit hello 수 있습니다. Vm 사용자 당 toolimit hello 수 하지 않으려면 선택 **아니요**합니다. 선택 하는 경우 **예**, hello를 만들거나 사용자가 소유 하는 Vm의 최대 수를 나타내는 숫자 값을 입력 합니다. 

1. 선택 **예** SSD (반도체 디스크)를 사용할 수 있는 Vm toolimit hello 수 있습니다. SSD를 사용할 수 있는 Vm toolimit hello 수 하지 않으려면 선택 **아니요**합니다. 선택 하는 경우 **예**, hello SSD를 사용 하 여 만들 수 있는 Vm의 최대 수를 나타내는 값을 입력 합니다. 

1. **저장**을 선택합니다.

## <a name="set-virtual-machines-per-lab"></a>랩당 가상 컴퓨터를 설정합니다.
에 대 한 정책을 hello **랩 당 가상 컴퓨터** hello 현재 랩에 대 한 hello toospecify 만들 수 있는 Vm의 최대 수를 허용 합니다. 사용자가 VM toocreate hello 랩 제한을 충족 될 경우에 경우 오류 메시지가 표시 되는 해당 hello VM을 만들 수 없습니다. 

1. Hello 랩에 **구성 및 정책** 메뉴 선택 **랩 당 가상 컴퓨터**합니다.
   
    ![랩당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. 선택 **예** Vm 랩 당 toolimit hello 수 있습니다. Vm 당 랩 toolimit hello 수 하지 않으려면 선택 **아니요**합니다. 선택 하는 경우 **예**, hello를 만들거나 사용자가 소유 하는 Vm의 최대 수를 나타내는 숫자 값을 입력 합니다. 

1. 선택 **예** SSD (반도체 디스크)를 사용할 수 있는 Vm toolimit hello 수 있습니다. SSD를 사용할 수 있는 Vm toolimit hello 수 하지 않으려면 선택 **아니요**합니다. 선택 하는 경우 **예**, hello SSD를 사용 하 여 만들 수 있는 Vm의 최대 수를 나타내는 값을 입력 합니다. 

1. **저장**을 선택합니다.

## <a name="set-auto-shutdown"></a>자동 종료 설정
hello 자동 종료 정책을 toominimize 랩이이 랩의이 Vm을 종료 하는 toospecify hello 시간을 허용 하 여 낭비를 사용 합니다.

1. Hello 랩에 **구성 및 정책** 블레이드를 **자동 종료**합니다.
   
    ![자동 종료](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. 선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.

1. 이 정책을 사용 하는 경우 모든 Vm 아래로 hello 시간 (및 표준 시간대) tooshut hello 현재 랩에 지정 합니다.

1. 지정 **예** 또는 **아니요** 알림 15 분 이전 toohello 옵션 toosend hello에 대 한 자동 종료 시간을 지정 합니다. 지정 하는 경우 **예**, webhook URL 끝점 tooreceive hello 알림을 입력 합니다. 웹후크에 대한 자세한 내용은 [웹후크 또는 API Azure Function 만들기](../azure-functions/functions-create-a-web-hook-or-api-function.md)를 참조하세요. 

1. **저장**을 선택합니다.

    기본적으로 활성화 되어 있는 경우,이 정책은 tooall Vm hello 현재 랩에 적용 됩니다. tooremove가 특정 VM에서이 설정을 열고 hello VM 블레이드 및 변경의 **자동 종료** 설정 

## <a name="set-auto-start"></a>자동 시작 설정
hello 자동 시작 정책은 있도록 toospecify hello 현재 랩에 hello Vm을 시작 해야 합니다.  

1. Hello 랩에 **구성 및 정책** 블레이드를 **자동 시작**합니다.
   
    ![자동 시작](./media/devtest-lab-set-lab-policy/auto-start.png)

2. 선택 **에** tooenable이이 정책 및 **오프** toodisable 것입니다.

3. 이 정책을 사용 하면 예약 된 hello 시작 시간, 표준 시간대 및 시간에 적용 되는 hello에 대 한 hello 주의 hello 일을 지정 합니다. 

4. **저장**을 선택합니다.

    사용할 수 있는 경우이 정책은에 없는 경우 자동으로 적용 된 tooany Vm hello 현재 랩 tooapply이 설정은 tooa 특정 VM, 열기 hello VM 블레이드 및 변경의 **자동 시작** 설정 

## <a name="set-expiration-date"></a>만료 날짜 설정
만료 날짜를 설정할 수 있습니다 날짜 있습니다 [hello VM을 만들](devtest-lab-add-vm.md)합니다. **고급 설정**, 선택 hello 달력 아이콘 toospecify hello VM에 날짜를 자동으로 삭제 됩니다.  기본적으로 VM hello 만료 되지 않습니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>다음 단계
정의 하 고 적용 되 면 hello 랩에 대 한 다양 한 VM 정책 설정, 다음 일부의 tootry 다음과 같습니다.

* [IP 주소를 공유 이해](devtest-lab-shared-ip.md) -어떻게 공유 IP에 설명 주소는 공용 IP 주소가 필요한 tooconnect tooyour 랩 Vm의 DevTest Labs toominimize hello 번호에 사용 됩니다.
* [비용 관리 구성](devtest-lab-configure-cost-management.md) -에서는 방법을 toouse hello **월별 예상 비용 추세** 차트  
  tooview 현재 달의 예상된 비용 누계와 프로젝션 hello 월말의 비용 hello 합니다.
* [사용자 지정 이미지 만들기](devtest-lab-create-template.md) - VM을 만들 때 사용자 지정 이미지 또는 마켓플레이스 이미지 중에서 기본 이미지를 지정할 수 있습니다. 이 문서에서는 어떻게 toocreate 사용자 지정은 VHD 파일에서을 이미지를 보여 줍니다.
* [마켓플레이스 이미지 구성](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs에서 Azure Marketplace 이미지에 기반하여 VM을 만들 수 있습니다. 이 문서에서는 설명 방법을 toospecify Azure 마켓플레이스 이미지 될 수 있는 경우 있는 환경에서 Vm을 만들 때 사용 합니다.
* [랩에서 VM 만들기](devtest-lab-add-vm-with-artifacts.md) -보여 줍니다 방법을 toocreate 기본 이미지에서 VM (어느 사용자 지정 또는 마켓플레이스), 방법과 VM의 아티팩트로 toowork 합니다.

