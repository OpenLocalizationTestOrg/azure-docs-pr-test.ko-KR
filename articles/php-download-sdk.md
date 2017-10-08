---
title: "aaaDownload hello PHP 용 Azure SDK"
description: "어떻게 toodownload 및 설치 hello Azure SDK for PHP에 알아봅니다."
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
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="59090-103">PHP 용 hello Azure SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="59090-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="59090-104">개요</span><span class="sxs-lookup"><span data-stu-id="59090-104">Overview</span></span>
<span data-ttu-id="59090-105">PHP 용 Azure SDK hello toodevelop 사용 하면 배포 하 고 Azure에 대 한 PHP 응용 프로그램을 관리 하는 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="59090-106">특히, PHP 용 Azure SDK hello hello 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59090-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="59090-107">**Azure 용 PHP 클라이언트 라이브러리를 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="59090-108">이러한 클래스 라이브러리는 Azure 기능(예: 데이터 관리 서비스 및 클라우드 서비스)에 액세스하기 위한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="59090-109">**Mac, Linux 및 Windows Azure CLI ()에 대 한 Azure 명령줄 인터페이스 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="59090-110">Azure 웹 사이트 및 Azure 가상 컴퓨터와 같은 Azure 서비스를 배포 및 관리하기 위한 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="59090-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="59090-111">Mac, Linux 및 Windows를 포함 하 여 모든 플랫폼에서 Azure CLI 작업 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="59090-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="59090-112">**Azure PowerShell(Windows에만 해당)**.</span><span class="sxs-lookup"><span data-stu-id="59090-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="59090-113">클라우드 서비스 및 가상 컴퓨터와 같은 Azure 서비스를 배포 및 관리하기 위한 PowerShell cmdlet 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="59090-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="59090-114">**Azure 에뮬레이터 (Windows만 해당) hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="59090-115">hello 계산 및 저장소 에뮬레이터는 클라우드 서비스 및 응용 프로그램을 로컬로 tootest 할 수 있도록 데이터 관리 서비스의 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="59090-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="59090-116">hello Azure 에뮬레이터만 Windows에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="59090-117">아래 섹션에서는 hello 방법을 toodownload 및 설치 hello 위에서 설명한 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="59090-118">hello이 항목의에서 지침에 있다고 가정 [PHP] [ install-php] 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="59090-119">Azure 용 PHP 5.5 또는 더 높은 toouse hello PHP 클라이언트 라이브러리가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="59090-120">Azure용 PHP 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="59090-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="59090-121">Azure 용 hello PHP 클라이언트 라이브러리는 데이터 관리 서비스 등의 Azure 기능에 액세스 하기 위한 인터페이스를 제공 및 클라우드 서비스를 운영 체제에서.</span><span class="sxs-lookup"><span data-stu-id="59090-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="59090-122">이러한 라이브러리는 hello 작성기를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59090-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="59090-123">Toouse Azure 용 PHP 클라이언트 라이브러리를 hello 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooUse hello Blob 서비스][blob-service], [어떻게 tooUse hello 테이블 서비스] [ table-service] 및 [어떻게 tooUse hello 큐 서비스][queue-service]합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="59090-124">작성기를 통해 설치</span><span class="sxs-lookup"><span data-stu-id="59090-124">Install via Composer</span></span>
1. <span data-ttu-id="59090-125">[Git를 설치합니다][install-git].</span><span class="sxs-lookup"><span data-stu-id="59090-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="59090-126">Windows에서는 또한 tooadd hello Git 실행 tooyour PATH 환경 변수를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="59090-127">라는 파일을 만들어 **composer.json** 에 프로젝트의 루트 hello 및 다음 코드 tooit hello 추가:</span><span class="sxs-lookup"><span data-stu-id="59090-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="59090-128">프로젝트 루트에 **[composer.phar][composer-phar]**을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="59090-129">명령 프롬프트를 열고 프로젝트 루트에서 이 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="59090-130">Azure PowerShell 및 Azure 에뮬레이터</span><span class="sxs-lookup"><span data-stu-id="59090-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="59090-131">Azure PowerShell는 Azure 서비스(예: 클라우드 서비스 및 가상 컴퓨터)를 배포 및 관리하기 위한 PowerShell cmdlet 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="59090-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="59090-132">hello Azure 에뮬레이터는 클라우드 서비스 및 응용 프로그램을 로컬로 tootest 할 수 있도록 데이터 관리 서비스 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="59090-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="59090-133">이러한 구성 요소는 Windows에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="59090-133">These components are supported Windows only.</span></span>

<span data-ttu-id="59090-134">권장 되는 방법은 Azure PowerShell tooinstall hello 및 hello Azure 에뮬레이터는 toouse hello [Microsoft 웹 플랫폼 설치 관리자][download-wpi]합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="59090-135">선택할 수 있는 또한 tooinstall PHP, SQL Server, hello Microsoft Drivers for PHP 및 WebMatrix에 대 한 SQL Server와 같은 다른 개발 구성 요소 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="59090-136">방법에 대 한 정보에 대 한 Azure PowerShell toouse 참조 [어떻게 tooUse Azure PowerShell][powershell-tools]합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="59090-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59090-137">Azure CLI</span></span>
<span data-ttu-id="59090-138">hello Azure CLI는 배포 하 고 Azure 웹 사이트 및 Azure 가상 컴퓨터와 같은 Azure 서비스 관리에 대 한 명령 집합.</span><span class="sxs-lookup"><span data-stu-id="59090-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="59090-139">Azure CLI를 설치 하는 방법에 대 한 정보를 참조 하십시오. [설치 hello Azure CLI](cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59090-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59090-140">Next steps</span></span>
<span data-ttu-id="59090-141">자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="59090-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
