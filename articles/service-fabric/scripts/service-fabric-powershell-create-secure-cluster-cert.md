---
title: "PowerShell 스크립트 샘플-aaaAzure 서비스 패브릭 클러스터 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 클러스터 만들기"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="934a3-103">Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="934a3-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="934a3-104">이 샘플 스크립트는 Service Fabric 클러스터를 X.509 인증서를 사용하여 보호되는 5노드 클러스터로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="934a3-105">hello 명령은 자체 서명 된 인증서를 만들고 tooa 새 키 자격 증명 모음에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="934a3-106">hello 인증서 복사한 tooa 로컬 디렉터리 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="934a3-107">집합 hello *-OS* toochoose hello 버전의 Windows 또는 Linux hello 클러스터 노드에서 실행 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="934a3-108">필요에 따라 hello 매개 변수를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="934a3-109">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview) 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="934a3-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="934a3-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="934a3-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="934a3-111">Clean up deployment</span></span> 

<span data-ttu-id="934a3-112">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 클러스터 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="934a3-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="934a3-113">Script explanation</span></span>

<span data-ttu-id="934a3-114">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-114">This script uses hello following commands.</span></span> <span data-ttu-id="934a3-115">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="934a3-116">명령</span><span class="sxs-lookup"><span data-stu-id="934a3-116">Command</span></span> | <span data-ttu-id="934a3-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="934a3-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="934a3-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="934a3-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="934a3-119">새 Service Fabric 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="934a3-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="934a3-120">Next steps</span></span>

<span data-ttu-id="934a3-121">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="934a3-122">Azure Service Fabric에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="934a3-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
