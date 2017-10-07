---
title: "DevTest Labs Azure에서에서 VM tooa 랩 aaaAdd | Microsoft Docs"
description: "자세한 내용은 방법 tooadd DevTest Labs Azure에서에서 가상 컴퓨터 tooa 랩"
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>DevTest Labs Azure에서에서 VM tooa 랩 추가
[첫 번째 VM을 이미 만든 경우](devtest-lab-create-first-vm.md) 미리 로드된 [Marketplace 이미지](devtest-lab-configure-marketplace-images.md)에서 만들었을 것입니다. 이제 tooadd 후속 Vm tooyour 랩 하려는 경우 선택할 수도 있습니다는 *기본* 즉는 [사용자 지정 이미지](devtest-lab-create-template.md) 또는 [수식](devtest-lab-manage-formulas.md)합니다. 이 자습서는 Azure 포털 tooadd VM tooa 랩 hello를 사용 하 여에서 DevTest Labs를 안내 합니다.

또한 이렇게 하면 toomanage 랩에는 VM에 대 한 아티팩트를 hello 하는 방법입니다.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>단계 tooadd DevTest Labs Azure에서에서 VM tooa 랩
1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
1. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
1. 랩의 hello 목록에서 toocreate hello VM 원하는 hello 랩을 선택 합니다.  
1. Hello 랩에 **개요** 블레이드를 **+ 추가**합니다.  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Hello에 **기본 선택** 블레이드에서 hello VM에 대 한 기준 선택 합니다.
1. Hello에 **가상 컴퓨터** 블레이드에서 hello에 hello 새 가상 컴퓨터에 대 한 이름을 입력 **가상 컴퓨터 이름** 입력란.

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. 입력 한 **사용자 이름** hello 가상 컴퓨터에서 관리자 권한이 부여 되 합니다.  
1. Toouse 원하는에 저장 된 암호 프로그램 [보안 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)을 선택 **저장 된 암호를 사용 하 여**, tooyour 암호 (암호)을 해당 하는 키 값을 지정 합니다. 그렇지 않으면 hello 텍스트 필드에 암호를 입력 **값을 입력**합니다.
1. hello **가상 컴퓨터 디스크 유형** hello 랩에서 hello 가상 컴퓨터에 대 한 허용 되는 저장소 디스크 형식을 결정 합니다.
1. 선택 **가상 컴퓨터 크기** hello 프로세서 코어, RAM 크기 및 hello VM toocreate의 hello 하드 드라이브 크기를 지정 하는 항목을 미리 정의 된 hello 중 하나를 선택 합니다.
1. 선택 **아티팩트** -아티팩트-hello 목록에서 선택 하 고 원하는 tooadd toohello 기본 이미지 hello 아티팩트를 구성 합니다.
    **참고:** 새 tooDevTest 랩 이거나 toohello 참조 아티팩트 구성 [기존 아티팩트 tooa VM 추가](#add-an-existing-artifact-to-a-vm) 섹션 및 다음 완료 되 면 여기로 돌아와 합니다.
1. 선택 **고급 설정** tooconfigure hello VM 네트워크 옵션 및 만료 옵션입니다. 

   tooset 만료 옵션을 선택 hello 달력 아이콘 toospecify hello VM에 날짜를 자동으로 삭제 됩니다.  기본적으로 VM hello 만료 되지 않습니다. 
1. 원하는 tooview 또는 hello Azure 리소스 관리자 템플릿을 복사 하는 경우 참조 toohello [저장 Azure 리소스 관리자 템플릿](#save-azure-resource-manager-template) 섹션을 완료 되 면 여기로 돌아와 합니다.
1. 선택 **만들기** tooadd hello VM toohello 랩을 지정 합니다.
1. hello 랩 블레이드 hello의 상태를 표시 hello VM 만들기-처음으로 **만들기**,으로 다음 **실행** hello VM을 시작한 후입니다.

> [!NOTE]
> [Claimable VM 추가](devtest-lab-add-claimable-vm.md) hello 랩의 모든 사용자가 사용 하기 위해 사용할 수 있도록 VM claimable toomake hello 하는 방법을 보여 줍니다.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>기존 아티팩트 tooa VM 추가
VM을 만드는 동안 기존 아티팩트를 추가할 수 있습니다. 각 lab hello 공개 DevTest Labs 아티팩트 저장소에서에서 아티팩트와 아티팩트 만든 및 아티팩트 리포지토리를 소유 하는 추가 된 tooyour가 포함 됩니다.

* Azure DevTest Labs *아티팩트* 지정할 수 *동작* hello VM 프로 비전 되 면 Windows PowerShell 스크립트 실행, Bash 명령 실행, 소프트웨어 설치 등 때 수행 하는 합니다.
* 아티팩트 *매개 변수* 특정 시나리오에 대 한 hello 아티팩트를 사용자 지정할 수 있도록

toocreate 아티팩트를 확인 하려면 어떻게 toodiscover hello 문서, [tooauthor 사용자 고유의 아티팩트에 대 한 포함 된 사용 방법을 DevTest Labs 자세한](devtest-lab-artifact-author.md)합니다.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
1. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
1. 랩의 hello 목록에서 toowork 하려는 hello VM이 포함 된 hello 랩을 선택 합니다.  
1. **내 가상 컴퓨터**를 선택합니다.
1. Select hello 원하는 VM입니다.
1. **아티팩트**를 선택합니다. 
1. **아티팩트 적용**을 선택합니다.
1. Hello에 **아티팩트 적용** 블레이드, 선택 hello 아티팩트 tooadd toohello VM을 선택 합니다.
1. Hello에 **추가 아티팩트** 블레이드에서 필수 hello 매개 변수 값 및 해야 하는 선택적 매개 변수를 입력 합니다.  
1. 선택 **추가** tooadd hello 아티팩트 및 반환 toohello **아티팩트 적용** 블레이드입니다.
1. VM에 필요한 만큼 계속해서 아티팩트를 추가합니다.
1. 아티팩트를 추가한 후 [는 hello 아티팩트 실행 hello 순서 변경](#change-the-order-in-which-artifacts-are-run)합니다. 또한 뒤로 이동할 수 너무[확인 하거나 수정할 아티팩트](#view-or-modify-an-artifact)합니다.
1. 아티팩트 추가를 마친 경우 **적용**을 선택합니다.

## <a name="change-hello-order-in-which-artifacts-are-run"></a>아티팩트 실행 되는 hello 순서 변경
기본적으로 hello 아티팩트의 hello 작업이 hello는 추가 순서 대로 toohello VM에서에서 실행 됩니다. hello 아래 단계에 설명 방법을 toochange hello는 hello 아티팩트의 실행 순서입니다.

1. Hello의 hello 위쪽 **아티팩트 적용** 블레이드, hello toohello VM에 추가 된 아티팩트 수를 나타내는 선택 hello 링크 합니다.
   
    ![다양 한 아티팩트 추가 tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Hello에 **아티팩트 선택** 블레이드, 끌어서 놓기 hello 아티팩트 hello 원하는 순서입니다. **참고:** hello 아티팩트를 끄는 데 문제가 있는 경우 hello hello 아티팩트의 왼쪽에서 끌어온 있는지 확인 합니다. 
1. 완료되면 **확인** 을 선택합니다.  

## <a name="view-or-modify-an-artifact"></a>아티팩트를 확인 또는 수정
hello 아래 단계에 설명 방법을 tooview 아티팩트 hello 매개 변수 또는 수정 합니다.

1. Hello의 hello 위쪽 **아티팩트 적용** 블레이드, hello toohello VM에 추가 된 아티팩트 수를 나타내는 선택 hello 링크 합니다.
   
    ![다양 한 아티팩트 추가 tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. Hello에 **아티팩트 선택** 블레이드, 선택 hello 아티팩트 tooview 싶거나 편집 합니다.  
1. Hello에 **추가 아티팩트** 블레이드를 변경 필요 하 고 선택 하나 수행 **확인** tooclose hello **추가 아티팩트** 블레이드입니다.
1. 선택 **확인** tooclose hello **아티팩트 선택** 블레이드입니다.

## <a name="save-azure-resource-manager-template"></a>Azure Resource Manager 템플릿 저장
Azure 리소스 관리자 템플릿을 반복 가능한 배포가 선언적으로 toodefine를 제공합니다. 단계를 수행 하는 hello toosave hello 만드는 VM에 대 한 Azure 리소스 관리자 템플릿을 hello 하는 방법을 설명 합니다.
저장 한 후 템플릿을 사용 하 여 hello Azure 리소스 관리자 너무[Azure PowerShell을 사용한 새 Vm 배포](../azure-resource-manager/resource-group-overview.md#template-deployment)합니다.

1. Hello에 **가상 컴퓨터** 블레이드를 **ARM 템플릿 보기**합니다.
2. Hello에 **보기 Azure 리소스 관리자 템플릿** 블레이드, 선택 hello 템플릿 텍스트입니다.
3. Hello 선택한 텍스트 toohello 클립보드에 복사 합니다.
4. 선택 **확인** tooclose hello **Azure 리소스 관리자 템플릿 보기 블레이드에서**합니다.
5. 텍스트 편집기를 엽니다.
6. Hello 클립보드의 템플릿 텍스트 hello에에서 붙여 넣습니다.
7. 나중에 사용할 hello 파일을 저장 합니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>다음 단계
* 한 번 만든 VM hello, 연결할 수 있습니다 toohello VM을 선택 하 여 **연결** hello VM 블레이드에서 합니다.
* 너무 방법에 대해 알아봅니다[DevTest Labs VM에 대 한 사용자 지정 아티팩트를 만들면](devtest-lab-artifact-author.md)합니다.
* Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/Samples)합니다.
