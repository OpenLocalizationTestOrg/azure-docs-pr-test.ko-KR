---
title: "Azure 자동화 tootrigger aaaUse 작업 | Microsoft Docs"
description: "자세한 내용은 방법 StorSimple 데이터 관리자 작업 (비공개 미리 보기)를 트리거할 기준이 toouse Azure 자동화"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Azure 자동화 tootrigger 작업 (비공개 미리 보기)를 사용 하 여

이 문서에 설명 방법을 toouse Azure 자동화 tootrigger StorSimple Data Manager 작업입니다.

## <a name="prerequisites"></a>필수 조건

시작하기 전에 다음 항목이 있어야 합니다.

*   Azure Powershell을 설치합니다. [Azure Powershell을 다운로드합니다](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   구성 설정 tooinitialize hello 데이터 변환 작업 (지침 tooobtain 이러한 설정을 여기에 포함 됩니다).
*   리소스 그룹 내의 하이브리드 데이터 리소스에서 올바르게 구성된 작업 정의입니다.
*   다운로드 `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) hello github 리포지토리에서 파일입니다.
*   다운로드 `Get-ConfigurationParams.ps1` [스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) hello github 리포지토리에서 합니다.
*   다운로드 `Trigger-DataTransformation-Job.ps1` [스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) hello github 리포지토리에서 합니다.

## <a name="step-by-step"></a>단계별 과정

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Hello 자동화 작업 toorun hello 작업 정의 대 한 Azure Active Directory 사용 권한 가져오기

1. Active Directory에 대 한 tooretrieve hello 구성 매개 변수는 다음 단계 hello지 않습니다.

    1. 로컬 컴퓨터에서 Windows PowerShell을 엽니다. [Azure PowerShell](https://azure.microsoft.com/downloads/)이 설치되었는지 확인합니다.
    1. Hello 실행 `Get-ConfigurationParams.ps1` hello 폴더에서 위의 다운로드 한 스크립트입니다. Hello 다음 hello PowerShell 창에서 명령을 입력 합니다.

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        hello ActiveDirectoryKey 나중에 사용할 암호입니다. 사용자가 선택한 암호를 입력합니다. AppName에는 아무 문자열이나 사용할 수 있습니다.

2. 이 스크립트는 다음 hello 자동화 runbook을 트리거하는 동안 사용 해야 하는 값에는 hello를 출력 합니다. 이러한 값을 기록해 둡니다.

    - 클라이언트 ID
    - 테넌트 ID
    - Active Directory 키 (동일: hello 위에 입력 한 하나)
    - 구독 ID

### <a name="set-up-hello-automation-account"></a>자동화 계정 hello 설정

1. TooAzure 로그온 하 고 자동화 계정 키를 누릅니다.
2. 클릭 **자산** 자산의 타일 tooopen hello 목록입니다.
3. 클릭 **모듈** 타일 tooopen hello 모듈 목록입니다.
4. 클릭 **모듈 추가 +** 단추와 hello 추가 모듈 블레이드 시작 됩니다.

    ![Automation 계정 설정](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Hello를 선택한 후 `DataTransformationApp.zip` 로컬 컴퓨터에서 파일을 클릭 하 여 **확인** tooimport hello 모듈입니다.

   Azure 자동화 모듈 tooyour 계정을 가져오면 hello 모듈에 대 한 메타 데이터를 추출 합니다. 이 작업에는 몇 분 정도 걸릴 수 있습니다.

   ![Automation 계정 설정](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. 알림이 해당 hello 모듈 배포 되 고 및 hello 프로세스가 완료 되 면 다른 알림입니다.  Hello 상태를 확인할 수도 있습니다 **모듈** 바둑판식으로 배열입니다.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>hello 작업 정의 트리거하는 tooimport hello runbook

1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.
3. **+ Runbook 추가**를 클릭한 다음, **기존 Runbook 가져오기**를 클릭합니다.

   ![기존 Runbook 가져오기](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. 클릭 **Runbook 파일** 및 선택 hello 파일 tooimport `Trigger-DataTransformation-Job.ps1`합니다.
5. 클릭 **만들기** tooimport hello runbook입니다. 새 runbook hello hello 자동화 계정에 대 한 runbook의 hello 목록에 나타납니다.
7. **Trigger-DataTransformation-Job** Runbook을 클릭한 다음 **편집**을 클릭합니다.
8. 확인 메시지가 표시되면 **게시**, **예**를 차례로 클릭합니다.


### <a name="toorun-hello-runbook"></a>toorun hello runbook의 경우:
1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.
3. **Trigger-DataTransformation-Job**을 클릭합니다.
4. 클릭 **시작** toostart hello runbook입니다.

   ![Runbook 시작](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. Hello에 **runbook을 시작** 블레이드에서 모든 hello 매개 변수를 입력 합니다. 클릭 **확인** toosubmit hello 데이터 변환 작업 합니다.

   ![Runbook 시작](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>다음 단계

[데이터 tootransform StorSimple 데이터 관리자 UI를 사용 하 여](storsimple-data-manager-ui.md)합니다.
