---
title: "Azure에서 플라스도 aaaCreating 웹 앱"
description: "Toorunning Azure에서 Python 웹 응용 프로그램을 소개 하는 자습서입니다."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Azure에서 Flask를 사용하여 웹앱 만들기
이 자습서에서는 tooget 시작 Python을 실행 하는 방법을 설명 [Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.  웹앱은 제한된 무료 호스팅 및 신속한 배포 기능을 제공하며, Python을 사용할 수 있습니다!  응용 프로그램 증가, toopaid 호스팅 전환할 수 있습니다 및 모든와 통합할 수 있습니다 때 hello 다른 Azure 서비스입니다.

Hello 플라스 웹 프레임 워크를 사용 하 여 응용 프로그램을 만들 됩니다 (참조에 대 한이 자습서의 대체 버전 [Django](web-sites-python-create-deploy-django-app.md) 및 [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Hello 웹 사이트 hello Azure 갤러리에서에서 Git 배포 설정 만들고 hello 로컬 리포지토리를 복제 합니다.  다음은 hello 응용 프로그램을 로컬로 실행, 변경, 커밋 하 고 tooAzure 푸시 합니다.  자습서에서는 어떻게 hello toodo Windows 또는 Mac/Linux에서이 있습니다.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
* Windows, Mac 또는 Linux
* Python 2.7 또는 3.4
* setuptools, pip, virtualenv(Python 2.7 전용)
* Git
* [Python Tools for Visual Studio][Python Tools for Visual Studio](PTVS) - 참고: 선택 사항입니다.

**참고**: 현재 Python 프로젝트에서는 TFS 게시를 사용할 수 없습니다.

### <a name="windows"></a>Windows
Python 2.7 또는 3.4(32비트)를 아직 설치하지 않은 경우 웹 플랫폼 설치 관리자를 사용하여 [Azure SDK for Python 2.7] 또는 [Azure SDK for Python 3.4]를 설치하는 것이 좋습니다.  이 Python, setuptools, pip, virtualenv 등의 (32 비트 Python hello Azure 호스트 컴퓨터에 설치 된 항목은) hello 32 비트 버전을 설치 합니다.  또는 [python.org]에서 Python을 다운로드할 수 있습니다.

Git의 경우 [Windows용 Git] 또는 [Windows용 GitHub]를 설치하는 것이 좋습니다.  Visual Studio를 사용 하는 경우 통합 hello Git 지원을 사용할 수 있습니다.

또한 [Python Tools 2.2 for Visual Studio]를 설치하는 것이 좋습니다.  이 속성은 선택적 있는 경우 [Visual Studio]hello를 포함 하 여 가능한 Visual Studio Community 2013 또는 Visual Studio Express 2013 for Web 차례로 이렇게 하면 한 훌륭한 인 Python IDE 인 합니다.

### <a name="maclinux"></a>Mac/Linux
Python 및 Git를 이미 설치했어야 하지만 Python 버전은 2.7 또는 3.4여야 합니다.

## <a name="web-app-create-on-hello-azure-portal"></a>Hello Azure 포털에서 웹 앱 만들기
hello 앱을 만드는 첫 번째 단계는 hello 통해 toocreate hello 웹 앱 [Azure 포털](https://portal.azure.com)합니다. 

1. Hello Azure 포털에 로그인 하 고 hello 클릭 **새로** hello 왼쪽된 하단에서 단추입니다. 
2. **웹 + 모바일**을 클릭합니다.
3. Hello 검색 상자에 "python"를 입력 합니다.
4. Hello 검색 결과에서 선택 **플라스**, 클릭 **만들기**합니다.
5. Hello 새 플라스 같은 앱에 대 한 새 앱 서비스 계획을 만들고 새 리소스 그룹을 구성 합니다. 그런 다음에 **만들기**를 클릭합니다.
6. Hello 지침에 따라 새로 만든된 웹 앱에 대 한 Git 게시를 구성 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.

## <a name="application-overview"></a>응용 프로그램 개요
### <a name="git-repository-contents"></a>Git 리포지토리 콘텐츠
Hello 다음 섹션에서 복제 hello 초기 Git 리포지토리에 있습니다 hello 파일의 개요는 다음과 같습니다.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Hello 응용 프로그램에 대 한 주 소스입니다.  마스터 레이아웃과 함께 3페이지(index, about, contact)로 구성됩니다.  정적 콘텐츠와 스크립트에는 bootstrap, jquery, modernizr 및 respond가 포함되어 있습니다.

    \runserver.py

로컬 개발 서버 지원. 로컬이 toorun hello 응용 프로그램을 사용 합니다.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

[Python Tools for Visual Studio]에서 사용되는 프로젝트 파일

    \ptvs_virtualenv_proxy.py

가상 환경용 IIS 프록시 및 PTVS 원격 디버깅 지원

    \requirements.txt

이 응용 프로그램에 필요한 외부 패키지. hello 배포 스크립트에는이 파일에 나열 된 설치 hello 패키지 pip 됩니다.

    \web.2.7.config
    \web.3.4.config

IIS 구성 파일.  hello 배포 스크립트는 hello 적절 한 web.x.y.config 사용 되 고 web.config로 복사 됩니다.

### <a name="optional-files---customizing-deployment"></a>선택적 파일 - 배포 사용자 지정
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>선택적 파일 - Python 런타임
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>서버의 추가 파일
일부 파일 hello 서버에 존재 하지만 toohello git 리포지토리를 추가 되지 않습니다.  Hello 배포 스크립트에 의해 만들어집니다.

    \web.config

IIS 구성 파일.  모든 배포에서 web.x.y.config를 통해 생성됩니다.

    \env\

Python 가상 환경.  호환 되는 가상 환경 hello 응용 프로그램에 존재 하지 않는 경우 배포 중에 생성 합니다.  Requirements.txt에 나열 된 패키지를 설치 하는 pip는 pip는 hello 패키지가 이미 설치 되어 있는 경우 설치를 건너뜁니다.

hello 다음 3 설명 어떻게 hello로 tooproceed 웹 3 다양 한 환경에서 응용 프로그램 개발:

* Windows, Python Tools for Visual Studio 사용
* Windows, 명령줄 사용
* Mac/Linux, 명령줄 사용

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>웹앱 배포 - Windows - Python Tools for Visual Studio
### <a name="clone-hello-repository"></a>Hello 리포지토리 복제
첫째, hello Azure 포털에서 제공 하는 hello URL를 사용 하 여 hello 리포지토리를 복제 합니다. 자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.

Hello 저장소의 hello 루트에 포함 된 hello 솔루션 파일 (.sln)을 엽니다.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>가상 환경 만들기
이제 로컬 개발을 위한 가상 환경을 만듭니다.  **Python Environments**를 마우스 오른쪽 단추로 클릭하고 **Add Virtual Environment...**를 선택합니다.

* Hello 환경의 hello 이름 인지 확인 `env`합니다.
* Hello 기본 인터프리터를 선택 합니다.  Toouse hello 동일한 버전의 웹 앱에 대해 선택 된 Python 있는지 확인 (runtime.txt 또는 hello **응용 프로그램 설정** hello Azure 포털에서에서 웹 응용 프로그램의 블레이드)입니다.
* Hello 옵션 toodownload 및 설치 패키지 선택 되어 있는지 확인 합니다.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

**만들기**를 클릭합니다.  이 hello 가상 환경을 만들고 requirements.txt에 나열 된 종속성을 설치 합니다.

### <a name="run-using-development-server"></a>개발 서버를 사용하여 실행
디버깅, 키를 눌러 F5 toostart 및 웹 브라우저가 자동으로 toohello 페이지가 열립니다 로컬로 실행 합니다.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

Hello 소스, 사용 하 여 hello 조사식 창에서 중단점을 설정할 수 있습니다.  Hello 참조 [Python Tools for Visual Studio 설명서] 대 한 자세한 내용은 hello 다양 한 기능입니다.

### <a name="make-changes"></a>변경 작업
이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.

변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>추가 패키지 설치
응용 프로그램에 Python 및 Flask 이외의 종속성이 있을 수 있습니다.

pip를 사용하여 추가 패키지를 설치할 수 있습니다.  선택 및 hello 가상 환경에서 tooinstall 패키지를 마우스 오른쪽 단추로 클릭 **Python 패키지 설치**합니다.

예를 들어 tooinstall hello 액세스할 수 있도록 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스를 입력 하는 Python 용 Azure SDK `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **requirements.txt 생성** tooupdate requirements.txt 합니다.

그런 다음 커밋 hello toorequirements.txt toohello Git 리포지토리를 변경합니다.

### <a name="deploy-tooazure"></a>TooAzure 배포
해당 배포를 tootrigger 클릭 **동기화** 또는 **푸시**합니다.  Sync는 밀어넣기와 끌어오기를 둘 다 수행합니다.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

hello 첫 번째 배포 된 가상 환경, 설치 패키지 등 생성 될 약간의 시간이 걸립니다.

Visual Studio hello 배포의 진행 상황 hello 표시 되지 않습니다.  Tooreview hello 출력을 원하는 경우에 hello 섹션을 참조 [문제 해결-배포](#troubleshooting-deployment)합니다.

Toohello Azure URL tooview 변경 내용을 찾습니다.

## <a name="web-app-development---windows---command-line"></a>웹앱 배포 - Windows - 명령줄
### <a name="clone-hello-repository"></a>Hello 리포지토리 복제
첫째, hello Azure 포털에서 제공 하는 hello URL을 사용 하 여 hello 리포지토리를 복제 하 고 원격으로 hello Azure 저장소를 추가 합니다. 자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>가상 환경 만들기
개발 목적으로 (추가 하지 않아도 toohello 저장소)에 대 한 새 가상 환경이 만들겠습니다.  Python에서 가상 환경을 위치 변경이 가능한, 되지 않으므로 hello 응용 프로그램에서 작업 하는 모든 개발자는 자체적으로 만드는 로컬로.

Toouse hello 동일한 버전의 웹 앱에 대해 선택 된 Python 있는지 확인 (runtime.txt 또는 hello **응용 프로그램 설정** hello Azure 포털에서에서 웹 응용 프로그램의 블레이드)입니다.

Python 2.7:

    c:\python27\python.exe -m virtualenv env

Python 3.4:

    c:\python34\python.exe -m venv env

응용 프로그램에 필요한 모든 외부 패키지를 설치합니다. 가상 환경에서 hello 리포지토리 tooinstall hello 패키지의 hello 루트를 hello requirements.txt 파일을 사용할 수 있습니다.

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>개발 서버를 사용하여 실행
Hello 응용 프로그램 개발 서버에서 다음 명령을 hello로 시작할 수 있습니다.

    env\scripts\python runserver.py

hello 콘솔 hello URL이 표시 됩니다 및를 수신 대기 포트 hello 서버:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

그런 다음 웹 브라우저 toothat URL을 엽니다.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>변경 작업
이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.

변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>추가 패키지 설치
응용 프로그램에 Python 및 Flask 이외의 종속성이 있을 수 있습니다.

pip를 사용하여 추가 패키지를 설치할 수 있습니다.  예를 들어 tooinstall hello을 제공 하는 Python 용 Azure SDK 액세스 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스 유형:

    env\scripts\pip install azure

Tooupdate requirements.txt 있는지 확인 하십시오.

    env\scripts\pip freeze > requirements.txt

Hello 변경 내용을 커밋하십시오.

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>TooAzure 배포
배포 tootrigger 푸시 hello tooAzure를 변경합니다.

    git push azure master

가상 환경 만들기, 패키지를 설치 web.config의 생성을 포함 하 여 hello 배포 스크립트의 hello 출력이 표시 됩니다.

Toohello Azure URL tooview 변경 내용을 찾습니다.

## <a name="web-app-development---maclinux---command-line"></a>웹앱 배포 - Mac/Linux - 명령줄
### <a name="clone-hello-repository"></a>Hello 리포지토리 복제
첫째, hello Azure 포털에서 제공 하는 hello URL을 사용 하 여 hello 리포지토리를 복제 하 고 원격으로 hello Azure 저장소를 추가 합니다. 자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>가상 환경 만들기
개발 목적으로 (추가 하지 않아도 toohello 저장소)에 대 한 새 가상 환경이 만들겠습니다.  Python에서 가상 환경을 위치 변경이 가능한, 되지 않으므로 hello 응용 프로그램에서 작업 하는 모든 개발자는 자체적으로 만드는 로컬로.

Toouse hello 동일한 버전의 웹 앱에 대해 선택 된 Python 있는지 확인 (runtime.txt 또는 hello **응용 프로그램 설정** hello Azure 포털에서에서 웹 응용 프로그램의 블레이드)입니다.

Python 2.7:

    python -m virtualenv env

Python 3.4:

    python -m venv env
또는 pyvenv env

응용 프로그램에 필요한 모든 외부 패키지를 설치합니다. 가상 환경에서 hello 리포지토리 tooinstall hello 패키지의 hello 루트를 hello requirements.txt 파일을 사용할 수 있습니다.

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>개발 서버를 사용하여 실행
Hello 응용 프로그램 개발 서버에서 다음 명령을 hello로 시작할 수 있습니다.

    env/bin/python runserver.py

hello 콘솔 hello URL이 표시 됩니다 및를 수신 대기 포트 hello 서버:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

그런 다음 웹 브라우저 toothat URL을 엽니다.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>변경 작업
이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.

변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>추가 패키지 설치
응용 프로그램에 Python 및 Flask 이외의 종속성이 있을 수 있습니다.

pip를 사용하여 추가 패키지를 설치할 수 있습니다.  예를 들어 tooinstall hello을 제공 하는 Python 용 Azure SDK 액세스 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스 유형:

    env/bin/pip install azure

Tooupdate requirements.txt 있는지 확인 하십시오.

    env/bin/pip freeze > requirements.txt

Hello 변경 내용을 커밋하십시오.

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>TooAzure 배포
배포 tootrigger 푸시 hello tooAzure를 변경합니다.

    git push azure master

가상 환경 만들기, 패키지를 설치 web.config의 생성을 포함 하 여 hello 배포 스크립트의 hello 출력이 표시 됩니다.

Toohello Azure URL tooview 변경 내용을 찾습니다.

## <a name="troubleshooting---package-installation"></a>문제 해결 - 패키지 설치
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>문제 해결 - 가상 환경
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>다음 단계
Visual Studio에 대 한 이러한 링크 toolearn 플라스 및 Python Tools에 대 한 자세한를 수행 합니다. 

* [Flask 설명서]
* [Python Tools for Visual Studio 설명서]

Azure 테이블 저장소 및 MongoDB에 대한 자세한 정보:

* [Azure의 Flask 및 MongoDB와 Python Tools for Visual Studio]
* [Azure의 Flask 및 Azure 테이블 저장소와 Python Tools for Visual Studio]

자세한 내용은 참고 항목 hello [Python 개발자 센터](/develop/python/)합니다.

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Azure의 Flask 및 MongoDB와 Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Azure의 Flask 및 Azure 테이블 저장소와 Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Windows용 Git]: http://msysgit.github.io/
[Windows용 GitHub]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Flask 설명서]: http://flask.pocoo.org/ 

