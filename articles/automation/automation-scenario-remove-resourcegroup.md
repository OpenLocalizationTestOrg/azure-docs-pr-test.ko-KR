---
title: "리소스 그룹의 aaaAutomate 제거 | Microsoft Docs"
description: "Azure 자동화 runbook tooremove를 포함 하 여 시나리오의 PowerShell 워크플로 버전 구독에서 모든 리소스를 그룹화 합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Azure Automation 시나리오 - 리소스 그룹 제거 자동화
많은 고객이 하나 이상의 리소스 그룹을 만듭니다. 일부는 프로덕션 응용 프로그램을 관리하는 데 사용하고 일부는 환경을 개발, 테스트 및 스테이징하는 데 사용할 수 있습니다. 이러한 리소스의 hello 배포를 자동화 한 가지 않으며 수 toodecommission hello 단추 클릭으로 리소스 그룹은 다른입니다. Azure Automation를 사용하여 이 일반 관리 태스크를 간소화할 수 있습니다. MSDN 또는 Microsoft Partner Network Cloud Essentials 프로그램 hello와 같은 회원 혜택을 통해 지출 한도 Azure 구독이 사용 하는 경우에 유용 합니다.

이 시나리오는 PowerShell runbook을 기반으로 하며 디자인 된 tooremove 구독에서 지정 하는 하나 이상의 리소스 그룹 hello runbook의 hello 기본 설정을 계속 진행 하기 전에 tootest입니다. 이렇게 하면 삭제 하면 안 실수로 hello 리소스 그룹 준비 toocomplete 본인이 전에이 절차입니다.   

## <a name="getting-hello-scenario"></a>Hello 시나리오를 가져오기
이 시나리오 hello에서 다운로드할 수 있는 PowerShell runbook 이루어져 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript)합니다. Hello에서 직접 가져올 수도 [Runbook 갤러리](automation-runbook-gallery.md) hello Azure 포털의에서.<br><br>

| Runbook | 설명 |
| --- | --- |
| Remove-ResourceGroup |Hello 구독에서 하나 이상의 Azure 리소스 그룹 및 관련된 리소스를 제거합니다. |

<br>
이 runbook에 대 한 입력된 매개 변수 뒤 hello 정의 됩니다.

| 매개 변수 | 설명 |
| --- | --- |
| NameFilter(필수) |삭제에 이름 필터 toolimit hello 리소스 그룹을 추가할지 여부를 지정 합니다. 쉼표로 구분된 목록을 사용하여 여러 값을 전달할 수 있습니다.<br>hello 필터는 대/소문자 구분 하지 않으며 hello 문자열을 포함 하는 모든 리소스 그룹을 일치 합니다. |
| PreviewMode(선택 사항) |Hello runbook toosee 리소스 그룹은 삭제할 수는 없지만 아무 작업도 수행을 실행 합니다.<br>hello 기본값은 **true** toohelp 하나 실수로 삭제를 방지 하거나 더 많은 리소스 그룹 toohello runbook을 전달 합니다. |

## <a name="install-and-configure-this-scenario"></a>이 시나리오 설치 및 구성
### <a name="prerequisites"></a>필수 조건
이 runbook hello를 사용 하 여 인증 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)합니다.    

### <a name="install-and-publish-hello-runbooks"></a>설치 하 고 hello runbook 게시
Hello runbook을 다운로드 한 후에 hello 절차를 사용 하 여 가져올 수 있습니다 [runbook 프로시저 가져오기](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)합니다. 자동화 계정으로 성공적으로 가져온 후 hello runbook을 게시 합니다.

## <a name="using-hello-runbook"></a>Hello runbook을 사용 하 여
hello 다음 단계는 과정을 단계별로이 runbook 및 작동 방법을 파악 하는 도움말의 hello 실행 합니다. 만 테스트 하는 hello runbook이 예제에서는 실제로 hello 리소스 그룹을 삭제 합니다.  

1. Hello Azure 포털에서에서 자동화 계정을 열고 클릭 **Runbook**합니다.
2. 선택 hello **제거 ResourceGroup** runbook 클릭 **시작**합니다.
3. Hello runbook을 시작할 때 hello **Runbook 시작** 블레이드가 열리고 hello 매개 변수를 구성할 수 있습니다. 테스트에 사용할 수 하더라도 피해 실수로 삭제 하는 경우 발생 하 여 구독에 리소스 그룹의 이름을 hello를 입력 합니다.<br> ![Remove-ResouceGroup 매개 변수](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > 있는지 확인 **Previewmode** 너무 설정**true** hello 삭제 tooavoid 리소스 그룹을 선택 합니다.  **참고** 이 runbook이이 runbook을 실행 하는 hello 자동화 계정이 포함 된 hello 리소스 그룹을 제거 하지 것입니다.  
   >
   >
4. 모든 hello 매개 변수 값을 구성을 클릭 **확인**, hello runbook은 실행을 위해 대기 하 고 있습니다.  

hello의 tooview hello 세부 정보 **제거 ResourceGroup** hello Azure 포털에서에서 runbook 작업 **작업** hello runbook에서 합니다. hello 작업 요약 표시 hello 입력된 매개 변수 및 hello 출력 또한 스트림 hello 작업에 대 한 toogeneral 정보 및 발생 한 예외입니다.<br> ![Remove-ResourceGroup Runbook 작업 상태](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png)

hello **작업 요약** hello 출력, 경고 및 오류 스트림에서 메시지가 포함 됩니다. 선택 **출력** tooview hello runbook 실행의 결과 자세히 설명 합니다.<br> ![Remove-ResourceGroup Runbook 출력 결과](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>다음 단계
* 사용자 고유의 runbook 만들기를 시작 하는 tooget 참조 [만들기 또는 Azure 자동화에서 runbook을 가져와](automation-creating-importing-runbook.md)합니다.
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)합니다.
