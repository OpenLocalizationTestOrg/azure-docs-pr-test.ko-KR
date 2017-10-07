---
title: "Azure DevTest Labs에 랩 aaaCreate | Microsoft Docs"
description: "가상 컴퓨터에 대한 Azure DevTest Labs에서 랩 만들기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs에서 랩 만들기
Azure DevTest Labs에 랩은 제한 및 할당량을 지정 하 여 해당 리소스를 관리 하는 더 나은 수 있는 가상 컴퓨터 (Vm) 등의 리소스 그룹을 포함 하는 hello 인프라 합니다. 이 문서는 hello hello Azure 포털을 사용 하 여 랩을 만드는 과정을 안내 합니다.

## <a name="prerequisites"></a>필수 조건
랩 toocreate 해야합니다.

* Azure 구독. Azure 구입 옵션에 대 한 toolearn 참조 [어떻게 toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) 또는 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다. Hello 구독 toocreate hello 랩의 hello 소유자 여야 합니다.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>단계 toocreate Azure DevTest Labs에 랩
단계를 수행 하는 hello를 방법을 toouse hello Azure 포털 toocreate Azure DevTest Labs에 랩 하는 방법을 보여 줍니다. 

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
1. Hello 왼쪽에 hello 주 메뉴에서 선택 **더 서비스** (하단의 hello hello 목록).

    ![추가 서비스 메뉴 옵션](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. 사용 가능한 서비스는 hello 목록에서 **DevTest Labs**합니다.
1. Hello에 **DevTest Labs** 블레이드를 **추가**합니다.
   
    ![랩 추가](./media/devtest-lab-create-lab/add-lab-button.png)

1. Hello에 **DevTest Lab 만들** 블레이드:
   
    1. 입력 한 **랩 이름이** hello 새 랩에 대 한 합니다.
    2. 선택 hello **구독** hello 랩에서 tooassociate 합니다.
    3. 선택 된 **위치** 어떤 toostore hello 랩에서 합니다.
    4. 선택 **자동 종료** toospecify tooenable--hello 매개 변수를 정의할 경우 hello 자동 종료 하 고 모든 hello 랩 Vm의 합니다. hello 자동 종료 기능은 주로 VM hello 할 때를 지정할 수는 그에 따라 비용 절감 기능 tooautomatically 종료 합니다. Hello 랩 hello 문서에서 설명 하는 hello 단계를 수행 하 여 만든 후 자동 종료 설정을 변경할 수 있습니다 [Azure DevTest Labs에 랩에 대 한 모든 정책을 관리](./devtest-lab-set-lab-policy.md#set-auto-shutdown)합니다.
    5. 선택 **Pin tooDashboard** hello 포털 대시보드에서 hello 랩 tooappear의 바로 가기에 들어 있습니다.
    6. 선택 **자동화 옵션** tooget Azure 리소스 관리자 템플릿을 구성 자동화에 대 한 합니다. 
    7. **만들기**를 선택합니다. 선택한 후 **만들기**, hello **DevTest Labs** 블레이드를 표시 합니다. Hello를 시청 하 여 hello 랩 만들기 프로세스의 hello 상태를 모니터링할 수 있습니다 **알림** 영역입니다. 완료 되 면 hello 페이지 toosee 새로 만든 hello 랩을 연구소 hello 목록에서 새로 고칩니다.  
    
    ![랩 블레이드 만들기](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>다음 단계
랩 만들었으면 다음 몇 가지 단계 tooconsider 다음과 같습니다.

* [보안 액세스 tooa 랩](devtest-lab-add-devtest-user.md)합니다.
* [랩 정책 설정](devtest-lab-set-lab-policy.md).
* [랩 템플릿 만들기](devtest-lab-create-template.md).
* [VM에 대한 사용자 지정 아티팩트  만들기](devtest-lab-artifact-author.md).
* [Tooa 랩 아티팩트를 사용 하 여 VM을 추가](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/)합니다.

