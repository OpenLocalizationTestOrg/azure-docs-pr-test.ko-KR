---
title: "CLI 스크립트 샘플 응용 프로그램의 고가용성에 대 한 트래픽 라우팅할 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="08695-103">응용 프로그램 고가용성을 위한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="08695-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="08695-104">이 스크립트는 리소스 그룹, 2개 App Service 계획, 2개 웹앱, Traffic Manager 프로필 및 2개 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08695-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="08695-105">트래픽 관리자는 hello 기본 지역의 hello 응용 프로그램을 사용할 수 없는 경우 hello 기본 지역으로 한 영역과 toohello 보조 지역에 트래픽을 toohello 응용 프로그램을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="08695-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="08695-106">Hello 스크립트를 실행 하기 전에 hello MyWebApp, MyWebAppL1 리소스 및 MyWebAppL2 Azure 간의 toounique 값 값입니다.</span><span class="sxs-lookup"><span data-stu-id="08695-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="08695-107">Hello 스크립트를 실행 한 후 hello 앱 URL mywebapp.trafficmanager.net hello 사용 하 여 hello 기본 영역에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08695-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="08695-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="08695-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="08695-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="08695-109">Clean up deployment</span></span> 

<span data-ttu-id="08695-110">Hello 스크립트 예제를 실행 한 후 hello 다음 명령을 사용 하는 tooremove hello 리소스 그룹, 앱 서비스 앱 및 관련 된 모든 리소스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08695-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="08695-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="08695-111">Script explanation</span></span>

<span data-ttu-id="08695-112">이 스크립트 명령 toocreate 리소스 그룹, 웹 응용 프로그램, 트래픽 관리자 프로필 뒤 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="08695-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="08695-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="08695-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="08695-114">명령</span><span class="sxs-lookup"><span data-stu-id="08695-114">Command</span></span> | <span data-ttu-id="08695-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="08695-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08695-116">az group create</span><span class="sxs-lookup"><span data-stu-id="08695-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="08695-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08695-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08695-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="08695-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="08695-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08695-119">Creates an App Service plan.</span></span> <span data-ttu-id="08695-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="08695-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="08695-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="08695-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="08695-122">Hello 앱 서비스 계획 내에서 Azure 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08695-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="08695-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="08695-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="08695-124">Azure Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08695-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="08695-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="08695-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="08695-126">끝점 tooan Azure 트래픽 관리자 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08695-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08695-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08695-127">Next steps</span></span>

<span data-ttu-id="08695-128">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="08695-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="08695-129">추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 설명서](../cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08695-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
