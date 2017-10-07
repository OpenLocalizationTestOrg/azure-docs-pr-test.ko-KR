---
title: "Azure DevTest Labs toocreate Vm에서에서 aaaManage 수식을 | Microsoft Docs"
description: "자세한 내용은 방법 tooupdate 및 제거 하는 Azure DevTest Labs 수식"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Azure DevTest Labs 수식 관리

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

이 문서에서는 설명 방법을 toocreate (사용자 지정 이미지, 마켓플레이스 이미지 또는 다른 수식) 자료 또는 기존 VM에서 수식입니다. 이 문서에서 기존 수식을 관리하는 방법을 안내합니다.

## <a name="create-a-formula"></a>수식 만들기
DevTest Labs 가진 사람이 면 누구나 *사용자* 수 toocreate Vm 수식을 기반으로 사용 하는 합니다. 두 가지가 toocreate 수식: 

* 기본-에서 toodefine hello 수식의 hello 특성을 모두를 원하는 경우를 사용 합니다.
* 기존 랩을 VM-toocreate 수식 hello의 설정을 기반으로 기존 VM 원할 때 사용 합니다.

사용자 및 사용 권한을 추가하는 방법에 대한 자세한 내용은 [Azure DevTest Labs에 소유자 및 사용자 추가](./devtest-lab-add-devtest-user.md)를 참조하세요.

### <a name="create-a-formula-from-a-base"></a>기준에서 수식 만들기
단계를 수행 하는 hello 사용자 지정 이미지, 마켓플레이스 이미지 또는 다른 수식에서 수식을 만드는 hello 과정을 안내 합니다.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.

2. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.

3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  

4. Hello 랩 블레이드에서 선택 **수식 (다시 사용할 수 있는 자료)**합니다.
   
    ![수식 메뉴](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Hello에 **수식** 블레이드를 **+ 추가**합니다.
   
    ![수식 추가](./media/devtest-lab-create-formulas/add-formula.png)

6. Hello에 **기본 선택** 블레이드에서 toocreate hello 수식이 들어 있는 select hello 자료 (사용자 지정 이미지, 마켓플레이스 이미지 또는 수식을).
   
    ![기본 목록](./media/devtest-lab-create-formulas/base-list.png)

7. Hello에 **수식을 만들** 블레이드에서 hello 다음 값을 지정 합니다.
   
    * **수식 이름** - 수식의 이름을 입력합니다. 이 값은 VM을 만들 때 기본 이미지의 hello 목록에 표시 됩니다. hello 이름은 입력 하 고 메시지에 대 한 올바른 이름 hello 요구 사항을 나타냅니다 유효 하지 않은 경우 유효성이 검사 됩니다.
    * **설명** - 수식에 대한 의미 있는 설명을 입력합니다. 이 값은 VM을 만들 때 hello 수식 상황에 맞는 메뉴에서 사용할 수 있습니다.
    * **사용자 이름** - 관리자 권한이 부여된 사용자 이름을 입력합니다.
    * **암호** -입력 또는 hello 드롭다운에서 선택 hello 지정 된 사용자에 대 한 toouse 되도록 hello 암호 (암호)와 연결 된 값입니다. Hello 비밀 정보에 대 한 자세한 내용은 참조 [Azure DevTest Labs: 개인 비밀 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/)합니다.
    * **가상 컴퓨터 디스크 유형** -HDD (하드 디스크 드라이브) 중 하나를 지정 하거나이 기본 이미지를 사용 하 여 hello 가상 컴퓨터에는 저장소 디스크 형식을 SSD (반도체 드라이브) tooindicate 허용 됩니다.
    * * * 가상 컴퓨터 크기 * *-hello 프로세서 코어, RAM 크기 및 hello VM toocreate의 hello 하드 드라이브 크기를 지정 하는 미리 정의 된 hello 항목 중 하나를 선택 합니다. 
    * **아티팩트** -선택 tooopen hello **아티팩트 추가** 선택 지정 하 고 원하는 tooadd toohello 기본 이미지 hello 아티팩트를 구성 합니다. 아티팩트에 대한 자세한 내용은 [Azure DevTest Labs에서 VM 아티팩트 관리](./devtest-lab-add-vm-with-artifacts.md)를 참조하세요.
    * **고급 설정** -선택 tooopen hello **고급** hello 다음 설정을 구성한 블레이드:
        * **가상 네트워크** -hello 필요한 가상 네트워크를 지정 합니다.
        * **서브넷** -원하는 hello 서브넷을 지정 합니다.    
        * **IP 주소 구성을** -hello Public, Private 또는 공유 IP 주소 여부를 지정 합니다. 공유 IP 주소에 대한 자세한 내용은 [Azure DevTest Labs에서 공유 IP 주소 이해](./devtest-lab-shared-ip.md)를 참조하세요.
        * **이 컴퓨터를 claimable 게** -있는지 것 할당 되지 것입니다 소유권 hello 생성 시 의미 "claimable"는 컴퓨터를 만드는 합니다. 대신 랩 사용자 hello 랩 블레이드에서 수 tootake 소유권 ("클레임") hello 컴퓨터 됩니다.     
    * **이미지** -이 필드 hello 이전 블레이드에서 선택한 hello 기본 이미지의 이름을 표시 합니다. 
     
       ![Create formula](./media/devtest-lab-create-formulas/create-formula.png)

8. 선택 **만들기** toocreate hello 수식입니다.

9. Hello hello 목록에 표시 하는 hello 수식을 만들 때 **수식** 블레이드입니다.

### <a name="create-a-formula-from-a-vm"></a>VM에서 수식 만들기
hello 다음 단계를 안내해 hello 수식을 기반으로 기존 VM을 만드는 과정을 통해. 

> [!NOTE]
> VM에서 수식을 toocreate hello VM 만들어야 2016 년 3 월 30 일 후 합니다. 
> 
> 

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  
4. Hello 랩에 **개요** 블레이드에서 toocreate hello 수식 원하는 선택 hello VM입니다.
   
    ![랩 VM](./media/devtest-lab-create-formulas/my-vms.png)
5. Hello VM 블레이드에서 선택 **(다시 사용할 수 있는 기본) 수식 만들기**합니다.
   
    ![Create formula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Hello에 **수식을 만들** 블레이드를 입력 한 **이름** 및 **설명** 새 수식에 대 한 합니다.
   
    ![수식 만들기 블레이드](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. 선택 **확인** toocreate hello 수식입니다.

## <a name="modify-a-formula"></a>수식 수정
수식 toomodify 다음이 단계를 따르십시오.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  
4. Hello 랩 블레이드에서 선택 **수식 (다시 사용할 수 있는 자료)**합니다.
   
    ![수식 메뉴](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Hello에 **랩 수식** 블레이드, toomodify 원하는 선택 hello 수식입니다.
6. Hello에 **수식을 업데이트** 블레이드에서 원하는 hello를 편집 하 고 선택 **업데이트**합니다.

## <a name="delete-a-formula"></a>수식 삭제
수식 toodelete 다음이 단계를 따르십시오.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  
4. Hello 랩에 **설정** 블레이드를 **수식**합니다.
   
    ![수식 메뉴](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Hello에 **랩 수식** 원하는 toodelete 블레이드, 선택 hello 줄임표 toohello hello 수식의 오른쪽입니다.
   
    ![수식 메뉴](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Hello 수식 상황에 맞는 메뉴에서 선택 **삭제**합니다.
   
    ![수식 상황에 맞는 메뉴](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. 선택 **예** toohello 삭제 확인 대화 상자.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>관련 블로그 게시물
* [사용자 지정 이미지 또는 수식?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>다음 단계
사용에 대 한 수식을 만든 VM을 만들 때, hello에는 너무[추가 VM tooyour 랩](devtest-lab-add-vm-with-artifacts.md)합니다.

