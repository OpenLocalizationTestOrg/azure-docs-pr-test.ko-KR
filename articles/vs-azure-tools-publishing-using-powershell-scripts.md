---
title: "개발 및 테스트 환경에 게시하기 위해 Windows PowerShell 스크립트 사용하기 | Microsoft Docs"
description: "Visual Studio에서 Windows PowerShell 스크립트를 사용하여 개발 및 테스트 환경에 게시하는 방법을 알아보세요."
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
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="e9245-103">Windows PowerShell 스크립트를 사용하여 개발 및 테스트 환경에 게시</span><span class="sxs-lookup"><span data-stu-id="e9245-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="e9245-104">Visual Studio에서 웹 응용 프로그램을 만들 경우 Windows PowerShell 스크립트를 만든 다음 나중에 Azure에 Azure 앱 서비스 또는 가상 컴퓨터로 웹 사이트 게시를 자동화하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="e9245-105">Visual Studio 편집기에서 요구 사항에 맞게 Windows PowerShell 스크립트를 편집 및 확장하거나 스크립트를 기존 빌드, 테스트, 게시 스크립트와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="e9245-106">이러한 스크립트를 사용하면 일시적으로 사용할 사이트의 사용자 지정 버전(개발 및 테스트 환경이라고도 함)을 프로비저닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="e9245-107">예를 들어 Azure 가상 컴퓨터 또는 웹 사이트의 스테이징 슬롯에 특정 버전의 웹 사이트를 설정하고 테스트 제품군 실행, 버그 재현, 버그 수정 사항 테스트, 제안된 변경 사항 시험, 데모 또는 프레젠테이션을 위한 사용자 지정 환경 설정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="e9245-108">프로젝트를 게시하는 스크립트를 만든 다음 필요에 따라 스크립트를 다시 실행하여 동일한 환경을 다시 만들거나 웹 응용 프로그램의 자체 빌드로 스크립트를 실행하여 테스트를 위한 사용자 지정 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9245-109">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e9245-109">What you need</span></span>
* <span data-ttu-id="e9245-110">Azure SDK 2.3 이상</span><span class="sxs-lookup"><span data-stu-id="e9245-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="e9245-111">자세한 내용은 [Visual Studio 다운로드](http://go.microsoft.com/fwlink/?LinkID=624384)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="e9245-112">웹 프로젝트의 스크립트를 생성하기 위해 Azure SDK는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="e9245-113">이 기능은 클라우드 서비스의 웹 역할이 아닌 웹 프로젝트용입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="e9245-114">Azure PowerShell 0.7.4 이상</span><span class="sxs-lookup"><span data-stu-id="e9245-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="e9245-115">자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="e9245-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) 이상</span><span class="sxs-lookup"><span data-stu-id="e9245-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="e9245-117">추가 도구</span><span class="sxs-lookup"><span data-stu-id="e9245-117">Additional tools</span></span>
<span data-ttu-id="e9245-118">Azure 개발 시 Visual Studio에서 PowerShell을 사용하기 위한 추가 도구와 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="e9245-119">[Visual Studio용 PowerShell](http://go.microsoft.com/fwlink/?LinkId=404012)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="e9245-120">게시 스크립트 생성</span><span class="sxs-lookup"><span data-stu-id="e9245-120">Generating the publish scripts</span></span>
<span data-ttu-id="e9245-121">새 프로젝트를 만들 때 [이 지침](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 따라 웹 사이트를 호스팅하는 가상 컴퓨터의 게시 스크립트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e9245-122">또한 [Azure App Service에서 웹앱용 게시 스크립트를 생성](app-service-web/app-service-web-get-started-dotnet.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="e9245-123">Visual Studio에서 생성하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="e9245-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="e9245-124">Visual Studio는 2개의 Windows PowerShell 파일이 포함되어 있는 솔루션 수준 폴더 **PublishScripts** , 가상 컴퓨터 또는 웹 사이트의 게시 스크립트, 스크립트에 사용할 수 있는 함수가 포함된 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="e9245-125">Visual Studio는 또한 배포하는 프로젝트의 상세 정보를 지정하는 JSON 형식으로 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="e9245-126">Windows PowerShell 게시 스크립트</span><span class="sxs-lookup"><span data-stu-id="e9245-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="e9245-127">게시 스크립트에는 웹 사이트 또는 가상 컴퓨터에 배포하기 위한 구체적 게시 단계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="e9245-128">Visual Studio는 Windows PowerShell 배포를 위한 구문 색 지정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="e9245-129">함수의 도움말을 사용할 수 있으며 달라진 요구 사항에 맞게 스크립트의 함수를 자유롭게 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="e9245-130">Windows PowerShell 모듈</span><span class="sxs-lookup"><span data-stu-id="e9245-130">Windows PowerShell module</span></span>
<span data-ttu-id="e9245-131">Visual Studio에서 생성하는 Windows PowerShell 모듈에는 게시 스크립트가 사용하는 함수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="e9245-132">이러한 함수는 Azure PowerShell 함수이며 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="e9245-133">자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="e9245-134">JSON 구성 파일</span><span class="sxs-lookup"><span data-stu-id="e9245-134">JSON configuration file</span></span>
<span data-ttu-id="e9245-135">JSON 파일은 **Configurations** 폴더에 생성되며 Azure에 배포할 리소스를 정확히 지정하는 구성 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="e9245-136">웹 사이트를 만든 경우 Visual Studio가 생성하는 파일의 이름은 project-name-WAWS-dev.json이며 가상 컴퓨터를 만든 경우에는 project name-VM-dev.json입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="e9245-137">다음은 웹 사이트를 만들 때 생성된 JSON 구성 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="e9245-138">대부분의 값은 따로 설명이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="e9245-139">웹 사이트 이름은 Azure에서 생성하므로 프로젝트 이름과 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-139">The website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="e9245-140">가상 컴퓨터를 만들면 JSON 구성 파일이 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="e9245-141">클라우드 서비스가 가상 컴퓨터의 컨테이너로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="e9245-142">가상 컴퓨터에 HTTP 및 HTTPS를 통한 웹 액세스에 사용할 일반적 끝점이 포함되어 있으며, 웹 배포용 끝점도 포함되어 있어 로컬 컴퓨터, 원격 데스크톱 및 Windows PowerShell에서 웹 사이트에 게시할 수 잇습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="e9245-143">JSON 구성을 편집하여 게시 스크립트를 실행할 때 발생하는 결과를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="e9245-144">`cloudService` 및 `virtualMachine` 섹션은 필수이며 `databases` 섹션은 필요하지 않을 경우 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="e9245-145">Visual Studio에서 생성한 기본 구성 파일에 비어 있는 속성은 선택 사항입니다. 기본 구성 파일에 값이 있는 속성은 필수 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="e9245-146">Azure에 단일 프로덕션 사이트가 아닌 여러 배포 환경(슬롯이라고 함)이 포함된 웹 사이트가 있을 경우 JSON 구성 파일에서 웹 사이트 이름에 슬롯 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="e9245-147">예를 들어 이름이 **mysite**인 웹 사이트와 **test**라는 슬롯이 있을 경우 URI는 mysite-test.cloudapp.net이지만 구성 파일에서 사용해야 할 올바른 이름은 mysite(test)입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="e9245-148">구독에 웹 사이트와 슬롯이 이미 있는 경우에만 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="e9245-149">없을 경우에는 슬롯을 지정하지 않고 스크립트를 실행한 다음 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에 슬롯을 만들고 수정한 웹 사이트 이름으로 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="e9245-150">웹앱의 배포 슬롯에 대한 자세한 내용은 [Azure App Service에서 웹앱에 대한 스테이징 환경 설정](app-service-web/web-sites-staged-publishing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="e9245-151">게시 스크립트 실행 방법</span><span class="sxs-lookup"><span data-stu-id="e9245-151">How to run the publish scripts</span></span>
<span data-ttu-id="e9245-152">이전에 Windows PowerShell 스크립트를 실행한 적이 없는 경우 우선 스크립트를 실행할 수 있도록 실행 정책을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="e9245-153">이 기능은 사용자가 맬웨어 또는 바이러스에 취약한 Windows PowerShell 스크립트를 실행하지 못하도록 방지하는 보안 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="e9245-154">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="e9245-154">Run the script</span></span>
1. <span data-ttu-id="e9245-155">프로젝트의 웹 배포 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="e9245-156">웹 배포 패키지는 웹 사이트 또는 가상 컴퓨터에 복사하려는 파일이 포함된 압축 아카이브(.zip 파일)입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="e9245-157">Visual Studio에서 모든 웹 응용 프로그램에 사용할 웹 배포 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![웹 배포 패키지 만들기](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="e9245-159">자세한 내용은 [방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="e9245-160">또한 이 항목의 뒷부분의 **게시 스크립트 사용자 지정 및 확장** 섹션에서 설명하는 대로 웹 배포 패키지 생성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="e9245-161">**솔루션 탐색기**에서 스크립트의 상황에 맞는 메뉴를 연 다음 **PowerShell ISE로 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="e9245-162">이 컴퓨터에서 Windows PowerShell 스크립트를 처음으로 실행하는 경우 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="e9245-163">다음 명령을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="e9245-164">메시지가 표시되면 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="e9245-165">스크립트를 자동화하면 이 방법으로 Azure 자격 증명을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="e9245-166">대신 .publishsettings 파일을 사용하여 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="e9245-167">한 번만 **Get-AzurePublishSettingsFile** 명령을 사용하여 Azure에서 파일을 다운로드한 다음 **Import-AzurePublishSettingsFile**을 사용하여 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="e9245-168">자세한 지침은 [Azure PoweShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="e9245-169">(선택 사항) 웹 응용 프로그램을 게시하지 않고 가상 컴퓨터, 데이터베이스, 웹 사이트와 같은 Azure 리소스를 만들려면 **-Configuration** 인수를 JSON 구성 파일로 설정하고 **Publish-WebApplication.ps1** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="e9245-170">이 명령줄은 JSON 구성 파일을 사용하여 만들 리소스를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="e9245-171">여기서 다른 명령줄 인스턴스에 대해 기본 설정을 사용하므로 리소스를 만들지만 웹 응용 프로그램을 게시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="e9245-172">–Verbose 옵션으로 진행 상황에 대한 자세한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="e9245-173">다음 예제 중 하나와 같이 **Publish-WebApplication.ps1** 명령을 사용하여 스크립트를 호출하고 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="e9245-174">구독 이름, 게시 패키지 이름, 가상 컴퓨터 자격 증명, 데이터베이스 서버 자격 증명과 같은 다른 인수의 기본 설정을 재정의하려면 이러한 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="e9245-175">게시 프로세스의 진행률을 자세히 보려면 **-Verbose** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="e9245-176">가상 컴퓨터를 만드는 경우 다음과 유사한 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="e9245-177">이 예제는 여러 데이터베이스의 자격 증명을 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="e9245-178">이러한 스크립트가 만드는 가상 컴퓨터에서 SSL 인증서는 신뢰할 수 있는 루트 인증 기관에서 제공한 인증서가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="e9245-179">따라서 **–AllowUntrusted** 옵션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="e9245-180">스크립트가 데이터베이스를 만들 수 있지만 데이터베이스 서버는 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="e9245-181">데이터베이스 서버를 만들려면 Azure 모드에서 **New-AzureSqlDatabaseServer** 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="e9245-182">게시 스크립트 사용자 지정 및 확장</span><span class="sxs-lookup"><span data-stu-id="e9245-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="e9245-183">게시 스크립트 및 JSON 구성 파일을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="e9245-184">Windows PowerShell 모듈 **AzureWebAppPublishModule.psm1** 의 함수는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="e9245-185">다른 데이터베이스를 지정하거나 가상 컴퓨터의 일부 속성을 변경하려면 JSON 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="e9245-186">스크립트의 기능을 확장하여 프로젝트 빌드 및 테스트를 자동화하려면 **Publish-WebApplication.ps1**에 함수 스텁을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="e9245-187">프로젝트 빌드를 자동화하려면 이 코드 예제와 같이 `New-WebDeployPackage` 에 MSBuild를 호출하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="e9245-188">MSBuild 명령에 대한 경로는 설치한 Visual Studio 버전에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="e9245-189">올바른 경로를 가져오려면 이 예제와 같이 **Get-MSBuildCmd**함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="e9245-190">프로젝트 빌드를 자동화하려면</span><span class="sxs-lookup"><span data-stu-id="e9245-190">To automate building your project</span></span>
1. <span data-ttu-id="e9245-191">전역 param 섹션에 `$ProjectFile` 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="e9245-192">`Get-MSBuildCmd` 함수를 스크립트 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="e9245-193">`New-WebDeployPackage`을(를) 다음 코드로 바꾸고 `$msbuildCmd` 생성 줄에서 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="e9245-194">이 코드는 Visual Studio 2015용입니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="e9245-195">Visual Studio 2013을 사용하는 경우 **VisualStudioVersion** 속성을 `12.0` 미만으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="e9245-196">웹 응용 프로그램을 빌드하려면 MsBuild.exe를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="e9245-197">도움말은 [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)에서 MSBuild 명령줄을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="e9245-198">빌드 명령 실행 시작</span><span class="sxs-lookup"><span data-stu-id="e9245-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="e9245-199">이 줄보다 먼저 `New-WebDeployPackage` 함수를 호출합니다. 웹 앱의 경우 `$Config = Read-ConfigFile $Configuration`, 가상 컴퓨터의 경우 `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)`.</span><span class="sxs-lookup"><span data-stu-id="e9245-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="e9245-200">다음 예제 명령줄과 같이 `$Project` 인수 전달을 사용하여 명령줄에서 사용자 지정 스크립트를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="e9245-201">응용 프로그램 테스트를 자동화하려면 `Test-WebApplication`에 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="e9245-202">이러한 함수가 호출되는 **Publish-WebApplication.ps1** 의 줄에서 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="e9245-203">구현을 제공하지 않을 경우 Visual Studio로 프로젝트를 수동으로 빌드한 다음 게시 스크립트를 실행하여 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="e9245-204">게시 함수 요약</span><span class="sxs-lookup"><span data-stu-id="e9245-204">Publishing function summary</span></span>
<span data-ttu-id="e9245-205">Windows PowerShell 명령 프롬프트에서 사용할 수 있는 함수에 대한 도움말을 보려면 `Get-Help function-name`명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="e9245-206">도움말에는 매개 변수 도움말과 예제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="e9245-207">동일한 도움말 텍스트가 스크립트 원본 파일인 **AzureWebAppPublishModule.psm1** 및 **Publish-WebApplication.ps1**에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="e9245-208">스크립트와 도움말은 Visual Studio 언어로 현지화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="e9245-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="e9245-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="e9245-210">함수 이름</span><span class="sxs-lookup"><span data-stu-id="e9245-210">Function name</span></span> | <span data-ttu-id="e9245-211">설명</span><span class="sxs-lookup"><span data-stu-id="e9245-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9245-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="e9245-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="e9245-213">새 Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="e9245-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="e9245-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="e9245-215">Visual Studio에서 생성하는 JSON 구성 파일의 값으로 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="e9245-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e9245-216">Add-AzureVM</span></span> |<span data-ttu-id="e9245-217">Azure 가상 컴퓨터를 만들고 배포된 VM의 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="e9245-218">함수가 필수 구성 요소를 설정한 다음 **New-AzureVM** 함수(Azure 모듈)를 호출하여 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="e9245-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="e9245-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="e9245-220">가상 컴퓨터에 새 입력 끝점을 추가하고 새 끝점으로 가상 컴퓨터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="e9245-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e9245-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="e9245-222">현재 구독에 새 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="e9245-223">계정 이름은 "devtest"로 시작하고 그 다음에 고유한 영숫자 문자열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="e9245-224">함수에서 새 저장소 계정의 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="e9245-225">새 저장소 계정에 대해 위치 또는 선호도 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="e9245-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="e9245-226">Add-AzureWebsite</span></span> |<span data-ttu-id="e9245-227">지정된 이름 및 위치로 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="e9245-228">이 함수는 Azure 모듈에서 **New-AzureWebsite** 함수라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="e9245-229">구독에 이미 지정된 이름의 웹 사이트가 없을 경우 이 함수는 웹 사이트를 만들고 웹 사이트 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="e9245-230">그렇지 않으면 `$null`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="e9245-231">백업-구독</span><span class="sxs-lookup"><span data-stu-id="e9245-231">Backup-Subscription</span></span> |<span data-ttu-id="e9245-232">현재 Azure 구독을 스크립트 범위의 `$Script:originalSubscription` 변수에 저장합니다. 이 함수는 현재 Azure 구독(`Get-AzureSubscription -Current`에서 가져옴) 및 해당 저장소 계정, 이 스크립트로 변경된 구독(`$UserSpecifiedSubscription` 변수에 저장) 및 해당 저장소 계정을 스크립트 범위에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="e9245-233">이러한 값을 저장하면 원래 현재 상태가 변경된 경우 `Restore-Subscription` 등의 함수를 사용하여 현재 구독 및 저장소 계정을 현재 상태로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="e9245-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e9245-234">Find-AzureVM</span></span> |<span data-ttu-id="e9245-235">지정된 Azure 가상 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="e9245-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="e9245-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="e9245-237">메시지 앞에 날짜와 시간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="e9245-238">이 함수는 오류 및 자세한 정보 표시 스트림에 작성되는 메시지를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="e9245-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="e9245-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="e9245-240">연결 문자열을 조립하여 Azure SQL 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="e9245-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e9245-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="e9245-242">지정된 위치 또는 선호도 그룹에 이름 패턴이 "devtest*"(대소문자 구분)인 첫 번째 저장소 계정의 이름을 반환합니다. "devtest*" 저장소 계정이 위치 또는 선호도 그룹과 일치하지 않을 경우 함수에서 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="e9245-243">위치 또는 선호도 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="e9245-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="e9245-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="e9245-245">MsDeploy.exe 도구를 실행하는 명령을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="e9245-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="e9245-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="e9245-247">JSON 구성 파일의 값과 일치하는 구독에서 가상 컴퓨터를 검색하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="e9245-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="e9245-248">Publish-WebPackage</span></span> |<span data-ttu-id="e9245-249">MsDeploy.exe 및 웹 게시 패키지인 .Zip 파일을 사용하여 리소스를 웹 사이트에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="e9245-250">이 함수는 출력을 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-250">This function doesn't generate any output.</span></span> <span data-ttu-id="e9245-251">MSDeploy.exe에 대한 호출이 실패할 경우 함수가 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="e9245-252">더 자세한 출력을 가져오려면 **-Verbose** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="e9245-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="e9245-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="e9245-254">매개 변수 값을 확인한 다음 **Publish-WebPackage** 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="e9245-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e9245-255">Read-ConfigFile</span></span> |<span data-ttu-id="e9245-256">JSON 구성 파일의 유효성을 검사하고 선택한 값의 해시 테이블을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="e9245-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="e9245-257">Restore-Subscription</span></span> |<span data-ttu-id="e9245-258">현재 구독을 원래 구독으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="e9245-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="e9245-259">Test-AzureModule</span></span> |<span data-ttu-id="e9245-260">설치된 Azure 모듈 버전이 0.7.4 이상인 경우 `$true` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="e9245-261">모듈이 설치되지 않았거나 이전 버전인 경우 `$false` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e9245-262">이 함수에는 매개 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-262">This function has no parameters.</span></span> |
| <span data-ttu-id="e9245-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="e9245-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="e9245-264">Azure 모듈의 버전이 0.7.4 이상인 경우 `$true` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="e9245-265">모듈이 설치되지 않았거나 이전 버전인 경우 `$false` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e9245-266">이 함수에는 매개 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-266">This function has no parameters.</span></span> |
| <span data-ttu-id="e9245-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="e9245-267">Test-HttpsUrl</span></span> |<span data-ttu-id="e9245-268">입력 URL을 System.Uri 개체로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="e9245-269">URL이 절대적이고 해당 스키마가 https인 경우 `$True` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="e9245-270">URL이 상대적이고 해당 스키마가 HTTPS가 아니거나 입력 문자열을 URL로 변환할 수 없을 경우 `$false` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="e9245-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="e9245-271">Test-Member</span></span> |<span data-ttu-id="e9245-272">속성 또는 메서드가 개체의 구성원인 경우 `$true` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="e9245-273">그렇지 않으면 `$false`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="e9245-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="e9245-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="e9245-275">현재 시간을 접두사로 하는 오류 메시지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="e9245-276">이 함수는 **Format-DevTestMessageWithTime** 함수를 호출하고 메시지를 쓰기 전의 시간을 오류 스트림 앞에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="e9245-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="e9245-277">Write-HostWithTime</span></span> |<span data-ttu-id="e9245-278">현재 시간을 접두사로 하는 호스트 프로그램(**Write-Host**)에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="e9245-279">호스트 프로그램에 쓰는 효과는 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="e9245-280">Windows PowerShell을 호스팅하는 대부분의 프로그램은 이러한 메시지를 표준 출력에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="e9245-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="e9245-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="e9245-282">현재 시간을 접두사로 하는 자세한 정보 메시지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="e9245-283">이 함수는 **Write-Verbose**를 호출하므로 **Verbose** 매개 변수로 스크립트가 실행되거나 **VerbosePreference** 기본 설정이 **계속**으로 설정된 경우에만 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="e9245-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="e9245-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="e9245-285">함수 이름</span><span class="sxs-lookup"><span data-stu-id="e9245-285">Function name</span></span> | <span data-ttu-id="e9245-286">설명</span><span class="sxs-lookup"><span data-stu-id="e9245-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9245-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="e9245-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="e9245-288">웹 사이트, 가상 컴퓨터와 같은 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="e9245-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="e9245-289">New-WebDeployPackage</span></span> |<span data-ttu-id="e9245-290">이 함수는 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-290">This function isn't implemented.</span></span> <span data-ttu-id="e9245-291">이 함수에 명령을 추가하여 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="e9245-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="e9245-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="e9245-293">Azure에 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="e9245-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e9245-294">Publish-WebApplication</span></span> |<span data-ttu-id="e9245-295">Visual Studio 웹 프로젝트를 위한 웹 앱, 가상 컴퓨터, SQL 데이터베이스, 저장소 계정을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="e9245-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e9245-296">Test-WebApplication</span></span> |<span data-ttu-id="e9245-297">이 함수는 구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-297">This function isn't implemented.</span></span> <span data-ttu-id="e9245-298">이 함수에 명령을 추가하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9245-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9245-299">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9245-299">Next steps</span></span>
<span data-ttu-id="e9245-300">[Windows PowerShell을 사용하여 스크립팅](https://technet.microsoft.com/library/bb978526.aspx)을 읽어 PowerShell 스크립팅에 대해 자세히 알아보고 [스크립트 센터](https://azure.microsoft.com/documentation/scripts/)에서 기타 Azure PowerShell 스크립트에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e9245-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
