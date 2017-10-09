---
title: "기계 학습 작업 영역 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure 기계 학습 스튜디오 작업 영역"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Azure 기계 학습 작업 영역 만들기 및 공유
이 메뉴 tootopics tooset hello 다양 한 데이터 과학 환경에서 어떻게 사용 hello Cortana 분석 프로세스 (CAP)를 설명 하는 연결 합니다.

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Azure 기계 학습 스튜디오 toouse toohave 기계 학습 작업 영역 필요합니다. 이 작업 영역에 toocreate 필요한 hello 도구, 관리 하 고 실험을 게시 합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate 작업 영역
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)

    > [!NOTE]
    > toosign 작업 영역을 만들 toobe Azure 구독 관리자가 사용 해야 합니다. 
    >
    > 

2. **+새로 만들기**를 클릭합니다.

3. **인텔리전스 + 분석**을 선택하고 **Machine Learning 작업 영역**을 클릭한 후 **만들기**를 클릭합니다.

4. 작업 영역 정보를 입력합니다.

    - hello *작업 영역 이름을* too260 문자, 공간에서 종료 되지 않는 up 될 수 있습니다. hello 이름은 다음이 문자를 포함할 수 없습니다.`< > * % & : \ ? + /`
    - hello *웹 서비스 계획* (또는 만들기)을 하면 연결 된 hello 함께 *가격 책정 계층* 선택,이 작업 영역에서 웹 서비스를 배포 하는 경우 사용 됩니다.

    ![새 작업 영역 만들기](media/machine-learning-create-workspace/create-new-workspace.png)

5. **만들기**

Hello 작업 영역을 배포한 후에 기계 학습 스튜디오에서 열 수 있습니다.

1. 찾아보기 tooMachine 학습 스튜디오에서 [https://studio.azureml.net/](https://studio.azureml.net/)합니다.

2. Hello 오른쪽 위 모서리에 작업 영역을 선택 합니다.

    ![작업 영역 선택](media/machine-learning-create-workspace/open-workspace.png)

3. **내 실험**을 클릭합니다.

    ![실험 열기](media/machine-learning-create-workspace/my-experiments.png)

작업 영역을 관리하는 방법에 대한 자세한 내용은 [Azure 기계 학습 작업 영역 관리](machine-learning-manage-workspace.md)를 참조하세요.
작업 영역을 만드는 동안 문제가 발생 하면 참조 [Troubleshooting guide: 만들고 tooa 기계 학습 작업 영역 연결](machine-learning-troubleshooting-creating-ml-workspace.md)합니다.


## <a name="sharing-an-azure-machine-learning-workspace"></a>Azure 기계 학습 작업 영역 공유
기계 학습 작업 영역을 만든 후에 사용자가 tooyour 작업 영역 tooshare access tooyour 작업 영역 및 모든 해당 실험, 데이터 집합, 전자 필기장 등 초대할 수 있습니다. 이 두 역할 중 하나에 사용자를 추가할 수 있습니다.

* **사용자** -작업 영역 사용자 수 만들고, 열고, 수정, 실험, 데이터 집합, 등 hello 작업 영역에서 삭제 합니다.
* **소유자** -소유자 초대할 수 하 고 사용자 추가 toowhat 사용자의에서 hello 작업 영역에서 작업을 수행할 수 있습니다.

> [!NOTE]
> hello 작업 영역을 만들고 hello 관리자 계정으로 작업 영역 소유자 toohello 작업 영역을 추가 됩니다. 그러나 다른 관리자나 사용자가 구독 자동으로 해제 될 수 있는 액세스 권한을 부여한 toohello 작업 영역-tooinvite 필요한을 명시적으로 합니다.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare 작업 영역

1. TooMachine 학습 스튜디오에 로그인 [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. Hello 왼쪽된 패널에서 **설정**

3. Hello 클릭 **사용자** 탭

4. 클릭 **더 사용자 초대** hello hello 페이지 맨 아래에

    ![Studio 설정](media/machine-learning-create-workspace/settings.png)

5. 하나 이상의 전자 메일 주소를 입력합니다. hello 사용자 유효한 Microsoft 계정 또는 조직 계정 (Azure Active Directory)에서 필요합니다.

6. 소유자 또는 사용자로 tooadd hello 사용자가 할 것인지를 선택 합니다.

7. Hello 클릭 **확인** 확인 표시 단추입니다.

추가한 각 사용자 toosign toohello에서 작업 영역을 공유 하는 방법에 대 한 설명이 이메일을 받게 됩니다.

> [!NOTE]
> 사용자가 toobe 수 toodeploy에 대 한이 작업 영역에서 웹 서비스를 관리 하거나 참가자 또는 hello Azure 구독에서에서 관리자 여야 합니다. 



