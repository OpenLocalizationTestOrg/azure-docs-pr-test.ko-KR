---
title: "aaaDjango 및 Python Tools 2.2 for Visual Studio를 사용 하 여 Azure에서 MySQL"
description: "어떻게 toouse hello Python Tools toocreate Visual Studio에 대 한 MySQL 데이터베이스 인스턴스의 데이터를 저장 하는 Django 웹 앱 학습과 tooAzure 앱 서비스 웹 앱을 배포 합니다."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Azure의 Django 및 MySQL과 Python Tools 2.2 for Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

이 자습서를 사용 하 여 [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate 단순 hello PTVS 샘플 템플릿 중 하나를 사용 하 여 웹 앱을 폴링합니다. 에 대해 배워 봅니다 toouse MySQL 서비스 호스팅 방법 Azure에서, 어떻게 tooconfigure hello 웹 앱 toouse MySQL 어떻게 toopublish hello 웹 응용 프로그램 너무[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.

> [!NOTE]
> 이 자습서에 포함 된 hello 정보 비디오를 따라 hello에 제공 됩니다.
> 
> [PTVS 2.1: MySQL을 사용하는 Django 앱][video]
> 
> 

Hello 참조 [Python 개발자 센터] Bottle를 사용 하 여 ptvs Azure 앱 서비스 웹 앱의 개발을 설명 하는 다른 문서 플라스 및 Django 웹 프레임 워크에서 Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스입니다. 개발 하는 경우 hello 단계는 유사 하지만이 문서에서는 앱 서비스, [Azure 클라우드 서비스]합니다.

## <a name="prerequisites"></a>필수 조건
* Visual Studio 2015
* [Python 2.7 32비트] 또는 [Python 3.4 32비트]
* [Python Tools 2.2 for Visual Studio]
* [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]
* [Azure SDK Tools for VS 2015]
* Django 1.9 이상

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드 및 약정은 필요하지 않습니다.
> 
> 

## <a name="create-hello-project"></a>Hello 프로젝트 만들기
이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다. 가상 환경을 만들고 필요한 패키지를 설치합니다. sqlite를 사용하여 로컬 데이터베이스를 만듭니다. 다음 hello 응용 프로그램을 로컬로 실행 합니다.

1. Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.
2. 프로젝트 템플릿 hello에서 hello [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2] 아래에서 사용할 수 있는 **Python**, **샘플**합니다. 선택 **설문 Django 웹 프로젝트** 확인 toocreate hello 프로젝트를 클릭 합니다.
   
    ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. 외부 패키지 입력 정보 요청된 tooinstall 됩니다. **가상 환경에 설치**를 선택합니다.
   
    ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. 선택 **Python 2.7** 또는 **Python 3.4** hello 기본 해석기로 합니다.
   
    ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.  그런 다음 **Django Create Superuser**를 선택합니다.
6. Django 관리 콘솔 열리며 hello 프로젝트 폴더에 sqlite 데이터베이스를 만듭니다. Hello 프롬프트 toocreate 사용자를 따릅니다.
7. Hello 응용 프로그램 키를 눌러 작동 하는지 확인 `F5`합니다.
8. 클릭 **로그인** hello hello 위쪽 탐색 모음에서.
   
    ![Django 탐색 모음](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Hello 데이터베이스를 동기화 할 때 만든 hello 사용자에 대 한 hello 자격 증명을 입력 합니다.
   
    ![로그인 형식](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. **Create Sample Polls**를 클릭합니다.
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. poll and vote를 클릭합니다.
    
     ![샘플 설문 조사 투표](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>MySQL 데이터베이스 만들기
Hello 데이터베이스에서는 Azure에서 호스팅된 ClearDB MySQL 데이터베이스를 만듭니다.

또는 Azure에서 실행되는 자체의 가상 컴퓨터를 만든 다음 MySQL을 직접 설치하고 관리할 수도 있습니다.

다음 단계에 따라 무료로 데이터베이스를 만들 수 있습니다.

1. Toohello 로그인 [Azure 포털]합니다.
2. Hello hello 탐색 창의 위쪽에 클릭 **새로**, 클릭 **데이터 + 저장소**, 클릭 하 고 **MySQL 데이터베이스**합니다.
3. 새 리소스 그룹을 만들어 hello 새 MySQL 데이터베이스를 구성 하 고 hello에 대 한 적절 한 위치를 선택 합니다.
4. Hello MySQL 데이터베이스를 만든 후 클릭 **속성** hello 데이터베이스 블레이드에서 합니다.
5. hello 복사 단추 tooput hello 값을 사용 하 여 **연결 문자열** hello 클립보드에 있습니다.

## <a name="configure-hello-project"></a>Hello 프로젝트 구성
이 섹션에서는 방금 만든 웹 응용 프로그램 toouse hello MySQL 데이터베이스를 구성 합니다. 또한 Django와 추가 Python 패키지 필요한 toouse MySQL 데이터베이스를 설치 합니다. 다음 hello 웹 응용 프로그램을 로컬로 실행 합니다.

1. Visual Studio에서 열고 **settings.py**, hello에서 *ProjectName* 폴더입니다. 일시적으로 hello 연결 문자열 hello 편집기에 붙여 넣으십시오. hello 연결 문자열은이 형식:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Hello 기본 데이터베이스 변경 **엔진** 집합과, MySQL, toouse hello에 대 한 값 **이름**, **사용자**, **암호** 및  **호스트** hello에서 **CONNECTIONSTRING**합니다.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. 솔루션 탐색기에서 아래 **Python 환경**hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **Python 패키지 설치**합니다.
3. Hello 패키지 설치 `mysqlclient` 를 사용 하 여 **pip**합니다.
   
    ![설치 패키지 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.  그런 다음 **Django Create Superuser**를 선택합니다.
   
    그러면 hello 이전 섹션에서 만든 hello MySQL 데이터베이스에 대 한 hello 테이블 생성 됩니다. Hello 프롬프트 toocreate toomatch hello 사용자 hello이 문서의 첫 번째 섹션에서 만든 hello sqlite 데이터베이스에 없는 사용자를 따릅니다.
5. Hello 응용 프로그램을 실행 `F5`합니다. 사용 하 여 만든 설문 **샘플 설문 만들** 투표 제출한 hello 데이터 hello MySQL 데이터베이스에 serialize 됩니다.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Hello 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.
Azure.NET SDK hello 쉽게 toodeploy 웹 앱 tooAzure 앱 서비스를 제공합니다.

1. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.
   
    ![웹 게시 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure 앱 서비스**를 클릭합니다.
3. 클릭 **새로** toocreate 새 웹 앱입니다.
4. Hello 필드 뒤에 입력 하 고 클릭 **만들기**:
   
   * **웹앱 이름**
   * **앱 서비스 계획**
   * **리소스 그룹**
   * **지역**
   * 둡니다 **데이터베이스 서버** 도**데이터베이스가 없습니다.**
5. 다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.
6. 웹 브라우저가 toohello 게시 된 웹 응용 프로그램을 자동으로 열립니다. Hello를 사용 하 여 예상 대로 hello 웹 응용 프로그램 작업을 참조 해야 **MySQL** Azure에서 호스팅되는 데이터베이스입니다.
   
    ![웹 브라우저](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    축하합니다. MySQL 기반 웹 응용 프로그램 tooAzure를 게시 했습니다.

## <a name="next-steps"></a>다음 단계
Visual Studio, Django 및 MySQL Python Tools에 대 한 자세한 링크 toolearn 이러한 방식을 따릅니다.

* [Python Tools for Visual Studio 설명서]
  * [웹 프로젝트]
  * [클라우드 서비스 프로젝트]
  * [Microsoft Azure의 원격 디버깅]
* [Django 설명서]
* [MySQL]

자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.

<!--Link references-->

[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure 포털]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32비트]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026
[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027
[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 설명서]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
