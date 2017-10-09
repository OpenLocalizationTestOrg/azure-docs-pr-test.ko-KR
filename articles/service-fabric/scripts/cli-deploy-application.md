---
title: "서비스 패브릭 CLI 스크립트 배포 샘플 aaaAzure"
description: "Azure 서비스 패브릭 CLI hello를 사용 하 여 응용 프로그램 tooan Azure 서비스 패브릭 클러스터 배포"
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="0c42e-103">응용 프로그램 tooa 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="0c42e-104">이 샘플 스크립트 응용 프로그램 패키지 tooa 클러스터 이미지 저장소에 복사 하 고 hello 클러스터에 hello 응용 프로그램 종류를 등록 한 hello 응용 프로그램 종류에서 응용 프로그램 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="0c42e-105">이때 기본 서비스도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="0c42e-106">필요한 경우 설치 hello [서비스 패브릭 CLI](../service-fabric-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="0c42e-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0c42e-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0c42e-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0c42e-108">Clean up deployment</span></span>

<span data-ttu-id="0c42e-109">을 완료 한 후 hello [제거](cli-remove-application.md) 스크립트에 사용 되는 tooremove hello 응용 프로그램 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="0c42e-110">hello 제거 스크립트 hello 응용 프로그램 인스턴스를 삭제 하 고 hello 응용 프로그램 종류의 등록을 취소 한 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c42e-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c42e-111">Next steps</span></span>

<span data-ttu-id="0c42e-112">자세한 내용은 참조 hello [서비스 패브릭 CLI 설명서](../service-fabric-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="0c42e-113">Azure Service Fabric에 대 한 추가 서비스 패브릭 CLI 샘플 hello에서 확인할 수 있습니다 [서비스 패브릭 CLI 샘플](../samples-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c42e-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
