---
title: "Azure Linux VM에서 Django를 사용하는 Python 웹앱 | Microsoft Docs"
description: "Azure에서 Linux VM을 사용하여 Django 기반 웹앱을 호스트하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="fcd57-103">Linux VM에서 Django Hello World 웹앱</span><span class="sxs-lookup"><span data-stu-id="fcd57-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcd57-104">Windows</span><span class="sxs-lookup"><span data-stu-id="fcd57-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="fcd57-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="fcd57-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="fcd57-106">이 자습서는 Azure Virtual Machines의 Linux에서 Django 기반 웹 사이트를 호스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="fcd57-107">이 자습서에서는 사전에 Azure 경험이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="fcd57-108">이 자습서를 완료하면 클라우드에서 Django 기반 응용 프로그램을 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="fcd57-109">방법 배우기:</span><span class="sxs-lookup"><span data-stu-id="fcd57-109">Learn how to:</span></span>

* <span data-ttu-id="fcd57-110">Django를 호스트하도록 Azure 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="fcd57-111">이 자습서에서는 **Linux**에서 작업을 수행하는 방법을 설명하지만, Azure에서 호스트되는 Windows Server VM에 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="fcd57-112">Linux에서 새 Django 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="fcd57-113">자습서는 기본적인 Hello World 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="fcd57-114">응용 프로그램은 Azure 가상 컴퓨터에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="fcd57-115">다음 스크린샷에 완성된 응용 프로그램이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-115">The following screenshot shows the completed application:</span></span>

![Azure의 Hello World 페이지가 표시된 브라우저 창](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="fcd57-117">Django를 호스트하기 위해 Azure 가상 컴퓨터 만들기 및 설정</span><span class="sxs-lookup"><span data-stu-id="fcd57-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="fcd57-118">Ubuntu Server 14.04 LTS 배포를 사용하여 Azure 가상 컴퓨터를 만들려면 참조 [Azure Portal에서 Linux 가상 컴퓨터 만들기](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcd57-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="fcd57-119">SSH 공개 키를 사용하는 대신 암호 인증을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="fcd57-120">포트 80에 들어오는 HTTP 트래픽을 허용하도록 네트워크 보안 그룹을 편집하려면 [Azure Portal에서 네트워크 보안 그룹 만들기](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcd57-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="fcd57-121">(선택 사항) 기본적으로 새 가상 컴퓨터에는 FQDN(정규화된 도메인 이름)이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="fcd57-122">FQDN을 사용하여 VM을 만들려면 [Windows VM에 대 한 Azure Portal의 FQDN을 만들기](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcd57-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="fcd57-123">이 단계는 이 자습서를 완료하는 데 필수는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="fcd57-124"><a id="setup"> </a>개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="fcd57-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="fcd57-125">Python을 설치해야 하거나 클라이언트 라이브러리를 사용하고 싶으면 [Python 설치 가이드](../../python-how-to-install.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcd57-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="fcd57-126">Ubuntu Linux VM에는 Python 2.7이 미리 설치되어 있지만 Apache 또는 Django를 제공하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="fcd57-127">다음 단계를 완료하여 VM에 연결하고 Apache 및 Django를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="fcd57-128">새 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="fcd57-129">Azure VM에 연결하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="fcd57-130">FQDN을 만들지 않은 경우 Azure Portal의 가상 컴퓨터 요약에 표시되는 공용 IP 주소를 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="fcd57-131">Django를 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="fcd57-132">Apache를 mod-wsgi와 함께 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="fcd57-133">새 Django 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fcd57-133">Create a new Django app</span></span>
1. <span data-ttu-id="fcd57-134">SSH를 사용하여 VM에 액세스하려면 이전 섹션에서 사용한 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="fcd57-135">새 Django 프로젝트를 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="fcd57-136">`django-admin.py` 스크립트는 Django 기반 웹 사이트의 기본 구조를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="fcd57-137">`helloworld/manage.py`는 Django 기반 웹 사이트의 호스팅을 시작 및 중지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="fcd57-138">`helloworld/helloworld/settings.py`에는 응용 프로그램에 대한 Django 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="fcd57-139">`helloworld/helloworld/urls.py`에는 각 URL과 뷰 사이 매핑 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="fcd57-140">/var/www/helloworld/helloworld 디렉터리에서 views.py라는 이름의 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="fcd57-141">이 파일에는 “hello world” 페이지를 렌더링하는 뷰가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="fcd57-142">코드 편집기에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="fcd57-143">urls.py 파일의 콘텐츠를 다음 명령으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="fcd57-144">Apache 설정</span><span class="sxs-lookup"><span data-stu-id="fcd57-144">Set up Apache</span></span>
1. <span data-ttu-id="fcd57-145">/etc/apache2/sites-available/helloworld.conf 폴더에서 Apache 가상 호스트 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="fcd57-146">콘텐츠를 다음 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-146">Set the contents to the following values.</span></span> <span data-ttu-id="fcd57-147">*yourVmName*을 현재 사용 중인 컴퓨터의 실제 이름(예: *pyubuntu*)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="fcd57-148">사이트를 활성화하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="fcd57-149">Apache를 다시 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="fcd57-150">브라우저에서 웹 페이지를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-150">Load the webpage in your browser:</span></span>
   
   ![Azure의 hello world 페이지가 표시된 브라우저 창](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="fcd57-152">Azure 가상 컴퓨터 종료</span><span class="sxs-lookup"><span data-stu-id="fcd57-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="fcd57-153">이 자습서를 완료하면 자습서용으로 만든 Azure VM을 종료하거나 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="fcd57-154">그러면 다른 자습서에 대한 리소스가 해제되어 Azure 사용량 요금이 발생하는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcd57-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

