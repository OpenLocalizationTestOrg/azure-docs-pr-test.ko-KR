---
title: "서비스 패브릭 응용 프로그램을 업그레이드 하는 PowerShell 스크립트 샘플-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="26dd1-103">Service Fabric 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="26dd1-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="26dd1-104">이 샘플 스크립트를 실행 중인 서비스 패브릭 응용 프로그램 인스턴스 tooversion 1.3.0 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="26dd1-105">hello 스크립트 hello 새 응용 프로그램 패키지 toohello 클러스터 이미지 저장소에 복사, hello 응용 프로그램 유형을 등록, 모니터링 되는 업그레이드를 시작 및 hello 업그레이드 완료 되거나 롤백합니다 때까지 계속 hello 업그레이드 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="26dd1-106">필요에 따라 hello 매개 변수를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="26dd1-107">필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="26dd1-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="26dd1-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="26dd1-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="26dd1-109">Script explanation</span></span>

<span data-ttu-id="26dd1-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-110">This script uses hello following commands.</span></span> <span data-ttu-id="26dd1-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="26dd1-112">명령</span><span class="sxs-lookup"><span data-stu-id="26dd1-112">Command</span></span> | <span data-ttu-id="26dd1-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="26dd1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26dd1-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="26dd1-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="26dd1-115">Hello 서비스 패브릭 클러스터의 모든 hello 응용 프로그램 또는 특정 응용 프로그램을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="26dd1-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="26dd1-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="26dd1-117">서비스 패브릭 응용 프로그램 업그레이드의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="26dd1-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="26dd1-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="26dd1-119">Hello 서비스 패브릭 클러스터에 등록 하는 hello 서비스 패브릭 응용 프로그램 종류를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="26dd1-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="26dd1-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="26dd1-121">Service Fabric 응용 프로그램 유형을 등록 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="26dd1-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="26dd1-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="26dd1-123">서비스 패브릭 응용 프로그램 패키지 toohello 이미지 저장소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="26dd1-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="26dd1-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="26dd1-125">Service Fabric 응용 프로그램 유형을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="26dd1-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="26dd1-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="26dd1-127">서비스 패브릭 응용 프로그램 toohello 지정 된 응용 프로그램 종류 버전을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="26dd1-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26dd1-128">Next steps</span></span>

<span data-ttu-id="26dd1-129">Hello 서비스 패브릭 PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="26dd1-130">Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26dd1-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
