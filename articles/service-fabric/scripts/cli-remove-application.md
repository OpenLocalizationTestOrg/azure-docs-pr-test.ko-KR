---
title: "aaaAzure 서비스 패브릭 CLI 스크립트 제거 예제 추가 정보"
description: "Azure 서비스 패브릭 CLI hello를 사용 하 여 Azure 서비스 패브릭 클러스터에서 응용 프로그램을 제거 합니다."
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="aef56-103">Service Fabric 클러스터에서 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="aef56-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="aef56-104">이 샘플 스크립트 실행 중인 서비스 패브릭 응용 프로그램 인스턴스가 삭제 되 면 응용 프로그램 유형 및 버전 hello 클러스터에서 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="aef56-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="aef56-105">Hello 응용 프로그램 인스턴스 삭제는 실행 중인 서비스 인스턴스를 해당 응용 프로그램과 관련 된 모든 hello도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aef56-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="aef56-106">다음으로 응용 프로그램 파일 hello hello 이미지 저장소에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aef56-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="aef56-107">필요한 경우 설치 hello [서비스 패브릭 CLI](../service-fabric-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef56-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="aef56-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="aef56-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="aef56-109">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aef56-109">Next steps</span></span>

<span data-ttu-id="aef56-110">자세한 내용은 참조 hello [서비스 패브릭 CLI 설명서](../service-fabric-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef56-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="aef56-111">Azure Service Fabric에 대 한 추가 서비스 패브릭 CLI 샘플 hello에서 확인할 수 있습니다 [서비스 패브릭 CLI 샘플](../samples-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aef56-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
