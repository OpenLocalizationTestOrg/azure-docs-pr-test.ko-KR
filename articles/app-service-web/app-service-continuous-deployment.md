---
title: "앱 서비스 배포 tooAzure aaaContinuous | Microsoft Docs"
description: "자세한 내용은 방법 tooenable 연속 배포 tooAzure 앱 서비스입니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>연속 배포 tooAzure 앱 서비스
이 자습서에서는 어떻게 tooconfigure 연속 배포 워크플로의 대 한 프로그램 [Azure 앱 서비스] 응용 프로그램입니다. BitBucket, GitHub와 서비스 응용 프로그램 통합 및 [VSTS Visual Studio Team Services ()](https://www.visualstudio.com/team-services/) 연속을 사용 하면 Azure 프로젝트에서 hello 가장 최근의 업데이트를 가져와서 여기서 배포 워크플로 tooone 이러한 서비스를 게시 합니다. 연속 배포는 여러 개의 빈번한 작성자가 통합되는 프로젝트에 적합한 옵션입니다.

어떻게 tooconfigure 연속 배포로 나열 되지 않은 클라우드 저장소에서 수동으로 hello Azure 포털 아웃 toofind (같은 [GitLab](https://gitlab.com/)), 참조 [수동 단계를 사용 하 여 연속 배포를 설정](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)합니다.

## <a name="overview"></a>연속 배포 활성화
tooenable 연속 배포

1. 연속 배포에 사용 될 응용 프로그램 콘텐츠 toohello 리포지토리를 게시 합니다.  
    프로젝트 toothese 서비스 게시에 대 한 자세한 내용은 참조 하십시오. [리포지토리 (GitHub)를 만들], [리포지토리 (BitBucket) 만들기], 및 [VSTS 시작]합니다.
2. Hello에 응용 프로그램의 메뉴 블레이드에서 [Azure 포털], 클릭 **응용 프로그램 배포 > 배포 옵션**합니다. 클릭 **소스 선택**을 선택한 후 hello 배포 원본이 있습니다.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > 앱 서비스 배포에 대 한 VSTS 계정을 tooconfigure 하십시오이 참조 [자습서](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)합니다.
   > 
   > 
3. Hello 권한 부여 워크플로 완료 합니다.
4. Hello에 **배포 원본** 블레이드에서 hello 프로젝트를 선택 하 고에서 toodeploy 분기 합니다. 완료되면 **확인**을 클릭합니다.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > GitHub 또는 BitBucket에서 지속적으로 배포할 수 있도록 하면 공용 및 개인 프로젝트가 둘 다 표시됩니다.
   > 
   > 
   
    Hello 선택한 저장소와의 연결을 만들고 hello 지정 된 분기에서 hello 파일에서 가져오는 앱 서비스 앱에 대 한 저장소의 복제본을 유지 관리 하는 응용 프로그램 서비스입니다. Hello 통합 hello 앱 서비스를 사용 하 여 VSTS hello Azure 포털의에서 연속 배포를 구성할 때 [Kudu 배포 엔진](https://github.com/projectkudu/kudu/wiki)어떤, 이미 있는 빌드 및 배포 작업을 자동화 모든 `git push`합니다. Tooseparately 불필요 VSTS에서 연속 배포를 설정 합니다. 이 프로세스가 완료 되 면 hello **배포 옵션** 앱 블레이드 배포를 나타내는 활성 배포 성공이 표시 됩니다.
5. tooverify hello 응용 프로그램이 성공적으로 배포 되었는지, hello 클릭 **URL** hello hello 앱 블레이드 hello Azure 포털의에서 위쪽에 있습니다.
6. 선택한 hello 리포지토리에서 지속적인 배포 발생 하 고 있는 tooverify 변경 toohello 리포지토리를 푸시합니다. 앱은 hello 푸시 toohello 리포지토리 완료 된 후에 곧 tooreflect hello 변경 사항을 업데이트 해야 합니다. Hello 업데이트 hello에 가져올에 확인할 수 있습니다 **배포 옵션** 응용 프로그램의 블레이드입니다.

## <a name="VSsolution"></a>Visual Studio 솔루션의 연속 배포
Visual Studio 솔루션 tooAzure 앱 서비스를 푸시하는 간단한 index.html 파일을 푸시하는 것 처럼 쉽게 합니다. 앱 서비스 배포 프로세스 hello NuGet 종속성을 복원 하 고 구축 hello 응용 프로그램 이진 파일을 포함 하 여 모든 hello 세부 정보를 간소화 합니다. Hello 소스 제어의 Git 리포지토리를 에서만 코드를 유지 관리 모범 사례에 따라 수 있으며 앱 서비스 배포 hello rest를 해결할 수 있습니다.

hello 서비스는 Visual Studio 솔루션 tooApp에 밀어 넣는 단계 hello 동일 hello와 같이 [이전 섹션](#overview), 구성 하는 경우 솔루션 및 리포지토리 다음과 같습니다.

* Visual Studio 소스 제어 옵션 toogenerate hello를 사용 하 여 한 `.gitignore` 아래 hello 이미지 등의 파일 또는 수동으로 추가 `.gitignore` 와 비슷한 toothis 콘텐츠 리포지토리 루트에 파일 [.gitignore 샘플](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)합니다.
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Hello.sln 파일 hello 리포지토리 루트에 있는 hello 전체 솔루션 디렉터리 트리 tooyour 리포지토리를 추가 합니다.

Visual Studio에서 로컬로 ASP.NET 응용 프로그램을 개발 하 고 지속적으로 코드를 하 여 배포 수, 설명 된 대로 저장소를 설정 하 고 Azure의 hello 온라인 Git 리포지토리 중 하나에서 지속적인 게시에 대 한 응용 프로그램을 구성 후 변경 내용을 tooyour 온라인 Git 리포지토리가 푸시합니다.

## <a name="disableCD"></a>지속적 배포 사용 안 함
toodisable 연속 배포

1. Hello에 응용 프로그램의 메뉴 블레이드에서 [Azure 포털], 클릭 **응용 프로그램 배포 > 배포 옵션**합니다. 클릭 **연결 끊기** hello에 **배포 옵션** 블레이드입니다.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. 에 답변 한 후 **예** toohello 확인 메시지에서 있습니다 수 tooyour 앱 블레이드 돌아가서 **응용 프로그램 배포 > 배포 옵션** tooset 다른 원본에서 게시를 원하는 경우.

## <a name="additional-resources"></a>추가 리소스
* [연속 배포와 tooinvestigate 공통 발급 하는 방법](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [어떻게 toouse Azure에 대 한 PowerShell]
* [Toouse는 Mac 및 Linux 용 Azure 명령줄 도구를 hello 하는 방법]
* [Git 설명서]
* [Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Azure를 사용 하 여 tooautomatically CI/CD 파이프라인 toodeploy ASP.NET 4 응용 프로그램 생성](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

[Azure 앱 서비스]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure 포털]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[어떻게 toouse Azure에 대 한 PowerShell]: /powershell/azureps-cmdlets-docs
[Toouse는 Mac 및 Linux 용 Azure 명령줄 도구를 hello 하는 방법]:../cli-install-nodejs.md
[Git 설명서]: http://git-scm.com/documentation

[리포지토리 (GitHub)를 만들]: https://help.github.com/articles/create-a-repo
[리포지토리 (BitBucket) 만들기]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[VSTS 시작]: https://www.visualstudio.com/docs/vsts-tfs-overview
