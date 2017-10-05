---
title: "Azure의 Linux 가상 컴퓨터에 LEMP 배포 | Microsoft Docs"
description: "자습서 - Azure에서 Linux VM에 LEMP 스택 설치"
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
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="e0d24-103">Azure VM에 LEMP 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="e0d24-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="e0d24-104">이 문서에서는 Azure의 Ubuntu VM에 NGINX 웹 서버, MySQL 및 PHP(LEMP 스택)를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="e0d24-105">LEMP 스택은 인기 있는 [LAMP 스택](tutorial-lamp-stack.md) 대신 사용할 수 있으며 Azure에도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="e0d24-106">작동 중인 LEMP 서버를 보려면 필요에 따라 WordPress 사이트를 설치하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="e0d24-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0d24-108">Ubuntu VM(LEMP 스택에서 'L') 만들기</span><span class="sxs-lookup"><span data-stu-id="e0d24-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="e0d24-109">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="e0d24-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e0d24-110">NGINX, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="e0d24-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="e0d24-111">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="e0d24-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="e0d24-112">LEMP 서버에 WordPress 설치</span><span class="sxs-lookup"><span data-stu-id="e0d24-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e0d24-113">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e0d24-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="e0d24-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0d24-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="e0d24-116">NGINX, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="e0d24-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="e0d24-117">다음 명령을 실행하여 Ubuntu 패키지 원본을 업데이트하고 NGINX, MySQL 및 PHP를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="e0d24-118">패키지 및 기타 종속성을 설치하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="e0d24-119">메시지가 표시되면 MySQL에 대한 루트 암호를 설정한 다음 [Enter] 키를 눌러 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="e0d24-120">나머지 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-120">Follow the remaining prompts.</span></span> <span data-ttu-id="e0d24-121">이 프로세스에서는 PHP와 MySQL을 함께 사용하는 데 필요한 최소한의 PHP 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![MySQL 루트 암호 페이지][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="e0d24-123">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="e0d24-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="e0d24-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="e0d24-124">NGINX</span></span>

<span data-ttu-id="e0d24-125">다음 명령으로 PHP의 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="e0d24-126">NGINX를 설치하고 VM에 포트 80을 열어서 인터넷에서 웹 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="e0d24-127">NGINX 시작 페이지를 보려면 웹 브라우저를 열고 VM의 공용 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="e0d24-128">VM에 SSH하는 데 사용한 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-128">Use the public IP address you used to SSH to the VM:</span></span>

![NGINX 기본 페이지][3]


### <a name="mysql"></a><span data-ttu-id="e0d24-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="e0d24-130">MySQL</span></span>

<span data-ttu-id="e0d24-131">다음 명령을 사용하여 MySQL의 버전을 확인합니다(대문자 `V` 매개 변수 주의).</span><span class="sxs-lookup"><span data-stu-id="e0d24-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="e0d24-132">MySQL의 설치를 보호하기 위해 다음 스크립트를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="e0d24-133">MySQL 루트 암호를 입력하고 사용자 환경에 대한 보안 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="e0d24-134">MySQL 데이터베이스를 만들려면 사용자를 추가하거나 구성 설정을 변경하고 MySQL에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e0d24-135">완료한 후 `\q`를 입력하여 mysql 프롬프트를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="e0d24-136">PHP</span><span class="sxs-lookup"><span data-stu-id="e0d24-136">PHP</span></span>

<span data-ttu-id="e0d24-137">다음 명령으로 PHP의 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="e0d24-138">PHP-FPM(PHP FastCGI Process Manager)를 사용하도록 NGINX를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="e0d24-139">다음 명령을 실행하여 원래 NGINX 서버 블록 구성 파일을 백업하고 원하는 편집기에 원본 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="e0d24-140">편집기에서 `/etc/nginx/sites-available/default`의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="e0d24-141">설정에 대한 설명을 보려면 주석을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0d24-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="e0d24-142">VM의 공용 IP 주소를 *yourPublicIPAddress*로 바꾸고 나머지 설정은 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="e0d24-143">그런 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-143">Then save the file.</span></span>

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

<span data-ttu-id="e0d24-144">NGINX 구성의 구문 오류를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="e0d24-145">구문이 올바른 경우 다음 명령을 사용하여 NGINX를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="e0d24-146">추가로 테스트하려는 경우 빠른 PHP 정보 페이지를 만들어 브라우저에서 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="e0d24-147">다음 명령은 PHP 정보 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="e0d24-148">이제 만든 PHP 정보 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="e0d24-149">웹 브라우저를 열고 `http://yourPublicIPAddress/info.php`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="e0d24-150">VM의 공용 IP 주소를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="e0d24-151">이 이미지와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-151">It should look similar to this image.</span></span>

![PHP 정보 페이지][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="e0d24-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0d24-153">Next steps</span></span>

<span data-ttu-id="e0d24-154">이 자습서에서는 Azure에서 LEMP 서버를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="e0d24-155">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0d24-156">Ubuntu VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e0d24-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="e0d24-157">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="e0d24-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e0d24-158">NGINX, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="e0d24-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="e0d24-159">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="e0d24-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="e0d24-160">LEMP 스택에 WordPress 설치</span><span class="sxs-lookup"><span data-stu-id="e0d24-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="e0d24-161">SSL 인증서로 웹 서버를 보호하는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d24-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e0d24-162">SSL로 웹 서버 보안</span><span class="sxs-lookup"><span data-stu-id="e0d24-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
