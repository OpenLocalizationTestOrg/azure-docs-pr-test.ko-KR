---
title: "PowerShell 스크립트 예제는 클러스터에서 응용 프로그램 제거 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 클러스터에서 응용 프로그램 제거"
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="01efa-103">Service Fabric 클러스터에서 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="01efa-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="01efa-104">이 샘플 스크립트는 실행 중인 서비스 패브릭 응용 프로그램 인스턴스를 삭제 하 고, 응용 프로그램 유형 및 버전 hello 클러스터에서 등록을 취소, hello 클러스터 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="01efa-105">Hello 응용 프로그램 인스턴스 삭제는 실행 중인 서비스 인스턴스를 해당 응용 프로그램과 관련 된 모든 hello도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="01efa-106">필요에 따라 hello 매개 변수를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="01efa-107">필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="01efa-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="01efa-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="01efa-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="01efa-109">Script explanation</span></span>

<span data-ttu-id="01efa-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-110">This script uses hello following commands.</span></span> <span data-ttu-id="01efa-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="01efa-112">명령</span><span class="sxs-lookup"><span data-stu-id="01efa-112">Command</span></span> | <span data-ttu-id="01efa-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="01efa-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01efa-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="01efa-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="01efa-115">Hello 클러스터에서 실행 중인 서비스 패브릭 응용 프로그램 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="01efa-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="01efa-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="01efa-117">서비스 패브릭 응용 프로그램 유형 및 버전 hello 클러스터에서 등록 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="01efa-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="01efa-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="01efa-119">Hello 이미지 저장소에서 서비스 패브릭 응용 프로그램 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="01efa-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01efa-120">Next steps</span></span>

<span data-ttu-id="01efa-121">Hello 서비스 패브릭 PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="01efa-122">Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01efa-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
