---
title: "Linux의 Azure App Service Web App에서 Ruby 사용 | Microsoft Docs"
description: "Linux의 Azure App Service Web App에서 Ruby 사용"
keywords: "azure app service, 웹앱, faq, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="02bc9-104">Linux의 웹앱에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="02bc9-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="02bc9-105">백 엔드 최신 업데이트에서는 Ruby v.2.3에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="02bc9-106">Linux 웹앱의 구성을 설정하여 응용 프로그램 스택을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="02bc9-107">Azure 포털 사용</span><span class="sxs-lookup"><span data-stu-id="02bc9-107">Using the Azure portal</span></span> ##

<span data-ttu-id="02bc9-108">[Azure Portal](https://portal.azure.com)의 새 메뉴에서 다음 이미지에 나와 있는 것처럼 Web + Mobile 옵션에서 Linux에 Web App을 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Azure Portal에서 웹앱 만들기][1]

<span data-ttu-id="02bc9-110">그러면 다음 그림과 같이 **만들기** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![만들기 블레이드][2]

1. <span data-ttu-id="02bc9-112">웹앱에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-112">Give your web app a name.</span></span>
2. <span data-ttu-id="02bc9-113">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="02bc9-114">([제한 사항 섹션](app-service-linux-intro.md)에서 사용 가능한 지역 참조)</span><span class="sxs-lookup"><span data-stu-id="02bc9-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="02bc9-115">기존 Azure App Service 계획을 선택하거나 새 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="02bc9-116">([제한 사항 섹션](app-service-linux-intro.md)에서 App Service 정보 참조)</span><span class="sxs-lookup"><span data-stu-id="02bc9-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="02bc9-117">기본 제공 런타임 스택에서 Ruby를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="02bc9-118">Ruby 웹앱이 만들어지면 Git 또는 FTP를 사용하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02bc9-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="02bc9-119">Ruby 앱 만들기에 대한 자세한 내용은 [시작 가이드](app-service-linux-ruby-get-started.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="02bc9-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="02bc9-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02bc9-120">Next steps</span></span>
* [<span data-ttu-id="02bc9-121">Linux의 웹앱이란?</span><span class="sxs-lookup"><span data-stu-id="02bc9-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="02bc9-122">Azure App Service에 대한 로컬 Git 배포</span><span class="sxs-lookup"><span data-stu-id="02bc9-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="02bc9-123">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="02bc9-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="02bc9-124">Linux에서 Azure 웹앱을 사용하여 Ruby 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="02bc9-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png