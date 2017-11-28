---
title: "Azure에서 Linux 가상 컴퓨터에서 램프 aaaDeploy | Microsoft Docs"
description: "자습서-Azure에서 Linux VM에 대 한 설치 hello LAMP 스택"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="3bff0-103">Azure VM에 LAMP 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="3bff0-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="3bff0-104">이 문서 toodeploy는 Apache 웹 서버, MySQL 및 Azure의 Ubuntu VM에서 PHP (hello LAMP 스택) 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="3bff0-105">Hello NGINX 웹 서버를 선호 하는 경우 참조 hello [LEMP 스택](tutorial-lemp-stack.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="3bff0-106">toosee hello 램프 서버 작업을 필요에 따라 설치 하 고 수 WordPress 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="3bff0-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3bff0-108">Ubuntu VM (hello LAMP 스택 hello 'L') 만들기</span><span class="sxs-lookup"><span data-stu-id="3bff0-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="3bff0-109">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="3bff0-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="3bff0-110">Apache, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="3bff0-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="3bff0-111">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="3bff0-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="3bff0-112">WordPress hello 램프 서버에 설치</span><span class="sxs-lookup"><span data-stu-id="3bff0-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="3bff0-113">Hello LAMP 스택, 프로덕션 환경에 대 한 권장 사항을 비롯 한 자세한 내용은 hello [Ubuntu 설명서](https://help.ubuntu.com/community/ApacheMySQLPHP)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3bff0-114">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="3bff0-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3bff0-115">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3bff0-116">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="3bff0-117">Apache, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="3bff0-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="3bff0-118">명령 tooupdate Ubuntu 패키지 원본 hello를 실행 하 고 Apache, MySQL 및 PHP를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="3bff0-119">Note hello hello 명령 끝에 hello 캐럿 (^).</span><span class="sxs-lookup"><span data-stu-id="3bff0-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="3bff0-120">모르는 증명된 tooinstall hello 패키지 및 기타 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="3bff0-121">메시지가 표시 되 면 MySQL을 선택한 다음 [Enter] toocontinue 루트 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="3bff0-122">Hello 남아 있는 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="3bff0-123">이 프로세스는 MySQL 가진 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![MySQL 루트 암호 페이지][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="3bff0-125">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="3bff0-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="3bff0-126">Apache</span><span class="sxs-lookup"><span data-stu-id="3bff0-126">Apache</span></span>

<span data-ttu-id="3bff0-127">다음 명령을 hello로 Apache의 hello 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="3bff0-128">설치 되어 있으며 포트 80 apache tooyour VM을 열고, hello에서 이제 hello 웹 서버에 액세스할 수 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="3bff0-129">tooview hello Apache2 Ubuntu 기본 페이지에서 웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="3bff0-130">Hello tooSSH toohello VM을 사용 하는 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Apache 기본 페이지][3]


### <a name="mysql"></a><span data-ttu-id="3bff0-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="3bff0-132">MySQL</span></span>

<span data-ttu-id="3bff0-133">다음 명령을 hello로 MySQL의 hello 버전을 확인 (참고 hello 자본 `V` 매개 변수):</span><span class="sxs-lookup"><span data-stu-id="3bff0-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="3bff0-134">Hello MySQL의 toohelp 보안 hello 설치 스크립트를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="3bff0-135">MySQL 루트 암호를 입력 하 고 사용자 환경에 대 한 hello 보안 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="3bff0-136">Toocreate MySQL 데이터베이스 사용자를 추가 하거나 로그인 tooMySQL 구성 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="3bff0-137">을 완료 한 후를 입력 하 여 hello mysql 프롬프트를 종료 `\q`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="3bff0-138">PHP</span><span class="sxs-lookup"><span data-stu-id="3bff0-138">PHP</span></span>

<span data-ttu-id="3bff0-139">다음 명령을 hello로 hello PHP 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="3bff0-140">Tootest 추가 하려는 경우 브라우저에서 빠른 PHP 정보 페이지 tooview를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="3bff0-141">다음 명령을 hello hello PHP 정보 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="3bff0-142">이제 만든 hello PHP 정보 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="3bff0-143">브라우저를 열고 너무 이동`http://yourPublicIPAddress/info.php`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="3bff0-144">VM의 hello 공용 IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="3bff0-145">이와 유사한 toothis 이미지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-145">It should look similar toothis image.</span></span>

![PHP 정보 페이지][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="3bff0-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3bff0-147">Next steps</span></span>

<span data-ttu-id="3bff0-148">이 자습서에서는 Azure에서 램프 서버를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="3bff0-149">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3bff0-150">Ubuntu VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3bff0-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="3bff0-151">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="3bff0-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="3bff0-152">Apache, MySQL 및 PHP 설치</span><span class="sxs-lookup"><span data-stu-id="3bff0-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="3bff0-153">설치 및 구성 확인</span><span class="sxs-lookup"><span data-stu-id="3bff0-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="3bff0-154">WordPress hello 램프 서버에 설치</span><span class="sxs-lookup"><span data-stu-id="3bff0-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="3bff0-155">다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bff0-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3bff0-156">SSL로 웹 서버 보안</span><span class="sxs-lookup"><span data-stu-id="3bff0-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png