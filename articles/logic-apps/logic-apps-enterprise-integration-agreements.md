---
title: "B2B 통신 규약 - Azure Logic Apps | Microsoft Docs"
description: "파트너가 Azure Logic Apps 및 엔터프라이즈 통합 팩에 대한 B2B 시나리오에서 통신할 수 있도록 계약 만들기"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="73d47-103">Azure Logic Apps 및 엔터프라이즈 통합 팩과의 B2B 통신에 대한 파트너 규약</span><span class="sxs-lookup"><span data-stu-id="73d47-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="73d47-104">규약은 산업 표준 프로토콜을 사용하여 비즈니스 엔터티가 원활하게 통신할 수 있도록 하며 B2B(기업 간) 통신의 토대입니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="73d47-105">엔터프라이즈 통합 팩을 사용하는 Logic Apps에 대한 B2B 시나리오를 설정할 때 규약은 B2B 거래 파트너 간의 통신 배열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="73d47-106">이 규약은 파트너가 설정하려고 하는 통신을 기반으로 하며 프로토콜 또는 전송별로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="73d47-107">엔터프라이즈 통합은 다음과 같은 세 가지 프로토콜 또는 전송 표준을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="73d47-108">AS2</span><span class="sxs-lookup"><span data-stu-id="73d47-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="73d47-109">X12</span><span class="sxs-lookup"><span data-stu-id="73d47-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="73d47-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="73d47-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="73d47-111">규약을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="73d47-111">Why use agreements</span></span>

<span data-ttu-id="73d47-112">규칙을 사용할 때는 몇 가지 일반적인 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="73d47-113">서로 다른 조직 및 비즈니스가 잘 알려진 형식으로 정보를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="73d47-114">B2B 트랜잭션을 수행할 경우 효율성을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="73d47-115">엔터프라이즈 통합 앱을 생성할 경우 쉽게 작성, 관리 및 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="73d47-116">규약 생성 방법</span><span class="sxs-lookup"><span data-stu-id="73d47-116">How to create agreements</span></span>

* [<span data-ttu-id="73d47-117">AS2 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="73d47-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="73d47-118">X12 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="73d47-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="73d47-119">EDIFACT 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="73d47-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="73d47-120">규약 사용 방법</span><span class="sxs-lookup"><span data-stu-id="73d47-120">How to use an agreement</span></span>

<span data-ttu-id="73d47-121">만든 규약을 사용하여 B2B 기능으로 [Logic Apps](logic-apps-what-are-logic-apps.md "논리 앱에 대해 알아보기")를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="73d47-122">규약 편집 방법</span><span class="sxs-lookup"><span data-stu-id="73d47-122">How to edit an agreement</span></span>

<span data-ttu-id="73d47-123">다음 단계를 수행하여 모든 규약을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="73d47-124">업데이트하려는 규약을 포함하는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="73d47-125">**규약** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="73d47-126">**규약** 블레이드에서 규약을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="73d47-127">**편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-127">Choose **Edit**.</span></span> <span data-ttu-id="73d47-128">변경을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-128">Make your changes.</span></span>

5. <span data-ttu-id="73d47-129">변경 내용을 저장하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="73d47-130">규약 삭제 방법</span><span class="sxs-lookup"><span data-stu-id="73d47-130">How to delete an agreement</span></span>

<span data-ttu-id="73d47-131">다음 단계를 수행하여 규약을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="73d47-132">삭제하려는 규약을 포함하는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="73d47-133">**규약** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="73d47-134">**규약** 블레이드에서 규약을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="73d47-135">**삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="73d47-136">선택한 규약을 삭제할지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="73d47-137">규약 블레이드에 삭제된 규약이 더 이상 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73d47-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73d47-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73d47-138">Next steps</span></span>
* [<span data-ttu-id="73d47-139">AS2 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="73d47-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
