---
title: "Azure 보안 모범 사례 및 패턴 | Microsoft Docs"
description: "이 문서는 Azure 보안 모범 사례 및 패턴에 관한 소개와 다른 Azure 리소스에 대한 보안 모범 사례의 엄선된 목록을 제공합니다."
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
ms.openlocfilehash: 1cc0d2d1e9a62ff8531f963413ff573713d508ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="7201c-103">Azure 보안 모범 사례 및 패턴</span><span class="sxs-lookup"><span data-stu-id="7201c-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="7201c-104">현재 다음과 같은 Azure 보안 모범 사례 및 패턴 문서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-104">We currently have the following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="7201c-105">Azure 보안 모범 사례 및 패턴과 관련하여 늘어가는 목록이 업데이트되는 것을 보려면 이 사이트를 정기적으로 방문하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-105">Make sure to visit this site periodically to see updates to our growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="7201c-106">Azure 네트워크 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7201c-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="7201c-107">Azure 데이터 보안 및 암호화 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7201c-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="7201c-108">ID 관리 및 액세스 제어 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7201c-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="7201c-109">사물 인터넷 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7201c-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="7201c-110">[Azure IaaS 보안 모범 사례] (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="7201c-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="7201c-111">Azure 경계 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7201c-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="7201c-112">Azure에서 보안 하이브리드 네트워크 아키텍처 구현</span><span class="sxs-lookup"><span data-stu-id="7201c-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="7201c-113">[Azure PaaS 모범 사례] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="7201c-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="7201c-114">Azure는 솔루션을 빌드할 수 있도록 안전한 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="7201c-115">Azure의 솔루션을 보다 안전하게 만들기 위한 서비스와 기술도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-115">We also provide services and technologies to make your solutions on Azure more secure.</span></span> <span data-ttu-id="7201c-116">사용할 수 있는 옵션이 많기 때문에 많은 분들이 Microsoft가 보안 개선의 모범 사례 및 패턴으로 추천하는 내용에 관해 관심을 표명했습니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-116">Because of the many options available to you, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="7201c-117">여러분의 관심을 이해하여, 이를 위해 적절한 상황에서 Azure 배포의 보안을 개선하기 위해 여러분이 할 수 있는 일을 설명하는 문서 컬렉션을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-117">We understand your interest and have created a collection of documents that describe things you can do, given the right context, to improve the security of Azure deployments.</span></span>

<span data-ttu-id="7201c-118">이러한 모범 사례 및 패턴 문서에, 특정 항목에 대한 모범 사례 및 유용한 패턴 컬렉션이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="7201c-119">이러한 모범 사례 및 패턴은 이런 기술에 대한 우리 경험과 여러분 같은 고객의 경험에서 얻은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-119">These best practices and patterns are derived from our experiences with these technologies and the experiences of customers like yourself.</span></span>

<span data-ttu-id="7201c-120">각 모범 사례에 대해 다음 사항을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-120">For each best practice we strive to explain:</span></span>

* <span data-ttu-id="7201c-121">각 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7201c-121">What the best practice is</span></span>
* <span data-ttu-id="7201c-122">해당 모범 사례를 사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="7201c-122">Why you want to enable that best practice</span></span>
* <span data-ttu-id="7201c-123">해당 모범 사례를 사용하지 않을 경우에 발생할 수 있는 결과</span><span class="sxs-lookup"><span data-stu-id="7201c-123">What might be the result if you fail to enable the best practice</span></span>
* <span data-ttu-id="7201c-124">해당 모범 사례를 대체할 수 있는 대안</span><span class="sxs-lookup"><span data-stu-id="7201c-124">Possible alternatives to the best practice</span></span>
* <span data-ttu-id="7201c-125">해당 모범 사례를 사용하는 방법을 알아보는 방법</span><span class="sxs-lookup"><span data-stu-id="7201c-125">How you can learn to enable the best practice</span></span>

<span data-ttu-id="7201c-126">Azure 보안 아키텍처 및 모범 사례에 대한 많은 문서를 갖추려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7201c-126">We look forward to including many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="7201c-127">추가할 항목이 있으시면 이 페이지의 아래쪽에 있는 토론 영역에서 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="7201c-127">If there are topics that you'd like us to include, let us know in the discussion area at the bottom of this page.</span></span>
