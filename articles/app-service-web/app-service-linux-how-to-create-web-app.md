---
title: "Linux에서 실행되는 Azure Web App 만들기 | Microsoft Docs"
description: "Linux의 Azure Web App용 웹앱 만들기 워크플로"
keywords: "azure app service, 웹앱, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="11c33-104">Linux에서 실행되는 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="11c33-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="11c33-105">Azure Portal을 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="11c33-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="11c33-106">다음 그림에 나와 있는 것처럼 [Azure Portal](https://portal.azure.com)에서 Linux의 웹앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Azure Portal에서 웹앱 만들기][1]

<span data-ttu-id="11c33-108">그러면 다음 그림과 같이 **만들기** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![만들기 블레이드][2]

1. <span data-ttu-id="11c33-110">웹앱에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-110">Give your web app a name.</span></span>
2. <span data-ttu-id="11c33-111">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="11c33-112">([제한 사항 섹션](app-service-linux-intro.md)에서 사용 가능한 지역 참조)</span><span class="sxs-lookup"><span data-stu-id="11c33-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="11c33-113">기존 Azure App Service 계획을 선택하거나 새 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="11c33-114">([제한 사항 섹션](app-service-linux-intro.md)에서 App Service 정보 참조)</span><span class="sxs-lookup"><span data-stu-id="11c33-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="11c33-115">사용하려는 응용 프로그램 스택을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="11c33-116">여러 버전의 Node.js, PHP, .Net Core, Ruby 중에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="11c33-117">앱을 만든 후 다음 그림에 나와 있는 것처럼 응용 프로그램 설정에서 응용 프로그램 스택을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![응용 프로그램 설정][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="11c33-119">웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="11c33-119">Deploy your web app</span></span>
<span data-ttu-id="11c33-120">관리 포털에서 **배포 옵션**을 선택하면 로컬 Git 또는 GitHub 리포지토리를 사용하여 응용 프로그램을 배포하기 위한 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="11c33-121">나머지 설명은 비 Linux 웹앱과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="11c33-122">[로컬 Git 배포](app-service-deploy-local-git.md) 또는 [연속 배포](app-service-continuous-deployment.md)의 지침에 따라 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="11c33-123">또한 FTP를 사용하여 사이트에 응용 프로그램을 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="11c33-124">다음 그림에 나와 있는 것처럼 진단 로그 섹션에서 웹앱에 대한 FTP 끝점을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11c33-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![진단 로그][4]

## <a name="next-steps"></a><span data-ttu-id="11c33-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11c33-126">Next steps</span></span>
* [<span data-ttu-id="11c33-127">Linux에서 Azure Web App이란?</span><span class="sxs-lookup"><span data-stu-id="11c33-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="11c33-128">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="11c33-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="11c33-129">Linux의 Azure App Service Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="11c33-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="11c33-130">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="11c33-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
