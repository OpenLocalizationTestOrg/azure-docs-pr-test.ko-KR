---
title: "aaaUsing tooPublish tooDev Windows PowerShell 스크립트 및 테스트 환경 | Microsoft Docs"
description: "Visual Studio toopublish toodevelopment 및 테스트 환경에서 Windows PowerShell toouse 스크립트 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="2d5dc-103">Windows PowerShell을 사용 하 여 스크립트를 toopublish toodev 및 테스트 환경</span><span class="sxs-lookup"><span data-stu-id="2d5dc-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="2d5dc-104">Visual Studio에서 웹 응용 프로그램을 만들 때 웹 사이트 tooAzure의 뒷부분에 나오는 tooautomate hello 게시를 사용 하면 Azure 앱 서비스 또는 가상 컴퓨터에서 웹 응용 프로그램으로 Windows PowerShell 스크립트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="2d5dc-105">편집 하 hello Visual Studio 편집기 toosuit에서 Windows PowerShell 스크립트를 hello 요구 사항, 확장 또는 기존 빌드, 테스트 및 게시 스크립트와 hello 스크립트를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="2d5dc-106">이러한 스크립트를 사용하면 일시적으로 사용할 사이트의 사용자 지정 버전(개발 및 테스트 환경이라고도 함)을 프로비저닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="2d5dc-107">예를 들어 있습니다 수 설정 웹 사이트의 특정 버전 슬롯에서 웹 사이트 toorun hello 또는 Azure 가상 컴퓨터에서 테스트 도구 모음, 버그를 재현, 버그 수정을, 평가판 제안된 된 변경 내용을 테스트 또는 데모 또는 프레젠테이션을 위한 사용자 지정 환경을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="2d5dc-108">프로젝트를 게시 하는 스크립트를 만든 후 필요에 따라 다시 hello 스크립트를 실행 하 여 동일한 환경을 다시 또는 테스트에 대 한 사용자 지정 환경을 웹 응용 프로그램 toocreate 직접 빌드할 hello 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2d5dc-109">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="2d5dc-109">What you need</span></span>
* <span data-ttu-id="2d5dc-110">Azure SDK 2.3 이상</span><span class="sxs-lookup"><span data-stu-id="2d5dc-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="2d5dc-111">자세한 내용은 [Visual Studio 다운로드](http://go.microsoft.com/fwlink/?LinkID=624384)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="2d5dc-112">웹 프로젝트에 대 한 hello Azure SDK toogenerate hello 스크립트 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="2d5dc-113">이 기능은 클라우드 서비스의 웹 역할이 아닌 웹 프로젝트용입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="2d5dc-114">Azure PowerShell 0.7.4 이상</span><span class="sxs-lookup"><span data-stu-id="2d5dc-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="2d5dc-115">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="2d5dc-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) 이상</span><span class="sxs-lookup"><span data-stu-id="2d5dc-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="2d5dc-117">추가 도구</span><span class="sxs-lookup"><span data-stu-id="2d5dc-117">Additional tools</span></span>
<span data-ttu-id="2d5dc-118">Azure 개발 시 Visual Studio에서 PowerShell을 사용하기 위한 추가 도구와 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="2d5dc-119">[Visual Studio용 PowerShell](http://go.microsoft.com/fwlink/?LinkId=404012)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="2d5dc-120">게시 스크립트 생성이 hello</span><span class="sxs-lookup"><span data-stu-id="2d5dc-120">Generating hello publish scripts</span></span>
<span data-ttu-id="2d5dc-121">Hello를 생성할 수에 따라 새 프로젝트를 만들 때 웹 사이트를 호스팅하는 가상 컴퓨터에 대 한 스크립트를 게시 [이러한 지침](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="2d5dc-122">또한 [Azure App Service에서 웹앱용 게시 스크립트를 생성](app-service-web/app-service-web-get-started-dotnet.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="2d5dc-123">Visual Studio에서 생성하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="2d5dc-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="2d5dc-124">Visual Studio에서 호출 하는 솔루션 수준의 폴더 생성 **PublishScripts** 두 개의 Windows PowerShell 파일을 포함 하 여 가상 컴퓨터 또는 웹 사이트 및 hello에 사용할 수 있는 함수가 포함 된 모듈에 대 한 게시 스크립트 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="2d5dc-125">Visual Studio는 배포 하는 hello 프로젝트의 hello 세부 정보를 지정 하는 hello JSON 형식의 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="2d5dc-126">Windows PowerShell 게시 스크립트</span><span class="sxs-lookup"><span data-stu-id="2d5dc-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="2d5dc-127">게시 스크립트를 hello 특정 포함 tooa 웹 사이트 또는 가상 컴퓨터를 배포 하기 위한 단계를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="2d5dc-128">Visual Studio는 Windows PowerShell 배포를 위한 구문 색 지정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="2d5dc-129">Hello 함수를 사용할 수 있습니다 자유롭게 hello 함수를에서 편집할 수 hello 스크립트 toosuit 변경 요구 사항에 대 한 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="2d5dc-130">Windows PowerShell 모듈</span><span class="sxs-lookup"><span data-stu-id="2d5dc-130">Windows PowerShell module</span></span>
<span data-ttu-id="2d5dc-131">hello Visual Studio에서 생성 하는 모듈 hello 하는 함수를 포함 하는 Windows PowerShell 스크립트 사용 하 여 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="2d5dc-132">이 Azure PowerShell 함수로 되며 의도 한 toobe 수정 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="2d5dc-133">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="2d5dc-134">JSON 구성 파일</span><span class="sxs-lookup"><span data-stu-id="2d5dc-134">JSON configuration file</span></span>
<span data-ttu-id="2d5dc-135">hello에 hello JSON 파일을 만들지 **구성을** 폴더 및 어떤 리소스 toodeploy tooAzure 정확 하 게 지정 하는 구성 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="2d5dc-136">hello Visual Studio에서 생성 하는 hello 파일 이름은 프로젝트-이름-w a w S-dev.json 가상 컴퓨터를 만든 경우 웹 사이트 또는 프로젝트 이름 VM dev.json를 만든 경우.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="2d5dc-137">다음은 웹 사이트를 만들 때 생성된 JSON 구성 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="2d5dc-138">Hello 값의 대부분은 자체 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="2d5dc-139">hello 웹 사이트 이름은 프로젝트 이름과 일치 하지 않을 수 있으므로 Azure에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="2d5dc-140">가상 컴퓨터를 만들 때 hello JSON 구성 파일에 비슷한 toohello 다음 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="2d5dc-141">만들어진 클라우드 서비스는 hello 가상 컴퓨터에 대 한 컨테이너로 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="2d5dc-142">hello 가상 컴퓨터에는 HTTP 및 HTTPS를 통한 웹 액세스용 일반 끝점과 hello 뿐만 아니라 로컬 컴퓨터, 원격 데스크톱 및 Windows PowerShell에서 toohello 웹 사이트를 게시할 수 있는 웹 배포에 대 한 끝점 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="2d5dc-143">Hello를 실행 하는 경우 JSON 구성 toochange hello 편집할 수 스크립트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="2d5dc-144">hello `cloudService` 및 `virtualMachine` 섹션이 모두 필요, 되지만 hello를 삭제할 수 있습니다 `databases` 필요 하지 않으면 섹션.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="2d5dc-145">Visual Studio에서 생성 하는 hello 기본 구성 파일에서 비어 있는 hello 속성은 선택 사항입니다. 값이 있는 hello 기본 구성 파일에는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="2d5dc-146">Azure에서 단일 프로덕션 사이트 대신 여러 배포 환경 (슬롯 이라고 함)가 있는 웹 사이트를 설정한 경우 hello JSON 구성 파일의 hello 웹 사이트의 hello 이름에 hello 슬롯 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="2d5dc-147">예를 들어, 명명 된 웹 사이트가 있는 경우 **mysite** 및 명명 된 것에 대 한 슬롯 **테스트** hello URI는 mysite-test.cloudapp.net 이지만 hello 구성 파일에 올바른 이름을 toouse hello 인 한 다음 .</span><span class="sxs-lookup"><span data-stu-id="2d5dc-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="2d5dc-148">수만 이렇게 하면 hello 웹 사이트와 슬롯이 이미 구독에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="2d5dc-149">없는 경우 hello 슬롯을 지정 하지 않고 hello 스크립트를 실행 하 여 hello 웹 사이트를 만든 다음 만듭니다 hello의 hello 슬롯 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), 그 후 hello 수정한 웹 사이트 이름으로 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="2d5dc-150">웹앱의 배포 슬롯에 대한 자세한 내용은 [Azure App Service에서 웹앱에 대한 스테이징 환경 설정](app-service-web/web-sites-staged-publishing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="2d5dc-151">Toorun hello 스크립트를 게시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2d5dc-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="2d5dc-152">하기 전에 Windows PowerShell 스크립트를 실행 하지 않아도 hello 실행 정책 tooenable 스크립트 toorun 먼저 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="2d5dc-153">취약 한 toomalware 또는 스크립트 실행과 관련이 있는 바이러스 인 경우 Windows PowerShell 스크립트 실행에서 보안 기능 tooprevent 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="2d5dc-154">Hello 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="2d5dc-154">Run hello script</span></span>
1. <span data-ttu-id="2d5dc-155">프로젝트에 대 한 hello 웹 배포 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="2d5dc-156">웹 배포 패키지는 toocopy tooyour 웹 사이트 또는 가상 컴퓨터 파일이 있는 압축된 보관 (.zip 파일).</span><span class="sxs-lookup"><span data-stu-id="2d5dc-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="2d5dc-157">Visual Studio에서 모든 웹 응용 프로그램에 사용할 웹 배포 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![웹 배포 패키지 만들기](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="2d5dc-159">자세한 내용은 [방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="2d5dc-160">Hello 섹션에 설명 된 대로 웹 배포 패키지의 hello 만들기를 자동화할 수도 있습니다 **사용자 지정 및 확장 hello에 대 한 게시 스크립트** 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="2d5dc-161">**솔루션 탐색기**를 hello 스크립트에 대 한 hello 상황에 맞는 메뉴를 열고 다음 선택 **PowerShell ISE로 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="2d5dc-162">인 경우 hello이이 컴퓨터에서 Windows PowerShell 스크립트를 실행 하는 처음으로 관리자 권한 및 형식 hello 다음 명령을 사용 하 여 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="2d5dc-163">다음 명령을 hello를 사용 하 여 tooAzure에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="2d5dc-164">메시지가 표시되면 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="2d5dc-165">Note hello 스크립트 자동화 하면 Azure 자격 증명을 제공이 방법을 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="2d5dc-166">대신, hello.publishsettings 파일 tooprovide 자격 증명을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="2d5dc-167">한 번만 명령을 사용 하면 hello **Get-azurepublishsettingsfile** toodownload hello azure에서 파일을 사용 하 여 이후 **Import-azurepublishsettingsfile** tooimport hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="2d5dc-168">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="2d5dc-169">(선택 사항) Azure toocreate 하려는 경우 hello 가상 컴퓨터, 데이터베이스 및 웹 응용 프로그램을 게시 하지 않고 웹 사이트와 같은 리소스 사용 hello **Publish-webapplication.ps1** hello로 명령을 **-구성** 인수 toohello JSON 구성 파일을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="2d5dc-170">이 명령줄 어떤 리소스 toocreate JSON 구성 파일 toodetermine hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="2d5dc-171">다른 명령줄 인수에 대 한 기본 설정을 hello를 사용 하기 때문에 hello 리소스를 만들지만 웹 응용 프로그램을 게시 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="2d5dc-172">hello-Verbose 옵션 자세한 정보를 제공 하는 상황에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="2d5dc-173">사용 하 여 hello **Publish-webapplication.ps1** hello 예제 tooinvoke hello 스크립트를 다음 중 하나에 표시 된 것 처럼 명령 및 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="2d5dc-174">필요한 경우 toooverride hello 기본 설정을 hello에 대 한 hello 구독 이름 등의 다른 인수 패키지 이름, 가상 컴퓨터 자격 증명 또는 데이터베이스 서버 자격 증명을 게시 합니다. 이러한 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="2d5dc-175">사용 하 여 hello **– Verbose** toosee hello 게시 프로세스의 hello 진행률에 대 한 자세한 내용은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="2d5dc-176">가상 컴퓨터를 만드는 경우 hello 명령 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="2d5dc-177">이 예제에서는 또한 toospecify hello 여러 데이터베이스에 대 한 자격 증명 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="2d5dc-178">이러한 스크립트로 만드는 hello 가상 컴퓨터에 대 한 hello SSL 인증서가 신뢰할 수 있는 루트 기관에서.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="2d5dc-179">따라서 toouse hello **– AllowUntrusted** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="2d5dc-180">hello 스크립트에 데이터베이스를 만들 수 있지만 데이터베이스 서버를 만들지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="2d5dc-181">Hello toocreate 데이터베이스 서버를 원하는 경우 사용할 수 있습니다 **New-azuresqldatabaseserver** hello Azure 모듈의에서 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="2d5dc-182">사용자 지정 및 확장 hello에 대 한 게시 스크립트</span><span class="sxs-lookup"><span data-stu-id="2d5dc-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="2d5dc-183">Hello를 사용자 지정할 수 있습니다 스크립트 및 JSON 구성 파일을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="2d5dc-184">hello Windows PowerShell 모듈의 함수 hello **AzureWebAppPublishModule.psm1** 의도 한 toobe 수정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="2d5dc-185">다른 데이터베이스 toospecify 방금 싶거나 hello 가상 컴퓨터의 hello 속성의 일부 변경 hello JSON 구성 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="2d5dc-186">에 함수 스텁을 구현 하면 hello 스크립트 tooautomate 빌드 및 테스트 프로젝트의 tooextend hello 기능을 사용 하려면 **Publish-webapplication.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="2d5dc-187">너무 MSBuild를 호출 하는 코드를 추가 하는 프로젝트를 빌드하지 tooautomate`New-WebDeployPackage` 이 코드 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="2d5dc-188">hello 경로 toohello MSBuild 명령을 설치한 Visual Studio의 hello 버전에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="2d5dc-189">tooget hello 올바른 경로 hello 함수를 사용할 수 있습니다 **Get-msbuildcmd**이 예제에 나온 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="2d5dc-190">프로젝트 빌드를 tooautomate</span><span class="sxs-lookup"><span data-stu-id="2d5dc-190">tooautomate building your project</span></span>
1. <span data-ttu-id="2d5dc-191">Hello 추가 `$ProjectFile` hello 전역 param 섹션에서 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="2d5dc-192">Copy 함수 hello `Get-MSBuildCmd` 스크립트 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="2d5dc-193">대체 `New-WebDeployPackage` 다음 코드로 바꾸고 줄 생성 hello에 hello 자리 표시자를 대체 하는 hello로 `$msbuildCmd`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="2d5dc-194">이 코드는 Visual Studio 2015용입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="2d5dc-195">Visual Studio 2013을 사용 하는 경우 변경 hello **VisualStudioVersion** 속성 아래 너무`12.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="2d5dc-196">toobuild 프로그램 웹 응용 프로그램을 MsBuild.exe를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="2d5dc-197">도움말은 [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)에서 MSBuild 명령줄을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="2d5dc-198">Hello 빌드 명령 실행 시작</span><span class="sxs-lookup"><span data-stu-id="2d5dc-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="2d5dc-199">Hello 호출 `New-WebDeployPackage` 이 줄 앞 함수: `$Config = Read-ConfigFile $Configuration` 는 웹 응용 프로그램 또는 `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="2d5dc-200">사용자 지정 하는 hello 스크립트 전달 hello를 사용 하 여 명령줄에서 호출할 `$Project` hello 다음 예에서는 명령 줄에서와 같이 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="2d5dc-201">코드를 너무 추가 응용 프로그램의 테스트 tooautomate`Test-WebApplication`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="2d5dc-202">수 있는지 toouncomment hello 줄에 **Publish-webapplication.ps1** 이러한 함수 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="2d5dc-203">구현을 제공 하지 않으면 수동으로 Visual Studio를 사용 하 여 프로젝트를 빌드할 수 있습니다 및 다음 실행된 hello 게시 스크립트 toopublish tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="2d5dc-204">게시 함수 요약</span><span class="sxs-lookup"><span data-stu-id="2d5dc-204">Publishing function summary</span></span>
<span data-ttu-id="2d5dc-205">hello Windows PowerShell 명령 프롬프트에서 사용 가능한 함수에 대 한 도움말 tooget hello 명령을 사용 하 여 `Get-Help function-name`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="2d5dc-206">hello 도움말에는 매개 변수 도움말과 예제가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="2d5dc-207">동일한 도움말 텍스트는 hello 스크립트 원본 파일에도 hello **AzureWebAppPublishModule.psm1** 및 **Publish-webapplication.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="2d5dc-208">hello 스크립트와 도움말은 Visual Studio 언어로 지역화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="2d5dc-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="2d5dc-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="2d5dc-210">함수 이름</span><span class="sxs-lookup"><span data-stu-id="2d5dc-210">Function name</span></span> | <span data-ttu-id="2d5dc-211">설명</span><span class="sxs-lookup"><span data-stu-id="2d5dc-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d5dc-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="2d5dc-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="2d5dc-213">새 Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="2d5dc-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="2d5dc-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="2d5dc-215">Visual Studio에서 생성 하는 hello JSON 구성 파일의 hello 값에서 Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="2d5dc-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="2d5dc-216">Add-AzureVM</span></span> |<span data-ttu-id="2d5dc-217">Azure 가상 컴퓨터를 만들고 hello의 hello URL VM 배포를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="2d5dc-218">hello 함수를 설정 hello 필수 조건 및 호출 hello **New-azurevm** (Azure 모듈) toocreate 새 가상 컴퓨터를 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="2d5dc-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="2d5dc-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="2d5dc-220">새 입력된 끝점 tooa 가상 컴퓨터를 추가 하 고 hello 새 끝점이 있는 hello 가상 컴퓨터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="2d5dc-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="2d5dc-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="2d5dc-222">Hello 현재 구독에서 새 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="2d5dc-223">hello 계정의 hello 이름을 다음 고유한 영숫자 문자열 "devtest"로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="2d5dc-224">hello 함수 hello hello 새 저장소 계정의 이름으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="2d5dc-225">위치 또는 hello 새 저장소 계정에 대 한 선호도 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="2d5dc-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="2d5dc-226">Add-AzureWebsite</span></span> |<span data-ttu-id="2d5dc-227">Hello 지정 된 이름 및 위치와 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="2d5dc-228">이 함수 호출 hello **New-azurewebsite** hello Azure 모듈의에서 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="2d5dc-229">Hello 구독 된 hello 지정 된 이름의 웹 사이트가 아직 없는, 하는 경우이 함수는 hello 웹 사이트를 만들고 웹 사이트 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="2d5dc-230">그렇지 않으면 `$null`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="2d5dc-231">백업-구독</span><span class="sxs-lookup"><span data-stu-id="2d5dc-231">Backup-Subscription</span></span> |<span data-ttu-id="2d5dc-232">저장 hello hello에 현재 Azure 구독 `$Script:originalSubscription` 스크립트 범위에서 변수입니다. Hello 현재 Azure 구독을 저장 하는이 함수 (여 얻어지는 `Get-AzureSubscription -Current`) 및 해당 저장소 계정과,이 스크립트에 의해 변경 된 hello 구독 (hello 변수에 저장 된 `$UserSpecifiedSubscription`) 및 해당 저장소 계정을 스크립트 범위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="2d5dc-233">Hello 값으로 저장 하 여 사용할 수 있습니다는 함수 같은 `Restore-Subscription`, toorestore hello 원래 현재 구독과 저장소 계정 toocurrent 상태 hello 현재 상태가 변경 된 경우.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="2d5dc-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="2d5dc-234">Find-AzureVM</span></span> |<span data-ttu-id="2d5dc-235">Azure 가상 컴퓨터를 지정 하는 hello 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="2d5dc-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="2d5dc-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="2d5dc-237">Hello 날짜 및 시간 tooa 메시지 앞에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="2d5dc-238">이 함수는 toohello 오류 및 자세한 정보 스트림에 기록 된 메시지에 대 한 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="2d5dc-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="2d5dc-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="2d5dc-240">연결 문자열 tooconnect tooan Azure SQL 데이터베이스를 어셈블합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="2d5dc-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="2d5dc-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="2d5dc-242">반환 hello hello 이름 패턴 hello 첫 번째 저장소 계정의 이름을 "devtest*" (대/소문자 구분) hello 지정 된 위치 또는 선호도 그룹에서. 경우 hello "devtest*" hello 위치 또는 선호도 그룹에 저장소 계정 일치 하지 않습니다, hello 함수가를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="2d5dc-243">위치 또는 선호도 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="2d5dc-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="2d5dc-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="2d5dc-245">명령 toorun hello MsDeploy.exe 도구를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="2d5dc-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="2d5dc-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="2d5dc-247">찾거나 hello JSON 구성 파일의 hello 값과 일치 하는 hello 구독에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="2d5dc-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="2d5dc-248">Publish-WebPackage</span></span> |<span data-ttu-id="2d5dc-249">사용 하 여 MsDeploy.exe 및 웹 게시 패키지 합니다. Zip 파일 toodeploy 리소스 tooa 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="2d5dc-250">이 함수는 출력을 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-250">This function doesn't generate any output.</span></span> <span data-ttu-id="2d5dc-251">Hello 호출 tooMSDeploy.exe 실패 hello 함수에서 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="2d5dc-252">tooget 자세한 출력을 사용 하 여 hello **-Verbose** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="2d5dc-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="2d5dc-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="2d5dc-254">Hello 매개 변수 값을 확인 한 다음 호출 하는 hello **Publish-webpackage** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="2d5dc-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2d5dc-255">Read-ConfigFile</span></span> |<span data-ttu-id="2d5dc-256">Hello JSON 구성 파일의 유효성을 검사 하 고 선택한 값의 해시 테이블을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="2d5dc-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="2d5dc-257">Restore-Subscription</span></span> |<span data-ttu-id="2d5dc-258">Hello 현재 구독 toohello 원래 구독을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="2d5dc-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="2d5dc-259">Test-AzureModule</span></span> |<span data-ttu-id="2d5dc-260">반환 `$true` 경우 hello 설치 된 Azure 모듈 버전이 0.7.4 이상.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="2d5dc-261">반환 `$false` 경우 hello 모듈이 설치 되지 않았거나 이전 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="2d5dc-262">이 함수에는 매개 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-262">This function has no parameters.</span></span> |
| <span data-ttu-id="2d5dc-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="2d5dc-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="2d5dc-264">반환 `$true` 경우 hello hello Azure 모듈 버전이 0.7.4 이상.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="2d5dc-265">반환 `$false` 경우 hello 모듈이 설치 되지 않았거나 이전 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="2d5dc-266">이 함수에는 매개 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-266">This function has no parameters.</span></span> |
| <span data-ttu-id="2d5dc-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="2d5dc-267">Test-HttpsUrl</span></span> |<span data-ttu-id="2d5dc-268">Hello 입력된 URL tooa System.Uri 개체로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="2d5dc-269">반환 `$True` hello URL이 절대 주소이 고 스키마가 https 경우.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="2d5dc-270">반환 `$false` 경우 hello URL은 상대의 구성표가 HTTPS가 아니거나 입력된 문자열 hello 변환된 tooa URL 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="2d5dc-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="2d5dc-271">Test-Member</span></span> |<span data-ttu-id="2d5dc-272">반환 `$true` 메서드나 속성에 hello 개체의 멤버 이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="2d5dc-273">그렇지 않으면 `$false`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="2d5dc-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="2d5dc-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="2d5dc-275">Hello로 현재 시간을 접두사로 한 오류 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="2d5dc-276">이 함수 호출 hello **Format-devtestmessagewithtime** hello 메시지 toohello 오류 스트림에 쓰기 전에 함수 tooprepend hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="2d5dc-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="2d5dc-277">Write-HostWithTime</span></span> |<span data-ttu-id="2d5dc-278">메시지 toohello 호스트 프로그램 씁니다 (**Write-host**) 접두사로 hello 현재 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="2d5dc-279">hello toohello 호스트 프로그램을 작성 효과 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="2d5dc-280">대부분의 프로그램 Windows PowerShell을 호스팅하는 이러한 메시지에 기록 toostandard 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="2d5dc-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="2d5dc-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="2d5dc-282">Hello로 현재 시간을 접두사로 한 자세한 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="2d5dc-283">호출 하므로 **Write-verbose**, hello 메시지 hello 스크립트를 실행할 때만 hello로 표시 됩니다. **Verbose** 매개 변수 또는 때 환영 **VerbosePreference** 기본 설정이입니다 도**계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="2d5dc-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="2d5dc-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="2d5dc-285">함수 이름</span><span class="sxs-lookup"><span data-stu-id="2d5dc-285">Function name</span></span> | <span data-ttu-id="2d5dc-286">설명</span><span class="sxs-lookup"><span data-stu-id="2d5dc-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d5dc-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="2d5dc-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="2d5dc-288">웹 사이트, 가상 컴퓨터와 같은 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="2d5dc-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="2d5dc-289">New-WebDeployPackage</span></span> |<span data-ttu-id="2d5dc-290">이 함수는 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-290">This function isn't implemented.</span></span> <span data-ttu-id="2d5dc-291">추가할 수 있습니다 명령에서이 함수 toobuild 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="2d5dc-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="2d5dc-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="2d5dc-293">웹 응용 프로그램 tooAzure를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="2d5dc-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="2d5dc-294">Publish-WebApplication</span></span> |<span data-ttu-id="2d5dc-295">Visual Studio 웹 프로젝트를 위한 웹 앱, 가상 컴퓨터, SQL 데이터베이스, 저장소 계정을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="2d5dc-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="2d5dc-296">Test-WebApplication</span></span> |<span data-ttu-id="2d5dc-297">이 함수는 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-297">This function isn't implemented.</span></span> <span data-ttu-id="2d5dc-298">있습니다 수에 명령을 추가 함수 tootest이 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2d5dc-299">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d5dc-299">Next steps</span></span>
<span data-ttu-id="2d5dc-300">참조 하 여 PowerShell 스크립트에 대 한 자세한 [Windows PowerShell과 함께 스크립팅](https://technet.microsoft.com/library/bb978526.aspx) hello에서 다른 Azure PowerShell 스크립트를 참조 하 고 [스크립트 센터](https://azure.microsoft.com/documentation/scripts/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d5dc-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
