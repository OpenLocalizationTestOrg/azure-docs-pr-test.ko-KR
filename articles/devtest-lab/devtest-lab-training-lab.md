---
title: "학습에 대 한 Azure DevTest Labs aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 교육 시나리오에 대 한 Azure DevTest Labs toouse 합니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>학습에 Azure DevTest Labs 사용
Azure DevTest Labs 사용된 tooimplement 더하기 toodev/테스트에 여러 주요 시나리오 일 수 있습니다. 이러한 시나리오 중 하나는 학습에 랩을 tooset 합니다. Azure DevTest Labs 사용 하면 사용자 지정 서식 파일을 제공할 수 있는 랩 toocreate 각 학습자를 학습에 toocreate 동일 하 고 격리 된 환경을 사용할 수 있습니다. 정책을 tooensure 학습 환경은 사용할 수 있는 tooeach 학습자 필요 하며 충분 한 리소스-hello 학습에 필요한 가상 컴퓨터-예: 포함 하는 경우에 적용할 수 있습니다. 마지막으로, 한 번의 클릭에서 액세스할 수 있는 교육와 hello 랩 쉽게 공유할 수 있습니다.

![학습에 DevTest Labs 사용](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs 가상 환경에서 필요한 tooconduct 학습 된 요구 사항을 준수 하는 hello를 충족 합니다. 

* 실습생은 다른 실습생이 만든 VM을 볼 수 없습니다.
* 모든 학습 컴퓨터는 동일해야 합니다.
* 실습생은 학습 환경을 신속하게 프로비전할 수 있습니다.
* 교육을 사용 하지 않는 경우 hello 교육 및 Vm 종료에 대 한 필요한 보다 더 많은 Vm을 가져올 수 없습니다 되도록 하 여 비용을 제어 합니다.
* Hello 교육 랩 각 학습자와 쉽게 공유할 수
* 나중에 다시 교육 랩 hello를 다시 사용

이 문서에서는 배웁니다 사용할 수 있는 다양 한 Azure DevTest Labs 기능에 대 한 toomeet hello 앞에서 설명한 교육 요구 사항 및 단계 학습을 위해 랩을 tooset를 따를 수 있습니다.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Azure DevTest Labs로 학습 구현
1. **Hello 랩 만들기** 
   
    랩은 hello Azure DevTest Labs의 시작 위치입니다. 랩을 만든 후 같은 추가 사용자 (교육) toohello 랩 정책 toocontrol 비용을 설정 하 고, 정의 VM 이미지를 신속 하 게 만들 수 있는 작업을 수행할 수 있습니다.   
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure DevTest Labs에서 랩 만들기](devtest-lab-create-lab.md) |Toocreate 랩에서 DevTest Labs를 Azure에는 Azure 포털 hello 하는 방법에 대해 알아봅니다. |
2. **바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 학습 VM 만들기** 
   
    Hello Azure Marketplace에서에서 다양 한 이미지에서에서 즉시 사용 가능한 이미지를 선택 하 고 hello 랩에서 hello 교육에 사용할 수 있도록 수 있습니다. 즉시 사용 가능한 이미지 hello 요구 사항을 충족 하지 않는 경우에 랩 hello 랩의 사용자 지정 이미지로 hello VM 저장 하 고 hello 학습에 필요한 모든 hello 소프트웨어를 설치 하는 Azure 마켓플레이스의 즉시 사용 가능한 이미지를 사용 하 여 VM을 만들어 사용자 지정 이미지를 만들 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Azure Marketplace 이미지 구성](devtest-lab-configure-marketplace-images.md) |화이트 리스트 Azure 마켓플레이스 이미지; 방법을 알아봅니다 hello 학습에 사용할 선택만 hello 이미지에 대 한 사용 가능 합니다. |
   | [사용자 지정 이미지 만들기](devtest-lab-create-template.md) |사전 교육 hello 사용자 지정 이미지를 사용 하는 VM을 신속 하 게 만들 수 있도록 hello 학습에 필요한 hello 소프트웨어를 설치 하 여 사용자 지정 이미지를 만듭니다. |
3. **학습용 컴퓨터에 대한 재사용 가능 템플릿 만들기** 
   
    Azure DevTest Labs의 수식에서는 toocreate VM을 사용 하는 기본 속성 값의 목록입니다. 이미지, VM 크기 (CPU 및 RAM의 조합), 및 가상 네트워크를 선택 하 여 hello 랩에서 수식을 만들 수 있습니다. 각 학습자 hello 랩에서 hello 수식을 보고 toocreate VM을 사용할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [DevTest Labs 수식 toocreate Vm 관리](devtest-lab-manage-formulas.md) |이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다. |
4. **비용 제어**
   
    DevTest Labs를 azure에 hello 랩 toospecify hello 최대 Vm 수 hello 랩에서 학습자에서 만들 수 있는 정책을 tooset를 허용 합니다. 
   
    여러 날 학습을 수행 하는 고 toostop 모든 hello Vm hello 하루 중 특정 시간에 원하는 다음 자동으로 다시 시작 날짜를 다음 hello 쉽게 자동 종료를 설정 하 여이 수행 하 고 수 hello 랩에서 정책 자동으로 시작 합니다. 
   
    마지막으로, 학습 완료 되 면 삭제할 수 있습니다 모든 hello Vm 한 번에 단일 PowerShell 스크립트를 실행 합니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [랩 정책 정의](devtest-lab-set-lab-policy.md) |Hello 랩에서 정책을 설정 하 여 비용을 제어 합니다. |
   | [모든 hello 랩 PowerShell 스크립트를 사용 하 여 Vm을 삭제 합니다.](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Hello 학습이 완료 될 때 한 번에 모든 hello labs를 삭제 합니다. |
5. **Hello 랩 각 학습자와 공유**
   
    실습생과 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다. 사용자 교육도 toohave는 Azure 계정이 없는 것으로 [Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)합니다. 실습생은 다른 실습생이 만든 VM을 볼 수 없습니다.  
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [학습자 tooa 랩 Azure DevTest Labs에 추가](devtest-lab-add-devtest-user.md) |Azure 포털 tooadd 교육 tooyour 교육 랩 hello를 사용 합니다. |
   | [PowerShell 스크립트를 사용 하 여 교육 toohello 랩을 추가합니다](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |PowerShell tooautomate 교육 tooyour 교육 랩 추가 사용 합니다. |
   | [링크 toohello 랩 가져오기](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |하이퍼링크를 통해 랩에 바로 액세스할 수 있는 방법을 알아봅니다. |
6. **계속 해 서 hello 랩 다시 사용** 
   
    사용자 지정 설정을 포함 하 여 리소스 관리자 템플릿을 만들어 사용 하 여 동일한 랩 toocreate 나중에 다시 랩 만들기를 자동화할 수 있습니다. 
   
    다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:
   
   | 작업 | 학습 내용 |
   | --- | --- |
   | [Resource Manager 템플릿을 사용하여 랩 만들기](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

