---
title: "aaaCreate 첫 번째 VM에 Azure DevTest Labs 랩에서 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure DevTest Labs에 랩의 첫 번째 가상 컴퓨터"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs에서 첫 번째 VM 만들기

처음에 DevTest Labs를 액세스 하 고 첫 번째 VM toocreate 원하는 있습니다 때 가능성이 이렇게 하려면 미리 로드를 사용 하 여 [기본 마켓플레이스 이미지](devtest-lab-configure-marketplace-images.md)합니다. 나중에 수 있습니다 수 toochoose에서는 [수식 및 사용자 지정 이미지](devtest-lab-add-vm.md) 더 많은 Vm을 만들 때. 

이 자습서에서는 Azure 포털 tooadd hello를 사용 하 여 첫 번째 VM tooa 랩에서 DevTest Labs 합니다.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>Azure DevTest Labs로 첫 번째 VM tooa 랩을 tooadd 단계
1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
1. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
1. 랩의 hello 목록에서 toocreate hello VM 원하는 hello 랩을 선택 합니다.  
1. Hello 랩에 **개요** 블레이드를 **+ 추가**합니다.  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. Hello에 **기본 선택** 블레이드, 선택는 마켓플레이스 이미지 hello VM에 대 한 합니다.
1. Hello에 **가상 컴퓨터** 블레이드에서 hello에 hello 새 가상 컴퓨터에 대 한 이름을 입력 **가상 컴퓨터 이름** 입력란.

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. 입력 한 **사용자 이름** hello 가상 컴퓨터에서 관리자 권한이 부여 되 합니다.  
1. 레이블이 지정 된 hello 텍스트 필드에 암호를 입력 **값을 입력**합니다.
1. hello **가상 컴퓨터 디스크 유형** hello 랩에서 hello 가상 컴퓨터에 대 한 허용 되는 저장소 디스크 형식을 결정 합니다.
1. 선택 **가상 컴퓨터 크기** hello 프로세서 코어, RAM 크기 및 hello VM toocreate의 hello 하드 드라이브 크기를 지정 하는 항목을 미리 정의 된 hello 중 하나를 선택 합니다.
1. 선택 **아티팩트** -아티팩트-hello 목록에서 선택 하 고 원하는 tooadd toohello 기본 이미지 hello 아티팩트를 구성 합니다.
    **참고:** 새 tooDevTest 랩 이거나 toohello 참조 아티팩트 구성 [기존 아티팩트 tooa VM 추가](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 섹션 및 다음 완료 되 면 여기로 돌아와 합니다.
1. 선택 **만들기** tooadd hello VM toohello 랩을 지정 합니다.

   hello 랩 블레이드 hello의 상태를 표시 hello VM 만들기-처음으로 **만들기**,으로 다음 **실행** hello VM을 시작한 후입니다.

## <a name="next-steps"></a>다음 단계
* 한 번 만든 VM hello, 연결할 수 있습니다 toohello VM을 선택 하 여 **연결** hello VM 블레이드에서 합니다.
* 체크 아웃 [추가 VM tooa 랩](devtest-lab-add-vm.md) 랩에서 다음 Vm을 추가 하는 방법에 대 한 자세한 정보에 대 한 합니다.
* Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)합니다.
