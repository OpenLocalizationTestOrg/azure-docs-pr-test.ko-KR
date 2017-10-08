---
title: "Azure DevTest Labs에서 aaaManage 기본 랩 정책 | Microsoft Docs"
description: "자세한 내용은 방법 tooset DevTest Labs에 랩에 대 한 hello 기본 정책 (설정)의 일부"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs에서 랩에 대한 기본 정책 관리

Azure DevTest Labs toocontrol 비용 수 있고 각 랩에 대 한 정책 설정 ()를 관리 하 여 환경에서 낭비를 최소화 합니다. 이 문서에서는 있습니다 정책 시작 방법을 tooset hello 가장 중요 정책-제한의 두 hello 수가 학습 하 여 생성 또는 한 명의 사용자와 구성 자동 종료에서 요구 될 수 있는 가상 컴퓨터 (VM). tooview 어떻게 tooset 모든 랩 정책 hello 문서 참조 [Azure DevTest Labs에 랩 정책을 정의](devtest-lab-set-lab-policy.md)합니다.  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Azure DevTest Labs의 랩 정책에 액세스
hello 다음 단계를 안내 합니다 Azure DevTest Labs에 랩에 대 한 정책 설정.

랩에 대 한 hello 정책 tooview (및 변경) 다음이 단계를 따르십시오.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.

1. 선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.

1. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.   

1. **구성 및 정책**을 선택합니다.

    ![정책 설정 블레이드](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. hello **구성 및 정책** 블레이드 지정할 수 있는 설정의 메뉴를 포함 합니다. 이 문서에서는 대 한 hello 설정만 **사용자 당 가상 컴퓨터** 및 **자동 종료**합니다. toolearn 설정을 남은 hello에 대 한 참조 [Azure DevTest Labs에 랩에 대 한 모든 정책을 관리](./devtest-lab-set-lab-policy.md)합니다. 
   
## <a name="set-virtual-machines-per-user"></a>사용자당 가상 컴퓨터를 설정합니다.
에 대 한 정책을 hello **사용자 당 가상 컴퓨터** toospecify hello 최대 개별 사용자가 만들 수 있는 Vm 수 있습니다. 경우 사용자가 toocreate 또는 클레임 VM hello 사용자도 충족 될 경우에 오류 메시지가 표시 되는 해당 hello VM 생성/을 요구할 수 없습니다. 

1. Hello 랩에 **구성 및 정책** 메뉴 선택 **사용자 당 가상 컴퓨터**합니다.
   
    ![사용자당 가상 컴퓨터](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. 선택 **예** Vm 사용자 당 toolimit hello 수 있습니다. Vm 사용자 당 toolimit hello 수 하지 않으려면 선택 **아니요**합니다. 선택 하는 경우 **예**, hello를 만들거나 사용자가 소유 하는 Vm의 최대 수를 나타내는 숫자 값을 입력 합니다. 

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

## <a name="next-steps"></a>다음 단계

- [Azure DevTest Labs에 랩 정책을 정의](devtest-lab-set-lab-policy.md) -자세한 방법을 toomodify 다른 랩 정책 
