---
title: "PHP용 Azure SDK 다운로드"
description: "Azure SDK for PHP를 다운로드하여 설치하는 방법에 대해 알아봅니다."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="d3c8a-103">PHP용 Azure SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="d3c8a-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="d3c8a-104">개요</span><span class="sxs-lookup"><span data-stu-id="d3c8a-104">Overview</span></span>
<span data-ttu-id="d3c8a-105">PHP용 Azure SDK에는 Azure용 PHP 응용 프로그램을 개발, 배포 및 관리할 수 있는 구성 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="d3c8a-106">구체적으로 말해서 PHP용 Azure SDK에는 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="d3c8a-107">**Azure용 PHP 클라이언트 라이브러리**.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="d3c8a-108">이러한 클래스 라이브러리는 Azure 기능(예: 데이터 관리 서비스 및 클라우드 서비스)에 액세스하기 위한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="d3c8a-109">**Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="d3c8a-110">Azure 웹 사이트 및 Azure 가상 컴퓨터와 같은 Azure 서비스를 배포 및 관리하기 위한 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="d3c8a-111">Azure CLI는 Mac, Linux 및 Windows를 포함한 모든 플랫폼에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="d3c8a-112">**Azure PowerShell(Windows에만 해당)**.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="d3c8a-113">클라우드 서비스 및 가상 컴퓨터와 같은 Azure 서비스를 배포 및 관리하기 위한 PowerShell cmdlet 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="d3c8a-114">**Azure 에뮬레이터(Windows에만 해당)**.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="d3c8a-115">계산 및 저장소 에뮬레이터는 응용 프로그램을 로컬로 테스트할 수 있는 클라우드 서비스 및 데이터 관리 서비스의 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="d3c8a-116">Azure 에뮬레이터는 Windows에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="d3c8a-117">아래 섹션에서는 위에서 언급한 구성 요소를 다운로드하고 설치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="d3c8a-118">이 항목의 설명에서는 [PHP][install-php]가 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="d3c8a-119">Azure용 PHP 클라이언트 라이브러리를 사용하려면 PHP 5.5 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="d3c8a-120">Azure용 PHP 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d3c8a-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="d3c8a-121">Azure용 PHP 클라이언트 라이브러리는 운영 체제에서 Azure 기능(예: 데이터 관리 서비스 및 클라우드 서비스)에 액세스하기 위한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="d3c8a-122">이러한 라이브러리는 작성기를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="d3c8a-123">Azure용 PHP 클라이언트 라이브러리를 사용하는 방법에 대한 내용은 [Blob Service 사용 방법][blob-service], [Table Service 사용 방법][table-service] 및 [큐 서비스 사용 방법][queue-service]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="d3c8a-124">작성기를 통해 설치</span><span class="sxs-lookup"><span data-stu-id="d3c8a-124">Install via Composer</span></span>
1. <span data-ttu-id="d3c8a-125">[Git를 설치합니다][install-git].</span><span class="sxs-lookup"><span data-stu-id="d3c8a-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="d3c8a-126">Windows에서는 PATH 환경 변수에도 Git 실행 파일을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="d3c8a-127">프로젝트 루트에 **composer.json** 이라는 파일을 만들고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="d3c8a-128">프로젝트 루트에 **[composer.phar][composer-phar]**을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="d3c8a-129">명령 프롬프트를 열고 프로젝트 루트에서 이 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="d3c8a-130">Azure PowerShell 및 Azure 에뮬레이터</span><span class="sxs-lookup"><span data-stu-id="d3c8a-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="d3c8a-131">Azure PowerShell는 Azure 서비스(예: 클라우드 서비스 및 가상 컴퓨터)를 배포 및 관리하기 위한 PowerShell cmdlet 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="d3c8a-132">Azure 에뮬레이터는 응용 프로그램을 로컬로 테스트할 수 있는 클라우드 서비스 및 데이터 관리 서비스의 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="d3c8a-133">이러한 구성 요소는 Windows에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-133">These components are supported Windows only.</span></span>

<span data-ttu-id="d3c8a-134">Azure PowerShell 및 Azure 에뮬레이터는 [Microsoft 웹 플랫폼 설치 관리자][download-wpi]를 사용하여 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="d3c8a-135">PHP, SQL Server, PHP용 Microsoft Drivers for SQL Server, WebMatrix와 같은 다른 개발 구성 요소를 설치하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="d3c8a-136">Azure PowerShell 사용 방법에 대한 내용은 [Azure PowerShell 사용 방법][powershell-tools]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="d3c8a-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d3c8a-137">Azure CLI</span></span>
<span data-ttu-id="d3c8a-138">Azure CLI는 Azure 웹 사이트 및 Azure 가상 컴퓨터와 같은 Azure 서비스를 배포 및 관리하기 위한 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="d3c8a-139">Azure CLI를 설치하는 방법에 대한 자세한 내용은 [Azure CLI 설치](cli-install-nodejs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3c8a-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3c8a-140">Next steps</span></span>
<span data-ttu-id="d3c8a-141">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c8a-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
