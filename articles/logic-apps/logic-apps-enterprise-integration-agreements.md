---
title: "B2B 통신-Azure 논리 앱에 대 한 aaaAgreements | Microsoft Docs"
description: "Azure 논리 앱 및 엔터프라이즈 통합 팩 hello에 대 한 파트너 B2B 시나리오에서 통신할 수 있도록 규약 만들기"
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
ms.openlocfilehash: 499edcbab1cd67fbc169e393c3cad7b81658a250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="17eef-103">Azure Logic Apps 및 엔터프라이즈 통합 팩과의 B2B 통신에 대한 파트너 규약</span><span class="sxs-lookup"><span data-stu-id="17eef-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="17eef-104">업계 표준 프로토콜을 사용 하 여 원활 하 게 통신 하는 비즈니스 엔터티 계약 및 hello cornerstone 기업 간 (B2B) 통신에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-104">Agreements let business entities communicate seamlessly using industry standard protocols and are hello cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="17eef-105">엔터프라이즈 통합 팩 hello 사용 하 여 논리 앱에 대 한 B2B 시나리오를 설정할 경우 규약은 B2B 거래 업체 간의 통신 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-105">When enabling B2B scenarios for logic apps with hello Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="17eef-106">본이 계약은 너무 hello 파트너 통신을 설정 및 프로토콜 또는 전송 별로 hello를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-106">This agreement is based on hello communications that hello partners want too establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="17eef-107">엔터프라이즈 통합은 다음과 같은 세 가지 프로토콜 또는 전송 표준을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="17eef-108">AS2</span><span class="sxs-lookup"><span data-stu-id="17eef-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="17eef-109">X12</span><span class="sxs-lookup"><span data-stu-id="17eef-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="17eef-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="17eef-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="17eef-111">규약을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="17eef-111">Why use agreements</span></span>

<span data-ttu-id="17eef-112">규칙을 사용할 때는 몇 가지 일반적인 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="17eef-113">잘 알려진 형식으로 서로 다른 조직 및 비즈니스 tooexchange 정보를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-113">Enables different organizations and businesses tooexchange information in a well-known format.</span></span>
* <span data-ttu-id="17eef-114">B2B 트랜잭션을 수행할 경우 효율성을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="17eef-115">쉬운 toocreate 관리 하 고 엔터프라이즈 통합 앱을 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-115">Easy toocreate, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-toocreate-agreements"></a><span data-ttu-id="17eef-116">어떻게 toocreate 계약</span><span class="sxs-lookup"><span data-stu-id="17eef-116">How toocreate agreements</span></span>

* [<span data-ttu-id="17eef-117">AS2 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="17eef-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="17eef-118">X12 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="17eef-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="17eef-119">EDIFACT 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="17eef-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-toouse-an-agreement"></a><span data-ttu-id="17eef-120">어떻게 toouse 규약</span><span class="sxs-lookup"><span data-stu-id="17eef-120">How toouse an agreement</span></span>

<span data-ttu-id="17eef-121">만든 규약을 사용하여 B2B 기능으로 [Logic Apps](logic-apps-what-are-logic-apps.md "논리 앱에 대해 알아보기")를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-tooedit-an-agreement"></a><span data-ttu-id="17eef-122">어떻게 tooedit 규약</span><span class="sxs-lookup"><span data-stu-id="17eef-122">How tooedit an agreement</span></span>

<span data-ttu-id="17eef-123">다음 단계를 수행하여 모든 규약을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="17eef-124">Hello 계약이 tooupdate 원하는 hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-124">Select hello integration account that has hello agreement you want tooupdate.</span></span>

2. <span data-ttu-id="17eef-125">Hello 선택 **계약** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-125">Choose hello **Agreements** tile.</span></span>

3. <span data-ttu-id="17eef-126">Hello에 **계약** 블레이드, 선택 hello 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-126">On hello **Agreements** blade, select hello agreement.</span></span>

4. <span data-ttu-id="17eef-127">**편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-127">Choose **Edit**.</span></span> <span data-ttu-id="17eef-128">변경을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-128">Make your changes.</span></span>

5. <span data-ttu-id="17eef-129">변경 내용을 선택 toosave **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-129">toosave your changes, choose **OK**.</span></span>

## <a name="how-toodelete-an-agreement"></a><span data-ttu-id="17eef-130">어떻게 toodelete 규약</span><span class="sxs-lookup"><span data-stu-id="17eef-130">How toodelete an agreement</span></span>

<span data-ttu-id="17eef-131">다음 단계를 수행하여 규약을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="17eef-132">Hello 계약이 toodelete 원하는 hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-132">Select hello integration account that has hello agreement you want toodelete.</span></span>
2. <span data-ttu-id="17eef-133">Hello 선택 **계약** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-133">Choose hello **Agreements** tile.</span></span>
3. <span data-ttu-id="17eef-134">Hello에 **계약** 블레이드, 선택 hello 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-134">On hello **Agreements** blade, select hello agreement.</span></span>
4. <span data-ttu-id="17eef-135">**삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="17eef-136">Toodelete hello 선택한 규약을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-136">Confirm that you want toodelete hello selected agreement.</span></span>

    <span data-ttu-id="17eef-137">hello 계약 블레이드는 더 이상 삭제 하는 hello 계약을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eef-137">hello Agreements blade no longer shows hello deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17eef-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17eef-138">Next steps</span></span>
* [<span data-ttu-id="17eef-139">AS2 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="17eef-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
