---
title: "aaaDeploy 사용자 앱 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스 | Microsoft Docs"
description: "자세한 방법을 toodeploy 앱 서비스를 사용 하 여 FTP 또는 FTPS 앱 tooAzure 프로그램."
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
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="b3f50-103">사용자 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="b3f50-104">이 문서에서는 어떻게 toouse FTP toodeploy를 웹 앱, 모바일 앱 백 엔드, 또는 API 앱 너무 FTPS 또는[Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b3f50-105">응용 프로그램에 대 한 hello FTP/S 끝점 이미 활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="b3f50-106">구성이 필요한 tooenable FTP/S 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3f50-107">단계 tooimprove Microsoft Azure 플랫폼 보안 수행 하 고 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="b3f50-108">이러한 지속적인 노력의 일환으로 독일 중부 및 독일 북동부 하위 지역에 대해 웹 응용 프로그램 업그레이드가 예정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="b3f50-109">이 프로세스 동안 웹 응용 프로그램 배포에 대 한 일반 텍스트 FTP 프로토콜의 hello 사용할을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="b3f50-110">권장 사항 tooour 고객 배포에 대 한 tooswitch tooFTPS입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="b3f50-111">이 업그레이드/9/5에 대 한 계획 되어 있는 동안 모든 중단 tooyour 서비스를 예상 되지 않는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="b3f50-112">여러분의 지원에 감사 드립니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="b3f50-113">1단계: 배포 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="b3f50-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="b3f50-114">앱에 대 한 tooaccess hello FTP 서버를 먼저 배포 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="b3f50-115">배포 자격 증명 참조 tooset 또는 리셋 [Azure 앱 서비스 배포 자격 증명](app-service-deployment-credentials.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="b3f50-116">이 자습서의 사용자 자격 증명 hello 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="b3f50-117">2단계: FTP 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="b3f50-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="b3f50-118">Hello에 [Azure 포털](https://portal.azure.com), 응용 프로그램을 열고 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="b3f50-119">선택 **개요** hello 왼쪽된 메뉴에 대 한 hello 값을 확인 한 다음 **P/배포 사용자**, **FTP 호스트 이름**, 및 **FTPS 호스트 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP 연결 정보](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="b3f50-121">hello **P/배포 사용자** 사용자가 값으로 표시 된 대로 hello 순서 tooprovide hello FTP 서버에 대 한 적절 한 컨텍스트에 hello 응용 프로그램 이름을 포함 하는 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="b3f50-122">찾을 수 선택 하면 동일한 정보를 hello **속성** hello 왼쪽된 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="b3f50-123">또한 hello 배포 암호 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="b3f50-124">배포 암호를 잊은 경우 돌아가서 너무[1 단계](#step1) 배포 암호를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="b3f50-125">3 단계: 파일 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="b3f50-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="b3f50-126">FTP 클라이언트에서 ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)등), tooconnect tooyour 앱 수집한 hello 연결 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="b3f50-127">파일 및 해당 해당 디렉터리 구조 toohello 복사 [ **/사이트/wwwroot** 디렉터리](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure에서 (또는 hello **/사이트/wwwroot/App_Data/작업/** 에 대 한 디렉터리 WebJobs)입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="b3f50-128">찾아보기 tooyour 앱의 URL tooverify hello 앱은 제대로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b3f50-129">와 달리 [Git 기반 배포](app-service-deploy-local-git.md), FTP 배포 배포 자동화를 수행 하는 hello를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="b3f50-130">종속성 복원(예: NuGet, NPM, PIP 및 Composer Automation)</span><span class="sxs-lookup"><span data-stu-id="b3f50-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="b3f50-131">.NET 이진 파일 컴파일</span><span class="sxs-lookup"><span data-stu-id="b3f50-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="b3f50-132">web.config 생성([Node.js 예제](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps) 참조)</span><span class="sxs-lookup"><span data-stu-id="b3f50-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="b3f50-133">로컬 컴퓨터에서 이러한 필요한 파일을 수동으로 복원, 빌드 및 생성한 후 앱과 함께 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b3f50-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3f50-134">Next steps</span></span>

<span data-ttu-id="b3f50-135">고급 배포 시나리오에 대 한 시도 [tooAzure Git가 포함 된 배포](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="b3f50-136">Git 기반 배포 tooAzure 버전 제어, 패키지를 복원, MSBuild, 등 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f50-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="b3f50-137">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b3f50-137">More Resources</span></span>

* <span data-ttu-id="b3f50-138">[PHP-MySQL 웹 앱을 만들고 FTP를 사용하여 배포합니다.](web-sites-php-mysql-deploy-use-ftp.md)</span><span class="sxs-lookup"><span data-stu-id="b3f50-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="b3f50-139">Azure App Service 배포 자격 증명</span><span class="sxs-lookup"><span data-stu-id="b3f50-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
