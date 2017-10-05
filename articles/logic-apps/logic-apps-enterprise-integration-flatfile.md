---
title: "Azure Logic Apps에서 플랫 파일 인코딩 또는 디코딩 | Microsoft Docs"
description: "Logic Apps에서 엔터프라이즈 통합 팩에 포함된 플랫 파일 인코더 또는 디코더를 사용하는 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bc3430624844cdeb92958433fba295f67a8ae0ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a><span data-ttu-id="72a7d-103">플랫 파일을 사용한 엔터프라이즈 통합 개요</span><span class="sxs-lookup"><span data-stu-id="72a7d-103">Overview of enterprise integration with flat files</span></span>

<span data-ttu-id="72a7d-104">B2B(Business-to-Business) 시나리오에서 비즈니스 파트너에게 보내기 전에 XML 콘텐츠를 인코딩하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-104">You may want to encode XML content before you send it to a business partner in a business-to-business (B2B) scenario.</span></span> <span data-ttu-id="72a7d-105">논리 앱에서 플랫 파일 인코딩 커넥터를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-105">In a logic app, you can use the flat file encoding connector to do this.</span></span> <span data-ttu-id="72a7d-106">만든 논리 앱은 HTTP 요청 트리거를 포함하여 다른 응용 프로그램 또는 다양한 [커넥터](../connectors/apis-list.md)에서도 다양한 원본의 XML 콘텐츠를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-106">The logic app that you create can get its XML content from a variety of sources, including from an HTTP request trigger, from another application, or even from one of the many [connectors](../connectors/apis-list.md).</span></span> <span data-ttu-id="72a7d-107">논리 앱에 대한 자세한 내용은 [논리 앱 설명서](logic-apps-what-are-logic-apps.md "논리 앱에 대해 자세히 알아보기")에서도 다양한 원본의 XML 콘텐츠를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-107">For more information about logic apps, see the [logic apps documentation](logic-apps-what-are-logic-apps.md "Learn more about Logic apps").</span></span>  

## <a name="create-the-flat-file-encoding-connector"></a><span data-ttu-id="72a7d-108">플랫 파일 인코딩 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="72a7d-108">Create the flat file encoding connector</span></span>
<span data-ttu-id="72a7d-109">다음 단계를 수행하여 플랫 파일 인코딩 커넥터를 논리 앱을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-109">Follow these steps to add a flat file encoding connector to your logic app.</span></span>

1. <span data-ttu-id="72a7d-110">논리 앱을 만들고 [통합 계정에 연결](logic-apps-enterprise-integration-accounts.md "논리 앱에 통합 계정을 연결하는 방법 알아보기")에서도 다양한 원본의 XML 콘텐츠를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-110">Create a logic app and [link it to your integration account](logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app").</span></span> <span data-ttu-id="72a7d-111">이 계정은 XML 데이터를 인코딩하는 데 사용할 스키마를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-111">This account contains the schema you will use to encode the XML data.</span></span>  
2. <span data-ttu-id="72a7d-112">**요청 - HTTP 요청을 받은 경우** 트리거를 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-112">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>  
   <span data-ttu-id="72a7d-113">![선택할 트리거의 스크린샷](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="72a7d-113">![Screenshot of trigger to select](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
3. <span data-ttu-id="72a7d-114">다음을 수행하여 플랫 파일 인코딩 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-114">Add the flat file encoding action, as follows:</span></span>
   
    <span data-ttu-id="72a7d-115">a.</span><span class="sxs-lookup"><span data-stu-id="72a7d-115">a.</span></span> <span data-ttu-id="72a7d-116">**더하기** 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-116">Select the **plus** sign.</span></span>
   
    <span data-ttu-id="72a7d-117">b.</span><span class="sxs-lookup"><span data-stu-id="72a7d-117">b.</span></span> <span data-ttu-id="72a7d-118">더하기 기호를 선택한 후에 표시되는 **작업 추가** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-118">Select the **Add an action** link (appears after you have selected the plus sign).</span></span>
   
    <span data-ttu-id="72a7d-119">c.</span><span class="sxs-lookup"><span data-stu-id="72a7d-119">c.</span></span> <span data-ttu-id="72a7d-120">검색 상자에 *플랫* 을 입력하여 사용하려는 작업에 대해 모든 작업을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-120">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span></span>
   
    <span data-ttu-id="72a7d-121">d.</span><span class="sxs-lookup"><span data-stu-id="72a7d-121">d.</span></span> <span data-ttu-id="72a7d-122">목록에서 **플랫 파일 인코딩** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-122">Select the **Flat File Encoding** option from the list.</span></span>   
   <span data-ttu-id="72a7d-123">![플랫 파일 인코딩 옵션의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="72a7d-123">![Screenshot of Flat File Encoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
4. <span data-ttu-id="72a7d-124">**플랫 파일 인코딩** 대화 상자에서 **콘텐츠** 텍스트 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-124">On the **Flat File Encoding** dialog box, select the **Content** text box.</span></span>  
   <span data-ttu-id="72a7d-125">![텍스트 상자 콘텐츠의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span><span class="sxs-lookup"><span data-stu-id="72a7d-125">![Screenshot of Content text box](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span></span>  
5. <span data-ttu-id="72a7d-126">본문 태그를 인코딩하려는 콘텐츠로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-126">Select the body tag as the content that you want to encode.</span></span> <span data-ttu-id="72a7d-127">본문 태그는 콘텐츠 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-127">The body tag will populate the content field.</span></span>     
   ![본문 태그의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. <span data-ttu-id="72a7d-129">**스키마 이름** 목록 상자를 선택하고 입력 콘텐츠를 인코딩하는 데 사용할 스키마를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-129">Select the **Schema Name** list box, and choose the schema you want to use to encode the input content.</span></span>    
   <span data-ttu-id="72a7d-130">![스키마 이름 목록 상자의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span><span class="sxs-lookup"><span data-stu-id="72a7d-130">![Screenshot of Schema Name list box](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span></span>  
7. <span data-ttu-id="72a7d-131">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-131">Save your work.</span></span>   
   ![저장 아이콘의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

<span data-ttu-id="72a7d-133">이 시점에서 플랫 파일 인코딩 커넥터의 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-133">At this point, you are finished setting up your flat file encoding connector.</span></span> <span data-ttu-id="72a7d-134">실제 응용 프로그램에서는 SalesForce와 같은 LOB(line-of-business) 응용 프로그램에 인코딩한 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-134">In a real world application, you may want to store the encoded data in a line-of-business application, such as Salesforce.</span></span> <span data-ttu-id="72a7d-135">또는 인코딩된 데이터를 거래 업체에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-135">Or you can send that encoded data to a trading partner.</span></span> <span data-ttu-id="72a7d-136">제공된 다른 커넥터 중 하나를 사용하여 Salesforce 또는 거래 파트너에게 인코딩 작업의 출력을 보내는 동작을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-136">You can easily add an action to send the output of the encoding action to Salesforce, or to your trading partner, by using any one of the other connectors provided.</span></span>

<span data-ttu-id="72a7d-137">이제 HTTP 끝점에 요청하고 요청 본문에 XML 콘텐츠를 포함하여 커넥터를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-137">You can now test your connector by making a request to the HTTP endpoint, and including the XML content in the body of the request.</span></span>  

## <a name="create-the-flat-file-decoding-connector"></a><span data-ttu-id="72a7d-138">플랫 파일 디코딩 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="72a7d-138">Create the flat file decoding connector</span></span>

> [!NOTE]
> <span data-ttu-id="72a7d-139">이러한 단계를 완료하려면 통합 계정에 이미 업로드된 스키마 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-139">To complete these steps, you need to have a schema file already uploaded into you integration account.</span></span>

1. <span data-ttu-id="72a7d-140">**요청 - HTTP 요청을 받은 경우** 트리거를 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-140">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>  
   <span data-ttu-id="72a7d-141">![선택할 트리거의 스크린샷](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="72a7d-141">![Screenshot of trigger to select](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
2. <span data-ttu-id="72a7d-142">다음을 수행하여 플랫 파일 디코딩 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-142">Add the flat file decoding action, as follows:</span></span>
   
    <span data-ttu-id="72a7d-143">a.</span><span class="sxs-lookup"><span data-stu-id="72a7d-143">a.</span></span> <span data-ttu-id="72a7d-144">**더하기** 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-144">Select the **plus** sign.</span></span>
   
    <span data-ttu-id="72a7d-145">b.</span><span class="sxs-lookup"><span data-stu-id="72a7d-145">b.</span></span> <span data-ttu-id="72a7d-146">더하기 기호를 선택한 후에 표시되는 **작업 추가** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-146">Select the **Add an action** link (appears after you have selected the plus sign).</span></span>
   
    <span data-ttu-id="72a7d-147">c.</span><span class="sxs-lookup"><span data-stu-id="72a7d-147">c.</span></span> <span data-ttu-id="72a7d-148">검색 상자에 *플랫* 을 입력하여 사용하려는 작업에 대해 모든 작업을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-148">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span></span>
   
    <span data-ttu-id="72a7d-149">d.</span><span class="sxs-lookup"><span data-stu-id="72a7d-149">d.</span></span> <span data-ttu-id="72a7d-150">목록에서 **플랫 파일 디코딩** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-150">Select the **Flat File Decoding** option from the list.</span></span>   
   <span data-ttu-id="72a7d-151">![플랫 파일 디코딩 옵션의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="72a7d-151">![Screenshot of Flat File Decoding option](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
3. <span data-ttu-id="72a7d-152">**콘텐츠** 제어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-152">Select the **Content** control.</span></span> <span data-ttu-id="72a7d-153">그러면 이전 단계에서 콘텐츠로 디코딩하는 데 사용할 수 있는 콘텐츠의 목록이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-153">This produces a list of the content from earlier steps that you can use as the content to decode.</span></span> <span data-ttu-id="72a7d-154">들어오는 HTTP 요청의 *본문* 을 콘텐츠로 디코딩하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-154">Notice that the *Body* from the incoming HTTP request is available to be used as the content to decode.</span></span> <span data-ttu-id="72a7d-155">**콘텐츠** 제어에 직접 디코딩할 콘텐츠를 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-155">You can also enter the content to decode directly into the **Content** control.</span></span>     
4. <span data-ttu-id="72a7d-156">*본문* 태그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-156">Select the *Body* tag.</span></span> <span data-ttu-id="72a7d-157">이제 본문 태그는 **콘텐츠** 제어에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-157">Notice the body tag is now in the **Content** control.</span></span>
5. <span data-ttu-id="72a7d-158">콘텐츠를 디코딩하는 데 사용할 스키마의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-158">Select the name of the schema that you want to use to decode the content.</span></span> <span data-ttu-id="72a7d-159">다음 스크린샷에서는 *OrderFile* 이 선택한 스키마 이름임을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-159">The following screenshot shows that *OrderFile* is the selected schema name.</span></span> <span data-ttu-id="72a7d-160">이전에 이 스키마 이름을 통합 계정에 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-160">This schema name had been uploaded into the integration account previously.</span></span>
   
   ![플랫 파일 디코딩 대화 상자의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. <span data-ttu-id="72a7d-162">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-162">Save your work.</span></span>  
   ![저장 아이콘의 스크린샷](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

<span data-ttu-id="72a7d-164">이 시점에서 플랫 파일 디코딩 커넥터의 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-164">At this point, you are finished setting up your flat file decoding connector.</span></span> <span data-ttu-id="72a7d-165">실제 응용 프로그램에서는 SalesForce와 같은 LOB(line-of-business) 응용 프로그램에 디코딩한 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-165">In a real world application, you may want to store the decoded data in a line-of-business application such as Salesforce.</span></span> <span data-ttu-id="72a7d-166">Salesforce에 디코딩 작업의 출력을 보내는 작업을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-166">You can easily add an action to send the output of the decoding action to Salesforce.</span></span>

<span data-ttu-id="72a7d-167">이제 HTTP 끝점에 요청하고 요청 본문에 디코딩하려는 XML 콘텐츠를 포함하여 커넥터를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a7d-167">You can now test your connector by making a request to the HTTP endpoint and including the XML content you want to decode in the body of the request.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="72a7d-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72a7d-168">Next steps</span></span>
* <span data-ttu-id="72a7d-169">[엔터프라이즈 통합 팩에 대해 자세히 알아보기](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")</span><span class="sxs-lookup"><span data-stu-id="72a7d-169">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack").</span></span>  

