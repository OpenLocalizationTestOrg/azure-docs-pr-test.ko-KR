---
title: "Linux VM에서 CustomScript 확장 사용 | Microsoft Docs"
description: "CustomScript 확장을 사용하여 클래식 배포 모델로 만든 Azure의 Linux 가상 컴퓨터에 응용 프로그램을 배포하는 방법을 알아봅니다."
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
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="90a72-103">Linux용 Azure CustomScript 확장을 사용하여 LAMP 앱 배포</span><span class="sxs-lookup"><span data-stu-id="90a72-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="90a72-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="90a72-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="90a72-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="90a72-107">Resource Manager 모델을 사용하여 LAMP 스택을 배포하는 방법에 대한 정보는 [여기](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90a72-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="90a72-108">Linux용 Microsoft Azure CustomScript 확장을 사용하면 Python 및 Bash와 같은 VM에서 지원하는 모든 스크립팅 언어로 작성된 임의 코드를 실행하여 VM(가상 컴퓨터)을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="90a72-109">이렇게 하면 매우 유동적으로 응용 프로그램을 여러 컴퓨터에 자동으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="90a72-110">Azure Portal, Windows PowerShell 또는 Azure CLI(Azure 명령줄 인터페이스)를 사용하여 CustomScript 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="90a72-111">이 문서에서는 Azure CLI를 사용하여 클래식 배포 모델로 만든 Ubuntu VM에 간단한 LAMP 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90a72-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="90a72-112">Prerequisites</span></span>
<span data-ttu-id="90a72-113">이 예제에서는 먼저 Ubuntu 14.04 이상을 실행하는 두 개의 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="90a72-114">VM의 이름은 *script-vm* 및 *lamp-vm*입니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="90a72-115">VM을 만드는 경우 고유한 이름을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="90a72-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="90a72-116">하나는 CLI 명령을 실행하고 다른 하나는 LAMP 앱을 배포하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="90a72-117">또한 Azure Storage 계정과 해당 계정에 액세스하는 데 사용할 키도 필요합니다(Azure Portal에서 가져올 수 있음).</span><span class="sxs-lookup"><span data-stu-id="90a72-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="90a72-118">Azure에서 Linux VM을 만들 때 도움이 필요하면 [Linux를 실행하는 가상 컴퓨터 만들기](createportal.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="90a72-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="90a72-119">설치 명령은 Ubuntu를 가정하지만 지원되는 Linux 배포판에 대한 설치를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="90a72-120">script-vm VM에는 Azure CLI가 설치되어 있어야 하며 Azure에 대한 정상적인 연결이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="90a72-121">도움이 필요하면 [Azure 명령줄 인터페이스 설치 및 구성](../../../cli-install-nodejs.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="90a72-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="90a72-122">스크립트 업로드</span><span class="sxs-lookup"><span data-stu-id="90a72-122">Upload a script</span></span>
<span data-ttu-id="90a72-123">CustomScript 확장을 통해 원격 VM에서 스크립트를 실행하여 LAMP 스택을 설치하고 PHP 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="90a72-124">어디서나 스크립트에 액세스할 수 있도록 Azure Blob으로 스크립트를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="90a72-125">스크립트 개요</span><span class="sxs-lookup"><span data-stu-id="90a72-125">Script overview</span></span>
<span data-ttu-id="90a72-126">스크립트 예제는 Ubuntu에 LAMP 스택을 설치하고(MySQL 자동 설치를 설정하는 작업도 수행함) 간단한 PHP 파일을 작성한 다음 Apache를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="90a72-127">스크립트 업로드</span><span class="sxs-lookup"><span data-stu-id="90a72-127">Upload script</span></span>
<span data-ttu-id="90a72-128">스크립트를 *install_lamp.sh*와 같은 텍스트 파일로 저장한 다음 Azure Storage에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="90a72-129">Azure CLI를 사용하면 이 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="90a72-130">다음 예제에서는 "scripts"라는 저장소 컨테이너에 이 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="90a72-131">컨테이너가 없으면 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="90a72-132">또한 Azure 저장소에서 스크립트를 다운로드하는 방법을 설명하는 JSON 파일도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="90a72-133">이 파일을 *public_config.json*으로 저장하고, "mystorage"는 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="90a72-134">확장 배포</span><span class="sxs-lookup"><span data-stu-id="90a72-134">Deploy the extension</span></span>
<span data-ttu-id="90a72-135">이제 Azure CLI를 사용하여 원격 VM에 Linux CustomScript 확장을 배포하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="90a72-136">이전 명령은 *lamp-vm*이라는 VM에 *install_lamp.sh* 스크립트를 다운로드하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="90a72-137">앱은 웹 서버를 포함하므로 원격 VM에서 다음 명령을 사용하여 HTTP 수신 대기 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="90a72-138">모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="90a72-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="90a72-139">원격 VM에서 로그 파일을 통해 사용자 지정 스크립트가 잘 실행되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="90a72-140">*lamp-vm* 에 대해 SSH를 실행하고 다음 명령을 사용하여 로그 파일의 끝부분을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="90a72-141">CustomScript 확장 프로그램을 실행한 후에 정보를 위해 만든 PHP 페이지를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="90a72-142">이 문서의 예제에서 PHP 페이지는 *http://lamp-vm.cloudapp.net/phpinfo.php*입니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90a72-143">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="90a72-143">Additional resources</span></span>
<span data-ttu-id="90a72-144">동일한 기본 단계를 사용하여 보다 복잡한 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="90a72-145">이 예제에서는 설치 스크립트를 Azure 저장소에 공용 Blob으로 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="90a72-146">이보다 안전한 옵션은 [SAS(보안 액세스 서명)](https://msdn.microsoft.com/library/azure/ee395415.aspx) 를 사용하여 보안 Blob으로 설치 스크립트를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="90a72-147">Azure CLI, Linux 및 CustomScript 확장을 위한 일부 추가 리소스는 다음에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="90a72-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="90a72-148">CustomScript 확장을 사용하여 Linux VM 사용자 지정 작업 자동화</span><span class="sxs-lookup"><span data-stu-id="90a72-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="90a72-149">Azure Linux 확장(GitHub)</span><span class="sxs-lookup"><span data-stu-id="90a72-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)