---
title: "Azure 앱 서비스 웹 앱과 Python aaaConfiguring"
description: "이 자습서에서는 Azure 앱 서비스 웹앱에서 기본 WSGI(Web Server Gateway Interface) 규격 Python 응용 프로그램을 제작 및 구성하는 옵션을 설명합니다."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Azure 앱 서비스 웹앱에서 Python 구성
이 자습서에서는 [Azure 앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)에서 기본 WSGI(Web Server Gateway Interface) 규격 Python 응용 프로그램을 제작 및 구성하는 옵션을 설명합니다.

또한 가상 환경 및 requirements.txt를 사용한 패키지 설치 등 Git 배포의 추가 기능에 대해 설명합니다.

## <a name="bottle-django-or-flask"></a>Bottle, Django 또는 Flask
Azure 마켓플레이스 hello hello Bottle, Django 및 플라스 프레임 워크에 대 한 템플릿을 포함합니다. Azure 앱 서비스의 첫 번째 웹 앱을 개발 하는 경우 Git가 포함 된 모르는, Git 배포를 사용 하 여 hello 갤러리에서 응용 프로그램을 구축 하기 위한 단계별 지침을 포함 하는 이러한 자습서 중 하나를 수행 하는 것이 좋습니다. Windows 또는 Mac:

* [Bottle을 사용하여 웹앱 만들기](web-sites-python-create-deploy-bottle-app.md)
* [Django를 사용하여 웹앱 만들기](web-sites-python-create-deploy-django-app.md)
* [Flask를 사용하여 웹앱 만들기](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Azure 포털에서 웹앱 만들기
이 자습서는 기존 Azure 구독 및 액세스 toohello Azure 포털을 가정합니다.

기존 웹 앱이 없는 경우 hello에서 하나를 만들 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.  Hello hello 맨 왼쪽된 위 모퉁이에서 새로 만들기 단추를 클릭 한 다음 클릭 **웹 + 모바일** > **웹 앱**합니다.

## <a name="git-publishing"></a>Git 게시
Hello 지침에 따라 새로 만든된 웹 앱에 대 한 Git 게시를 구성 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다. 이 자습서에서는 Git toocreate, 관리 및 우리의 Python 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.

Git 게시가 설정되면 Git 리포지토리가 생성되고 웹앱과 연결됩니다. hello 리포지토리 URL 표시 되 고 hello 로컬 개발 환경 toohello 클라우드에서 사용 되는 toopush 데이터 수 예측이 있습니다. Git 통해 toopublish 응용 프로그램 사용 하 여 hello 지침은 제공 toopush 실행 하 여 웹 응용 프로그램 콘텐츠 tooAzure 앱 서비스 및 Git 클라이언트도 설치 되어 있는지 확인 합니다.

## <a name="application-overview"></a>응용 프로그램 개요
Hello 다음 섹션의 다음 파일이 hello 생성 됩니다. Hello Git 리포지토리의 루트 hello에에서 있어야 합니다.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>WSGI 처리기
WSGI는에 설명 된 Python 표준 [PEP 3333](http://www.python.org/dev/peps/pep-3333/) hello 웹 서버와 Python 간의 인터페이스를 정의 합니다. WSGI는 Python을 사용하여 다양한 웹 응용 프로그램 및 프레임워크 쓰기에 대해 표준화된 인터페이스를 제공합니다. 오늘날 인기 있는 Python 웹 프레임워크는 WSGI를 사용합니다. Azure 앱 서비스 웹 앱은 이러한 프레임 워크;에 대 한 지원 또한 고급 사용자도 작성할 수 자신의으로 hello 사용자 지정 처리기 hello WSGI 사양 지침을 따릅니다.

다음은 사용자 지정 처리기를 정의하는 `app.py`의 예입니다.

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

이 응용 프로그램을 사용 하 여 로컬로 실행할 수 있습니다 `python app.py`, 다음 너무 탐색`http://localhost:5555` 웹 브라우저에서 합니다.

## <a name="virtual-environment"></a>가상 환경
위의 hello 예제 응용 프로그램에는 모든 외부 패키지 필요 하지 않습니다, 하지만 일부 응용 프로그램 필요 합니다 가능성이 높습니다.

toohelp 외부 패키지 종속성을 관리, Azure Git 배포에서는 가상 환경의 hello 생성을 지원 합니다.

requirements.txt hello 저장소의 hello 루트에서 검색을 자동으로 만들어집니다 라는 가상 환경 `env`합니다. 이 hello 첫 번째 배포에만 발생 하거나 hello 후 배포 하는 동안 선택한 Python 런타임의 변경 되었습니다.

로컬 개발을 위한 가상 환경 toocreate 수도 있지만 Git 리포지토리가에 포함 하지 않습니다.

## <a name="package-management"></a>패키지 관리
Requirements.txt에 나열 된 패키지는 pip를 사용 하 여 hello 가상 환경에서 자동으로 설치 됩니다. 이는 모든 배포에서 발생하지만 패키지가 이미 설치된 경우에는 pip에서 설치를 건너뜁니다.

예제 `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Python 버전
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

예제 `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Web.config 파일 toospecify toocreate 해야 hello 서버에서 요청을 처리 하는 방법입니다.

Note web.x.y.config 파일 x.y와 일치 하는 저장소에 있는 경우 hello Python 런타임의 선택한 다음 Azure는 자동으로 web.config로 hello 적절 한 파일을 복사 합니다.

hello 다음 web.config 예제는 가상 환경 프록시 스크립트 기반의 hello 다음 섹션에 설명 되어 있습니다.  Hello 예에 사용 된 hello WSGI 핸들러와 작동 `app.py` 위에 있습니다.

Python 2.7용 예제 `web.config` :

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Python 3.4용 예제 `web.config` :

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


정적 파일이 처리 되는 hello 웹 서버에서 직접 성능 향상된을 위해 Python 코드를 통하지 않고 합니다.

위의 예제는 hello에서 디스크에 hello 정적 파일의 hello 위치 hello URL에 hello 위치를 일치 해야 합니다. 즉,에 대 한 요청 `http://pythonapp.azurewebsites.net/static/site.css` hello 파일 디스크에 사용 될 `\static\site.css`합니다.

`WSGI_ALT_VIRTUALENV_HANDLER`hello WSGI 처리기를 지정 하는 위치입니다. 예제를 보려면 위에서 hello에 있기 `app.wsgi_app` hello 처리기 라는 함수 이므로 `wsgi_app` 에 `app.py` hello 루트 폴더에 있습니다.

`PYTHONPATH`사용자 지정할 수 있습니다, toochange 필요는 없습니다 requirements.txt에 지정 하 여 hello 가상 환경에서 모든 종속성을 설치 하지만 것입니다.

## <a name="virtual-environment-proxy"></a>가상 환경 프록시
다음 스크립트는 hello 사용 되는 tooretrieve hello WSGI 처리기가 hello 가상 환경 및 로그 오류를 활성화 합니다. 디자인 된 toobe 일반적이 고 수정 하지 않고 사용 되는 경우

`ptvs_virtualenv_proxy.py`의 내용:

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a>Git 배포 사용자 지정
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>문제 해결 - 패키지 설치
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>문제 해결 - 가상 환경
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

