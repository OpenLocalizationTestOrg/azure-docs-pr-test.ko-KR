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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="a22f6-103">Linux VM에서 Django Hello World 웹앱</span><span class="sxs-lookup"><span data-stu-id="a22f6-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a22f6-104">Windows</span><span class="sxs-lookup"><span data-stu-id="a22f6-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="a22f6-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="a22f6-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="a22f6-106">이 자습서에서는 어떻게 toohost Django 기반 웹 사이트에서 Azure 가상 컴퓨터의 Linux.</span><span class="sxs-lookup"><span data-stu-id="a22f6-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="a22f6-107">Hello 자습서에서는 Azure 사용한 이전 경험이 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="a22f6-108">Hello 자습서를 완료 하면를 Django 기반 응용 프로그램 및 hello 클라우드에서 실행 중인를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="a22f6-109">방법 배우기:</span><span class="sxs-lookup"><span data-stu-id="a22f6-109">Learn how to:</span></span>

* <span data-ttu-id="a22f6-110">Azure 가상 컴퓨터 toohost Django 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="a22f6-111">이 자습서에 설명 하지만 방법을 toodo에 대해이 **Linux**를 할 수 있는 Azure에서 호스트 되는 Windows Server VM에 대 한 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="a22f6-112">Linux에서 새 Django 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="a22f6-113">hello 자습서 toobuild 기본 Hello World 웹 응용 프로그램 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="a22f6-114">hello 응용 프로그램이 Azure 가상 컴퓨터에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="a22f6-115">다음 스크린 샷 hello 완료 hello 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-115">hello following screenshot shows hello completed application:</span></span>

![Azure의 hello Hello World 페이지를 표시 하는 브라우저 창](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="a22f6-117">만들고 Azure 가상 컴퓨터 toohost Django 설정</span><span class="sxs-lookup"><span data-stu-id="a22f6-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="a22f6-118">Ubuntu Server 14.04 LTS 배포 hello로 Azure 가상 컴퓨터 toocreate 참조 [hello Azure 포털에서에서 Linux 가상 컴퓨터 만들기](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a22f6-119">SSH 공개 키를 사용하는 대신 암호 인증을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="a22f6-120">tooedit hello 네트워크 보안 그룹 tooallow 들어오는 HTTP 트래픽이 tooport 80, 참조 [hello Azure 포털에서에서 네트워크 보안 그룹을 만든](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="a22f6-121">(선택 사항) 기본적으로 새 가상 컴퓨터에는 FQDN(정규화된 도메인 이름)이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="a22f6-122">FQDN 사용 하 여 VM toocreate 참조 [Windows vm의 FQDN hello Azure 포털에서에서 만들](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a22f6-123">이 단계는 이 자습서를 완료하는 데 필수는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="a22f6-124"><a id="setup"></a>Hello 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="a22f6-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="a22f6-125">Python tooinstall 필요 하거나 toouse hello 클라이언트 라이브러리를 사용할 경우 참조 hello [Python 설치 가이드](../../python-how-to-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="a22f6-126">hello Ubuntu Linux VM을 미리 설치, Python 2.7 갖지만 Apache 또는 Django 함께 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="a22f6-127">다음 단계 tooconnect tooyour VM hello를 완료 하 고 Apache와 Django를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="a22f6-128">새 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="a22f6-129">Azure VM tooconnect toohello hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="a22f6-130">FQDN을 만들지 않은 경우에 hello Azure 포털에서에서 요약 hello 가상 컴퓨터에 표시 되는 hello 공용 IP 주소를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="a22f6-131">tooinstall Django, hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="a22f6-132">mod-wsgi와 Apache tooinstall hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="a22f6-133">새 Django 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a22f6-133">Create a new Django app</span></span>
1. <span data-ttu-id="a22f6-134">toouse SSH tooaccess hello 앞 섹션에서에서 사용한 VM, 터미널 윈도우를 열고 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="a22f6-135">toocreate 새 Django 프로젝트 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="a22f6-136">hello `django-admin.py` Django 기반 웹 사이트에 대 한 기본 구조를 생성 하는 스크립트:</span><span class="sxs-lookup"><span data-stu-id="a22f6-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="a22f6-137">`helloworld/manage.py`는 Django 기반 웹 사이트의 호스팅을 시작 및 중지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="a22f6-138">`helloworld/helloworld/settings.py`에는 응용 프로그램에 대한 Django 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="a22f6-139">`helloworld/helloworld/urls.py`각 URL과 해당 뷰 사이 hello 매핑 코드를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="a22f6-140">Hello /var/www/helloworld/helloworld 디렉터리 views.py 라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="a22f6-141">이 파일에 hello "hello world" 페이지를 렌더링 하는 hello 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="a22f6-142">코드 편집기에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="a22f6-143">명령을 수행 하는 hello hello urls.py 파일의 hello 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="a22f6-144">Apache 설정</span><span class="sxs-lookup"><span data-stu-id="a22f6-144">Set up Apache</span></span>
1. <span data-ttu-id="a22f6-145">Hello /etc/apache2/sites-available/helloworld.conf 폴더에는 Apache 가상 호스트 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="a22f6-146">Hello 내용을 toohello 다음 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="a22f6-147">대체 *yourVmName* hello 사용 하는 hello 컴퓨터의 실제 이름으로 (예를 들어 *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="a22f6-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="a22f6-148">다음 명령을 사용 하 여 hello tooactivate hello 사이트:</span><span class="sxs-lookup"><span data-stu-id="a22f6-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="a22f6-149">Apache toorestart hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="a22f6-150">브라우저에서 hello 웹 페이지를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-150">Load hello webpage in your browser:</span></span>
   
   ![Azure의 hello hello world 페이지를 표시 하는 브라우저 창](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="a22f6-152">Azure 가상 컴퓨터 종료</span><span class="sxs-lookup"><span data-stu-id="a22f6-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="a22f6-153">이 자습서를 완료 하는 경우에 종료 나 hello hello 자습서에 대해 만든 Azure VM을 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="a22f6-154">그러면 다른 자습서에 대한 리소스가 해제되어 Azure 사용량 요금이 발생하는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a22f6-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

