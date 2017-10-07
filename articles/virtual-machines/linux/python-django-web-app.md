---
title: "Django Azure Linux VM에서 웹 앱 aaaPython | Microsoft Docs"
description: "Django 기반 a toohost Linux VM을 사용 하 여 Azure에서 응용 프로그램 웹 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Linux VM에서 Django Hello World 웹앱
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

이 자습서에서는 어떻게 toohost Django 기반 웹 사이트에서 Azure 가상 컴퓨터의 Linux. Hello 자습서에서는 Azure 사용한 이전 경험이 가정합니다. Hello 자습서를 완료 하면를 Django 기반 응용 프로그램 및 hello 클라우드에서 실행 중인를 가질 수 있습니다.

방법 배우기:

* Azure 가상 컴퓨터 toohost Django 설정 합니다. 이 자습서에 설명 하지만 방법을 toodo에 대해이 **Linux**를 할 수 있는 Azure에서 호스트 되는 Windows Server VM에 대 한 hello 동일 합니다. 
* Linux에서 새 Django 응용 프로그램을 만듭니다.

hello 자습서 toobuild 기본 Hello World 웹 응용 프로그램 하는 방법을 보여 줍니다. hello 응용 프로그램이 Azure 가상 컴퓨터에서 호스팅됩니다.

다음 스크린 샷 hello 완료 hello 응용 프로그램을 보여 줍니다.

![Azure의 hello Hello World 페이지를 표시 하는 브라우저 창](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>만들고 Azure 가상 컴퓨터 toohost Django 설정

1. Ubuntu Server 14.04 LTS 배포 hello로 Azure 가상 컴퓨터 toocreate 참조 [hello Azure 포털에서에서 Linux 가상 컴퓨터 만들기](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. SSH 공개 키를 사용하는 대신 암호 인증을 선택할 수도 있습니다.
2. tooedit hello 네트워크 보안 그룹 tooallow 들어오는 HTTP 트래픽이 tooport 80, 참조 [hello Azure 포털에서에서 네트워크 보안 그룹을 만든](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md)합니다.
3. (선택 사항) 기본적으로 새 가상 컴퓨터에는 FQDN(정규화된 도메인 이름)이 없습니다.  FQDN 사용 하 여 VM toocreate 참조 [Windows vm의 FQDN hello Azure 포털에서에서 만들](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 이 단계는 이 자습서를 완료하는 데 필수는 아닙니다.

## <a id="setup"></a>Hello 개발 환경 설정
> [!NOTE]
> Python tooinstall 필요 하거나 toouse hello 클라이언트 라이브러리를 사용할 경우 참조 hello [Python 설치 가이드](../../python-how-to-install.md)합니다.

hello Ubuntu Linux VM을 미리 설치, Python 2.7 갖지만 Apache 또는 Django 함께 제공 하지 않습니다. 다음 단계 tooconnect tooyour VM hello를 완료 하 고 Apache와 Django를 설치 합니다.

1. 새 터미널 창을 엽니다.
2. Azure VM tooconnect toohello hello 다음 명령을 입력 합니다. FQDN을 만들지 않은 경우에 hello Azure 포털에서에서 요약 hello 가상 컴퓨터에 표시 되는 hello 공용 IP 주소를 사용 하 여 연결할 수 있습니다.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, hello 다음 명령을 입력 합니다.
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. mod-wsgi와 Apache tooinstall hello 다음 명령을 입력 합니다.
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>새 Django 앱 만들기
1. toouse SSH tooaccess hello 앞 섹션에서에서 사용한 VM, 터미널 윈도우를 열고 hello 합니다.
2. toocreate 새 Django 프로젝트 hello 다음 명령을 입력 합니다.
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   hello `django-admin.py` Django 기반 웹 사이트에 대 한 기본 구조를 생성 하는 스크립트:
   
   * `helloworld/manage.py`는 Django 기반 웹 사이트의 호스팅을 시작 및 중지하는 데 도움이 됩니다.
   * `helloworld/helloworld/settings.py`에는 응용 프로그램에 대한 Django 설정이 있습니다.
   * `helloworld/helloworld/urls.py`각 URL과 해당 뷰 사이 hello 매핑 코드를 있습니다.
3. Hello /var/www/helloworld/helloworld 디렉터리 views.py 라는 새 파일을 만듭니다. 이 파일에 hello "hello world" 페이지를 렌더링 하는 hello 보기가 있습니다. 코드 편집기에서 다음 명령을 hello를 입력 합니다.
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. 명령을 수행 하는 hello hello urls.py 파일의 hello 내용을 바꿉니다.
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Apache 설정
1. Hello /etc/apache2/sites-available/helloworld.conf 폴더에는 Apache 가상 호스트 구성 파일을 만듭니다. Hello 내용을 toohello 다음 값을 설정 합니다. 대체 *yourVmName* hello 사용 하는 hello 컴퓨터의 실제 이름으로 (예를 들어 *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. 다음 명령을 사용 하 여 hello tooactivate hello 사이트:
   
       $ sudo a2ensite helloworld
3. Apache toorestart hello 다음 명령을 사용 합니다.
   
       $ sudo service apache2 reload
4. 브라우저에서 hello 웹 페이지를 로드 합니다.
   
   ![Azure의 hello hello world 페이지를 표시 하는 브라우저 창](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Azure 가상 컴퓨터 종료
이 자습서를 완료 하는 경우에 종료 나 hello hello 자습서에 대해 만든 Azure VM을 제거 하는 것이 좋습니다. 그러면 다른 자습서에 대한 리소스가 해제되어 Azure 사용량 요금이 발생하는 것을 방지할 수 있습니다.

