---
title: "Git 배포 tooAzure aaaLocal 앱 서비스"
description: "자세한 내용은 방법 tooenable 로컬 Git 배포 tooAzure 앱 서비스입니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>로컬 Git 배포 tooAzure 앱 서비스
이 자습서에서는 어떻게 toodeploy 앱 너무[Azure 앱 서비스] 로컬 컴퓨터의 Git 리포지토리에서 합니다. 앱 서비스는 hello로이 방법을 지원 합니다. **로컬 Git** hello에 대 한 배포 옵션 [Azure 포털]합니다.  
Hello를 사용 하 여 앱 서비스 앱을 만드는 경우 자동으로 수행 됩니다이 문서에서 설명 하는 hello Git 명령 중 많은 [Azure 명령줄 인터페이스] 설명 된 대로 [여기](app-service-web-get-started.md)합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete 해야이 자습서에서는:

* Git. Hello 설치 이진 파일을 다운로드할 수 있습니다 [여기](http://www.git-scm.com/downloads)합니다.  
* Git에 대한 기본 지식.
* Microsoft Azure 계정. 계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)할 수 있습니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 앱 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.  
> 
> 

## <a name="Step1"></a>1단계: 로컬 리포지토리 만들기
Hello 작업 toocreate 새 Git 리포지토리를 다음을 수행 합니다.

1. **GitBash** (Windows) 또는 **Bash** (Unix Shell)와 같은 명령줄 도구를 시작합니다. OS X 시스템에서 명령줄 hello hello를 통해 액세스할 수 있습니다 **터미널** 응용 프로그램입니다.
2. Hello 콘텐츠 toodeploy 찾을 수 없는 toohello 디렉터리를 이동 합니다.
3. Hello 다음 명령 tooinitialize 새 Git 리포지토리를 사용 합니다.

```bash  
git init
```

## <a name="Step2"></a>2단계: 콘텐츠 커밋
앱 서비스는 다양한 프로그래밍 언어로 만들어진 응용 프로그램을 지원합니다. 

1. 리포지토리에 이미 콘텐츠 skip을 포함 하는 경우이 가리킨 toopoint 아래 2 이동 합니다. 리포지토리에 콘텐츠가 포함되어 있지 않은 경우 다음과 같이 정적 .html 파일로 채웁니다. 
   
   * 라는 새 파일을 텍스트 편집기를 사용 하 여 만들 **index.html** hello Git 리포지토리 루트 hello에
   * Hello hello index.html에 대 한 hello 콘텐츠 파일을 저장 하는 대로 텍스트를 다음 추가: *Hello Git!*
2. Hello 명령줄에서 Git 리포지토리의 루트 hello 하위 있는지를 확인 합니다. 다음 명령은 tooadd 파일 tooyour 저장소 다음 hello를 사용 하 여:

```bash  
git add -A
```
3. 다음으로, 다음 명령을 hello를 사용 하 여 hello 변경 toohello 리포지토리를 커밋하십시오.

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>3 단계: 앱 서비스 앱 저장소 hello 설정
Hello 단계 tooenable 앱 서비스 앱에 대 한 Git 리포지토리를 다음을 수행 합니다.

1. Toohello 로그인 [Azure 포털]합니다.
2. App Service의 앱 블레이드에서 **설정 > 배포 원본**을 클릭합니다. **원본 선택**을 클릭한 다음 **로컬 Git 리포지토리**를 클릭하고 **확인**을 클릭합니다.  
   
    ![로컬 Git 리포지토리](./media/app-service-deploy-local-git/local_git_selection.png)
3. Azure에서 리포지토리를 첫 번째 시간 설정을 인 경우에 대 한 toocreate 로그인 자격 증명이 필요 합니다. 사용 합니다 해당 hello Azure 저장소에 toolog 및 푸시 변경 내용을 로컬 Git 리포지토리에서. 앱의 블레이드에서 **설정> 배포 자격 증명**을 클릭한 다음 배포 사용자 이름 및 암호를 구성합니다. 완료되면 **저장**을 클릭합니다.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>4단계: 프로젝트 배포
다음 단계 toopublish hello 사용자 앱 tooApp 로컬 Git를 사용 하 여 서비스를 사용 합니다.

1. Hello Azure 포털에서에서 앱의 블레이드에서 클릭 **설정 > 속성** hello에 대 한 **Git URL**합니다.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **Git URL** hello 원격 참조 toodeploy toofrom 로컬 리포지토리 됩니다. 단계를 수행 하는 hello에이 URL을 사용 합니다.
2. Hello 명령줄을 사용 하 여, 로컬 Git 리포지토리의 hello 루트에 있는지 확인 합니다.
3. 사용 하 여 `git remote` tooadd hello 원격 참조에 나열 된 **Git URL** 1 단계에서 만든 합니다. 명령 비슷한 toohello 다음 볼 수 있습니다.
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > hello **원격** 명령은 명명 된 참조 tooa 원격 리포지토리를 추가 합니다. 이 경우 웹 앱의 리포지토리용으로 'azure'라는 이름의 참조를 만듭니다.
   > 
   > 
4. 서비스 사용자 콘텐츠 tooApp 푸시 새 hello를 사용 하 여 **azure** 원격 방금 만든 합니다.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Hello Azure 포털에서에서 tooyour 응용 프로그램을 다시 이동 합니다. Hello 빌드되고 가장 최근의 푸시의 로그 항목을 표시 해야 **배포** 블레이드입니다. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Hello 클릭 **찾아보기** hello 앱 블레이드 tooverify hello 콘텐츠 hello 위쪽에 단추를 배포 합니다. 

## <a name="Step5"></a>문제 해결
hello 다음은 오류 또는 Azure에서 Git toopublish tooan 앱 서비스 앱을 사용 하는 경우 일반적으로 발생 하는 문제입니다.

- - -
**증상**: 수 없습니다. '[siteURL]' tooaccess: 너무 tooconnect 실패 했습니다 [scmAddress]

**원인**: hello 앱이 실행 하는 경우이 오류가 발생할 수 있습니다.

**해결 방법**: hello Azure 포털에서에서 hello 앱을 시작 합니다. Git 배포 hello 응용 프로그램을 실행 하지 않는 한 작동 하지 않습니다. 

- - -
**증상**: 'hostname' 호스트를 확인할 수 없음

**원인**:이 오류가 발생할 수 있습니다 hello 주소 정보를 만들 때 입력 하는 경우 원격 ' azure' hello 올바르지 않습니다.

**해상도**: 사용 하 여 hello `git remote -v` toolist hello 연결 된 URL 따라 모든 원격 명령입니다. 원격 ' azure' hello에 대 한 hello URL이 올바른지 확인 합니다. 필요에 따라 제거 하 고이 원격 hello 올바른 URL을 사용 하 여 다시 만듭니다.

- - -
**증상**: 공통 참조 없음 및 지정하지 않음; 아무것도 안 함. '마스터'와 같은 분기를 지정해야 할 수도 있습니다.

**원인**: git 푸시 작업을 수행할 때 분기를 지정 및 하지 설정 값을 가질 hello push.default Git에서 사용 하지 않는 경우이 오류가 발생할 수 있습니다.

**해결 방법**: hello 마스터 분기 지정 hello 푸시 작업을 다시 수행 합니다. 예:

```bash  
git push azure master
```
- - -
**증상**: src refspec [branchname]이 전혀 일치하지 않음

**원인**: hello 'azure' 원격에서 마스터 이외의 toopush tooa 분기 하려는 경우이 오류가 발생할 수 있습니다.

**해결 방법**: hello 마스터 분기 지정 hello 푸시 작업을 다시 수행 합니다. 예:

```bash  
git push azure master
```
- - -
**증상**: RPC 실패; 결과=22, HTTP 코드 = 502.

**원인**: HTTPS를 통해 toopush 큰 git 리포지토리를 시도 하는 경우이 오류가 발생할 수 있습니다.

**해결 방법**: hello 로컬 컴퓨터 toomake hello 전위 큰에 hello git 구성 변경

```bash  
git config --global http.postBuffer 524288000
```
- - -
**증상**: 오류-변경 내용이 커밋된 tooremote 저장소 하지만 웹 앱 업데이트 되지 않습니다.

**원인**: 이 오류는 추가 필수 모듈을 지정하는 package.json 파일이 포함된 Node.js 앱을 배포하는 경우에 발생할 수 있습니다.

**해결 방법**: 'npm ERR!'을 포함하는 추가 메시지를 기록 된 이전 toothis 오류 수준이 며 hello 실패 시 추가 컨텍스트를 제공할 수 있습니다. hello 다음이 오류의 원인은 알려진을 해당 'ERR npm!' hello 메시지:

* **잘못된 package.json 파일**: npm ERR! 종속성을 읽을 수 없음
* **Windows용 바이너리 배포가 없는 네이티브 모듈**:
  
  * npm ERR! \`cmd "/c" "node-gyp rebuild"\` failed with 1
    
      또는
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>추가 리소스
* [Git 설명서](http://git-scm.com/documentation)
* [프로젝트 Kudu 설명서](https://github.com/projectkudu/kudu/wiki)
* [연속 배포 tooAzure 앱 서비스](app-service-continuous-deployment.md)
* [어떻게 toouse Azure에 대 한 PowerShell](/powershell/azure/overview)
* [어떻게 toouse hello Azure 명령줄 인터페이스](../cli-install-nodejs.md)

[Azure 앱 서비스]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure 포털]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure 명령줄 인터페이스]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
