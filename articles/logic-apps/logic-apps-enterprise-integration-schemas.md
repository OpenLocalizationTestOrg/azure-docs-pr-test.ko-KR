---
title: "XML 유효성 검사용 스키마 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps 및 엔터프라이즈 통합 팩용 스키마로 XML 문서 유효성 검사"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="597b7-103">Azure Logic Apps 및 엔터프라이즈 통합 팩용 스키마로 XML 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="597b7-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="597b7-104">스키마는 수신한 XML 문서가 유효한지와 예상되는 데이터가 미리 정의된 형식으로 문서에 포함되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="597b7-105">스키마는 B2B 시나리오에서 교환되는 메시지의 유효성을 검사하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="597b7-106">스키마 추가</span><span class="sxs-lookup"><span data-stu-id="597b7-106">Add a schema</span></span>

1. <span data-ttu-id="597b7-107">Azure Portal에서 **더 많은 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-107">In the Azure portal, select **More services**.</span></span>

    ![Azure Portal, "더 많은 서비스"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="597b7-109">필터 검색 상자에 **통합**을 입력하고 결과 목록에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![필터 검색 상자](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="597b7-111">스키마를 추가할 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-111">Select the **integration account** where you want to add the schema.</span></span>

    ![통합 계정 목록](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="597b7-113">**스키마** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-113">Choose the **Schemas** tile.</span></span>

    ![예제 통합 계정, "스키마"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="597b7-115">2MB보다 작은 스키마 파일 추가</span><span class="sxs-lookup"><span data-stu-id="597b7-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="597b7-116">(이전 단계에서) 열린 **스키마** 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![스키마 블레이드, "추가"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="597b7-118">스키마의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-118">Enter a name for your schema.</span></span> <span data-ttu-id="597b7-119">**스키마** 텍스트 상자 옆의 폴더 아이콘을 선택하여 스키마 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="597b7-120">업로드 프로세스가 완료되면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-120">After the upload process completes, select **OK**.</span></span>

    !["작은 파일"이 강조 표시된 "스키마 추가" 스크린샷](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="597b7-122">2MB(최대 8MB)보다 큰 스키마 파일 추가</span><span class="sxs-lookup"><span data-stu-id="597b7-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="597b7-123">이러한 단계는 Blob 컨테이너 액세스 수준인 **공용** 또는 **익명 액세스 없음**에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="597b7-124">**이 액세스 수준을 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="597b7-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="597b7-125">**Azure Storage 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="597b7-126">**Blob 컨테이너** 아래에서 원하는 blob 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="597b7-127">**보안**, **액세스 수준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="597b7-128">Blob 보안 액세스 수준이 **공용**인 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-128">If the blob security access level is **Public**, follow these steps.</span></span>

!["Blob 컨테이너", "보안" 및 "공용"이 강조 표시된 Azure Storage 탐색기](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="597b7-130">스키마를 계정 저장소에 업로드하고 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![URI가 강조 표시된 저장소 계정](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="597b7-132">**스키마 추가**에서 **큰 파일**을 선택하고 **콘텐츠 URI** 텍스트 상자에 URI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    !["추가" 단추 및 " 큰 파일"이 강조 표시된 스키마](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="597b7-134">Blob 보안 액세스 수준이 **익명 액세스 없음**인 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

!["Blob 컨테이너", "보안" 및 "익명 액세스 없음"이 강조 표시된 Azure Storage 탐색기](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="597b7-136">저장소 계정에 스키마를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-136">Upload the schema to your storage account.</span></span>

    ![저장소 계정](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="597b7-138">스키마에 대한 공유 액세스 서명을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-138">Generate a shared access signature for the schema.</span></span>

    ![공유 액세스 서명 탭이 강조 표시된 저장소 계정](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="597b7-140">**스키마 추가**에서 **큰 파일**을 선택하고 **콘텐츠 URI** 텍스트 상자에 공유 액세스 서명 URI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    !["추가" 단추 및 " 큰 파일"이 강조 표시된 스키마](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="597b7-142">통합 계정의 **스키마** 블레이드에서 새로 추가된 스키마가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    !["스키마" 및 새 스키마가 강조 표시된 EIP 통합 계정](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="597b7-144">스키마 편집</span><span class="sxs-lookup"><span data-stu-id="597b7-144">Edit schemas</span></span>

1. <span data-ttu-id="597b7-145">**스키마** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="597b7-146">열린 **스키마** 블레이드에서 편집하려는 스키마를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="597b7-147">**스키마** 블레이드에서 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![스키마 블레이드](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="597b7-149">편집하려는 스키마 파일을 선택하고 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![편집할 스키마 파일 열기](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="597b7-151">스키마가 성공적으로 업로드했다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="597b7-152">스키마 삭제</span><span class="sxs-lookup"><span data-stu-id="597b7-152">Delete schemas</span></span>

1. <span data-ttu-id="597b7-153">**스키마** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="597b7-154">열린 **스키마** 블레이드에서 삭제하려는 스키마를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="597b7-155">**스키마** 블레이드에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![스키마 블레이드](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="597b7-157">선택한 스키마를 삭제할지 확인하려면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    !["스키마 삭제" 확인 메시지](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="597b7-159">**스키마** 블레이드에서 스키마 목록이 새로 고쳐지고 삭제된 스키마가 더 이상 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="597b7-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    !["스키마"가 강조 표시된 통합 계정](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="597b7-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="597b7-161">Next steps</span></span>
* <span data-ttu-id="597b7-162">[엔터프라이즈 통합 팩에 대해 자세히 알아보기](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")</span><span class="sxs-lookup"><span data-stu-id="597b7-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

