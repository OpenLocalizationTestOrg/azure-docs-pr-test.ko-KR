---
title: "Azure 앱 서비스 웹 앱과 aaaHow toouse io.js"
description: "자세한 내용은 방법 toouse io.js에 Azure 앱 서비스의 웹 앱입니다."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="e067d-103">방법 및 Azure 앱 서비스 웹 앱 toouse io.js</span><span class="sxs-lookup"><span data-stu-id="e067d-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="e067d-104">hello 인기 있는 노드 포크 [io.js] 다양 한 차이 tooJoyent Node.js 프로젝트를 보다 개방적 거 버 넌 스 모델, 더 빠른 릴리스 주기 및 더 빠른 단기간 새 실험적 JavaScript 기능을 포함 하 여 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="e067d-105">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps에는 많은 Node.js 버전이 미리 설치되어 있지만 사용자가 제공한 Node.js 이진 파일도 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="e067d-106">이 문서에서는 앱 서비스 웹 앱에 io.js hello 사용 하도록 설정 하는 두 가지 방법: hello io.js 이진 파일의 수동 업로드에 hello 뿐만 아니라 Azure toouse hello 최신 사용 가능한 io.js 버전을 자동으로 구성 하는 확장된 배포 스크립트의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="e067d-107">배포 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="e067d-107">Using a Deployment Script</span></span>
<span data-ttu-id="e067d-108">Node.js 응용 프로그램의 배포 시 응용 프로그램 서비스 웹 앱 환경을 hello tooensure가 올바르게 구성 하는 작은 명령의 수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="e067d-109">이 프로세스는 배포 스크립트를 사용 하 여 사용자 지정 된 tooinclude hello 다운로드 및 io.js의 구성을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="e067d-110">hello [io.js 배포 스크립트](https://github.com/felixrieseberg/iojs-azure) GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="e067d-111">웹 앱에 tooenable io.js 복사 하기만 하면 **.deployment**, **deploy.cmd** 및 **IISNode.yml** 응용 프로그램 폴더의 toohello 루트 tooWeb 앱 및 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="e067d-112">hello 첫 번째 파일 **.deployment**, 웹 앱 toorun 지시 **deploy.cmd** 배포 시.</span><span class="sxs-lookup"><span data-stu-id="e067d-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="e067d-113">이 스크립트는 Node.js 응용 프로그램에 대 한 모든 hello 일반적인 단계를 실행 하지만 또한 hello io.js의 최신 버전을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="e067d-114">마지막으로, **IISNode.yml** 웹 앱 toouse 다운로드 정당한 hello io.js 사전 설치 된 Node.js 이진 대신 이진을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="e067d-115">tooupdate hello io.js 이진 파일을 사용 하 고 응용 프로그램을 다시 배포 하면-hello 스크립트 io.js 마다 한 번 hello 응용 프로그램 배포의 새 버전을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="e067d-116">수동 설치 사용</span><span class="sxs-lookup"><span data-stu-id="e067d-116">Using Manual Installation</span></span>
<span data-ttu-id="e067d-117">사용자 지정 io.js 버전의 hello 수동 설치에만 두 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="e067d-118">먼저, hello 다운로드 **win x64** hello에서 직접 이진 [io.js 배포]합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="e067d-119">**iojs.exe** 및 **iojs.lib** 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="e067d-120">모두 저장 웹 응용 프로그램 내의 tooa 폴더 예의 파일 **bin/iojs**합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="e067d-121">웹 앱 toouse tooconfigure **iojs.exe** 사전 설치 된 노드 버전을 대신 만듭니다는 **IISNode.yml** 응용 프로그램의 hello 루트에 있는 파일 및 hello 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="e067d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e067d-122">Next Steps</span></span>
<span data-ttu-id="e067d-123">이 문서에서 toouse io.js 앱 서비스 웹 앱을 모두 사용 하 여 사용 배포 스크립트 뿐 아니라 수동 설치를 제공 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="e067d-124">io.js는 집중적으로 개발되고 있으며, Node.js보다 자주 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="e067d-125">여러 Node.js 모듈이 io.js와 함께 작동하지 않을 수 있으므로 문제 해결은 [GitHub의 io.js] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e067d-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e067d-126">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="e067d-126">What's changed</span></span>
* <span data-ttu-id="e067d-127">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e067d-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="e067d-128">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e067d-129">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e067d-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js 배포]: https://iojs.org/dist/
[GitHub의 io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
