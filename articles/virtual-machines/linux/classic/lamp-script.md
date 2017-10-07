---
title: "aaaUse hello Linux VM의 CustomScript 확장 | Microsoft Docs"
description: "Toouse hello CustomScript 확장 toodeploy 응용 프로그램이 Azure에서 Linux 가상 컴퓨터에 만드는 hello 클래식 배포 모델을 사용 하는 방법에 대해 알아봅니다."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="5e6fa-103">Linux 용 hello Azure CustomScript 확장을 사용 하 여 램프 앱 배포</span><span class="sxs-lookup"><span data-stu-id="5e6fa-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="5e6fa-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5e6fa-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5e6fa-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5e6fa-107">Hello 리소스 관리자 모델을 사용 하 여 LAMP 스택 배포에 대 한 내용은 [여기](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5e6fa-108">Linux 용 Microsoft Azure CustomScript 확장 hello hello (예를 들어 Python 및 Bash)의 VM에서 지 원하는 모든 스크립팅 언어로 작성 된 임의의 코드를 실행 하 여 방식으로 toocustomize 가상 컴퓨터 (Vm)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="5e6fa-109">응용 프로그램 배포 toomultiple 컴퓨터 매우 융통성 있게 tooautomate을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="5e6fa-110">Hello CustomScript 확장을 배포 하려면 Azure 포털, Windows PowerShell 또는 Azure CLI (명령줄 인터페이스 Azure) hello hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="5e6fa-111">이 문서에서는 hello Azure CLI toodeploy 간단한 램프 응용 프로그램 tooan Ubuntu VM hello 클래식 배포 모델을 사용 하 여 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e6fa-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5e6fa-112">Prerequisites</span></span>
<span data-ttu-id="5e6fa-113">이 예제에서는 먼저 Ubuntu 14.04 이상을 실행하는 두 개의 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="5e6fa-114">hello Vm 라고 *스크립트 vm* 및 *램프 vm*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="5e6fa-115">Hello Vm을 만들 때 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="5e6fa-116">하나는 사용 되는 toorun hello CLI 명령을 고 하나는 사용 되는 toodeploy hello 램프 앱.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="5e6fa-117">또한 해야 Azure 저장소 계정 및 키 tooaccess it (에서 얻을 수 있습니다이 hello Azure 포털).</span><span class="sxs-lookup"><span data-stu-id="5e6fa-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="5e6fa-118">Azure에서 Linux Vm을 만드는 데 도움이 필요한 경우 너무 참조[만들 가상 컴퓨터 실행 중인 Linux](createportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="5e6fa-119">hello 설치 명령은 Ubuntu, 가정 하지만 지원 되는 모든 Linux 배포판에 대 한 hello 설치를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="5e6fa-120">hello 스크립트 vm VM 필요 toohave 작업 연결 tooAzure와 함께 Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="5e6fa-121">에 대 한 도움말은이 너무 참조[설치 및 구성 hello Azure 명령줄 인터페이스](../../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="5e6fa-122">스크립트 업로드</span><span class="sxs-lookup"><span data-stu-id="5e6fa-122">Upload a script</span></span>
<span data-ttu-id="5e6fa-123">원격 VM tooinstall hello LAMP 스택 hello CustomScript 확장 toorun 스크립트를 사용 하 여 알아보고 PHP 페이지를 만들 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="5e6fa-124">어디에서 든 순서 tooaccess hello 스크립트에서 Azure blob으로 업로드 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="5e6fa-125">스크립트 개요</span><span class="sxs-lookup"><span data-stu-id="5e6fa-125">Script overview</span></span>
<span data-ttu-id="5e6fa-126">hello 스크립트 예제는 LAMP 스택 tooUbuntu (MySQL의 자동 설치를 설정 하는 등)를 설치 하 고, 간단한 PHP 파일을 작성, Apache 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="5e6fa-127">스크립트 업로드</span><span class="sxs-lookup"><span data-stu-id="5e6fa-127">Upload script</span></span>
<span data-ttu-id="5e6fa-128">예를 들어 hello 스크립트를 텍스트 파일로 저장 *install_lamp.sh*를 다음 저장소 tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="5e6fa-129">Azure CLI를 사용하면 이 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="5e6fa-130">hello 다음 예제에서는 업로드 hello 파일 tooa 저장소 컨테이너 이름이 "스크립트" 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="5e6fa-131">Toocreate 해야 hello 컨테이너 존재 하지 않는 경우 그 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="5e6fa-132">Toodownload Azure 저장소에서 스크립트를 hello 하는 방법을 설명 하는 JSON 파일을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="5e6fa-133">으로 저장할 *public_config.json* ("mystorage" hello 저장소 계정의 이름으로 대체):</span><span class="sxs-lookup"><span data-stu-id="5e6fa-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="5e6fa-134">Hello 확장 배포</span><span class="sxs-lookup"><span data-stu-id="5e6fa-134">Deploy hello extension</span></span>
<span data-ttu-id="5e6fa-135">Hello 다음 명령 toodeploy hello Linux CustomScript 확장 toohello 원격에서는 이제 Azure CLI hello 사용 하 여 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="5e6fa-136">이전 명령은 hello 다운로드 하 고 hello 실행 *install_lamp.sh* hello 라는 VM에서 스크립트 *램프 vm*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="5e6fa-137">웹 서버를 포함 하는 hello 앱, 이후 기억 hello에 수신 대기 포트는 HTTP tooopen hello 다음 명령 사용 하 여 원격 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="5e6fa-138">모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5e6fa-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="5e6fa-139">얼마나 잘 hello 로그 파일 확인 하 여 사용자 지정 스크립트 실행 hello hello 원격 VM을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="5e6fa-140">SSH 너무*램프 vm* 및 hello 다음 명령 사용 하 여 비상 hello 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="5e6fa-141">Hello CustomScript 확장을 실행 한 후에 정보에 대해 만든 toohello PHP 페이지를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="5e6fa-142">이 문서의 hello 예제는 hello PHP 페이지 *http://lamp-vm.cloudapp.net/phpinfo.php*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e6fa-143">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5e6fa-143">Additional resources</span></span>
<span data-ttu-id="5e6fa-144">에서는 동일한 기본 단계 toodeploy hello 더 복잡 한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="5e6fa-145">이 예에서 hello 설치 스크립트는 Azure 저장소에 공개 blob으로 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="5e6fa-146">보다 안전한 옵션을 사용 하 여 보안 blob toostore hello 설치 스크립트 됩니다는 [보안 액세스 서명](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="5e6fa-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="5e6fa-147">Azure CLI, Linux 및 hello CustomScript 확장을 위한 추가 리소스는 다음에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6fa-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="5e6fa-148">CustomScript 확장을 사용하여 Linux VM 사용자 지정 작업 자동화</span><span class="sxs-lookup"><span data-stu-id="5e6fa-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="5e6fa-149">Azure Linux 확장(GitHub)</span><span class="sxs-lookup"><span data-stu-id="5e6fa-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)