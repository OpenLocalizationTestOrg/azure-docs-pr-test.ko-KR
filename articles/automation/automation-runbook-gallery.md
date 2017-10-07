---
title: "Azure 자동화에 대 한 aaaRunbook 및 모듈 갤러리 | Microsoft Docs"
description: "Runbook 및 모듈에서 Microsoft 및 hello 커뮤니티 tooinstall 있습니다 사용할 수 있는 및 Azure 자동화 환경에서 사용 합니다.  이 문서에 액세스 하는 방법을 이러한 리소스와 toocontribute runbook toohello 갤러리 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Azure 자동화용 Runbook 및 모듈 갤러리
Azure 자동화에서 사용자 고유의 runbook 및 모듈을 작성 하지 않고 다양 한 Microsoft 및 hello 커뮤니티에 의해 이미 빌드된 시나리오를 액세스할 수 있습니다.  이러한 시나리오는 수정 없이 그대로 사용하거나, 이를 기초로 특정 요구 사항에 맞게 편집하여 사용할 수 있습니다.

Hello에서 runbook을 가져올 수 있습니다 [Runbook 갤러리](#runbooks-in-runbook-gallery) hello에서 모듈을 검색 하 고 [PowerShell 갤러리](#modules-in-powerShell-gallery)합니다.  개발 하는 시나리오를 공유 하 여 toohello 커뮤니티를 느려지게 할 수 있습니다.

## <a name="runbooks-in-runbook-gallery"></a>Runbook 갤러리의 Runbook
hello [Runbook 갤러리](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) runbook의 다양 한 Azure 자동화로 가져올 수 있는 Microsoft 및 hello 커뮤니티에서 제공 합니다. Hello에서 호스팅되는 hello 갤러리에서 runbook을 다운로드 하거나 [TechNet 스크립트 센터](https://gallery.technet.microsoft.com/scriptcenter/site/upload), hello Azure 클래식 포털 또는 Azure 포털에서 hello 갤러리에서 runbook을 직접 가져올 수 있습니다.

가져올 수 있습니다 hello Runbook 갤러리에서 직접 hello Azure 클래식 포털 또는 Azure 포털을 사용 하 여 합니다. Windows PowerShell을 사용하여 이 함수를 수행할 수 없습니다.

> [!NOTE]
> Hello Runbook 갤러리에서에서 가져올 때 각별히 주의 해야 설치 하 고 프로덕션 환경에서 실행을 사용 하는 모든 runbook의 hello 내용의 유효성을 검사 해야 합니다. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>Azure 클래식 포털 hello로 hello Runbook 갤러리에서에서 runbook tooimport
1. Hello Azure 포털에서에서 클릭 하 고, **새로**, **응용 프로그램 서비스**, **자동화**, **Runbook**, **갤러리에서**.
2. 범주 tooview 선택 관련 runbook 및 runbook tooview 세부 정보를 선택 합니다. 원하는 hello runbook을 선택 하면 hello 오른쪽 화살표 단추를 클릭 합니다.
   
    ![Runbook 갤러리](media/automation-runbook-gallery/runbook-gallery.png)
3. Hello runbook의 내용을 hello를 검토 하 고 hello 설명에서 모든 요구 사항을 확인 합니다. 완료 되 면 hello 오른쪽 화살표 단추를 클릭 합니다.
4. Hello runbook 세부 정보를 입력 하 고 hello 확인 표시 단추를 클릭 합니다. hello runbook 이름 이미 입력 되어 있습니다.
5. hello runbook hello에 나타납니다. **Runbook** hello 자동화 계정에 대 한 탭 합니다.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>Azure 포털 hello로 hello Runbook 갤러리에서에서 runbook tooimport
1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.
3. **갤러리 찾아보기** 단추를 클릭합니다.
   
    ![갤러리 찾아보기 단추](media/automation-runbook-gallery/browse-gallery-button.png)
4. 한 tooview 선택 hello 갤러리 항목을 찾아 해당 세부 정보입니다.
   
    ![갤러리 찾아보기](media/automation-runbook-gallery/browse-gallery.png)
5. 클릭 **보기 소스 프로젝트** hello에서 tooview hello 항목 [TechNet 스크립트 센터](http://gallery.technet.microsoft.com/)합니다.
6. tooimport 항목을 클릭 하 여 조치 tooview 세부 정보 클릭 hello 및 **가져오기** 단추입니다.
   
    ![가져오기 단추](media/automation-runbook-gallery/gallery-item-detail.png)
7. 필요에 따라 hello runbook의 hello 이름을 변경 하 고 클릭 **확인** tooimport hello runbook입니다.
8. hello runbook hello에 나타납니다. **Runbook** hello 자동화 계정에 대 한 탭 합니다.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Runbook toohello runbook 갤러리를 추가합니다.
Microsoft는 tooadd runbook toohello 유용한 tooother 고객 것으로 판단 되는 Runbook 갤러리를 권장 합니다.  runbook을 추가할 수 [toohello 스크립트 센터 업로드](http://gallery.technet.microsoft.com/site/upload) 계정 hello 다음 세부 정보를 고려 합니다.

* 지정 해야 *Windows Azure* hello에 대 한 **범주** 및 *자동화* hello에 대 한 **Subcategory** hello runbook toobe 표시에 대 한 hello 마법사의 합니다.  
* hello 업로드는 단일.ps1 또는.graphrunbook 파일 이어야 합니다.  Hello runbook에는 모든 모듈, 자식 runbook 또는 자산이 필요한 경우 다음 나열 해야 hello runbook의 주석 섹션 hello 및 hello 제출의 hello 설명에 해당 합니다.  여러 runbook을 요구 하는 시나리오를 설정한 경우에 각각 개별적으로 업로드 하 고 목록 hello 형태의 hello 관련 해당 설명의 각 runbook입니다. Hello에 표시 됩니다 되도록 동일한 태그를 삽입 하는 hello를 사용 하면 동일한 범주입니다. 다른 runbook은 필요한 hello 시나리오 toowork는 tooread hello 설명 tooknow를 해야 합니다.
* 게시 하는 경우 "GraphicalPS" hello 태그를 추가 **그래픽 runbook** (하지 그래픽 워크플로). 
* Hello 설명을 사용 하 여 PowerShell 워크플로 또는 PowerShell 코드 조각을 삽입 **코드 섹션을 삽입** 아이콘입니다.
* hello hello 업로드에 대 한 요약에에서 표시 됩니다 hello Runbook 갤러리 결과 사용자 hello runbook의 hello 기능을 식별 하는 데 도움이 되는 자세한 정보를 제공 해야 합니다.
* Hello 태그 toohello 업로드 다음의 하나 toothree를 할당 해야 합니다.  hello runbook hello 마법사 해당 태그와 일치 하는 hello 범주 아래에 나열 됩니다.  이 목록에 없는 모든 태그 hello 마법사에 의해 무시 됩니다. 일치 하는 태그를 지정 하지 않는 경우 hello runbook 됩니다 다른 범주 hello 아래에 나열 합니다.
  
  * 백업
  * 용량 관리
  * 변경 제어
  * 규정 준수
  * 개발/테스트 환경
  * 재해 복구
  * 모니터링
  * 패치
  * 프로비전
  * 재구성
  * VM 수명 주기 관리
* 자동화 하므로 업로드 한 항목이 즉시 표시 되지 않습니다는 시간에 한 번씩 hello 갤러리를 업데이트 합니다.

## <a name="modules-in-powershell-gallery"></a>PowerShell 갤러리의 모듈
PowerShell 모듈, runbook에서 사용할 수 있는 cmdlet을 포함 하 고 Azure 자동화에서 설치할 수 있는 기존 모듈 hello에서 사용할 수 있으며 [PowerShell 갤러리](http://www.powershellgallery.com)합니다.  Hello Azure 포털에서에서이 갤러리를 시작 하 고 Azure 자동화로 직접 설치 하거나을 다운로드 하 고 수동으로 설치할 수 있습니다.  Hello Azure 클래식 포털에서 직접 hello 모듈을 설치할 수 없지만 다운로드할 수 있는 다른 모듈와 마찬가지로 설치 합니다.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>Azure 포털 hello로 hello 자동화 모듈 갤러리에서에서 모듈 tooimport
1. Hello Azure 포털에서에서 자동화 계정을 엽니다.
2. Hello 클릭 **자산** 자산의 타일 tooopen hello 목록입니다.
3. Hello 클릭 **모듈** 타일 tooopen hello 모듈 목록입니다.
4. Hello 클릭 **찾아보기 갤러리** 단추와 hello 찾아보기 갤러리 블레이드 시작 됩니다.
   
    ![모듈 갤러리](media/automation-runbook-gallery/modules-blade.png) <br>
5. Hello 찾아보기 갤러리 블레이드를 시작한 후에 hello 필드를 수행 하 여 검색할 수 있습니다.
   
   * 모듈 이름
   * 태그
   * 작성자
   * Cmdlet/DSC 리소스 이름
6. 관심이 tooview 선택 하는 모듈을 찾습니다 세부 정보입니다.  
   링크 백 toohello를 포함 하 여 hello 모듈에 대 한 자세한 정보를 볼 수를 특정 모듈에 드릴 종속성, 필요한 PowerShell 갤러리 및 hello cmdlet 및/또는 DSC 리소스 모듈 hello를 모두 포함 합니다.
   
    ![PowerShell 모듈 세부 정보](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. Azure 자동화로 직접 tooinstall hello 모듈 클릭 hello **가져오기** 단추입니다.
   
    ![모듈 가져오기 단추](media/automation-runbook-gallery/module-import-button.png)
8. Hello 가져오기 단추를 클릭 하면 tooimport 넣으려는 hello 모듈 이름이 표시 됩니다. 모든 hello 종속성 설치 된 경우 hello **확인** 단추가 활성화 됩니다. 종속성 목록에 없으면 있어야만 tooimport 하는 것이 모듈을 가져올 수 있습니다.
9. 클릭 **확인** tooimport hello 모듈 및 모듈 블레이드 hello 시작 됩니다. Azure 자동화 모듈 tooyour 계정을 가져오면 hello 모듈 및 hello cmdlet에 대 한 메타 데이터를 추출 합니다.
   
    ![모듈 가져오기 블레이드](media/automation-runbook-gallery/module-import-blade.png)
   
    각 활동 추출 toobe 있기 때문에 몇 분 정도 걸릴 수 있습니다.
10. 알림을 받게 배포 되 고 해당 hello 모듈 및 완료 되지 않았을 때의 알림입니다.
11. Hello 모듈을 가져온 후 hello 사용 가능한 활동 표시 되 고 runbook 및 원하는 상태 구성의 해당 리소스를 사용할 수 있습니다.

## <a name="requesting-a-runbook-or-module"></a>Runbook 또는 모듈 요청 중
요청을 너무 보낼 수[사용자 음성](https://feedback.azure.com/forums/246290-azure-automation/)합니다.  Runbook을 작성 하는 데 도움이 필요 하거나 PowerShell에 대 한 질문을 하는 경우 게시 질문 tooour [포럼](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc)합니다.

## <a name="next-steps"></a>다음 단계
* runbook을 시작 하는 tooget 참조 [만들기 또는 Azure 자동화에서 runbook 가져오기](automation-creating-importing-runbook.md)
* toounderstand hello 차이점 PowerShell 및 PowerShell 워크플로 runbook으로 참조 [학습 PowerShell 워크플로](automation-powershell-workflow.md)

