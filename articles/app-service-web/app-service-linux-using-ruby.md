---
title: "Linux에서 Azure 앱 서비스 웹 앱에 대 한 Ruby aaaUsing | Microsoft Docs"
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
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="d73e4-104">Linux의 웹앱에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="d73e4-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="d73e4-105">Hello 최신 업데이트 tooour 백 엔드와 Ruby v.2.3에 대 한 지원이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="d73e4-106">Linux 웹 응용 프로그램의 hello 구성을 설정 하 여 응용 프로그램 스택의 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="d73e4-107">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d73e4-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="d73e4-108">Hello에 hello 새로 만들기 메뉴에서 [Azure 포털](https://portal.azure.com)에서 선택할 수 있습니다 toocreate Linux에서 웹 응용 프로그램 안녕하세요 웹 + 모바일 옵션 hello 다음 이미지에에서 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="d73e4-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Hello Azure 포털에서 웹 앱을 만들기 시작][1]

<span data-ttu-id="d73e4-110">다음으로 hello **만들기 블레이드** hello 다음 이미지와 같이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![hello 만들기 블레이드][2]

1. <span data-ttu-id="d73e4-112">웹앱에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-112">Give your web app a name.</span></span>
2. <span data-ttu-id="d73e4-113">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="d73e4-114">(사용 가능한 지역이 hello에 [제한 사항 섹션](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="d73e4-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="d73e4-115">기존 Azure App Service 계획을 선택하거나 새 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="d73e4-116">(Hello에 앱 서비스 계획을 참조 하십시오 [제한 사항 섹션](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="d73e4-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="d73e4-117">기본 제공 된 런타임 스택 hello에서에서 Ruby hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="d73e4-118">Ruby 웹 앱을 생성 한 후 tooit Git 또는 FTP를 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73e4-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="d73e4-119">에 대해 더 알아봅니다 toolearn hello 확인 Ruby 앱을 만들어 [get 시작된 가이드](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="d73e4-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d73e4-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d73e4-120">Next steps</span></span>
* [<span data-ttu-id="d73e4-121">Linux의 웹앱이란?</span><span class="sxs-lookup"><span data-stu-id="d73e4-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="d73e4-122">로컬 Git 배포 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="d73e4-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="d73e4-123">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="d73e4-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="d73e4-124">Linux에서 Azure 웹앱을 사용하여 Ruby 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d73e4-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png