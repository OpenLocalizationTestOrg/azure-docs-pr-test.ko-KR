---
title: "Azure Service Fabric CLI 스크립트 제거 샘플"
description: "Azure Service Fabric CLI를 사용하여 Azure Service Fabric 클러스터에 응용 프로그램 제거"
services: service-fabric
documentationcenter: 
author: thraka
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
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="4e534-103">Service Fabric 클러스터에서 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="4e534-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="4e534-104">이 샘플 스크립트는 실행 중인 Service Fabric 응용 프로그램 인스턴스를 삭제하고, 클러스터에서 응용 프로그램 유형 및 버전의 등록을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="4e534-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="4e534-105">응용 프로그램 인스턴스를 삭제하면 해당 응용 프로그램과 연결된 실행 중인 모든 서비스 인스턴스도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e534-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="4e534-106">다음으로 응용 프로그램 파일을 이미지 저장소에서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4e534-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="4e534-107">필요한 경우 [Service Fabric CLI](../service-fabric-cli.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4e534-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="4e534-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4e534-108">Sample script</span></span>

<span data-ttu-id="4e534-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "클러스터에서 응용 프로그램 제거")]</span><span class="sxs-lookup"><span data-stu-id="4e534-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e534-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e534-110">Next steps</span></span>

<span data-ttu-id="4e534-111">자세한 내용은 [Service Fabric CLI 설명서](../service-fabric-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e534-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="4e534-112">Azure Service Fabric에 대한 추가 Service Fabric CLI 샘플은 [Service Fabric CLI 샘플](../samples-cli.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e534-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
