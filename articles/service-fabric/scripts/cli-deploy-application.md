---
title: "Azure Service Fabric CLI 스크립트 배포 샘플"
description: "Azure Service Fabric CLI를 사용하여 Azure Service Fabric 클러스터에 응용 프로그램 배포"
services: service-fabric
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: c77ecfccdf7d3e34b0b3133e9c63810a04fb1132
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="3e732-103">Service Fabric 클러스터에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="3e732-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="3e732-104">이 샘플 스크립트는 클러스터 이미지 저장소에 응용 프로그램 패키지를 복사하고, 응용 프로그램 유형을 클러스터에 등록하고, 해당 응용 프로그램 유형에서 응용 프로그램 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e732-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span> <span data-ttu-id="3e732-105">이때 기본 서비스도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3e732-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="3e732-106">필요한 경우 [Service Fabric CLI](../service-fabric-cli.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3e732-106">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="3e732-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3e732-107">Sample script</span></span>

<span data-ttu-id="3e732-108">[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "클러스터에 응용 프로그램 배포")]</span><span class="sxs-lookup"><span data-stu-id="3e732-108">[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3e732-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3e732-109">Clean up deployment</span></span>

<span data-ttu-id="3e732-110">완료했으면 [제거](cli-remove-application.md) 스크립트를 사용하여 응용 프로그램을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e732-110">When done, the [remove](cli-remove-application.md) script can be used to remove the application.</span></span> <span data-ttu-id="3e732-111">제거 스크립트는 응용 프로그램 인스턴스를 삭제하고 응용 프로그램 형식을 등록 취소하며 이미지 저장소에서 응용 프로그램 패키지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3e732-111">The remove script deletes the application instance, unregisters the application type, and deletes the application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e732-112">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e732-112">Next steps</span></span>

<span data-ttu-id="3e732-113">자세한 내용은 [Service Fabric CLI 설명서](../service-fabric-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e732-113">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="3e732-114">Azure Service Fabric에 대한 추가 Service Fabric CLI 샘플은 [Service Fabric CLI 샘플](../samples-cli.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e732-114">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
