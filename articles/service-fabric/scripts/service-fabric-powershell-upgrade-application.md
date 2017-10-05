---
title: "Azure PowerShell 스크립트 샘플 - Service Fabric 응용 프로그램 업그레이드 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 응용 프로그램 업그레이드"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="5f480-103">Service Fabric 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="5f480-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="5f480-104">이 샘플 스크립트는 실행 중인 Service Fabric 응용 프로그램 인스턴스를 버전 1.3.0으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-104">This sample script upgrades a running Service Fabric application instance to version 1.3.0.</span></span> <span data-ttu-id="5f480-105">이 스크립트는 클러스터 이미지 저장소에 새 응용 프로그램 패키지를 복사하고, 응용 프로그램 유형을 등록하고, 모니터링되는 업그레이드를 시작하고, 업그레이드가 완료되거나 롤백될 때까지 업그레이드 상태를 계속 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-105">The script copies the new application package to the cluster image store, registers the application type, starts a monitored upgrade, and continuously checks the upgrade status until the upgrade completes or rolls back.</span></span> <span data-ttu-id="5f480-106">필요에 따라 매개 변수를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="5f480-107">필요한 경우 [Service Fabric SDK](../service-fabric-get-started.md)를 사용하여 Service Fabric PowerShell 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5f480-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5f480-108">Sample script</span></span>

<span data-ttu-id="5f480-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "응용 프로그램 업그레이드")]</span><span class="sxs-lookup"><span data-stu-id="5f480-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="5f480-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5f480-110">Script explanation</span></span>

<span data-ttu-id="5f480-111">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-111">This script uses the following commands.</span></span> <span data-ttu-id="5f480-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5f480-113">명령</span><span class="sxs-lookup"><span data-stu-id="5f480-113">Command</span></span> | <span data-ttu-id="5f480-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5f480-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f480-115">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="5f480-115">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="5f480-116">Service Fabric 클러스터의 모든 응용 프로그램 또는 특정 응용 프로그램을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-116">Gets all the applications in the Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="5f480-117">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="5f480-117">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="5f480-118">Service Fabric 응용 프로그램 업그레이드의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-118">Gets the status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="5f480-119">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="5f480-119">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="5f480-120">Service Fabric 클러스터에 등록된 Service Fabric 응용 프로그램 유형을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-120">Gets the Service Fabric application types registered on the Service Fabric cluster.</span></span> |
| [<span data-ttu-id="5f480-121">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="5f480-121">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="5f480-122">Service Fabric 응용 프로그램 유형을 등록 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-122">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="5f480-123">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="5f480-123">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="5f480-124">Service Fabric 응용 프로그램 패키지를 이미지 저장소에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-124">Copies a Service Fabric application package to the image store.</span></span>  |
| [<span data-ttu-id="5f480-125">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="5f480-125">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="5f480-126">Service Fabric 응용 프로그램 유형을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-126">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="5f480-127">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="5f480-127">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="5f480-128">Service Fabric 응용 프로그램을 지정된 응용 프로그램 유형 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-128">Upgrades a Service Fabric application to the specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5f480-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f480-129">Next steps</span></span>

<span data-ttu-id="5f480-130">Service Fabric PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f480-130">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="5f480-131">Azure Service Fabric에 대한 추가 PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f480-131">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
