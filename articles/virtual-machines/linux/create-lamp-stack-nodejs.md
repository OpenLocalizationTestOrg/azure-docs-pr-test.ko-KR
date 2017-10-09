---
title: "Azure CLI 1.0 hello로 Linux 가상 컴퓨터에서 램프 aaaDeploy | Microsoft Docs"
description: "Azure에서 Linux VM의 tooinstall hello LAMP 스택 하는 방법을 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="fa753-103">LAMP 스택 hello Azure CLI 1.0로 배포</span><span class="sxs-lookup"><span data-stu-id="fa753-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="fa753-104">이 문서 toodeploy는 Apache 웹 서버, MySQL 및 Azure에서 PHP (hello LAMP 스택) 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="fa753-105">Azure 계정이 필요 합니다 ([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/)) 및 hello [Azure CLI](../../cli-install-nodejs.md) 즉 [tooyour Azure 계정을 연결](../../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fa753-106">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="fa753-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="fa753-107">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="fa753-108">[Azure CLI 1.0]-우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="fa753-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fa753-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="fa753-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="fa753-110">기존 VM에 LAMP 배포</span><span class="sxs-lookup"><span data-stu-id="fa753-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="fa753-111">새 VM에 LAMP 배포 연습</span><span class="sxs-lookup"><span data-stu-id="fa753-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="fa753-112">만들어서 시작할 수는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md) 를 포함할 새 VM hello:</span><span class="sxs-lookup"><span data-stu-id="fa753-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="fa753-113">toocreate VM 자체 hello, 찾을 수는 이미 작성 된 Azure 리소스 관리자 템플릿을 사용 하 여 [GitHub에서 여기](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="fa753-114">입력을 몇 가지 더 하라는 메시지가 담긴 응답을 보게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="fa753-115">이미 설치된 LAMP를 사용해 이제 Linux VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="fa753-116">원하는 경우 너무 아래로 이동 하 여 hello 설치를 확인할 수 있습니다[확인 램프 성공적으로 설치](#verify-lamp-successfully-installed)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="fa753-117">기존 VM에 LAMP 배포 연습</span><span class="sxs-lookup"><span data-stu-id="fa753-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="fa753-118">Head 수 Linux VM을 만드는 데 도움이 필요한 경우 [여기 toolearn 어떻게 toocreate Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="fa753-119">Hello Linux VM에 tooSSH을 다음으로, 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="fa753-120">Head 수 SSH 키 만들기에서 도움이 필요한 경우 [여기 toolearn 어떻게 toocreate Linux/Mac에서 SSH 키](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="fa753-121">SSH 키가 있는 경우 계속해서 `ssh exampleUsername@exampleDNS`을 사용하여 Linux VM에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="fa753-122">Linux VM에서 작업 하는 했으므로 Debian 기반 배포판의 hello LAMP 스택 설치 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="fa753-123">다른 Linux 배포판에 대 한 hello 정확한 명령 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="fa753-124">Debian/Ubuntu에 설치</span><span class="sxs-lookup"><span data-stu-id="fa753-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="fa753-125">설치 된 패키지를 다음 hello 필요한: `apache2`, `mysql-server`, `php5`, 및 `php5-mysql`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="fa753-126">이러한 패키지를 직접 가져오거나 Tasksel을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="fa753-127">아래에는 두 옵션 모두에 대한 지침이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="fa753-128">설치 하기 전에 필요한 toodownload 및 패키지 목록을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="fa753-129">개별 패키지</span><span class="sxs-lookup"><span data-stu-id="fa753-129">Individual packages</span></span>
<span data-ttu-id="fa753-130">apt-get을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="fa753-131">Tasksel 사용</span><span class="sxs-lookup"><span data-stu-id="fa753-131">Using tasksel</span></span>
<span data-ttu-id="fa753-132">또는 관련된 여러 패키지를 하나의 조정된 “작업”으로 시스템에 설치하는 Debian/Ubuntu 도구인 Tasksel을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="fa753-133">hello 이전 옵션 중 하나를 실행 한 후이 패키지 및 기타 다양 한 종속성 증명된 tooinstall 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="fa753-134">'Y' 및 'Enter' toocontinue 누르고 MySQL에 대 한 모든 다른 프롬프트 tooset 관리자 암호를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="fa753-135">이 MySQL와 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="fa753-136">다음 명령은 toosee hello 패키지로 사용할 수 있는 기타 PHP 확장을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="fa753-137">Info.php 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="fa753-137">Create info.php document</span></span>
<span data-ttu-id="fa753-138">이제 있을 수 toocheck Apache, MySQL 및 PHP의 버전 있는 hello 명령줄을 통해 입력 하 여 `apache2 -v`, `mysql -v`, 또는 `php -v`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="fa753-139">Tootest 같은 앞서는, 경우에 브라우저에서 빠른 PHP 정보 페이지 tooview를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="fa753-140">이 명령을 사용하여 Nano 텍스트 편집기로 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="fa753-141">Hello GNU Nano 텍스트 편집기에서 줄을 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="fa753-142">그런 다음 저장 하 고 hello 텍스트 편집기를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="fa753-143">모든 새 설치 항목이 적용되도록 이 명령을 사용하여 Apache를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="fa753-144">LAMP 설치가 성공적인지 확인</span><span class="sxs-lookup"><span data-stu-id="fa753-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="fa753-145">이제 브라우저를 열고 toohttp://youruniqueDNS/info.php 라인으로 전환 하 여 만든 hello PHP 정보 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="fa753-146">이와 유사한 toothis 이미지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="fa753-147">Tooyou http://youruniqueDNS/ 이동 하 여 hello Apache2 Ubuntu 기본 페이지를 확인 하 여 Apache 설치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="fa753-148">다음 이미지와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa753-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="fa753-149">축하합니다. 이제 방금 Azure Vm에 LAMP 스택 설정을 마쳤습니다!</span><span class="sxs-lookup"><span data-stu-id="fa753-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa753-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fa753-150">Next steps</span></span>
<span data-ttu-id="fa753-151">체크 아웃 하 hello hello 램프 스택에 Ubuntu 설명서:</span><span class="sxs-lookup"><span data-stu-id="fa753-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="fa753-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="fa753-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png