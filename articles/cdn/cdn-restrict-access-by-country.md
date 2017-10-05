---
title: "국가별 Azure CDN 콘텐츠 제한 | Microsoft Docs"
description: "[지역 필터링] 기능을 사용하여 Azure CDN 콘텐츠에 대한 액세스를 제한하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="8e56e-103">국가별 Azure CDN 콘텐츠 제한</span><span class="sxs-lookup"><span data-stu-id="8e56e-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="8e56e-104">개요</span><span class="sxs-lookup"><span data-stu-id="8e56e-104">Overview</span></span>
<span data-ttu-id="8e56e-105">기본적으로 사용자가 콘텐츠를 요청하는 경우 사용자가 이 요청을 수행하는 위치에 관계 없이 콘텐츠 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="8e56e-106">경우에 따라 국가별로 콘텐츠에 액세스를 제한 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="8e56e-107">이 항목에서는 국가별로 액세스를 허용하거나 차단하도록 서비스를 구성하기 위해 **지역 필터링** 기능을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e56e-108">Verizon 및 Akamai 제품은 동일한 지역 필터링 기능을 제공하지만 지원하는 국가 코드가 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="8e56e-109">차이점에 대한 링크는 3단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e56e-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="8e56e-110">이 유형의 제한 구성에 적용되는 고려 사항에 대한 자세한 내용은 항목의 끝에 있는 [고려 사항](cdn-restrict-access-by-country.md#considerations) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e56e-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![국가 필터링](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="8e56e-112">1 단계: 디렉터리 경로 정의</span><span class="sxs-lookup"><span data-stu-id="8e56e-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="8e56e-113">포털 안에서 끝점을 선택하고 왼쪽 탐색에서 지역 필터링 탭을 찾아 이 기능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="8e56e-114">국가 필터를 구성하는 경우 사용자에게 액세스를 허용하거나 거부하는 위치에 대한 상대 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="8e56e-115">디렉터리 경로 "/pictures/"를 지정하여 "/" 또는 선택된 폴더를 사용하여 모든 파일에 대해 지역 필터링을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="8e56e-116">마지막 슬래시를 생략하고 파일을 지정하여 "/pictures/city.png"로 단일 파일에 지역 필터링을 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="8e56e-117">예제 디렉터리 경로 필터:</span><span class="sxs-lookup"><span data-stu-id="8e56e-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="8e56e-118">2 단계: 차단 또는 허용 동작을 정의</span><span class="sxs-lookup"><span data-stu-id="8e56e-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="8e56e-119">**차단** : 지정한 국가의 사용자는 해당 재귀 경로에서 요청된 자산에 대해 액세스가 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="8e56e-120">해당 위치에 대해 다른 국가 필터링 옵션이 구성되지 않은 경우에는 다른 모든 사용자는 액세스가 허용 됩니다</span><span class="sxs-lookup"><span data-stu-id="8e56e-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="8e56e-121">**허용** : 지정한 국가의 사용자만 해당 재귀 경로에서 요청된 자산에 대해 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="8e56e-122">3 단계: 국가 정의하기</span><span class="sxs-lookup"><span data-stu-id="8e56e-122">Step 3: Define the countries</span></span>
<span data-ttu-id="8e56e-123">경로에 대해 차단 또는 허용하기 원하는 국가를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="8e56e-124">예를 들어 /Photos/Strasbourg/ 차단 규칙은 다음을 포함하는 파일을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="8e56e-125">국가 코드</span><span class="sxs-lookup"><span data-stu-id="8e56e-125">Country codes</span></span>
<span data-ttu-id="8e56e-126">**지역 필터링** 기능은 국가 코드를 사용하여 보안된 디렉터리에 대해 요청이 허용 또는 차단될 국가를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="8e56e-127">[Azure CDN 국가 코드](https://msdn.microsoft.com/library/mt761717.aspx)에서 국가 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="8e56e-128"><a id="considerations"></a>고려 사항</span><span class="sxs-lookup"><span data-stu-id="8e56e-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="8e56e-129">지리 필터링 구성에 대한 변경이 적용되려면 Verizon의 경우 최대 90분, Akamai의 경우 2~3분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="8e56e-130">이 기능은 와일드카드 문자를 지원하지 않습니다 (예: '*').</span><span class="sxs-lookup"><span data-stu-id="8e56e-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="8e56e-131">상대 경로와 관련된 지역 필터링 구성은 해당 경로에 재귀적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="8e56e-132">동일한 상대 경로에 하나의 규칙만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="8e56e-133">(동일한 상대 경로를 가리키는 여러 국가 필터를 만들 수 없습니다  그러나 폴더에는 여러 국가 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="8e56e-134">이는 국가 필터의 재귀적 특성 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="8e56e-135">즉, 이전에 구성된 폴더의 하위 폴더에 다른 국가 필터를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e56e-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

