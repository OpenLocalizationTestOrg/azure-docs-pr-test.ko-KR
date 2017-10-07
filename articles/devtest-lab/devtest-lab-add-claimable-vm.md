---
title: "Azure DevTest Labs에서 claimable VM tooa 랩 aaaAdd | Microsoft Docs"
description: "자세한 내용은 방법 tooadd Azure DevTest Labs에서 가상 컴퓨터 claimable tooa 랩"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Azure DevTest Labs claimable VM tooa 랩 추가
Claimable VM tooa 랩 비슷한 방식으로 toohow에 추가 하면 [표준 VM 추가](devtest-lab-add-vm.md) –에서 *기본* 즉는 [사용자 지정 이미지](devtest-lab-create-template.md), [수식을](devtest-lab-manage-formulas.md), 또는 [마켓플레이스 이미지](devtest-lab-configure-marketplace-images.md)합니다. 이 자습서 안내 하 Azure 포털 tooadd hello를 사용 하 여에서 DevTest Labs claimable VM tooa 랩 고 사용자 뒤에 오는 tooclaim hello VM hello 프로세스를 보여 줍니다.

> [!NOTE]
> 통해 랩 Vm을 배포 하는 경우 [Azure 리소스 관리자 템플릿을](devtest-lab-create-environment-from-arm.md), 설정 hello 여 claimable Vm을 만들 수 있습니다 **allowClaim** 속성 tootrue hello 속성 섹션에 있습니다.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>단계 tooadd Azure DevTest Labs에서 claimable VM tooa 랩
1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
1. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
1. 랩의 hello 목록에서 선택 hello 랩을 toocreate hello claimable VM입니다.  
1. Hello 랩에 **개요** 블레이드를 **+ 추가**합니다.  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Hello에 **기본 선택** 블레이드에서 hello VM에 대 한 기준 선택 합니다.
1. Hello에 **가상 컴퓨터** 블레이드에서 hello에 hello 새 가상 컴퓨터에 대 한 이름을 입력 **가상 컴퓨터 이름** 입력란.

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. 입력 한 **사용자 이름** hello 가상 컴퓨터에서 관리자 권한이 부여 되 합니다.  
1. Toouse 원하는에 저장 된 암호 프로그램 [보안 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)을 선택 **저장 된 암호를 사용 하 여**, tooyour 암호 (암호)을 해당 하는 키 값을 지정 합니다. 그렇지 않으면 hello 텍스트 필드에 암호를 입력 **값을 입력**합니다.
1. hello **가상 컴퓨터 디스크 유형** hello 랩에서 hello 가상 컴퓨터에 대 한 허용 되는 저장소 디스크 형식을 결정 합니다.
1. 선택 **가상 컴퓨터 크기** hello 프로세서 코어, RAM 크기 및 hello VM toocreate의 hello 하드 드라이브 크기를 지정 하는 항목을 미리 정의 된 hello 중 하나를 선택 합니다.
1. 선택 **아티팩트** 아티팩트의 hello 목록에서 선택 하 고 원하는 tooadd toohello 기본 이미지 hello 아티팩트를 구성 합니다. 새 tooDevTest 랩 이거나 toohello 참조 아티팩트 구성 [기존 아티팩트 tooa VM 추가](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 섹션 및 다음 완료 되 면 여기로 돌아와 합니다.
1. 선택 **고급 설정** tooconfigure hello VM 네트워크 옵션 및 만료 옵션입니다. 아래 **옵션 클레임**, 선택 **예** claimable toomake hello 컴퓨터.

  ![Toomake hello claimable VM을 선택 합니다.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. 원하는 tooview 또는 hello Azure 리소스 관리자 템플릿을 복사 하는 경우 참조 toohello [저장 Azure 리소스 관리자 템플릿](devtest-lab-add-vm.md#save-azure-resource-manager-template) 섹션을 완료 되 면 여기로 돌아와 합니다.
1. 선택 **만들기** tooadd hello VM toohello 랩을 지정 합니다.
1. hello 랩 블레이드 hello의 상태를 표시 hello VM 만들기-처음으로 **만들기**,으로 다음 **실행** hello VM을 시작한 후입니다.


## <a name="using-a-claimable-vm"></a>클레임할 수 있는 VM 사용

사용자는 다음이 단계 중 하나를 수행 하 여 "Claimable 가상 컴퓨터"의 hello 목록에서 VM을 요구할 수 있습니다.:

* Hello hello 랩 개요 블레이드 맨 아래에 "Claimable 가상 컴퓨터"의 hello 목록에서 hello 목록의 hello Vm 중 하나를 마우스 오른쪽 단추로 클릭 하 고 선택 **클레임 컴퓨터**합니다.

 ![클레임할 수 있는 특정 VM을 요청합니다.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* Hello의 hello 위쪽 **개요** 블레이드에서 선택 **모든 클레임**합니다. Claimable Vm의 hello 목록에서 임의의 가상 컴퓨터 할당 됩니다.

 ![클레임할 수 있는 임의의 VM을 요청합니다.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


사용자가 VM을 클레임한 후에는 사용자의 "내 가상 컴퓨터" 목록으로 이동되고 더 이상 다른 사용자가 클레임할 수 없습니다.

## <a name="next-steps"></a>다음 단계
* 한 번 만든 VM hello, 연결할 수 있습니다 toohello VM을 선택 하 여 **연결** hello VM 블레이드에서 합니다.
* Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
