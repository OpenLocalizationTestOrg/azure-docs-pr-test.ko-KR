---
title: "Azure 포털을 사용 하 여 응용 프로그램 복제 aaaWeb"
description: "자세한 내용은 어떻게 tooclone 웹 응용 프로그램을 Azure 포털을 사용 하 여 웹 앱 toonew 합니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="e2e35-103">Azure 포털을 사용하여 Azure 앱 서비스 앱 복제</span><span class="sxs-lookup"><span data-stu-id="e2e35-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="e2e35-104">복제 기능에서 hello [Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714) 기존 웹 응용 프로그램 새로 만든 tooa 앱 또는 다른 지역에 쉽게 복제할 수 있습니다. 동일한 지역 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="e2e35-105">이렇게 쉽고 신속 하 게 서로 다른 지역의 여러 고객 toodeploy 수의 앱 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="e2e35-106">앱 복제는 현재 프리미엄 계층의 앱 서비스 계획에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="e2e35-107">새 기능 사용 hello hello 동일한 웹 앱 백업 기능으로, 제한 사항 참조 [Azure 앱 서비스의 웹 앱 백업](web-sites-backup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="e2e35-108">기존 앱 복제</span><span class="sxs-lookup"><span data-stu-id="e2e35-108">Cloning an existing App</span></span>
<span data-ttu-id="e2e35-109">hello에서 hello 웹 응용 프로그램을 실행 해야 **프리미엄** toocreate hello 웹 앱에 대 한 복제본을 위해에서 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="e2e35-110">Hello에 [Azure 포털](https://portal.azure.com/), 웹 앱 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="e2e35-111">**도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-111">Click **Tools**.</span></span> <span data-ttu-id="e2e35-112">그런 다음, hello **도구** 블레이드에서 클릭 **복제 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="e2e35-113">Hello 웹 앱에에서 없는 경우 이미 hello **프리미엄** 모드를 나타내는 응용 프로그램 복제에 대 한 지원 hello 모드는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="e2e35-114">이 시점에서 hello 옵션 tooselect를 있는 **업그레이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="e2e35-115">Hello에 **복제 앱** 블레이드 hello 새 웹 앱, 리소스 그룹 및 앱 서비스 계획의 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="e2e35-116">또한 hello 사용자 됩니다 수 toochoose 여부 tooclone 다양 한 소스 웹 응용 프로그램 설정 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="e2e35-117">클릭 한 후 **만들** hello 플랫폼 hello 소스 웹 응용 프로그램의 복제본을 만드는 방법에 대 한 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="e2e35-118">기존 앱 tooan 앱 서비스 환경 복제</span><span class="sxs-lookup"><span data-stu-id="e2e35-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="e2e35-119">Hello에 **복제 앱** 블레이드 hello 고객 hello 옵션 toochoose 기존 앱 서비스 환경에 응용 프로그램 풀 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="e2e35-120">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="e2e35-120">Current Restrictions</span></span>
<span data-ttu-id="e2e35-121">이 기능은 현재 미리 보기, 시간이 지남에 따라 tooadd 새로운 기능을 노력 하 고, hello 목록 다음에 Azure 포털에서 응용 프로그램 복제 hello 현재 지원에 대 한 알려진된 제한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="e2e35-122">Azure 트래픽 관리자 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="e2e35-123">자동 크기 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="e2e35-124">백업 일정 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="e2e35-125">VNET 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="e2e35-126">App Insights 설정 되지 않는 자동으로 hello 대상 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e2e35-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="e2e35-127">간편한 인증 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="e2e35-128">Kudu 확장은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="e2e35-129">TiP 규칙은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="e2e35-130">데이터베이스 내용이 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2e35-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="e2e35-131">참조</span><span class="sxs-lookup"><span data-stu-id="e2e35-131">References</span></span>
* [<span data-ttu-id="e2e35-132">PowerShell을 사용하여 웹앱 복제</span><span class="sxs-lookup"><span data-stu-id="e2e35-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="e2e35-133">Azure 앱 서비스에서 웹앱 백업</span><span class="sxs-lookup"><span data-stu-id="e2e35-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="e2e35-134">어떻게 tooCreate 앱 서비스 환경</span><span class="sxs-lookup"><span data-stu-id="e2e35-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="e2e35-135">App Service 환경에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e2e35-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="e2e35-136">소개 tooApp 서비스 환경</span><span class="sxs-lookup"><span data-stu-id="e2e35-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
