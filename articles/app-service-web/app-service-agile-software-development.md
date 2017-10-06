---
title: "Azure 앱 서비스와 aaaAgile 소프트웨어 개발"
description: "자세한 내용은 방법 toocreate 확장성이 뛰어난 복잡 한 응용 프로그램 Azure 앱 서비스와 agile 소프트웨어 개발을 지 원하는 방식으로 합니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발
이 자습서에서는 살펴보겠습니다 방법을 toocreate 확장성이 뛰어난 복잡 한 응용 프로그램을 [Azure 앱 서비스](/azure/app-service/) 지 원하는 방식으로 [agile 소프트웨어 개발](https://en.wikipedia.org/wiki/Agile_software_development)합니다. 이미 알고 있다고 너무 어떻게 가정[Azure에 예측 가능한 방식으로 복잡 한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md)합니다.

Agile 방법론의 성공적인 구현의 hello 방식에서 기술 프로세스의 제한 사항을 위반 독립 종종 수도 있습니다. Azure 앱 서비스와 같은 기능과 함께 [지속적인 게시](app-service-continuous-deployment.md), [스테이징 환경의](web-sites-staged-publishing.md) (슬롯) 및 [모니터링](web-sites-monitor.md)hello 오케스트레이션과 현명 하 게 결합 하는 경우 및 배포의 관리 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md), agile 소프트웨어 개발 수용 개발자를 위한 가장 좋은 방법의 일부일 수 있습니다.

hello 다음 표는 민첩 한 개발와 관련 된 요구 사항의 짧은 목록을 방법과 Azure 서비스를 사용 하 고 각 합니다.

| 요구 사항 | Azure 사용할 수 있는 방법 |
| --- | --- |
| -모든 커밋을 사용하여 구축<br>- 빠르게 자동적으로 구축합니다. |지속적인 배포를 구성할 때, Azure 앱 서비스는 개발 분기점에 따라 실시간 구축 기능을 수행합니다. 코드 toohello 분기 푸시됩니다, 될 때마다 자동으로 빌드된 한는 실시간 Azure 에서입니다. |
| - 자체-테스트 빌드 구축하기 |테스트, 웹 테스트 등 로드할 하시기 바랍니다 hello Azure 리소스 관리자 템플릿을 사용 하 여 배포할 수 있습니다. |
| - 프로덕션 환경의 클론에 테스트를 수행합니다. |Azure 리소스 관리자 템플릿 hello Azure 프로덕션 환경 (응용 프로그램 설정, 연결 문자열 템플릿, 배율, 등 포함) 신속 하 고 예측 가능한 방식으로 테스트를 위해 사용 되는 toocreate 복제 될 수 있습니다. |
| -최근 구축 결과를 쉽게 볼 수 있습니다. |리포지토리에서 지속적인 배포 tooAzure 변경 내용을 커밋한 후에 즉시 라이브 응용 프로그램에서 새 코드를 테스트할 수를 의미 합니다. |
| -커밋 주 분기 toohello 매일<br>-배포를 자동화하기 |연속 통합 저장소의 main 분기와 프로덕션 응용 프로그램의 모든 커밋/병합 toohello main 분기 tooproduction를 자동으로 배포합니다. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>수행할 사항
순서 toopublish 새 변경 내용 toohello에서 일반적인 작업 테스트 단계 프로덕션 개발 과정을 안내 합니다 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 두 구성 되는 샘플 응용 프로그램 [웹 앱](/services/app-service/web/), 하나의 프론트 엔드 (FE) 및 웹 API 백 엔드 (BE) 되 고 다른 hello 및 [SQL 데이터베이스](/services/sql-database/)합니다. 배포 아키텍처를 따르는 hello를 사용 합니다.

![](./media/app-service-agile-software-development/what-1-architecture.png)

단어로 tooput hello 그림:

* hello 배포 아키텍처는 세 가지 서로 다른 환경으로 구분 됩니다 (또는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) Azure에서)를 각각 고유의 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [배율](web-sites-scale.md) 설정 및 SQL 데이터베이스입니다. 
* 각 환경을 별도로 관리할 수 있습니다. 서로 다른 구독에도 존재할 수 있습니다.
* 스테이징 및 프로덕션 hello의 두 슬롯으로 구현 됩니다 동일한 앱 서비스 앱. hello 마스터 분기 슬롯 hello로 연속 통합에 대 한 설정 되어 있습니다.
* 커밋 toomaster 분기 hello 슬롯 (프로덕션 데이터를 사용)에서 확인 되며, 준비 응용 프로그램은 hello 프로덕션 슬롯으로 교환 된 hello 확인 [중단 시간 없이](web-sites-staged-publishing.md)합니다.

hello 프로덕션 및 스테이징 환경 템플릿에 의해 정의 됩니다 hello에 [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json)합니다.

hello 개발 및 테스트 환경에서 hello 템플릿에서 정의 [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json)합니다.

또한 toohello 테스트 분기를 dev 분기 hello toohello 마스터 분기 (따라서 toospeak 품질에서 이동)에서 이동 하는 코드와 함께 hello 일반적인 분기 전략을 사용 합니다.

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>필요한 항목
* Azure 계정.
* [GitHub](https://github.com/) 계정
* Git 셸 (설치 된 [Windows 용 GitHub](https://windows.github.com/))-동일한 hello에 사용 하도록 설정 하면 toorun 둘 다 hello Git 및 PowerShell 명령을 세션 
* 최신 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 비트
* 기본적으로 도구 다음 hello 이해:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 템플릿 배포([Azure에서 예측 가능하도록 복잡한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md) 참조)
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> 이 자습서는 Azure 계정 toocomplete 필요합니다.
> 
> * 할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/) -크레딧을 얻게 Azure 서비스를 유료 아웃 tootry 사용할 수 있으며 모두 사용 하는 후에 hello 계정 등에 사용 가능한 웹 응용 프로그램 등의 Azure 서비스입니다.
> * [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.
> 
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="set-up-your-production-environment"></a>프로덕션 환경을 설정합니다.
> [!NOTE]
> 이 자습서에 자동으로 사용 하는 hello 스크립트 GitHub 리포지토리에서 지속적인 게시를 구성 합니다. GitHub 자격 증명 Azure에 이미 저장 되어, hello 웹 앱에 대 한 소스 제어 설정 tooconfigure 시도할 때 hello 배포 실패를 스크립팅 하는 그렇지 않은 경우 필요 합니다. 
> 
> azure에서 자격 증명에 GitHub toostore hello에 웹 앱 만들기 [Azure 포털](https://portal.azure.com/) 및 [GitHub 배포 구성](app-service-continuous-deployment.md)합니다. 하기만 하면 toodo 한 번이 됩니다. 
> 
> 

일반적인 DevOps 시나리오에서는 Azure에서 동시에 실행 하는 응용 프로그램 하 고 지속적인 게시를 통해 변경 내용을 tooit toomake 하려는 있습니다. 이 시나리오에서는 사용자에 게 템플릿이 있습니다 개발, 테스트 및 사용 되는 toodeploy hello 프로덕션 환경입니다. 이 섹션에서는 설정 합니다.

1. 사용자 고유의 분기의 hello 만들기 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 저장소입니다. 분기를 만드는 방법에 대한 자세한 내용은 [리포지토리 분기](https://help.github.com/articles/fork-a-repo/)를 참조하세요. 사용자의 포크를 생성하면, 브라우저에서 볼 수 있습니다.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Git 셸 세션을 엽니다. Git 셸이 없는 경우 [Windows용 GitHub](https://windows.github.com/) 를 설치합니다.
3. Hello 다음 명령을 실행 하 여 포크의 로컬 복제본을 만듭니다.

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. 로컬 복제본을 사용 하는 후 너무 이동*&lt;repository_root >*\ARMTemplates, 및 실행된 hello deploy.ps1 다음과 같이 스크립트:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. 대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다.
   
   다양 한 Azure 리소스의 진행 상태를 프로 비전 하는 hello를 표시 되어야 합니다. 배포가 완료 되 면 hello 스크립트 hello 브라우저에서 hello 응용 프로그램을 시작 하 고 친숙 한 경고음을 제공 합니다.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > 살펴보기  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee 어떻게 고유 Id 사용 하 여 리소스를 생성 합니다. Hello 동일한 접근 방식을 toocreate의 복제를 사용할 수 있습니다 충돌 하는 리소스 이름에 대 한 걱정 없이 동일한 배포 hello 합니다.
   > 
   > 
6. Git 셸 세션으로 돌아가서 다음을 실행합니다.
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Hello 스크립트 작업을 마치면 toobrowse toohello 프런트 엔드의 주소 돌아가서 (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee hello 응용 프로그램을 프로덕션 환경에서 실행 합니다.
8. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 무엇이 확인 하 고 있습니다.
   
   Hello에 수 toosee 두 웹 응용 프로그램 수 같은 리소스 그룹, hello 사용 하 여 `Api` hello 이름에서 접미사입니다. Hello 리소스 그룹 보기를 보면 hello SQL 데이터베이스 및 서버, 앱 서비스 계획 hello 및 hello 웹 앱에 대 한 스테이징 슬롯 hello도 표시 됩니다. Hello 다양 한 리소스를 탐색 하 고 비교를 사용 하 여  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 서식 파일에 구성 된 방법입니다.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

이제 설정한 hello 프로덕션 환경입니다. 다음으로 새 업데이트 toohello 응용 프로그램 시작과 있습니다.

## <a name="create-dev-and-test-branches"></a>Dev를 생성하고 분기점을 테스트 합니다.
Azure에서 프로덕션 환경에서 실행 되는 복잡 한 응용 프로그램을가지고 agile 방법론에 따라 업데이트 tooyour 응용 프로그램을 생성 됩니다. 이 섹션에서는 hello toomake hello 필요한 업데이트 해야 하는 개발 및 테스트 분기를 만들 됩니다.

1. 먼저 hello 테스트 환경을 만듭니다. Git 셸 세션에서 실행된 hello 다음 명령을 호출 하는 새 분기에 대 한 toocreate hello 환경을 **NewUpdate**합니다. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. 대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다. 
   
   배포가 완료 되 면 hello 스크립트 hello 브라우저에서 hello 응용 프로그램을 시작 하 고 친숙 한 경고음을 제공 합니다. 이제 자체 테스트 환경이 포함된 새로운 분기점이 생성되었습니다. 이 테스트 환경에 대 한 몇 가지 순간 tooreview를 수행 합니다.
   
   * 모든 Azure 구독에서 만들 수 있습니다. 즉, hello 프로덕션 환경과 테스트 환경에서 별도로 관리할 수 있습니다.
   * 테스트 환경을 라이브 Azure에서 실행 중입니다.
   * 테스트 환경에 스테이징 슬롯 hello 및 hello 배율 설정을 제외 하 고 동일한 toohello 프로덕션 환경이입니다. 알고 있는 ProdandStage.json와 Dev.json 간의 유일한 차이점 hello 되기 때문에 있습니다.
   * 다른 가격 계층(예: **무료**)으로 자체 앱 서비스 계획에서 테스트 환경을 관리할 수 있습니다.
   * 이 테스트 환경을 삭제 작업은을 hello 리소스 그룹을 삭제 합니다. 방법을 배울 toodo이 [나중](#delete)합니다.
3. 다음 명령을 실행 하 여 dev 분기 hello toocreate 참조.
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. 대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다. 
   
   순간 tooreview이 개발 환경에 대 한 몇 가지를 수행 합니다. 
   
   * 배포 되어 서 hello를 사용 하 여 개발 환경에 구성 동일한 toohello 테스트 환경에 같은 템플릿.
   * Hello 개발자의 Azure 구독에서 별도로 관리 하는 hello 테스트 환경 toobe 두면 각 개발 환경을 만들 수 있습니다.
   * 개발 환경이 Azure에서 실시간 작동 중입니다.
   * 환경은 hello dev를 삭제 하기만 하면 hello 리소스 그룹을 삭제 하는입니다. 방법을 배울 toodo이 [나중](#delete)합니다.

> [!NOTE]
> 여러 개발자가 hello 새 업데이트에서 작업을 사용 하는 경우 각 사람 쉽게 만들 수 있는 분기와 전용된 개발 환경을 단계를 수행 하는 hello로:
> 
> 1. GitHub에서 자신의 hello 리포지토리 분기를 만듭니다 (참조 [는 리포지토리를 분기](https://help.github.com/articles/fork-a-repo/)).
> 2. 로컬 컴퓨터에서 복제 hello 분기
> 3. Hello 실행 동일 명령 toocreate 자신의 dev 분기와 환경입니다.
> 
> 

완료되면, GitHub 포크는 세 개의 분기가 있어야 합니다.

![](./media/app-service-agile-software-development/test-1-github-view.png)

3 개의 별도 리소스 그룹에서 6개의 웹앱(한 그룹에 2개의 응용 프로그램)이 있어야 합니다.

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json 지정 hello 프로덕션 환경 toouse hello **표준** 가격 책정 계층 hello 프로덕션 응용 프로그램의 확장성에 적절 합니다.
> 
> 

## <a name="build-and-test-every-commit"></a>모든 커밋을 구축하고 테스트합니다.
템플릿 파일 ProdAndStage.json hello 및 Dev.json 이미 hello 소스 제어 매개 변수를 지정 hello 웹 응용 프로그램에 지속적인 게시를 설정 하는 기본적으로 합니다. 따라서 모든 커밋 toohello GitHub 분기 로부터 자동 배포 tooAzure를 트리거합니다. 이제 설치 작업을 하는 방법에 대해 알아보겠습니다.

1. Hello 로컬 저장소의 hello Dev 분기에 있는지 확인 합니다. toodo 다음 명령을 Git 셸에서이, 실행된 hello:
   
        git checkout Dev
2. Hello 코드 toouse 변경 하 여 변경 toohello 앱의 UI 계층을 만들 [부트스트랩](http://getbootstrap.com/components/) 나열 합니다. 열기  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml 고 강조 표시 된 변경 hello:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > 읽을 수 없는 경우에 위 그림 hello: 
    > 
    > * 18 줄에서 변경 `check-list` 너무`list-group`합니다.
    > * 19 줄에서 변경 `class="check-list-item"` 너무`class="list-group-item"`합니다.
    > 
    > 
3. Hello 변경 내용을 저장 합니다. 다시 Git 셸에서 hello 다음 명령을 실행 합니다.
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Git 유사한 너무 "확인" 코드에서 TFS와 같은 다른 소스 제어 시스템에 있습니다. 실행 하는 경우 `git push`, hello 새 커밋에는 다음 다시 작성 hello hello 개발 환경에서 응용 프로그램 tooreflect hello 변경 하는 자동 코드 푸시 tooAzure 트리거합니다.
4. 이 코드 푸시 tooyour 개발 환경 발생 했음을 tooverify tooyour 개발 환경 웹 응용 프로그램 페이지를 이동 하 고 hello 확인 **배포** 부분입니다. 최신 커밋 있는 메시지 수 toosee 있어야 합니다.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. 여기에서 클릭 **찾아보기** toosee hello Azure의 hello 라이브 응용 프로그램에 새로운 변경 합니다.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   최소 변경 toohello 응용 프로그램입니다. 그러나 새 변경 내용 tooa 복잡 한 웹 응용 프로그램 시간 대부분에 의도 하지 않은 및 원치 않는 부작용입니다. 수 tooeasily 테스트 되 고 모든 커밋과 라이브 빌드에 사용 하면 toocatch 있습니다 이러한 문제 고객에 게 표시 되기 전에.

지금까지 hello 인식 방법을 잘 알고 있어야 hello에 개발자는 **NewUpdate** 프로젝트를 빌드하고 수 있습니다를 직접 위한 개발 환경을 만들려면 다음 모든 커밋과 모든 빌드를 테스트 합니다.

## <a name="merge-code-into-test-environment"></a>테스트 환경에 코드를 병합
을 사용 하는 준비 toopush tooNewUpdate 분기를 Dev에서 코드를 분기는 hello 표준 git 프로세스:

1. 다른 개발자가 만든 커밋이 같은 github를 hello Dev 분기에 모든 새 커밋이 tooNewUpdate를 병합 합니다. GitHub에 대 한 모든 새 커밋을 코드 푸시 및 hello 개발 환경에서 빌드를 트리거합니다. 그런 다음 Dev 분기의 코드로 hello 최신 비트로 NewUpdate 분기에서 여전히 작동 하는지을 만들 수 있습니다.
2. 개발 분기의 모든 새 커밋을 GitHub의 새 업데이트 브랜치로 병합합니다. 이 동작은 코드 푸시 및 hello 테스트 환경에서 빌드를 트리거합니다. 

Note 다시 연속 배포는 이미 이러한 git 분기를 설정 하기 때문에 실행 통합 같은 다른 작업을 모두 빌드 tootake 필요 하지 않습니다. Git를 사용 하 여 tooperform 표준 소스 제어 사례를 제공 하기만 하 고 Azure 사용자에 대 한 모든 hello 빌드 프로세스를 수행 합니다.

이제 코드를 너무 푸시 보겠습니다**NewUpdate** 분기 합니다. Git 셸에서 hello 다음 명령을 실행 합니다.

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

끝났습니다. 

이동 toohello 웹 응용 프로그램 페이지에 대 한 테스트 환경 toosee (NewUpdate 분기에 병합) 새 커밋 이제 푸시 toohello 테스트 환경. 클릭 **찾아보기** 스타일 변경 hello toosee Azure 동시에 실행 됩니다.

## <a name="deploy-update-tooproduction"></a>업데이트 tooproduction 배포
코드 toohello 푸시 스테이징 및 프로덕션 환경까지 이미 작업 한 내용을 코드 toohello 테스트 환경 푸시되는 방법과 다르지 않습니다 느끼지 것입니다. 매우 간단합니다. 

Git 셸에서 hello 다음 명령을 실행 합니다.

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

ProdandStage.json에 hello 스테이징 및 프로덕션 환경이 설정 된 hello 방식을 기준으로 새 코드 toohello 푸시됩니다 **준비** 슬롯 없습니다 실행 되 고 있습니다. 따라서 toohello 스테이징 슬롯의 URL을 탐색 하는 경우에 hello 여기서 실행 되는 새 코드를 나타납니다. toodo Git 셸에서 cmdlet을 다음이 실행된 hello 합니다.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

Hello 슬롯의 hello 업데이트를 확인 한 후 남았습니다 toodo tooswap 파일인 hello 하는 이제 및 프로덕션 환경에 해당 합니다. Git 셸에서 hello 다음 명령을 실행 하면 됩니다.

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

축하합니다. 새 업데이트 tooyour 프로덕션 웹 응용 프로그램을 성공적으로 게시 했습니다. 게다가 쉽게 개발과 테스트 환경을 생성하고, 모든 커밋을 구축하고 테스트함으로써 완료했습니다. 이들은 agile 소프트웨어 개발의 중요한 구성 요소입니다.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>개발 환경과 테스트 환경 삭제
되기 쉬운 toodelete 프로그램 개발의 의도적으로 설계 하 고 테스트 환경 toobe 자체 포함 된 리소스 그룹 때문에 해당 합니다. toodelete hello hello GitHub 분기와 Azure 아티팩트를 모두이 자습서에서 만든 것 hello 셸에서 Git 명령을 다음 실행 하면 됩니다.

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>요약
Agile 소프트웨어 개발에는 응용 프로그램 플랫폼으로 Azure tooadopt 하려는 대부분의 회사은 합니다. 이 자습서에서는 어떻게 toocreate와 정확 하 게 아래로 또는 옆의 복제본 삭제 hello 프로덕션 환경으로 복잡 한 응용 프로그램에도 쉽게 알아 보았습니다. 이 기능은 toocreate 개발 처리 하는 tooleverage 방법 또한 배웠습니다 빌드하고 Azure의 단일 커밋 모든 테스트 수입니다. 이 자습서에서는 다행 스럽게도 살펴보았습니다 사용 하는 방법을 가장 함께 toocreate Azure 앱 서비스 및 Azure 리소스 관리자는 DevOps 솔루션 tooagile 방법론 빈도가 낮은입니다. 다음으로 [프로덕션에서 테스트](app-service-web-test-in-production-get-start.md)와 고급 DevOps 기술을 수행하여 시나리오를 계속 빌드할 수 있습니다. 일반적인 프로덕션 시나리오 테스트의 경우 [Azure 앱 서비스에서 Flighting 배포(베타 테스트)](app-service-web-test-in-production-controlled-test-flight.md)를 참조하세요.

## <a name="more-resources"></a>추가 리소스
* [Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포](app-service-deploy-complex-application-predictably.md)
* [Agile 개발 연습에서: 현대화 개발 주기의 팁과 트릭](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [리소스 관리자 템플릿을 사용하여 Azure 웹앱의 고급 배포 전략](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Azure 리소스 관리자 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint-hello JSON 유효성 검사기](http://jsonlint.com/)
* [ARMClient – 게시 toosite GitHub 설정](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Git 분기-기본 분기 및 병합](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo의 블로그](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure 플랫폼간 명령줄 도구](../cli-install-nodejs.md)
* [Azure AD에서 사용자 만들기 또는 편집](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [프로젝트 Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

