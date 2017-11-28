---
title: "XSLT를 사용하여 XML 변환 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps 및 엔터프라이즈 통합 팩을 사용하여 XML 데이터를 변환하기 위한 XSLT 맵 추가"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="8ade4-103">XML 데이터 변환을 위한 맵 추가</span><span class="sxs-lookup"><span data-stu-id="8ade4-103">Add maps for XML data transform</span></span>

<span data-ttu-id="8ade4-104">엔터프라이즈 통합에서는 맵을 사용하여 XML 데이터를 다른 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="8ade4-105">맵은 문서에서 어떤 데이터를 다른 형식으로 변환해야 하는지를 정의하는 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="8ade4-106">맵을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="8ade4-106">Why use maps?</span></span>

<span data-ttu-id="8ade4-107">날짜에 YYYMMDD 형식을 사용하는 고객에게서 정기적으로 B2B 주문 또는 송장을 받는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="8ade4-108">그러나 조직에서 날짜를 MMDDYYY 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="8ade4-109">고객 작업 데이터베이스에서 주문 또는 송장 세부 정보를 저장하기 전에 맵을 사용하여 YYYMMDD 날짜 형식을 MMDDYYY로 *변환* 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="8ade4-110">맵을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="8ade4-110">How do I create a map?</span></span>

<span data-ttu-id="8ade4-111">Visual Studio 2015용 [엔터프라이즈 통합 팩](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")을 사용하여 Biztalk 통합 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="8ade4-112">그런 후 두 개의 XML 스키마 파일 간에 항목을 시각적으로 매핑할 수 있는 통합 맵 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="8ade4-113">이 프로젝트를 빌드하면 XSLT 문서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="8ade4-114">맵을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="8ade4-114">How do I add a map?</span></span>

1. <span data-ttu-id="8ade4-115">Azure Portal에서 **찾아보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="8ade4-116">필터 검색 상자에 **통합**을 입력하고 결과 목록에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="8ade4-117">맵을 추가할 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="8ade4-118">**맵** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="8ade4-119">맵 블레이드가 열리면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="8ade4-120">맵의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="8ade4-121">맵 파일을 업로드하려면 **맵** 텍스트 상자 오른쪽에 있는 폴더 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="8ade4-122">업로드 프로세스가 완료되면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="8ade4-123">Azure에서 통합 계정에 맵을 추가하면 맵 파일이 추가되었는지 여부를 보여 주는 화면 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="8ade4-124">이 메시지가 표시되면 새로 추가된 맵을 볼 수 있도록 **맵** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="8ade4-125">맵을 편집하는 방법</span><span class="sxs-lookup"><span data-stu-id="8ade4-125">How do I edit a map?</span></span>

<span data-ttu-id="8ade4-126">원하는 변경 내용을 포함한 새 맵 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="8ade4-127">먼저 편집을 위해 맵을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-127">You can first download the map for editing.</span></span>

<span data-ttu-id="8ade4-128">기존 맵을 대체하는 새 맵을 업로드하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="8ade4-129">**맵** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="8ade4-130">맵 블레이드가 열리면 편집할 수 있는 맵을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="8ade4-131">**맵** 블레이드에서 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="8ade4-132">파일 선택에서 업로드하려는 맵 파일을 선택하고 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="8ade4-133">맵 삭제 방법</span><span class="sxs-lookup"><span data-stu-id="8ade4-133">How to delete a map?</span></span>

1. <span data-ttu-id="8ade4-134">**맵** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="8ade4-135">맵 블레이드가 열리면 삭제할 수 있는 맵을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="8ade4-136">**삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="8ade4-137">맵을 삭제할지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ade4-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="8ade4-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ade4-138">Next Steps</span></span>
* [<span data-ttu-id="8ade4-139">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="8ade4-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")  
* [<span data-ttu-id="8ade4-140">규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="8ade4-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  
* [<span data-ttu-id="8ade4-141">변환에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="8ade4-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "엔터프라이즈 통합 변환에 대해 알아보기")  

