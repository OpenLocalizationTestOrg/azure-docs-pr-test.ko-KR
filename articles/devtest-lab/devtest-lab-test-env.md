---
title: "VM 및 PaaS aaaUse Azure DevTest Labs 테스트 환경 | Microsoft Docs"
description: "VM 및 PaaS toouse Azure DevTest Labs 환경 시나리오를 테스트 하는 방법에 대해 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>VM 및 PaaS 테스트 환경에 Azure DevTest Labs 사용

Azure DevTest Labs tooimplement 여러 주요 시나리오를 사용할 수 있습니다 하지만 기본 시나리오에서는 DevTest Labs toohost 컴퓨터를 사용 하 여 테스터에 대 한 합니다. 

이 시나리오에서 DevTest Labs는 다음과 같은 이점을 제공합니다.

- 테스터 신속 하 게 다시 사용할 수 있는 템플릿 및 아티팩트를 사용 하 여 Windows 및 Linux 환경 프로 비전 하 여 hello 응용 프로그램의 최신 버전을 테스트할 수 있습니다.
- 테스터가 다수의 테스트 에이전트를 프로비전하여 부하 테스트를 강화할 수 있습니다.
- 관리자는 다음을 확인하여 비용을 제어할 수 있습니다.
  - 테스터는 VM을 필요 이상으로 가질 수 없습니다.
  - VM은 사용되지 않을 때 종료됩니다.

![학습에 DevTest Labs 사용](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

이 문서에서는 다양 한 Azure DevTest Labs 사용 되는 기능 toomeet 테스터 요구 사항 및 자세한 단계 toofollow tooset 랩을 hello 합니다.

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>Azure DevTest Labs를 사용하여 테스트 환경 구현
1. **Hello 랩 만들기** 
   
    랩은 hello Azure DevTest Labs의 시작 위치입니다. 랩을 만든 후 사용자 (테스터) toohello 랩, 설정 정책 toocontrol 비용을 신속 하 게 만들 수 있는 VM 이미지를 정의 및 추가 같은 작업을 수행할 수 있습니다.  
   
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
   | [Azure Marketplace 이미지 구성](devtest-lab-configure-marketplace-images.md) |방법을 알아봅니다 화이트 리스트 Azure 마켓플레이스 이미지 hello 테스터에 대해 원하는 선택만 hello 이미지를 사용할 수 있도록 합니다.|
   | [사용자 지정 이미지 만들기](devtest-lab-create-template.md) |사전 테스터 hello 사용자 지정 이미지를 사용 하는 VM을 신속 하 게 만들 수 있도록 해야 하는 hello 소프트웨어를 설치 하 여 사용자 지정 이미지를 만듭니다.|
   | [이미지 팩터리에 대한 자세한 정보](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |설명 하는 비디오를 시청 방법을 tooset 및 이미지 팩터리를 사용 합니다.|

3. **테스트 컴퓨터에 재사용 가능한 템플릿 만들기** 
   
    Azure DevTest Labs의 수식에서는 toocreate VM을 사용 하는 기본 속성 값의 목록입니다. 이미지, VM 크기 (CPU 및 RAM의 조합), 및 가상 네트워크를 선택 하 여 hello 랩에서 수식을 만들 수 있습니다. 각 테스터 hello 랩에서 hello 수식을 보고 toocreate VM을 사용할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [DevTest Labs 수식 toocreate Vm 관리](devtest-lab-manage-formulas.md) |이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.|

3. **다중 VM 테스트 환경 만들기** 
   
    Azure 리소스 관리자 템플릿 toodefine hello 인프라 및 Azure 솔루션의 구성을 사용할 수 있으며 여러 테스트 Vm 일관 된 상태에서 반복적으로 배포 수 있습니다.

    Azure PaaS 리소스는 Resource Manager 템플릿의 환경에서 프로비전할 수 있고 비용 추적에 표시됩니다. 그러나 VM 자동 종료 tooPaaS 리소스 적용 되지 않습니다.

    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스 만들기](devtest-lab-create-environment-from-arm.md) |테스트 환경에 일관된 상태로 여러 VM을 배포하는 방법에 대해 알아봅니다.|

4. **아티팩트 tooenable 유연한 VM 사용자 지정 만들기**

   아티팩트는 사용 되는 toodeploy 및 VM 프로 비전 된 후 응용 프로그램을 구성 합니다. 아티팩트는 다음과 같을 수 있습니다.

   - 에이전트, Fiddler 및 Visual Studio와 같은 VM-hello에 tooinstall 원하는 도구입니다.
   - 리포지토리 복제 같은 VM-hello에 toorun 되도록 동작입니다.
   - 응용 프로그램 tootest 한다는 것입니다.

   많은 아티팩트는 이미 기본 제공되어 있습니다. 특정 요구에 맞게 추가로 사용자 지정하려는 경우 자시만의 사용자 지정 아티팩트를 만들 수 있습니다.

   다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기](devtest-lab-artifact-author.md) |랩에서 hello 가상 컴퓨터에 대 한 사용자 고유의 사용자 지정 아티팩트를 만듭니다.|
   | [Azure DevTest Labs에서 Git 리포지토리 toostore 사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿을 사용 하기 위해 추가](devtest-lab-add-artifact-repo.md) |자세한 내용은 방법 toostore 자신의 개인 Git 리포지토리에 있는 사용자 지정 아티팩트입니다.|

5. **비용 제어**
   
    Azure DevTest Labs hello 랩 toospecify hello 최대 Vm 수 hello 랩에서 테스터에 의해 만들어진에 tooset 정책을 허용 합니다. 
   
    테스트 팀에 작업 일정 집합 toostop 모든 hello Vm hello 하루 중 특정 시간에을 자동으로 다시 시작을 하루 뒤 hello을 쉽게 매핑할 수 있습니다 하는 설정 자동 종료 및 정책에 의해 자동으로 시작 hello 랩에서 합니다. 
   
    마지막으로, 앱 개발이 완료 되 면 여 삭제할 수 있습니다 모든 hello Vm을 한 번에 단일 PowerShell 스크립트를 실행 합니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [랩 정책 정의](devtest-lab-set-lab-policy.md) |Hello 랩에서 정책을 설정 하 여 비용을 제어 합니다. |
   | [모든 hello 랩 PowerShell 스크립트를 사용 하 여 Vm을 삭제 합니다.](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |테스트가 완료 되 면 한 번에 모든 hello labs를 삭제 합니다.|

1. **가상 네트워크 tooa 랩 추가** 
   
    DevTest Labs는 랩이 생성될 때마다 새 VNET(가상 네트워크)를 만듭니다. -예를 들어 사이트 간 VPN 또는 express 경로 사용 하는 – 여 사용자 고유의 VNET을 구성한 경우에 Vm을 만들 때 사용할 수 있도록이 VNET tooyour 랩의 가상 네트워크 설정을 추가할 수 있습니다.

    또한 Azure Active Directory 도메인 가입 아티팩트 사용할 수 있는 hello VM이 생성 될 때 VM tooa 도메인에 가입 하는 합니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure DevTest Labs에서 가상 네트워크 구성](devtest-lab-configure-vnet.md) |Tooconfigure Azure DevTest Labs를 사용 하 여 가상 네트워크를 Azure 포털 hello 하는 방법에 대해 알아봅니다.|

6. **각 테스터와 hello 랩 공유**
   
    테스터와 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다. 도 있지 않아도 toohave Azure 계정을 보유 하는 [Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)합니다. 테스터는 다른 테스터가 만든 VM을 볼 수 없습니다.  
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure DevTest Labs에서 테스터 tooa 랩 추가](devtest-lab-add-devtest-user.md) |Azure 포털 tooadd 테스터 tooyour 랩 hello를 사용 합니다.|
   | [PowerShell 스크립트를 사용 하 여 테스터 toohello 랩을 추가합니다](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |PowerShell tooautomate 테스터 tooyour 랩 추가 사용 합니다. |
   | [링크 toohello 랩 가져오기](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |테스터가 하이퍼링크를 통해 랩에 직접 액세스하는 방법을 알아봅니다.|

7. **추가 팀을 위한 랩 생성 자동화** 
   
    사용자 지정 설정을 포함 하 여 리소스 관리자 템플릿을 만들어 사용 하 여 동일한 랩 toocreate 나중에 다시 랩 만들기를 자동화할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Resource Manager 템플릿을 사용하여 랩 만들기](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

