---
title: "XML 유효성 검사-Azure 논리 앱에 대 한 aaaSchemas | Microsoft Docs"
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
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="e232f-103">Azure 논리 앱 및 엔터프라이즈 통합 팩 hello에 대 한 XML 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e232f-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="e232f-104">스키마 확인 하 고 나타나면 hello XML 문서가 모두 유효한 hello 예상한 데이터를 미리 정의 된 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="e232f-105">스키마는 B2B 시나리오에서 교환되는 메시지의 유효성을 검사하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="e232f-106">스키마 추가</span><span class="sxs-lookup"><span data-stu-id="e232f-106">Add a schema</span></span>

1. <span data-ttu-id="e232f-107">Hello Azure 포털에서에서 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-107">In hello Azure portal, select **More services**.</span></span>

    ![Azure Portal, "더 많은 서비스"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="e232f-109">Hello 필터 검색 상자에 입력 **통합**를 선택 하 고 **통합 계정** hello 결과 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![필터 검색 상자](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="e232f-111">선택 hello **통합 계정** tooadd hello 스키마 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![통합 계정 목록](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="e232f-113">Hello 선택 **스키마** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-113">Choose hello **Schemas** tile.</span></span>

    ![예제 통합 계정, "스키마"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="e232f-115">2MB보다 작은 스키마 파일 추가</span><span class="sxs-lookup"><span data-stu-id="e232f-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="e232f-116">Hello에 **스키마** hello 이전 단계), (에서 열리면 선택 블레이드 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![스키마 블레이드, "추가"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="e232f-118">스키마의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-118">Enter a name for your schema.</span></span> <span data-ttu-id="e232f-119">Hello 폴더 다음 toohello 아이콘을 선택 하 여 hello 스키마 파일을 업로드 **스키마** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="e232f-120">Hello 업로드 프로세스가 완료 된 후 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-120">After hello upload process completes, select **OK**.</span></span>

    !["작은 파일"이 강조 표시된 "스키마 추가" 스크린샷](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="e232f-122">스키마 파일 (위쪽 too8 MB 최대) 2MB 이상의 추가</span><span class="sxs-lookup"><span data-stu-id="e232f-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="e232f-123">이러한 단계 hello blob 컨테이너 액세스 수준에 따라 다릅니다: **공용** 또는 **익명 액세스할 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="e232f-124">**toodetermine이 액세스 수준**</span><span class="sxs-lookup"><span data-stu-id="e232f-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="e232f-125">**Azure Storage 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="e232f-126">아래 **Blob 컨테이너**선택, 원하는 hello blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="e232f-127">**보안**, **액세스 수준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="e232f-128">Hello blob 보안 액세스 수준이 **공용**, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-128">If hello blob security access level is **Public**, follow these steps.</span></span>

!["Blob 컨테이너", "보안" 및 "공용"이 강조 표시된 Azure Storage 탐색기](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="e232f-130">Hello 스키마 tooyour 저장소 계정에 업로드 하 고 hello URI를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![URI가 강조 표시된 저장소 계정](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="e232f-132">**스키마 추가**선택, **큰 파일**, hello에 hello URI를 제공 하 고 **콘텐츠 URI** 입력란.</span><span class="sxs-lookup"><span data-stu-id="e232f-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    !["추가" 단추 및 " 큰 파일"이 강조 표시된 스키마](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="e232f-134">Hello blob 보안 액세스 수준이 **익명 액세스할 수 없는**, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

!["Blob 컨테이너", "보안" 및 "익명 액세스 없음"이 강조 표시된 Azure Storage 탐색기](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="e232f-136">Hello 스키마 tooyour 저장소 계정에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-136">Upload hello schema tooyour storage account.</span></span>

    ![저장소 계정](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="e232f-138">Hello 스키마에 대 한 공유 액세스 서명을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-138">Generate a shared access signature for hello schema.</span></span>

    ![공유 액세스 서명 탭이 강조 표시된 저장소 계정](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="e232f-140">**스키마 추가**선택, **큰 파일**, hello에 hello 공유 액세스 서명 URI를 제공 하 고 **콘텐츠 URI** 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    !["추가" 단추 및 " 큰 파일"이 강조 표시된 스키마](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="e232f-142">Hello에 **스키마** 통합 계정 블레이드를 새로 추가 된 스키마 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![통합 계정에 "스키마" 및 강조 표시 하는 hello 새 스키마](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="e232f-144">스키마 편집</span><span class="sxs-lookup"><span data-stu-id="e232f-144">Edit schemas</span></span>

1. <span data-ttu-id="e232f-145">Hello 선택 **스키마** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="e232f-146">Hello 후 **스키마** tooedit 선택 hello 스키마 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="e232f-147">Hello에 **스키마** 블레이드에서 선택 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![스키마 블레이드](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="e232f-149">선택 hello 스키마 파일을 tooedit, 원하는 선택한 다음 하면 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![파일 tooedit 스키마 열기](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="e232f-151">스키마 hello 메시지를 azure에서는 성공적으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="e232f-152">스키마 삭제</span><span class="sxs-lookup"><span data-stu-id="e232f-152">Delete schemas</span></span>

1. <span data-ttu-id="e232f-153">Hello 선택 **스키마** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="e232f-154">Hello 후 **스키마** toodelete 선택 hello 스키마 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="e232f-155">Hello에 **스키마** 블레이드에서 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![스키마 블레이드](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="e232f-157">tooconfirm toodelete hello 않겠다고 선택한 스키마를 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    !["스키마 삭제" 확인 메시지](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="e232f-159">Hello에 **스키마** 블레이드에서 hello 스키마 목록을 새로 고치고 더 이상 삭제 된 hello 스키마를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    !["스키마"가 강조 표시된 통합 계정](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="e232f-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e232f-161">Next steps</span></span>
* <span data-ttu-id="e232f-162">[엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "hello 엔터프라이즈 통합 팩에 대 한 자세한 정보")합니다.</span><span class="sxs-lookup"><span data-stu-id="e232f-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

