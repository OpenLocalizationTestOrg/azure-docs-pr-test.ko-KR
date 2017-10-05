---
title: "Azure CLI 스크립트 샘플 - 응용 프로그램 고가용성을 위한 트래픽 라우팅 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 응용 프로그램 고가용성을 위한 트래픽 라우팅"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="af7a4-103">응용 프로그램 고가용성을 위한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="af7a4-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="af7a4-104">이 스크립트는 리소스 그룹, 2개 App Service 계획, 2개 웹앱, Traffic Manager 프로필 및 2개 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="af7a4-105">Traffic Manager는 주 지역인 한 지역의 응용 프로그램 및 주 지역의 응용 프로그램을 사용할 수 없을 때 보조 지역으로 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="af7a4-106">스크립트를 실행하기 전에 MyWebApp, MyWebAppL1 및 MyWebAppL2 값을 Azure에서 고유한 값으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="af7a4-107">스크립트를 실행한 후에는 mywebapp.trafficmanager.net URL을 사용하여 주 지역의 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="af7a4-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="af7a4-108">Sample script</span></span>

<span data-ttu-id="af7a4-109">[!code-azurecli-interactive[주](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "고가용성을 위한 트래픽 라우팅")]</span><span class="sxs-lookup"><span data-stu-id="af7a4-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="af7a4-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="af7a4-110">Clean up deployment</span></span> 

<span data-ttu-id="af7a4-111">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, App Service 앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="af7a4-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="af7a4-112">Script explanation</span></span>

<span data-ttu-id="af7a4-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱, Traffic Manager 프로필 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="af7a4-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="af7a4-115">명령</span><span class="sxs-lookup"><span data-stu-id="af7a4-115">Command</span></span> | <span data-ttu-id="af7a4-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="af7a4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="af7a4-117">az group create</span><span class="sxs-lookup"><span data-stu-id="af7a4-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="af7a4-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="af7a4-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="af7a4-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="af7a4-120">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-120">Creates an App Service plan.</span></span> <span data-ttu-id="af7a4-121">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="af7a4-122">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="af7a4-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="af7a4-123">App Service 계획 내에서 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="af7a4-124">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="af7a4-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="af7a4-125">Azure Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="af7a4-126">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="af7a4-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="af7a4-127">Azure Traffic Manager 프로필에 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="af7a4-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af7a4-128">Next steps</span></span>

<span data-ttu-id="af7a4-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af7a4-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="af7a4-130">추가 App Service CLI 스크립트 샘플은 [Azure 네트워킹 설명서](../cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af7a4-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
