---
title: "Azure DevTest Labs VM에서 아티팩트 실패 진단 | Microsoft Docs"
description: "DevTest Labs에서 아티팩트 실패 문제를 해결하는 방법 알아보기"
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
ms.openlocfilehash: e4f2946d0ba0756f36622aded0e8594acabb9527
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="diagnose-artifact-failures-in-the-lab"></a>랩에서 아티팩트 실패 진단 
아티팩트를 만든 후에 성공 또는 실패 여부를 확인할 수 있습니다. DevTest Labs의 아티팩트 로그는 아티팩트 실패를 진단하는 데 사용할 수 있는 정보를 제공합니다. Windows VM에 대한 아티팩트 로그 정보를 볼 수 있는 몇 가지 방법이 있습니다.

> [!NOTE]
> 실패가 올바르게 식별되고 설명되었는지 확인하려면 아티팩트가 제대로 구성되는 것이 중요합니다. 아티팩트를 올바르게 만드는 방법에 대한 정보는 [사용자 지정 아티팩트 만들기](devtest-lab-artifact-author.md)를 참조하세요. 올바르게 구조화된 아티팩트의 예를 보려면 이 [테스트 매개 변수 형식](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) 아티팩트를 확인하세요.

## <a name="troubleshoot-artifact-failures-using-the-azure-portal"></a>Azure Portal을 사용하여 아티팩트 실패 문제 해결
아티팩트를 만드는 동안 Azure Portal을 사용하여 실패를 진단하려면 다음 단계를 수행합니다.

1. 리소스의 목록에서 랩을 선택합니다.

2. 조사하려는 아티팩트를 포함하는 Windows VM을 선택합니다.

3. **일반** 아래의 왼쪽 패널에서 **아티팩트**를 선택합니다. 아티팩트의 이름 및 해당 상태를 나타내는 해당 VM과 연결된 아티팩트 목록이 표시됩니다.

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. **실패**의 상태를 보여 주는 아티팩트를 선택합니다. 아티팩트가 열리고 아티팩트의 실패에 대한 세부 정보를 포함하는 확장 메시지를 표시합니다.

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-the-vm"></a>VM 내에서 아티팩트 실패 문제 해결
가상 컴퓨터 내에서 아티팩트 로그를 보려면 다음 단계를 수행합니다.

1. 진단하려는 아티팩트를 포함하는 VM에 로그인합니다.

2. C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status로 이동합니다. 여기서 "1.9"는 CSE 버전 번호입니다.

   ![아티팩트 Git 리포지토리 예](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. **상태** 파일을 열어 해당 VM에 대한 아티팩트 실패를 진단하는 데 도움이 되는 정보를 봅니다.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>관련 블로그 게시물
* [Azure DevTest Labs에서 리소스 관리자 템플릿을 사용하여 기존 AD 도메인에 VM 가입](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>다음 단계
* [랩에 Git 리포지토리를 추가](devtest-lab-add-artifact-repo.md)하는 방법에 대해 알아봅니다.

