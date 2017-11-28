---
title: "Azure에서 Linux 가상 컴퓨터에서 LEMP aaaDeploy | Microsoft Docs"
description: "자습서-Azure에서 Linux VM에 대 한 설치 hello LEMP 스택"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="3f8f6-103">Azure VM에 LEMP 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="3f8f6-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="3f8f6-104">이 문서 toodeploy는 NGINX 웹 서버, MySQL 및 Azure의 Ubuntu VM에서 PHP (hello LEMP 스택) 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="3f8f6-105">hello LEMP 스택은 널리 사용 되는 대체 toohello [LAMP 스택](tutorial-lamp-stack.md)는 Azure에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="3f8f6-106">toosee hello LEMP 서버 작업을 필요에 따라 설치 하 고 수 WordPress 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="3f8f6-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f8f6-108">Ubuntu VM (hello 'L' hello LEMP 스택의) 만들기</span><span class="sxs-lookup"><span data-stu-id="3f8f6-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="3f8f6-109">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="3f8f6-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="3f8f6-110">NGINX, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="3f8f6-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="3f8f6-111">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="3f8f6-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="3f8f6-112">WordPress hello LEMP 서버에 설치</span><span class="sxs-lookup"><span data-stu-id="3f8f6-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3f8f6-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3f8f6-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3f8f6-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="3f8f6-116">NGINX, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="3f8f6-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="3f8f6-117">Hello 명령 tooupdate Ubuntu 패키지 원본 실행 NGINX, MySQL 및 PHP를 설치 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="3f8f6-118">모르는 증명된 tooinstall hello 패키지 및 기타 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="3f8f6-119">메시지가 표시 되 면 MySQL을 선택한 다음 [Enter] toocontinue 루트 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="3f8f6-120">Hello 남아 있는 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="3f8f6-121">이 프로세스는 MySQL 가진 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![MySQL 루트 암호 페이지][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="3f8f6-123">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="3f8f6-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="3f8f6-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="3f8f6-124">NGINX</span></span>

<span data-ttu-id="3f8f6-125">다음 명령을 hello로 NGINX의 hello 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="3f8f6-126">NGINX 설치 되어 있으며 포트 80 엽니다 tooyour VM hello 웹 서버 hello에서 액세스할 수 있습니다, 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="3f8f6-127">tooview hello NGINX 시작 페이지에서 웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="3f8f6-128">Hello tooSSH toohello VM을 사용 하는 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![NGINX 기본 페이지][3]


### <a name="mysql"></a><span data-ttu-id="3f8f6-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="3f8f6-130">MySQL</span></span>

<span data-ttu-id="3f8f6-131">다음 명령을 hello로 MySQL의 hello 버전을 확인 (참고 hello 자본 `V` 매개 변수):</span><span class="sxs-lookup"><span data-stu-id="3f8f6-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="3f8f6-132">Hello MySQL의 toohelp 보안 hello 설치 스크립트를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="3f8f6-133">MySQL 루트 암호를 입력 하 고 사용자 환경에 대 한 hello 보안 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="3f8f6-134">Toocreate MySQL 데이터베이스 사용자를 추가 하거나 로그인 tooMySQL 구성 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="3f8f6-135">을 완료 한 후를 입력 하 여 hello mysql 프롬프트를 종료 `\q`합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="3f8f6-136">PHP</span><span class="sxs-lookup"><span data-stu-id="3f8f6-136">PHP</span></span>

<span data-ttu-id="3f8f6-137">다음 명령을 hello로 hello PHP 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="3f8f6-138">NGINX toouse hello PHP FastCGI 프로세스 관리자 (PHP FPM)를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="3f8f6-139">다음 명령은 tooback hello 원래 NGINX 서버를 구성 파일을 차단 하 고 다음 hello 원하는 편집기에 원본 파일을 편집 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="3f8f6-140">Hello 편집기에서의 hello 내용을 대체 `/etc/nginx/sites-available/default` hello 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="3f8f6-141">에 대 한 설명은 hello 설정의 hello 주석을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="3f8f6-142">Hello에 대 한 VM의 공용 IP 주소 대체 *yourPublicIPAddress*, hello 남은 설정을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="3f8f6-143">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-143">Then save hello file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="3f8f6-144">구문 오류에 대 한 hello NGINX 구성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="3f8f6-145">Hello 구문이 올바른 경우 다음 명령을 hello로 NGINX 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="3f8f6-146">Tootest 추가 하려는 경우 브라우저에서 빠른 PHP 정보 페이지 tooview를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="3f8f6-147">다음 명령을 hello hello PHP 정보 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="3f8f6-148">이제 만든 hello PHP 정보 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="3f8f6-149">브라우저를 열고 너무 이동`http://yourPublicIPAddress/info.php`합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="3f8f6-150">VM의 hello 공용 IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="3f8f6-151">이와 유사한 toothis 이미지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-151">It should look similar toothis image.</span></span>

![PHP 정보 페이지][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="3f8f6-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f8f6-153">Next steps</span></span>

<span data-ttu-id="3f8f6-154">이 자습서에서는 Azure에서 LEMP 서버를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="3f8f6-155">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f8f6-156">Ubuntu VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3f8f6-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="3f8f6-157">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="3f8f6-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="3f8f6-158">NGINX, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="3f8f6-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="3f8f6-159">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="3f8f6-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="3f8f6-160">Hello LEMP 스택에 WordPress 설치</span><span class="sxs-lookup"><span data-stu-id="3f8f6-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="3f8f6-161">다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8f6-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f8f6-162">SSL로 웹 서버 보안</span><span class="sxs-lookup"><span data-stu-id="3f8f6-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
