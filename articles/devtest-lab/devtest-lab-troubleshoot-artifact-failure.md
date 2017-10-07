---
title: "DevTest Labs Azure VM의 aaaDiagnose 아티팩트 오류 | Microsoft Docs"
description: "자세한 내용은 방법에서 DevTest Labs tootroubleshoot 아티팩트 오류"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Hello 랩에서 아티팩트 오류를 진단 
아티팩트를 만든 후에 성공 또는 실패 하는 경우 toosee를 확인할 수 있습니다. DevTest Labs에서 아티팩트 로그 toodiagnose 아티팩트 오류를 사용할 수 있는 정보를 제공 합니다. Windows VM에 대 한 hello 아티팩트 로그 정보를 볼 수는 몇 가지가 있습니다.

> [!NOTE]
> tooensure 실패는 올바르게 식별 및 설명,이 hello 아티팩트 제대로 구성 되어 중요 합니다. Toocorrectly 아티팩트를 생성 하는 방법에 대 한 정보를 참조 하십시오. [사용자 지정 아티팩트를 만들](devtest-lab-artifact-author.md)합니다. 하 고 올바르게 구조화 된 아티팩트의 예로 toosee이 [테스트 매개 변수 형식](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) 아티팩트입니다.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 아티팩트 오류 문제 해결
다음이 단계를 수행 하는 아티팩트를 만드는 동안 toouse hello Azure 포털 toodiagnose 오류가 발생 했습니다.

1. 리소스의 hello 목록에서 랩을 선택 합니다.

2. Hello tooinvestigate 원하는 hello 아티팩트를 포함 하는 Windows VM을 선택 합니다.

3. 아래에 hello 왼쪽된 패널에 **일반**, 선택 **아티팩트**합니다. 해당 VM과 연결 된 아티팩트 목록이 표시를 나타내는 hello 이름 hello 아티팩트 및 서버 인스턴스의 상태입니다.

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. **실패**의 상태를 보여 주는 아티팩트를 선택합니다. hello 아티팩트가 열리고 hello 아티팩트 hello 실패에 대 한 세부 정보가 포함 된 확장 메시지를 표시 합니다.

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Hello VM 내에서 아티팩트 오류 문제 해결
hello 가상 컴퓨터 내에서 tooview hello 아티팩트 로그에서 다음이 단계를 따르십시오.

1. Toohello toodiagnose 원하는 hello 아티팩트를 포함 하는 VM에에서 로그인 합니다.

2. 여기서 "1.9는 hello CSE 버전 번호 tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status 이동입니다.

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. 열기 hello **상태** 파일 tooview 정보 해당 VM에 대 한 아티팩트 실패를 진단 하는 데 도움이 됩니다.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>관련 블로그 게시물
* [VM tooexisting Azure DevTest Labs에서 리소스 관리자 템플릿을 사용 하는 AD 도메인 가입](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[Git 리포지토리 tooa 랩 추가](devtest-lab-add-artifact-repo.md)합니다.

