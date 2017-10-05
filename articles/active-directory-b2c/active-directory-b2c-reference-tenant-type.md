---
title: "Azure Active Directory B2C: 지역 가용성 및 데이터 상주 | Microsoft Docs"
description: "Azure Active Directory B2C 테넌트 유형에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="dd39c-103">Azure Active Directory B2C: 지역 가용성 및 데이터 상주</span><span class="sxs-lookup"><span data-stu-id="dd39c-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="dd39c-104">지역 가용성 및 데이터 상주는 나머지 Azure에서 Azure AD B2C에 다르게 적용되는 두 가지 매우 다른 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="dd39c-105">이 문서에서는 이러한 두 개념의 차이점을 설명하고 이러한 개념이 Azure 및 Azure AD B2C에 적용되는 방식을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="dd39c-106">요약</span><span class="sxs-lookup"><span data-stu-id="dd39c-106">Summary</span></span>
<span data-ttu-id="dd39c-107">Azure AD B2C는 **미국 또는 유럽의 데이터 상주**에 대한 옵션을 통해 **일반적으로 전 세계에서 사용할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="dd39c-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="dd39c-108">개념</span><span class="sxs-lookup"><span data-stu-id="dd39c-108">Concepts</span></span>
* <span data-ttu-id="dd39c-109">**지역 가용성**은 서비스를 사용할 수 있는 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="dd39c-110">**데이터 상주**는 사용자 데이터가 저장된 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="dd39c-111">지역 가용성</span><span class="sxs-lookup"><span data-stu-id="dd39c-111">Region availability</span></span>
<span data-ttu-id="dd39c-112">Azure AD B2C는 Azure 공용 클라우드를 통해 전 세계에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="dd39c-113">이것은 가용성과 데이터 상주를 결합하는 대부분의 다른 Azure 서비스가 따르는 모델과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="dd39c-114">Azure의 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/) 페이지 및 [Azure Active Directory B2C 가격](https://azure.microsoft.com/pricing/details/active-directory-b2c/)에서 이와 같은 예제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="dd39c-115">데이터 상주</span><span class="sxs-lookup"><span data-stu-id="dd39c-115">Data residency</span></span>
<span data-ttu-id="dd39c-116">Azure AD B2C는 사용자 데이터를 미국 또는 유럽에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="dd39c-117">데이터 상주는 [Azure AD B2C 테넌트](active-directory-b2c-get-started.md)를 만들 때 선택된 국가/지역에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![미리 보기 테넌트의 스크린 샷](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="dd39c-119">다음 국가/지역의 경우 데이터는 미국에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="dd39c-120">미국, 캐나다, 코스타리카, 도미니카 공화국, 엘살바도르, 과테말라, 멕시코, 파나마, 푸에르토리코, 트리니다드토바고</span><span class="sxs-lookup"><span data-stu-id="dd39c-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="dd39c-121">다음 국가/지역의 경우 데이터는 유럽에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="dd39c-122">알제리, 오스트리아, 아제르바이잔, 바레인, 벨로루시, 벨기에, 불가리아, 크로아티아, 키프로스, 체코, 덴마크, 이집트, 에스토니아, 핀란드, 프랑스, 독일, 그리스, 헝가리, 아이슬란드, 아일랜드, 이스라엘, 이탈리아, 요르단, 카자흐스탄, 케냐, 쿠웨이트, 라트비아, 레바논, 리히텐슈타인, 리투아니아, 룩셈부르크, 마케도니아(FYROM), 몰타, 몬테네그로, 모로코, 네덜란드, 나이지리아, 노르웨이, 오만, 파키스탄, 폴란드, 포르투갈, 카타르, 루마니아, 러시아, 사우디아라비아, 세르비아, 슬로바키아, 슬로베니아, 남아프리카 공화국, 스페인, 스웨덴, 스위스, 튀니지, 터키, 우크라이나 아랍에미리트 및 영국.</span><span class="sxs-lookup"><span data-stu-id="dd39c-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="dd39c-123">나머지 국가/지역은 목록에 추가되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="dd39c-124">이제 위의 국가/지역을 선택하여 Azure AD B2C를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="dd39c-125">아프가니스탄, 아르헨티나, 오스트레일리아, 브라질, 칠레, 콜롬비아, 에콰도르, 홍콩 특별 행정구, 인도, 인도네시아, 이라크, 일본, 한국, 말레이시아, 뉴질랜드, 파라과이, 페루, 필리핀, 싱가포르, 스리랑카, 대만, 태국, 우루과이 및 베네수엘라.</span><span class="sxs-lookup"><span data-stu-id="dd39c-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="dd39c-126">미리 보기 테넌트</span><span class="sxs-lookup"><span data-stu-id="dd39c-126">Preview tenant</span></span>
<span data-ttu-id="dd39c-127">Azure AD B2C 미리 보기 기간 동안 B2C 테넌트를 만든 경우 **테넌트 유형**은 **미리 보기 테넌트**라고 할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="dd39c-128">이런 경우 테넌트를 개발 및 테스트 목적에만 사용하고 프로덕션 앱용으로 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd39c-129">미리 보기 B2C 테넌트로부터 프로덕션 규모 B2C 테넌트로의 마이그레이션 경로가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="dd39c-130">미리 보기 B2C 테넌트를 삭제하고 동일한 도메인 이름으로 프로덕션 규모 B2C 테넌트를 다시 만들어야 하는 경우 알려진 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="dd39c-131">다른 도메인 이름으로 프로덕션 규모 B2C 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd39c-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![미리 보기 테넌트의 스크린 샷](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
