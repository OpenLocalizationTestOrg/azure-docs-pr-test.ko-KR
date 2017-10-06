---
title: "개발자를 위한 Azure DevTest Labs aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure DevTest Labs 개발자 시나리오용입니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a>개발자를 위한 Azure DevTest Labs 사용
DevTest Labs azure 개발자를 위한 DevTest Labs toohost 개발 컴퓨터를 사용 하 여 여러 주요 시나리오 중 하나 hello 기본 시나리오 중 하나를 사용 하는 tooimplement 될 수 있습니다. 이 시나리오에서 DevTest Labs는 다음과 같은 이점을 제공합니다.

- 개발자는 필요에 따라 개발 컴퓨터를 신속하게 프로비전할 수 있습니다.
- 개발자는 필요할 때마다 개발 컴퓨터를 쉽게 사용자 지정할 수 있습니다.
- 관리자는 다음을 확인하여 비용을 제어할 수 있습니다.
  - 개발자는 개발에 필요한 것보다 더 많은 VM을 가져올 수 없습니다.
  - VM은 사용되지 않을 때 종료됩니다. 

![학습에 DevTest Labs 사용](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

이 문서에서는 사용 되는 toomeet 개발자 요구 사항 및 랩을 tooset를 따를 수 하는 자세한 단계 hello 수 있는 다양 한 Azure DevTest Labs 기능에 대 한 설명입니다.

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a>Azure DevTest Labs를 사용하여 개발자 환경 구현
1. **Hello 랩 만들기** 
   
    랩은 hello Azure DevTest Labs의 시작 위치입니다. 랩을 만든 후 사용자 (개발자) toohello 랩, 설정 정책 toocontrol 비용을 신속 하 게 만들 수 있는 VM 이미지를 정의 및 추가 같은 작업을 수행할 수 있습니다.  
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure DevTest Labs에서 랩 만들기](devtest-lab-create-lab.md) |Toocreate 랩에서 DevTest Labs를 Azure에는 Azure 포털 hello 하는 방법에 대해 알아봅니다. |
2. **바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 VM 만들기** 
   
    Hello Azure Marketplace에서에서 다양 한 이미지에서에서 즉시 사용 가능한 이미지를 선택 하 고 hello 랩에서 사용할 수 있도록 수 있습니다. Hello 즉시 사용 가능한 이미지 요구 사항을 충족 하지 않는 경우에 랩 hello 랩에 대 한 사용자 지정 이미지로 Azure 마켓플레이스를 필요한 모든 hello 소프트웨어를 설치 하 고 저장 하는 hello VM에서 이미 만들어진 이미지를 사용 하 여 VM을 만들어 사용자 지정 이미지를 만들 수 있습니다.

    사용자 지정 이미지를 사용 하는 경우 이미지 팩터리 toocreate를 사용 하 여 분산 하 여 이미지 합니다. 이미지 팩터리는 구성된 이미지를 자동으로 정기적으로 작성 및 배포하는 "코드로 구성" 솔루션입니다. 이 저장 hello 필요한 시간 toomanually hello로 VM이 만들어진 후 hello 시스템 구성 운영 체제를 기반 합니다.
  
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure Marketplace 이미지 구성](devtest-lab-configure-marketplace-images.md) |방법을 알아봅니다 화이트 리스트 Azure 마켓플레이스 이미지 hello 개발자를 위한 원하는 선택만 hello 이미지를 사용할 수 있도록 합니다.|
   | [사용자 지정 이미지 만들기](devtest-lab-create-template.md) |사전 개발자 hello 사용자 지정 이미지를 사용 하는 VM을 신속 하 게 만들 수 있도록 해야 하는 hello 소프트웨어를 설치 하 여 사용자 지정 이미지를 만듭니다.|
   | [이미지 팩터리에 대한 자세한 정보](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |설명 하는 비디오를 시청 방법을 tooset 및 이미지 팩터리를 사용 합니다.|

3. **개발자 컴퓨터에 대한 재사용 가능 템플릿 만들기** 
   
    Azure DevTest Labs의 수식에서는 toocreate VM을 사용 하는 기본 속성 값의 목록입니다. 이미지, VM 크기 (CPU 및 RAM의 조합), 및 가상 네트워크를 선택 하 여 hello 랩에서 수식을 만들 수 있습니다. 각 개발자 hello 랩에서 hello 수식을 보고 toocreate VM을 사용할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [DevTest Labs 수식 toocreate Vm 관리](devtest-lab-manage-formulas.md) |이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.|

4. **아티팩트 tooenable 유연한 VM 사용자 지정 만들기**

   아티팩트는 사용 되는 toodeploy 및 VM 프로 비전 된 후 응용 프로그램을 구성 합니다. 아티팩트는 다음과 같을 수 있습니다.

   - 에이전트, Fiddler 및 Visual Studio와 같은 VM-hello에 tooinstall 원하는 도구입니다.
   - 리포지토리 복제 같은 VM-hello에 toorun 되도록 동작입니다.
   - 응용 프로그램 tootest 한다는 것입니다.

   많은 아티팩트는 이미 기본 제공되어 있습니다. 특정 요구에 맞게 추가로 사용자 지정하려는 경우 사용자 고유의 사용자 지정 아티팩트를 만들 수 있습니다.

   다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기](devtest-lab-artifact-author.md) |랩에서 hello 가상 컴퓨터에 대 한 사용자 고유의 사용자 지정 아티팩트를 만듭니다.|
   | [Azure DevTest Labs에서 Git 리포지토리 toostore 사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿을 사용 하기 위해 추가](devtest-lab-add-artifact-repo.md) |자세한 내용은 방법 toostore 자신의 개인 Git 리포지토리에 있는 사용자 지정 아티팩트입니다.|

5. **비용 제어**
   
    DevTest Labs를 azure에 hello 랩 toospecify hello 최대 Vm 수 hello 랩에서 개발자가 만들 수 있는 정책을 tooset를 허용 합니다. 
   
    개발자 팀에 작업 일정 집합 toostop 모든 hello Vm hello 하루 중 특정 시간에을 자동으로 다시 시작을 하루 뒤 hello을 쉽게 매핑할 수 있습니다 하는 설정 자동 종료 및 정책에 의해 자동으로 시작 hello 랩에서 합니다. 
   
    마지막으로, 앱 개발이 완료 되 면 여 삭제할 수 있습니다 모든 hello Vm을 한 번에 단일 PowerShell 스크립트를 실행 합니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [랩 정책 정의](devtest-lab-set-lab-policy.md) |Hello 랩에서 정책을 설정 하 여 비용을 제어 합니다. |
   | [모든 hello 랩 PowerShell 스크립트를 사용 하 여 Vm을 삭제 합니다.](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |개발이 완료 되 면 한 번에 모든 hello labs를 삭제 합니다.|

1. **가상 네트워크 tooa VM 추가** 
   
    DevTest Labs는 랩이 생성될 때마다 새 VNET(가상 네트워크)를 만듭니다. -예를 들어 사이트 간 VPN 또는 express 경로 사용 하는 – 여 사용자 고유의 VNET을 구성한 경우에 Vm을 만들 때 사용할 수 있도록이 VNET tooyour 랩의 가상 네트워크 설정을 추가할 수 있습니다.

    또한 Azure Active Directory 도메인 가입 아티팩트 hello VM이 생성 될 때 VM tooa 도메인에 가입 됩니다는 사용할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure DevTest Labs에서 가상 네트워크 구성](devtest-lab-configure-vnet.md) |Tooconfigure Azure DevTest Labs를 사용 하 여 가상 네트워크를 Azure 포털 hello 하는 방법에 대해 알아봅니다.|

6. **Hello 랩 각 개발자와 공유**
   
    개발자와 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다. 도 있지 않아도 toohave Azure 계정을 보유 하는 [Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)합니다. 개발자는 다른 개발자가 만든 VM을 볼 수 없습니다.  
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [개발자 tooa 랩 Azure DevTest Labs에 추가](devtest-lab-add-devtest-user.md) |Azure 포털 tooadd 개발자 tooyour 랩 hello를 사용 합니다.|
   | [PowerShell 스크립트를 사용 하 여 개발자가 toohello 랩을 추가합니다](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |PowerShell tooautomate 개발자 tooyour 랩 추가 사용 합니다. |
   | [링크 toohello 랩 가져오기](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |개발자가 하이퍼링크를 통해 랩에 직접 액세스하는 방법을 알아봅니다.|

7. **추가 팀을 위한 랩 생성 자동화** 
   
    사용자 지정 설정을 포함 하 여 리소스 관리자 템플릿을 만들어 사용 하 여 동일한 랩 toocreate 나중에 다시 랩 만들기를 자동화할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Resource Manager 템플릿을 사용하여 랩 만들기](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

