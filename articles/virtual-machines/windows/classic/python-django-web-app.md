---
title: "Windows Server Azure VM에서 웹 앱 aaaDjango | Microsoft Docs"
description: "자세한 내용은 방법 toohost hello 클래식 배포 모델에는 Windows Server 2012 R2 Datacenter VM을 사용 하 여 Azure에서 Django 기반 웹 사이트입니다."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Windows Server VM의 Django Hello World 웹앱

> [!IMPORTANT] 
> Azure는 만들고 리소스를 사용 하기 위한 두 가지 서로 다른 배포 모델이: [Azure 리소스 관리자 및 hello 클래식 배포 모델](../../../resource-manager-deployment-model.md)합니다. 이 문서에서는 hello 클래식 배포 모델을 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

이 자습서에서는 Azure 가상 컴퓨터의 Windows Server에서 Django 기반 웹 사이트 toohost 합니다. Hello 자습서에서는 Azure 사용한 이전 경험이 가정합니다. Hello 자습서를 완료 하면를 Django 기반 응용 프로그램 및 hello 클라우드에서 실행 중인를 가질 수 있습니다.

방법 배우기:

* Azure 가상 컴퓨터 toohost Django 설정 합니다. 이 자습서에 설명 하지만 방법을 toodo에 대해이 **Windows Server**를 할 수 있는 Azure에서 호스트 되는 Linux VM에 대해 동일한 hello 합니다.
* Windows에서 새 Django 응용 프로그램을 만듭니다.

hello 자습서 toobuild 기본 Hello World 웹 응용 프로그램 하는 방법을 보여 줍니다. hello 응용 프로그램이 Azure 가상 컴퓨터에서 호스팅됩니다.

다음 스크린 샷 hello 완료 hello 응용 프로그램을 보여 줍니다.

![Azure의 hello hello world 페이지를 표시 하는 브라우저 창][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>만들고 Azure 가상 컴퓨터 toohost Django 설정

1. Azure 가상 컴퓨터를 Windows Server 2012 R2 Datacenter 배포 hello로 toocreate 참조 [hello Azure 포털에서에서 Windows를 실행 중인 가상 컴퓨터를 만드는](tutorial.md)합니다.
2. Hello 웹 tooport 80 hello 가상 컴퓨터에서 Azure toodirect 포트 80 트래픽을 설정 합니다.
   
   1. Hello Azure 포털에서에서 toohello 대시보드를 이동 하 고 새로 만든된 가상 컴퓨터를 선택 합니다.
   2. **끝점**을 클릭한 후 **추가**를 클릭합니다.

     ![끝점 추가](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. Hello에 **끝점 추가** 페이지에 대 한 **이름**, 입력 **HTTP**합니다. Hello 공용 및 개인 TCP 포트를 너무 설정**80**합니다.

     ![이름을 입력하고 공용 및 개인 포트를 설정](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. **확인**을 클릭합니다.
     
3. Hello 대시보드에서 VM을 선택 합니다. Azure 가상 컴퓨터를 새로 만든 toohello 로그인 프로토콜 RDP (원격 데스크톱) tooremotely toouse 클릭 **연결**합니다.  

> [!IMPORTANT] 
> hello 지침에 따라 사용자가 등록 toohello 가상 컴퓨터에 올바르게 가정 합니다. 또한 hello 가상 컴퓨터에 로컬 컴퓨터에 없는 명령을 수행 하는 가정 합니다.

## <a id="setup"> </a>Python, Django 및 WFastCGI 설치
> [!NOTE]
> Internet Explorer를 사용 하 여 toodownload, Internet Explorer tooconfigure 있을 수 있습니다 **보안 강화 구성** 설정 합니다. toodo이를 클릭 하이 여 **시작** > **관리 도구** > **서버 관리자** > **로컬서버**. **IE 보안 강화 구성**을 클릭한 후 **끄기**를 선택합니다.

1. Hello 최신 버전의 Python 2.7 또는에서 Python 3.4 설치 [python.org][python.org]합니다.
2. Pip를 사용 하 여 hello wfastcgi 및 django 패키지를 설치 합니다.
   
    Python 2.7 hello 다음 명령을 사용 합니다.
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Python 3.4 hello 다음 명령을 사용 합니다.
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>FastCGI를 포함하는 IIS 설치
* FastCGI 지원을 통해 IIS(인터넷 정보 서비스)를 설치합니다. 몇 분 tooexecute를 걸릴 수 있습니다.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>새 Django 응용 프로그램 만들기
1. C:\inetpub\wwwroot, 새 Django 프로젝트 toocreate hello 다음 명령을 입력 합니다.
   
   Python 2.7 hello 다음 명령을 사용 합니다.
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Python 3.4 hello 다음 명령을 사용 합니다.
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![hello New-azureservice 명령의 hello 결과](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. hello `django-admin` 명령은 Django 기반 웹 사이트에 대 한 기본 구조를 생성 합니다.
   
   * `helloworld\manage.py`는 Django 기반 웹 사이트의 호스팅을 시작 및 중지하는 데 도움이 됩니다.
   * `helloworld\helloworld\settings.py`에는 응용 프로그램에 대한 Django 설정이 있습니다.
   * `helloworld\helloworld\urls.py`각 URL과 해당 뷰 사이 hello 매핑 코드를 있습니다.
3. Hello C:\inetpub\wwwroot\helloworld\helloworld 디렉터리 views.py 라는 새 파일을 만듭니다. 이 파일에 hello "hello world" 페이지를 렌더링 하는 hello 보기가 있습니다. 코드 편집기에서 다음 명령을 hello를 입력 합니다.
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. 명령을 수행 하는 hello hello urls.py 파일의 hello 내용을 바꿉니다.
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>IIS 설정
1. Hello 글로벌 applicationhost.config 파일에 hello 처리기 섹션의 잠금을 해제 합니다.  따라서 web.config 파일 toouse hello Python 처리기가 있습니다. 다음 명령을 추가합니다.
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. WFastCGI를 활성화합니다. 이 응용 프로그램 toohello 글로벌 applicationhost.config 파일을 tooyour Python 인터프리터 실행 파일 및 hello wfastcgi.py 스크립트 참조를 추가 합니다.
   
    Python 2.7에서:
   
        C:\python27\scripts\wfastcgi-enable
   
    Python 3.4에서:
   
        C:\python34\scripts\wfastcgi-enable
3. C:\inetpub\wwwroot\helloworld에서 web.config 파일을 만듭니다. 값의 hello hello `scriptProcessor` 특성 hello 출력 hello 단계 앞에서 일치 해야 합니다. Hello wfastcgi 설정에 대 한 자세한 내용은 참조 [pypi wfastcgi][wfastcgi]합니다.
   
   Python 2.7에서:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   Python 3.4에서:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. Hello IIS 기본 웹 사이트 toopoint toohello Django 프로젝트 폴더의 hello 위치를 업데이트 합니다.
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. 브라우저에서 hello 웹 페이지를 로드 합니다.

![Azure의 hello hello world 페이지를 표시 하는 브라우저 창][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Azure 가상 컴퓨터 종료
이 자습서를 완료 하는 경우에 종료 나 hello hello 자습서에 대해 만든 Azure VM을 제거 하는 것이 좋습니다. 그러면 다른 자습서에 대한 리소스가 해제되어 Azure 사용량 요금이 발생하는 것을 방지할 수 있습니다.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
