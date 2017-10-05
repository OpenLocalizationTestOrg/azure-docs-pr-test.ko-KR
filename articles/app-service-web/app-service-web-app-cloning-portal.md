---
title: "Azure 포털을 사용하여 웹앱 복제"
description: "Azure 포털을 사용하여 웹앱을 새 웹앱에 복제하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="38da5-103">Azure 포털을 사용하여 Azure 앱 서비스 앱 복제</span><span class="sxs-lookup"><span data-stu-id="38da5-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="38da5-104">[Azure 앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714) 에서 복제 기능을 사용하면 다른 지역 또는 같은 지역에 새로 만든 앱으로 기존 웹앱을 쉽게 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="38da5-105">이를 통해 고객은 수많은 앱을 다른 지역에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="38da5-106">앱 복제는 현재 프리미엄 계층의 앱 서비스 계획에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="38da5-107">새로운 기능은 웹앱 백업 기능과 동일한 제한 사항을 사용합니다. [Azure App Service에서 웹앱 백업](web-sites-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38da5-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="38da5-108">기존 앱 복제</span><span class="sxs-lookup"><span data-stu-id="38da5-108">Cloning an existing App</span></span>
<span data-ttu-id="38da5-109">**프리미엄** 모드에서 웹앱을 실행해야 웹앱에 대한 복제본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="38da5-110">[Azure 포털](https://portal.azure.com/)에서 웹앱의 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="38da5-111">**도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-111">Click **Tools**.</span></span> <span data-ttu-id="38da5-112">그런 다음 **도구** 블레이드에서 **앱 복제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="38da5-113">웹앱이 **프리미엄** 모드가 아닌 경우 앱 복제에 대한 지원 모델을 나타내는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="38da5-114">이때 **업그레이드**옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="38da5-115">**앱 복제** 블레이드에서 새 웹앱, 리소스 그룹 및 앱 서비스 계획의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="38da5-116">또한 많은 원본 웹앱 설정을 복제할 것인지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="38da5-117">**만들기** 를 클릭하면 플랫폼은 원본 웹앱의 복제본을 만드는 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="38da5-118">기존 앱을 앱 서비스 환경으로 복제</span><span class="sxs-lookup"><span data-stu-id="38da5-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="38da5-119">**앱 복제** 블레이드에서 고객이 기존 앱 서비스 환경의 앱 풀을 옵션으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="38da5-120">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="38da5-120">Current Restrictions</span></span>
<span data-ttu-id="38da5-121">이 기능은 현재 미리 보기 상태이며 점차 새 기능을 추가하기 위해 작업 중입니다. 다음 목록은 Azure 포털에서 앱 복제의 현재 지원에 대해 알려진 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="38da5-122">Azure 트래픽 관리자 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="38da5-123">자동 크기 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="38da5-124">백업 일정 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="38da5-125">VNET 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="38da5-126">App Insights는 대상 웹앱에서 자동으로 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="38da5-127">간편한 인증 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="38da5-128">Kudu 확장은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="38da5-129">TiP 규칙은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="38da5-130">데이터베이스 내용이 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38da5-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="38da5-131">참조</span><span class="sxs-lookup"><span data-stu-id="38da5-131">References</span></span>
* [<span data-ttu-id="38da5-132">PowerShell을 사용하여 웹앱 복제</span><span class="sxs-lookup"><span data-stu-id="38da5-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="38da5-133">Azure 앱 서비스에서 웹앱 백업</span><span class="sxs-lookup"><span data-stu-id="38da5-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="38da5-134">앱 서비스 환경을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="38da5-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="38da5-135">앱 서비스 환경에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="38da5-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="38da5-136">앱 서비스 환경 소개</span><span class="sxs-lookup"><span data-stu-id="38da5-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
