---
title: "aaaAzure 보안 모범 사례 및 패턴 | Microsoft Docs"
description: "hello 문서에서는 Azure 보안에 대 한 유용한 정보 및 패턴 및 큐 레이트 목록이 서로 다른 Azure 리소스에 대 한 보안 모범 사례에 대 한 소개 합니다."
services: azure-security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1cbbf8dc-ea94-4a7e-8fa0-c2cb198956c5
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: terrylan
ms.openlocfilehash: eaaa9457faa1d5906275eb1fd8988d4d4aad101a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="613d6-103">Azure 보안 모범 사례 및 패턴</span><span class="sxs-lookup"><span data-stu-id="613d6-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="613d6-104">현재 Azure 보안 모범 사례 및 패턴 문서 다음 hello를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-104">We currently have hello following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="613d6-105">이 사이트 있는지 toovisit 확인 toosee tooour 목록이 패턴과 Azure 보안에 대 한 유용한 정보를 정기적으로 업데이트:</span><span class="sxs-lookup"><span data-stu-id="613d6-105">Make sure toovisit this site periodically toosee updates tooour growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="613d6-106">Azure 네트워크 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="613d6-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="613d6-107">Azure 데이터 보안 및 암호화 모범 사례</span><span class="sxs-lookup"><span data-stu-id="613d6-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="613d6-108">ID 관리 및 액세스 제어 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="613d6-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="613d6-109">사물 인터넷 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="613d6-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="613d6-110">[Azure IaaS 보안 모범 사례] (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="613d6-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="613d6-111">Azure 경계 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="613d6-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="613d6-112">Azure에서 보안 하이브리드 네트워크 아키텍처 구현</span><span class="sxs-lookup"><span data-stu-id="613d6-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="613d6-113">[Azure PaaS 모범 사례] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="613d6-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="613d6-114">Azure는 솔루션을 빌드할 수 있도록 안전한 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="613d6-115">또한 서비스 및 기술 toomake 솔루션에 제공 Azure 더 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-115">We also provide services and technologies toomake your solutions on Azure more secure.</span></span> <span data-ttu-id="613d6-116">여러 옵션 사용 가능한 tooyou을 hello 때문에 어떤 Microsoft 권장 모범 사례 및 보안 향상을 위한 패턴에 관심을 탁음가 여러분 중 많은 합니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-116">Because of hello many options available tooyou, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="613d6-117">관심을 이해 하 고 수행할 수 있는 작업, 해당 Azure 배포의 tooimprove hello 보안 hello 오른쪽 기능에 설명 하는 문서 컬렉션을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-117">We understand your interest and have created a collection of documents that describe things you can do, given hello right context, tooimprove hello security of Azure deployments.</span></span>

<span data-ttu-id="613d6-118">이러한 모범 사례 및 패턴 문서에, 특정 항목에 대한 모범 사례 및 유용한 패턴 컬렉션이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="613d6-119">이러한 모범 사례 및 패턴은 이러한 기술 우리의 경험에서 파생 된 하 고 고객의 hello 경험 형식 직접 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-119">These best practices and patterns are derived from our experiences with these technologies and hello experiences of customers like yourself.</span></span>

<span data-ttu-id="613d6-120">각 모범 사례에 대 한 tooexplain을 줄이려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-120">For each best practice we strive tooexplain:</span></span>

* <span data-ttu-id="613d6-121">어떤 hello 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-121">What hello best practice is</span></span>
* <span data-ttu-id="613d6-122">이유는 tooenable 최선의 방법을</span><span class="sxs-lookup"><span data-stu-id="613d6-122">Why you want tooenable that best practice</span></span>
* <span data-ttu-id="613d6-123">Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴</span><span class="sxs-lookup"><span data-stu-id="613d6-123">What might be hello result if you fail tooenable hello best practice</span></span>
* <span data-ttu-id="613d6-124">가능한 대안 toohello 모범 사례</span><span class="sxs-lookup"><span data-stu-id="613d6-124">Possible alternatives toohello best practice</span></span>
* <span data-ttu-id="613d6-125">Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-125">How you can learn tooenable hello best practice</span></span>

<span data-ttu-id="613d6-126">의견에 귀 tooincluding Azure 보안 아키텍처 및 모범 사례에 더 많은 문서가 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="613d6-126">We look forward tooincluding many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="613d6-127">싶다는 의사를 우리는 항목이 있는 경우 tooinclude, hello이이 페이지 맨 아래에 hello 토론 영역에서 선택 해 주십시오.</span><span class="sxs-lookup"><span data-stu-id="613d6-127">If there are topics that you'd like us tooinclude, let us know in hello discussion area at hello bottom of this page.</span></span>
