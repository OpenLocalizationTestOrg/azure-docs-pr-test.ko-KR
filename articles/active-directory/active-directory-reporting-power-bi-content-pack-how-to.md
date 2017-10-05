---
title: "Azure Active Directory Power BI 콘텐츠 팩 사용 방법 | Microsoft Docs"
description: "Azure Active Directory Power BI 콘텐츠 팩 사용 방법 알아보기"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5c642bb814a279756e8391f12fdc86b6ec0b4a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="81595-103">Azure Active Directory Power BI 콘텐츠 팩 사용 방법</span><span class="sxs-lookup"><span data-stu-id="81595-103">How to use the Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="81595-104">사용자가 Azure Active Directory 기능을 채택하고 사용하는 방법을 이해하는 것은 IT 관리자로서 중요한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="81595-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin.</span></span> <span data-ttu-id="81595-105">IT 인프라와 통신을 계획하여 사용량을 늘리고 AAD 기능을 최대한 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-105">It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span></span> <span data-ttu-id="81595-106">Azure Active Directory용 Power BI 콘텐츠 팩을 통해 사용자는 데이터를 보다 세부적으로 분석하여 이 데이터를 사용하는 방법을 이해하고 Azure Active Directory를 통해 사용자가 크게 의존하는 다양한 기능의 상황에 대해 더 많은 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-106">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span></span>  <span data-ttu-id="81595-107">Azure Active Directory API를 Power BI에 통합하면 미리 빌드된 콘텐츠 팩을 쉽게 다운로드하고 Power BI가 제공하는 풍부한 시각화 환경을 사용하여 Azure Active Directory 내에서 모든 작업에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-107">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="81595-108">사용자 고유의 대시보드를 만들고 조직 내 사람들과 쉽게 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-108">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="81595-109">이 항목에서는 사용자 환경에서 콘텐츠 팩을 설치하고 사용하는 방법에 대한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-109">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="81595-110">설치</span><span class="sxs-lookup"><span data-stu-id="81595-110">Installation</span></span>  

<span data-ttu-id="81595-111">**Power BI 콘텐츠 팩을 설치하려면:**</span><span class="sxs-lookup"><span data-stu-id="81595-111">**To install the Power BI Content Pack:**</span></span>

1. <span data-ttu-id="81595-112">Power BI 계정으로 [Power BI](https://app.powerbi.com/groups/me/getdata/services)에 로그인합니다(이 계정은 O365 계정 또는 Azure AD 계정과 동일).</span><span class="sxs-lookup"><span data-stu-id="81595-112">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="81595-113">왼쪽 탐색 창의 아래쪽에서 **데이터 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-113">At the bottom of the left navigation pane, select **Get Data**.</span></span>

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="81595-115">**서비스** 상자에서 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-115">In the **Services** box, click **Get**.</span></span>
   
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="81595-117">**Azure Active Directory** 검색</span><span class="sxs-lookup"><span data-stu-id="81595-117">Search for **Azure Active Directory**.</span></span>

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="81595-119">프롬프트가 나타나면 Azure AD 테넌트 ID를 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-119">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="81595-120">Office 365/Azure AD 테넌트용 테넌트 Id를 가져오는 간단한 방법은 Azure AD 포털에 로그인하고 디렉터리를 드릴다운한 다음 URL에서 ID를 복사하는 것입니다. https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="81595-120">A quick way to get the Tenant Id for your Office 365 / Azure AD tenant is to login to the Azure AD Portal, drill down to the directory and copy the ID from the following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="81595-122">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-122">Click **Sign-in**.</span></span> 
 
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="81595-124">사용자 이름 및 암호를 입력한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-124">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="81595-126">앱 동의 대화 상자에서 **동의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-126">On the app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="81595-127">Azure Active Directory 작업 로그 대시보드가 만들어지면 이를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-127">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="81595-129">이 콘텐츠 팩으로 무엇을 할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="81595-129">What can I do with this content pack?</span></span>

<span data-ttu-id="81595-130">이 콘텐츠 팩으로 할 수 있는 작업으로 이동하기 전에 콘텐츠 팩의 다양 한 보고서의 빠른 미리 보기가 여기에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-130">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span></span> <span data-ttu-id="81595-131">**지난 30일** 간의 보고서 데이터가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-131">Report data goes back to the **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="81595-132">이 버전의 Azure Active Directory 로그 콘텐츠 팩에 포함된 보고서</span><span class="sxs-lookup"><span data-stu-id="81595-132">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="81595-133">**앱 사용 및 추세 보고서**: 조직에서 사용된 앱과 어떤 앱이 언제 가장 많이 사용되는지에 대한 정보를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-133">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span></span> <span data-ttu-id="81595-134">조직에서 최근에 출시된 앱이 어떻게 사용되고 있는지에 대한 정보를 수집하고 어떤 앱이 인기가 있는지 파악하기 위해 이 보고서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-134">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="81595-135">이 작업을 수행하면 앱이 사용되고 있지 않는지 확인할 때 활용도를 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-135">By doing this, you can improve usage if you see if the app is not being used.</span></span>

<span data-ttu-id="81595-136">**위치 및 사용자별 로그인**: Azure ID를 사용하여 수행된 모든 로그인에 대한 정보를 수집하고 사용자 ID에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-136">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span></span> <span data-ttu-id="81595-137">이를 통해 개별 로그인에 대해 심층적으로 분석할 수 있으며 다음과 같은 질문에 답변할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-137">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="81595-138">이 사용자는 어디에서 로그인했는가?</span><span class="sxs-lookup"><span data-stu-id="81595-138">From where did this user sign-ins?</span></span>
- <span data-ttu-id="81595-139">어느 사용자가 가장 많이 로그인하고 어디에서 로그인하는가?</span><span class="sxs-lookup"><span data-stu-id="81595-139">Which user has the most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="81595-140">성공적으로 로그인되었는가?</span><span class="sxs-lookup"><span data-stu-id="81595-140">Was the sign-in successful?</span></span>  
 
<span data-ttu-id="81595-141">특정 날짜 또는 위치를 클릭하여 세부 정보를 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-141">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="81595-142">**앱당 고유 사용자**: 지정된 앱을 사용하여 모든 고유 사용자를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="81595-142">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="81595-143">여기에는 응용 프로그램에 "*성공적으로*" 로그인한 사용자만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81595-143">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="81595-144">**장치 로그인**: 다음을 포함하여 사용자에 대한 자세한 정보와 함께 조직에서 사용자가 사용하는 OS 및 브라우저 형식을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="81595-144">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span></span>

- <span data-ttu-id="81595-145">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="81595-145">User Name</span></span>
- <span data-ttu-id="81595-146">IP 주소</span><span class="sxs-lookup"><span data-stu-id="81595-146">IP Address</span></span>
- <span data-ttu-id="81595-147">위치</span><span class="sxs-lookup"><span data-stu-id="81595-147">Location</span></span> 
- <span data-ttu-id="81595-148">로그인 상태</span><span class="sxs-lookup"><span data-stu-id="81595-148">Sign-in status</span></span> 

<span data-ttu-id="81595-149">이 보고서를 통해 조직 내에서 사용된 다양한 장치 프로필을 이해하고 용도에 따라 장치 정책을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-149">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="81595-150">**SSPR 깔때기**: 조직에서 암호 재설정이 어떻게 수행되는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-150">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="81595-151">SSPR 도구를 통해 암호를 재설정하는 데 몇 개의 암호가 필요하고 그 중 몇 개가 성공하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-151">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="81595-152">SSPR 깔때기를 사용하여 암호 재설정 실패를 심층적으로 분석하고 특정 오류가 발생하는 이유를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-152">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="81595-153">이 보고서를 통해 SSPR 도구가 조직 내에서 어떻게 사용되는지 자세히 알 수 있어 올바른 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-153">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="81595-154">Azure AD 활동 콘텐츠 팩 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="81595-154">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="81595-155">**시각화 변경**: **보고서 편집**을 클릭하여 보고서 시각화를 변경하고 원하는 시각화를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-155">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span></span>
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="81595-158">**추가 필드 포함**: 필드를 추가/제거하려는 시각적 개체를 선택하여 보고서에 필드를 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-158">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span></span> <span data-ttu-id="81595-159">아래 예에서는 "로그인 상태" 필드를 테이블 뷰에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-159">In the example below, I am adding “sign-in status” field to the table view.</span></span> 
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="81595-161">**시각화를 대시보드에 고정**: 대시보드를 사용자 지정하여 시각화를 보고서에 포함시켜 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-161">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span></span> <span data-ttu-id="81595-162">아래 예에서는 "로그인 상태"라는 새 필터를 추가하여 보고서에 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-162">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span></span> <span data-ttu-id="81595-163">또 시각화를 가로 막대형 차트에서 꺾은선형 차트로 변경했으며 새로운 시각적 개체를 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-163">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span></span>

![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="81595-166">**대시보드 공유**: 원하는 콘텐츠를 만든 후 대시보드를 조직의 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-166">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span></span> <span data-ttu-id="81595-167">보고서를 공유하면 보고서에서 선택한 필드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-167">Please remember that once you share the report, they can see the fields you have selected in the report.</span></span>
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="81595-169">Power BI 보고서의 매일 새로 고침 예약</span><span class="sxs-lookup"><span data-stu-id="81595-169">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="81595-170">Power BI 보고서의 매일 새로 고침을 예약하려면 **데이터 집합 > 설정 > 새로 고침 예약**으로 이동하고 아래와 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-170">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-to-newer-version-of-content-pack"></a><span data-ttu-id="81595-172">콘텐츠 팩의 최신 버전으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="81595-172">Updating to newer version of content pack</span></span>

<span data-ttu-id="81595-173">최신 버전을 얻기 위해 콘텐츠 팩을 업데이트 하려면:</span><span class="sxs-lookup"><span data-stu-id="81595-173">If you want to update your content pack to get a newer version:</span></span>

- <span data-ttu-id="81595-174">새 콘텐츠 팩을 다운로드하고 이 문서에 나열된 지침에 따라 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-174">Download the new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="81595-175">설정되면 **데이터 소스 > 설정 > 데이터 원본 자격 증명**으로 이동하여 아래와 같이 자격 증명을 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81595-175">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Azure Active Directory Power BI 콘텐츠 팩](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="81595-177">콘텐츠 팩의 새 버전이 작동하면 필요한 경우 이전 버전의 콘텐츠 팩과 연결된 기본 보고서 및 데이터 집합을 삭제하여 이전 버전을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81595-177">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="81595-178">아직도 문제가 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="81595-178">Still having issues?</span></span> 

<span data-ttu-id="81595-179">[문제 해결 가이드](active-directory-reporting-troubleshoot-content-pack.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="81595-179">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="81595-180">Power BI와 관련된 일반적인 도움말은 이 [도움말 문서](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="81595-180">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="81595-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81595-181">Next steps</span></span>

<span data-ttu-id="81595-182">보고 개요는 [Azure Active Directory 보고](active-directory-reporting-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81595-182">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
