---
title: "FTP/S를 사용하여 Azure App Service에 앱 배포 | Microsoft Docs"
description: "FTP 또는 FTPS를 사용하여 Azure App Service에 앱을 배포하는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="e5e32-103">FTP/S를 사용하여 앱에 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="e5e32-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="e5e32-104">이 문서는 FTP 또는 FTPS를 사용하여 웹앱, 모바일 앱 백 엔드 또는 API 앱을 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e5e32-105">앱에 대한 FTP/S 끝점은 이미 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="e5e32-106">FTP/S 배포를 사용하도록 설정하는 데 필요한 구성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5e32-107">Microsoft Azure 플랫폼 보안을 개선하기 위해 계속해서 작업하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="e5e32-108">이러한 지속적인 노력의 일환으로 독일 중부 및 독일 북동부 하위 지역에 대해 웹 응용 프로그램 업그레이드가 예정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="e5e32-109">이 프로세스 동안 웹앱은 배포에 일반 텍스트 FTP 프로토콜이 사용되지 않도록 설정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="e5e32-110">고객은 배포를 위해 FTPS로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="e5e32-111">9월 5일로 계획된 이 업그레이드 동안 서비스를 중단하지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="e5e32-112">여러분의 지원에 감사 드립니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="e5e32-113">1단계: 배포 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="e5e32-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="e5e32-114">앱에 대한 FTP 서버에 액세스하려면 먼저 배포 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="e5e32-115">배포 자격 증명을 설정하거나 다시 설정하려면 [Azure App Service 배포 자격 증명](app-service-deployment-credentials.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5e32-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="e5e32-116">이 자습서는 사용자 수준의 자격 증명 사용 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="e5e32-117">2단계: FTP 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="e5e32-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="e5e32-118">[Azure Portal](https://portal.azure.com)에서 앱의 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="e5e32-119">왼쪽 메뉴에서 **개요**를 선택하고 **P/배포 사용자**, **FTP 호스트 이름** 및 **FTPS 호스트 이름** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP 연결 정보](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="e5e32-121">FTP 서버에 올바른 컨텍스트를 제공하기 위해 Azure 포털에 표시된 **FTP/배포 사용자** 사용자 값(앱 이름 포함)을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="e5e32-122">왼쪽 메뉴에서 **속성**을 선택하면 같은 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="e5e32-123">또한 배포 암호는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="e5e32-124">배포 암호를 잊은 경우 [1단계](#step1)로 이동한 후 배포 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="e5e32-125">3단계: Azure에 파일 배포</span><span class="sxs-lookup"><span data-stu-id="e5e32-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="e5e32-126">FTP 클라이언트([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client) 등)에서 수집한 연결 정보를 사용하여 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="e5e32-127">파일 및 해당 디렉터리 구조를 Azure의 [**/site/wwwroot** 디렉터리](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)(또는 WebJobs의 경우 **/site/wwwroot/App_Data/Jobs/** 디렉터리)에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="e5e32-128">앱의 URL을 찾아 앱이 제대로 실행하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="e5e32-129">[Git 기반 배포](app-service-deploy-local-git.md)와 달리, FTP 배포에서는 다음과 같은 배포 자동화를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="e5e32-130">종속성 복원(예: NuGet, NPM, PIP 및 Composer Automation)</span><span class="sxs-lookup"><span data-stu-id="e5e32-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="e5e32-131">.NET 이진 파일 컴파일</span><span class="sxs-lookup"><span data-stu-id="e5e32-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="e5e32-132">web.config 생성([Node.js 예제](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps) 참조)</span><span class="sxs-lookup"><span data-stu-id="e5e32-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="e5e32-133">로컬 컴퓨터에서 이러한 필요한 파일을 수동으로 복원, 빌드 및 생성한 후 앱과 함께 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e5e32-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5e32-134">Next steps</span></span>

<span data-ttu-id="e5e32-135">고급 배포 시나리오에 대해서는 [Git를 사용하여 Azure에 배포](app-service-deploy-local-git.md)를 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="e5e32-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="e5e32-136">Azure로의 Git 기반 배포를 수행하면 버전 제어, 패키지 복원, MSBuild 등을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5e32-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="e5e32-137">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e5e32-137">More Resources</span></span>

* <span data-ttu-id="e5e32-138">[PHP-MySQL 웹 앱을 만들고 FTP를 사용하여 배포합니다.](web-sites-php-mysql-deploy-use-ftp.md)</span><span class="sxs-lookup"><span data-stu-id="e5e32-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="e5e32-139">Azure App Service 배포 자격 증명</span><span class="sxs-lookup"><span data-stu-id="e5e32-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
