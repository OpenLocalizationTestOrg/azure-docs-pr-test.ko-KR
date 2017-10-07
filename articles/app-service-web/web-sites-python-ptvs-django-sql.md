---
title: "aaaDjango 및 Python Tools 2.2 for Visual Studio를 사용 하 여 Azure에서 SQL 데이터베이스"
description: "어떻게 toouse hello Python Tools toocreate Visual Studio에 대 한 SQL 데이터베이스 인스턴스의 데이터를 저장 하는 Django 웹 앱 학습과 tooAzure 앱 서비스 웹 앱을 배포 합니다."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Azure의 Django 및 SQL 데이터베이스와 Python Tools 2.2 for Visual Studio
이 자습서에서는 [Python Tools for Visual Studio] toocreate 단순 hello PTVS 샘플 템플릿 중 하나를 사용 하 여 웹 앱을 폴링합니다. 이 자습서는 [비디오](https://www.youtube.com/watch?v=ZwcoGcIeHF4)로도 제공됩니다.

Toouse SQL 데이터베이스 호스팅 방법 Azure에서, 어떻게 tooconfigure hello 웹 응용 프로그램 toouse SQL 데이터베이스 및 어떻게 toopublish hello 웹 응용 프로그램 너무 알아봅니다 म[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.

Hello 참조 [Python 개발자 센터] Bottle를 사용 하 여 ptvs Azure 앱 서비스 웹 앱의 개발을 설명 하는 다른 문서 플라스 및 Django 웹 프레임 워크에서 Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스입니다. 개발 하는 경우 hello 단계는 유사 하지만이 문서에서는 앱 서비스, [Azure 클라우드 서비스]합니다.

## <a name="prerequisites"></a>필수 조건
* Visual Studio 2015
* [Python 2.7 32비트]
* [Python Tools 2.2 for Visual Studio]
* [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]
* [Azure SDK Tools for VS 2015]
* Django 1.9 이상

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
>
>

## <a name="create-hello-project"></a>Hello 프로젝트 만들기
이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다. 가상 환경을 만들고 필요한 패키지를 설치합니다. sqlite를 사용하여 로컬 데이터베이스를 만듭니다. 그런 다음 hello 웹 응용 프로그램을 로컬로 실행할 합니다.

1. Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.
2. 프로젝트 템플릿 hello에서 hello [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2] 아래에서 사용할 수 있는 **Python**, **샘플**합니다. 선택 **설문 Django 웹 프로젝트** 확인 toocreate hello 프로젝트를 클릭 합니다.

     ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. 외부 패키지 입력 정보 요청된 tooinstall 됩니다. **가상 환경에 설치**를 선택합니다.

     ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. 선택 **Python 2.7** hello 기본 해석기로 합니다.

     ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.  그런 다음 **Django Create Superuser**를 선택합니다.
6. Django 관리 콘솔 열리며 hello 프로젝트 폴더에 sqlite 데이터베이스를 만듭니다. Hello 프롬프트 toocreate 사용자를 따릅니다.
7. Hello 응용 프로그램 키를 눌러 작동 하는지 확인 <kbd>F5</kbd>합니다.
8. 클릭 **로그인** hello hello 위쪽 탐색 모음에서.

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Hello 데이터베이스를 동기화 할 때 만든 hello 사용자에 대 한 hello 자격 증명을 입력 합니다.

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. **Create Sample Polls**를 클릭합니다.

      ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. poll and vote를 클릭합니다.

      ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>SQL 데이터베이스 만들기
Hello 데이터베이스에 대 한 Azure SQL 데이터베이스를 만들어 보겠습니다.

다음 단계에 따라 데이터베이스를 만들 수 있습니다.

1. Hello에 로그인 [Azure 포털]합니다.
2. Hello hello 탐색 창 아래쪽에 있는 클릭 **새로**합니다. **데이터 + 저장소** > **SQL Database**를 클릭합니다.
3. 구성 선택 hello에 대 한 적절 한 위치 및 새 리소스 그룹을 만들어 새 SQL 데이터베이스 hello 합니다.
4. Hello SQL 데이터베이스를 만든 후 클릭 **Visual Studio에서 열기** hello 데이터베이스 블레이드에서 합니다.
5. **방화벽 구성**을 클릭합니다.
6. Hello에 **방화벽 설정** 블레이드를 사용 하 여 방화벽 규칙을 추가할 **시작 IP** 및 **끝 IP** toohello 개발 컴퓨터의 공용 IP 주소를 설정 합니다. **Save**를 클릭합니다.

   이렇게 하면 개발 컴퓨터에서 연결 toohello 데이터베이스 서버입니다.
7. Hello 데이터베이스 블레이드를 다시 클릭 **속성**, 클릭 **데이터베이스 연결 문자열 표시**합니다.
8. hello 복사 단추 tooput hello 값을 사용 하 여 **ADO.NET** hello 클립보드에 있습니다.

## <a name="configure-hello-project"></a>Hello 프로젝트 구성
이 섹션에서는 방금 만든 웹 응용 프로그램 toouse hello SQL 데이터베이스를 구성 합니다. 에서는도 Django와 추가 Python 패키지 필요한 toouse SQL 데이터베이스를 설치 합니다. 그런 다음 hello 웹 응용 프로그램을 로컬로 실행할 합니다.

1. Visual Studio에서 열고 **settings.py**, hello에서 *ProjectName* 폴더입니다. 일시적으로 hello 연결 문자열 hello 편집기에 붙여 넣으십시오. hello 연결 문자열은이 형식:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

hello 정의 편집 `DATABASES` 위의 toouse hello 값입니다.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. 솔루션 탐색기에서 아래 **Python 환경**hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **Python 패키지 설치**합니다.
2. Hello 패키지 설치 `pyodbc` 를 사용 하 여 **pip**합니다.

     ![Python 패키지 설치 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Hello 패키지 설치 `django-pyodbc-azure` 를 사용 하 여 **pip**합니다.

     ![Python 패키지 설치 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.  그런 다음 **Django Create Superuser**를 선택합니다.

   그러면 hello 이전 섹션에서 만든 hello SQL 데이터베이스에 대 한 hello 테이블 생성 됩니다. Hello 프롬프트 toocreate toomatch hello 사용자 hello 첫 번째 섹션에서 만든 hello sqlite 데이터베이스에 없는 사용자를 따릅니다.
5. Hello 응용 프로그램을 실행 `F5`합니다. 사용 하 여 만든 설문 **샘플 설문 만들** 투표 제출한 hello 데이터 hello SQL 데이터베이스에 serialize 됩니다.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Hello 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.
hello Azure.NET SDK 웹 웹 응용 프로그램 tooAzure 앱 서비스 웹 앱을 쉽게 toodeploy를 제공합니다.

1. **솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

     ![웹 게시 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure 웹앱**을 클릭합니다.
3. 클릭 **새로** toocreate 새 웹 앱입니다.
4. Hello 필드 뒤에 입력 하 고 클릭 **만들기**합니다.

   * **웹앱 이름**
   * **앱 서비스 계획**
   * **리소스 그룹**
   * **지역**
   * 둡니다 **데이터베이스 서버** 도**데이터베이스가 없습니다.**
5. 다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.
6. 웹 브라우저가 toohello 게시 된 웹 응용 프로그램을 자동으로 열립니다. Hello를 사용 하 여 예상 대로 hello 웹 응용 프로그램 작업을 참조 해야 **SQL** Azure에서 호스팅되는 데이터베이스입니다.

   축하합니다.

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>다음 단계
Visual Studio, Django 및 SQL 데이터베이스에 대 한 Python Tools에 대 한 자세한 이러한 링크 toolearn를 따릅니다.

* [Python Tools for Visual Studio 설명서]
  * [웹 프로젝트]
  * [클라우드 서비스 프로젝트]
  * [Microsoft Azure의 원격 디버깅]
* [Django 설명서]
* [SQL 데이터베이스]

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure 포털]: https://portal.azure.com
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026
[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027
[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 설명서]: https://www.djangoproject.com/
[SQL 데이터베이스]: /documentation/services/sql-database/
