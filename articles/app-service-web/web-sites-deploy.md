---
title: "aaaDeploy 사용자 앱 tooAzure 앱 서비스 | Microsoft Docs"
description: "자세한 방법을 toodeploy 사용자 앱 tooAzure 앱 서비스입니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>사용자 응용 프로그램 tooAzure 앱 서비스 배포
이 문서를 사용 하면 파일을 결정 hello 최상의 옵션 toodeploy hello 웹 앱, 모바일 앱 백 엔드, 또는 API 앱에 대 한 너무[Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714), 다음 과정을 안내 특정 tooyour 지침을 사용 하 여 tooappropriate 리소스 기본 옵션입니다.

## <a name="overview"></a>Azure 앱 서비스 배포 개요
Azure 앱 서비스는 hello 응용 프로그램 프레임 워크 (ASP.NET, PHP, Node.js 등)를 유지합니다. 일부 프레임 워크는 Python 및 Java와 같은 다른 기본적으로 사용, 간단한 확인 표시 구성 tooenable 할 수 것입니다. 또한 프로그램 런타임의 hello 비트 hello PHP 버전 등 응용 프로그램 프레임 워크를 사용자 지정할 수 있습니다. 자세한 내용은 [Azure 앱 서비스에서 앱 구성](web-sites-configure.md)을 참조하세요.

Hello 웹 서버 또는 응용 프로그램 프레임 워크에 대 한 tooworry 없으므로 코드, 바이너리, 콘텐츠 파일 및 toohello의 해당 디렉터리 구조, 배포 하는 것은 사용자 응용 프로그램 tooApp 서비스 배포 [   **/사이트 /wwwroot** 디렉터리](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure에서 (또는 hello **/사이트/wwwroot/App_Data/작업/** WebJobs에 대 한 디렉터리). App Service는 세 가지 배포 프로세스를 지원합니다. 이 문서에서 모든 hello 배포 방법 hello 프로세스를 다음 중 하나를 사용 합니다. 

* [FTP 또는 FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): 프로그램 즐겨 찾는 FTP 또는 FTPS 도구 toomove 파일 tooAzure 프로그램에서 사용할 [FileZilla](https://filezilla-project.org) toofull 기능을 갖춘 Ide 같은 [NetBeans](https://netbeans.org)합니다. 이는 엄격한 파일 업로드 프로세스입니다. 버전 제어, 파일 구조 관리 등과 같은 추가 서비스는 앱 서비스에서 제공되지 않습니다. 
* [Kudu (OneDrive/Dropbox 또는 Mercurial Git /)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu는 hello [배포 엔진](https://github.com/projectkudu/kudu/wiki) 앱 서비스에서 합니다. 모든 저장소에서 직접 코드 tooKudu 푸시하십시오. Kudu는 또한 추가 된 서비스를 제공 코드 버전 제어, 패키지를 복원, MSBuild를 포함 하 여 tooit를 밀어넣을 때마다 및 [후크 웹](https://github.com/projectkudu/kudu/wiki/Web-hooks) 연속 배포 및 기타 자동화 작업에 대 한 합니다. hello Kudu 배포 엔진에서는 3 가지 유형의 배포 소스:   
  
  * OneDrive 및 Dropbox의 콘텐츠 동기화   
  * GitHub, Bitbucket, Visual Studio Team Services의 자동 동기화를 이용한 리포지토리 기반 연속 배포  
  * 로컬 Git의 수동 동기화를 이용한 리포지토리 기반 배포  
* [웹 배포](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): tooIIS 서버 배포를 자동화 하는 동일한 도구 hello를 사용 하 여 Visual Studio와 같은 배포 코드 tooApp 즐겨 찾는 Microsoft에서 직접 서비스 도구입니다. 이 도구는 차이나는 부분만 배포, 데이터베이스 만들기, 연결 문자열 변환 등을 지원합니다. 웹 배포 응용 프로그램 이진 파일 되기 전에 빌드됩니다 배포 tooAzure 점에서 Kudu와 다릅니다. 비슷한 tooFTP 추가 서비스 응용 프로그램 서비스에 의해 제공 됩니다.

널리 사용되는 웹 개발 도구는 이러한 배포 프로세스 중 하나 이상을 지원합니다. 확인 하는 동안 hello 선택한 도구 hello 배포 프로세스를 활용할 수 있습니다, hello 사용할 실제 DevOps 기능에 따라 달라 집니다 hello 배포 프로세스의 hello 조합을 선택한 hello 특정 도구. 예를 들어 [Visual Studio(Azure SDK 포함)](#vspros)에서 웹 배포를 수행하면 Kudu에서 자동화를 이용할 수 없는 경우에도 Visual Studio에서 패키지 복원 및 MSBuild 자동화가 가능합니다. 

> [!NOTE]
> 이러한 배포 프로세스를 실제로 하지 [프로 비전 Azure 리소스 hello](../azure-resource-manager/resource-group-template-deploy-portal.md) 앱 필요할 수 있는 합니다. 그러나 대부분의 연결 된 hello 방법 tooarticles 표시 tooprovision hello 응용 프로그램 및 프로그램 코드 tooit에 종단 간 배포 방법을 있습니다. Hello에 Azure 리소스가 프로 비전 하기 위한 추가 옵션을 찾을 수 있습니다 [명령줄 도구를 사용 하 여](#automate) 섹션.
> 
> 

## <a name="ftp"></a>FTP를 사용하여 파일을 업로드하여 수동으로 배포
웹 콘텐츠 tooa 웹 서버를 복사 하는 사용 되는 toomanually 인 경우 사용할 수 있습니다는 [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) Windows 탐색기와 같은 유틸리티 toocopy 파일 또는 [FileZilla](https://filezilla-project.org/)합니다.

hello 전문가 라면 파일을 수동으로 복사 됩니다.

* FTP 도구 사용에 익숙하며 복잡성이 최소화됨 
* 파일의 이동 위치를 정확히 인지
* FTPS를 사용한 보안 강화

hello 단점 파일을 수동으로 복사 됩니다.

* Tooknow 있으면 toodeploy 앱 서비스에서 toohello 올바른 디렉터리에 파일 하는 방법입니다. 
* 오류가 발생할 때 롤백을 위한 버전 제어가 없음
* 배포 문제 해결을 위한 기본 배포 기록이 없음
* 잠재적인 긴 배포는 대부분의 FTP 도구 diff 전용 복사 제공 하지 않는 모든 hello 파일을 복사 하기만 하므로 시간이 됩니다.  

### <a name="howtoftp"></a>FTP로 tooupload 파일 하는 방법
hello [Azure 포털](https://portal.azure.com) tooconnect tooyour 응용 프로그램의 디렉터리를 FTP 또는 FTPS를 사용 하 여 필요한 모든 hello 정보를 제공 합니다.

* [사용자 응용 프로그램 tooAzure 앱 서비스 배포 FTP를 사용 하 여](app-service-deploy-ftp.md)

## <a name="dropbox"></a>클라우드 폴더와 동기화하여 배포
대신 너무[파일을 수동으로 복사](#ftp) OneDrive와 Dropbox와 같은 클라우드 저장소 서비스에서 파일 및 폴더 tooApp 서비스를 동기화 합니다. 배포에 대 한 hello Kudu 프로세스는 사용 하 여 클라우드 폴더와 동기화 하는 중 (참조 [배포 프로세스의 개요](#overview)).

클라우드 폴더와 동기화 하는 hello 전문가 라면 됩니다.

* 배포의 간소화. OneDrive 및 Dropbox와 같은 서비스는 데스크톱 동기화 클라이언트를 제공하므로 로컬 작업 디렉터리도 배포 디렉터리입니다.
* 한 번의 클릭으로 배포
* Hello Kudu 배포 엔진의 모든 기능을 사용할 수 (예: 패키지를 복원, 자동화).

클라우드 폴더와 동기화 하는 hello 단점 됩니다.

* 오류가 발생할 때 롤백을 위한 버전 제어가 없음
* 자동화된 배포가 지원되지 않으며 수동 동기화가 필요함

### <a name="howtodropbox"></a>방법에서 클라우드 폴더가 동기화 여 toodeploy
Hello에 [Azure 포털](https://portal.azure.com), 응용 프로그램 코드와 해당 폴더의 콘텐츠 작업, OneDrive 또는 Dropbox 클라우드 저장소의 콘텐츠는 동기화에 대 한 폴더를 지정할 수 있습니다 및 hello로 동기화 tooApp 서비스의 단추를 클릭 합니다.

* [클라우드 폴더 tooAzure 앱 서비스에서에서 콘텐츠를 동기화](app-service-deploy-content-sync.md)합니다. 

## <a name="continuousdeployment"></a>클라우드 기반 소스 제어 서비스에서 연속 배포
개발 팀에 같은 클라우드 기반 소스 코드 관리 (SCM) 서비스를 사용 하는 경우 [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), 또는 [BitBucket](https://bitbucket.org/), 응용 프로그램을 구성할 수 있습니다 리포지토리에 toointegrate를 서비스 하 고 지속적으로 배포 합니다. 

hello 전문가 클라우드 기반 소스 제어 서비스에서 배포 됩니다.

* 버전 제어 tooenable 롤백입니다.
* 기능 tooconfigure 연속 배포 (및 해당 되는 Mercurial) Git에 대 한 저장소입니다. 
* 분기 단계별 배포 toodifferent 다른 분기를 배포할 수 [슬롯](web-sites-staged-publishing.md)합니다.
* Hello Kudu 배포 엔진의 모든 기능을 사용할 수 (예: 배포 버전 관리, 롤백, 패키지를 복원, 자동화).

클라우드 기반 소스 제어 서비스에서 배포 hello con은입니다.

* 필요한 hello 해당 SCM 서비스의 일부 정보입니다.

### <a name="vsts"></a>클라우드 기반 원본에서 지속적으로 toodeploy 서비스를 제어 하는 방법
Hello에 [Azure 포털](https://portal.azure.com), GitHub, Bitbucket, 및 Visual Studio Team Services의 연속 배포를 구성할 수 있습니다.

* [연속 배포 tooAzure 앱 서비스](app-service-continuous-deployment.md)합니다. 

어떻게 tooconfigure 연속 배포로 나열 되지 않은 클라우드 저장소에서 수동으로 hello Azure 포털 아웃 toofind (같은 [GitLab](https://gitlab.com/)), 참조 [수동 단계를 사용 하 여 연속 배포를 설정](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)합니다.

## <a name="localgitdeployment"></a>로컬 Git에서 배포
개발 팀에 Git 기반는 온-프레미스 로컬 소스 코드 관리 (SCM) 서비스를 사용 하는 경우 배포 소스 tooApp 서비스도 구성할 수 있습니다. 

로컬 Git에서 배포할 경우 장점:

* 버전 제어 tooenable 롤백입니다.
* 분기 단계별 배포 toodifferent 다른 분기를 배포할 수 [슬롯](web-sites-staged-publishing.md)합니다.
* Hello Kudu 배포 엔진의 모든 기능을 사용할 수 (예: 배포 버전 관리, 롤백, 패키지를 복원, 자동화).

로컬 Git에서 배포할 경우 단점:

* 필요한 hello 해당 SCM 시스템의 일부 정보입니다.
* 연속 배포를 위한 턴키 솔루션이 없음 

### <a name="vsts"></a>어떻게 toodeploy 로컬 Git에서
Hello에 [Azure 포털](https://portal.azure.com), 로컬 Git 배포를 구성할 수 있습니다.

* [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다. 
* [모든 git/hg 리포지토리에서 tooWeb 앱 게시](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html)합니다.  

## <a name="deploy-using-an-ide"></a>IDE를 사용하여 배포
이미 사용 중인 경우 [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 와 [Azure SDK](https://azure.microsoft.com/downloads/), 또는 다른 IDE 도구 모음이 like [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), 및 [ IntelliJ 아이디어](https://www.jetbrains.com/idea/), IDE 내에서 직접 tooAzure를 배포할 수 있습니다. 이 옵션은 개인 개발자에 이상적입니다.

Visual Studio 지원 기본 설정에 따라 모든 세 가지 배포 프로세스 (FTP, Git, 및 웹 배포), FTP 또는 Git 통합 있는 경우 다른 Ide tooApp 서비스를 배포할 수 있습니다 (참조 [배포 프로세스의 개요](#overview)).

hello 전문가 라면 IDE를 사용 하 여 배포 됩니다.

* 잠재적으로 hello에 종단 간 응용 프로그램 수명 주기 하기 위한 도구를 최소화 합니다. 개발, 디버깅, 추적 및 IDE 외부에서 이동 하지 않고도 앱 tooAzure 배포 합니다. 

hello 단점 IDE를 사용 하 여 배포 됩니다.

* 도구 사용의 복잡성 증가
* 팀 프로젝트의 경우 여전히 소스 제어 시스템 필요

<a name="vspros"></a> Azure SDK가 있는 Visual Studio를 사용하여 배포할 때의 추가 장점:

* Azure SDK를 통해 Visual Studio에서 Azure 리소스를 최고의 리소스로 만들 수 있음. 만들기, 삭제, 편집, 시작 및 중지할 응용 프로그램, 쿼리 hello 백 엔드 SQL 데이터베이스, 라이브 디버그 hello Azure 응용 프로그램 등에입니다. 
* Azure에서 코드 파일의 라이브 편집
* Azure에서 앱의 라이브 디버깅
* 통합된 Azure 탐색기
* 차이나는 부분만 배포 

### <a name="vs"></a>어떻게 직접 toodeploy Visual Studio에서
* [Azure 및 ASP.NET 시작](app-service-web-get-started-dotnet.md). 어떻게 toocreate Visual Studio 및 웹 배포를 사용 하 여 간단한 ASP.NET MVC 웹 프로젝트를 배포 합니다.
* [어떻게 tooDeploy Visual Studio를 사용 하 여 Azure WebJobs](websites-dotnet-deploy-webjobs.md)합니다. 어떻게 tooconfigure 콘솔 응용 프로그램 프로젝트가 WebJobs로 배포할 수 있도록 지정 합니다.  
* [Visual Studio를 사용한 ASP.NET 웹 배포](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction)(영문). 이 목록의 다른 hello 보다 배포 작업의 전체 범위를 포함 하는 12 부분으로 이루어진 자습서 시리즈 합니다. Hello 자습서를 쓴 있지만 누락 된 항목과 나중에 추가 하는 정보에 설명 하므로 일부 Azure 배포 기능이 추가 되었습니다.
* [Git 리포지토리에서 Visual Studio 2012에는 ASP.NET 웹 사이트 tooAzure를 직접 배포](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881)합니다. Visual studio에서 Git 플러그 인 toocommit hello 코드 tooGit hello를 사용 하 고 Azure toohello Git 리포지토리 연결 toodeploy ASP.NET 웹 프로젝트 방법에 대해 설명 합니다. Visual Studio 2013부터 Git 지원이 기본 제공되므로 플러그 인을 설치할 필요가 없습니다.

### <a name="aztk"></a>어떻게 toodeploy를 사용 하 여 Eclipse 및 IntelliJ 개념에 대 한 Azure 도구 키트 hello
Microsoft는 hello 통해 IntelliJ 하 여 Eclipse에서 직접 웹 응용 프로그램 tooAzure 가능한 toodeploy [Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse.md) 및 [IntelliJ 용 Azure 도구 키트](../azure-toolkit-for-intellij.md)합니다. hello 다음 자습서를 보여 줍니다 간단한 "Hello" 세계 웹 앱 tooAzure 두 IDE 중 하나를 사용 하 여 배포 하는 hello 단계를.

* [Eclipse에서 Azure용 Hello World Web Apps을 만듭니다](app-service-web-eclipse-create-hello-world-web-app.md). 이 자습서에는 toouse Azure 도구 키트에 Eclipse toocreate hello 하 고 Azure 용 Hello World 웹 앱을 배포 하는 방법을 보여줍니다.
* [IntelliJ에서 Azure용 Hello World Web Apps을 만듭니다](app-service-web-intellij-create-hello-world-web-app.md). 이 자습서에는 toouse IntelliJ toocreate에 대 한 Azure 도구 키트 hello 하 고 Azure 용 Hello World 웹 앱을 배포 하는 방법을 보여줍니다.

## <a name="automate"></a>명령줄 도구를 사용하여 배포 자동화
선택한 hello 개발 환경으로 hello 명령줄 터미널을 선호 하는 경우에 명령줄 도구를 사용 하 여 앱 서비스 앱에 대 한 배포 작업을 스크립팅할 수 있습니다. 

명령줄 도구를 사용한 배포의 장점:

* 스크립트 배포 시나리오가 가능합니다.
* Azure 리소스와 코드 배포의 프로비저닝을 통합합니다.
* Azure 배포를 기존 연속 통합 스크립트에 통합합니다.

명령줄 도구를 사용한 배포의 단점:

* GUI를 선호하는 개발자에게는 적합하지 않습니다.

### <a name="automatehow"></a>어떻게 tooautomate 배포 명령줄 도구

참조 [명령줄 도구와 함께 Azure 응용 프로그램의 배포를 자동화](app-service-deploy-command-line.md) 명령줄 도구 및 링크 tootutorials 목록은 합니다. 

## <a name="nextsteps"></a>다음 단계
일부 시나리오에서는 toobe 수 tooeasily 스위치 간에 스테이징 및 프로덕션 버전의 앱 사이 할 수 있습니다. 자세한 내용은 [웹 앱에서 준비된 배포](web-sites-staged-publishing.md)를 참조하세요.

백업 및 복원 계획을 마련하는 일은 배포 워크플로의 중요한 부분입니다. Hello 서비스 응용 프로그램 백업 및 복원 기능에 대 한 정보를 참조 하십시오. [웹 앱 백업](web-sites-backup.md)합니다.  

Toouse Azure의 역할 기반 액세스 제어 toomanage tooApp 서비스 배포를 액세스 하는 방법에 대 한 정보를 참조 하십시오. [RBAC 및 웹 응용 프로그램 게시](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/)합니다.

