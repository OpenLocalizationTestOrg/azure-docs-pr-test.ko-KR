---
title: "PowerShell 스크립트 샘플-aaaAzure tooa 클러스터 응용 프로그램 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 예제-응용 프로그램 tooa 서비스 패브릭 클러스터를 배포 합니다."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="b8b21-103">응용 프로그램 tooa 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="b8b21-104">이 샘플 스크립트 응용 프로그램 패키지 tooa 클러스터 이미지 저장소에 복사 하 고 hello 클러스터에 hello 응용 프로그램 종류를 등록 한 hello 응용 프로그램 종류에서 응용 프로그램 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="b8b21-105">기본 서비스 hello 대상 응용 프로그램 종류의 hello 응용 프로그램 매니페스트에서 정의 된 경우에 해당 서비스이 이번에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="b8b21-106">필요에 따라 hello 매개 변수를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="b8b21-107">필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b8b21-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b8b21-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b8b21-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="b8b21-109">Clean up deployment</span></span> 

<span data-ttu-id="b8b21-110">Hello 스크립트 예제를 실행 한 후에 스크립트 hello [응용 프로그램을 제거](service-fabric-powershell-remove-application.md) 사용된 tooremove hello 응용 프로그램 인스턴스 수, hello 응용 프로그램 종류의 등록을 취소 및 hello 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="b8b21-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b8b21-111">Script explanation</span></span>

<span data-ttu-id="b8b21-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-112">This script uses hello following commands.</span></span> <span data-ttu-id="b8b21-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b8b21-114">명령</span><span class="sxs-lookup"><span data-stu-id="b8b21-114">Command</span></span> | <span data-ttu-id="b8b21-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b8b21-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b8b21-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="b8b21-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="b8b21-117">응용 프로그램 패키지 toohello 클러스터 이미지 저장소에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="b8b21-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="b8b21-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="b8b21-119">응용 프로그램 유형 및 버전 hello 클러스터에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="b8b21-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="b8b21-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="b8b21-121">등록된 응용 프로그램 유형에서 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b8b21-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8b21-122">Next steps</span></span>

<span data-ttu-id="b8b21-123">Hello 서비스 패브릭 PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="b8b21-124">Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b21-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
