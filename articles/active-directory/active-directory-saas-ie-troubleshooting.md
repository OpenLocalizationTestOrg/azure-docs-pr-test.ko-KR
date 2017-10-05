---
title: "IE에 대한 액세스 패널 확장 문제 해결| Microsoft Azure"
description: "그룹 정책을 사용하여 My Apps 포털용 Internet Explorer 추가 기능을 배포하는 방법"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="d8d90-103">Internet Explorer용 액세스 패널 확장 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d8d90-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="d8d90-104">이 문서는 다음과 같은 문제를 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="d8d90-105">Internet Explorer를 사용하는 중에 My Apps 포털을 통해 응용 프로그램에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="d8d90-106">소프트웨어를 이미 설치했는데도 "소프트웨어 설치" 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="d8d90-107">관리자인 경우 [Internet Explorer용 액세스 패널 확장을 배포하는 방법](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="d8d90-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="d8d90-108">진단 도구 실행</span><span class="sxs-lookup"><span data-stu-id="d8d90-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="d8d90-109">액세스 패널 진단 도구를 다운로드 및 실행하여 액세스 패널 확장의 설치 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="d8d90-110">진단 도구를 다운로드하려면 여기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="d8d90-111">파일을 열고 **모두 추출** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-111">Open the file, and press **Extract all** button.</span></span>
   
    ![모두 추출 누르기](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="d8d90-113">그런 다음 **추출** 단추를 눌러 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-113">Then press the **Extract** button to continue.</span></span>
   
    ![추출 누르기](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="d8d90-115">도구를 실행하려면 이름이 **AccessPanelExtensionDiagnosticTool**인 파일을 마우스 오른쪽 단추로 클릭한 다음 **열기 > Microsoft Windows 기반 스크립트 호스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![열기 > Microsoft Windows 기반 스크립트 호스트](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="d8d90-117">그러면 다음 진단 창이 표시되어 가능한 설치 문제를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![진단 창 샘플](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="d8d90-119">"**예**"를 클릭하여 프로그램이 발견한 문제를 수정하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="d8d90-120">이러한 변경 내용을 저장하려면 모든 Internet Explorer 창을 닫은 다음 Internet Explorer를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="d8d90-121">여전히 앱에 액세스할 수 없으면 다음 단계를 수행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d8d90-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="d8d90-122">액세스 패널 확장을 사용할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="d8d90-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="d8d90-123">액세스 패널 확장이 Internet Explorer에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="d8d90-124">Internet Explorer에서 창 오른쪽 위 모퉁이에 있는 **기어 아이콘**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="d8d90-125">그런 다음 **인터넷 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="d8d90-126">이전 버전의 Internet Explorer에서는 **도구 > 인터넷 옵션** 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![도구 > 인터넷 옵션으로 이동](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="d8d90-128">**프로그램** 탭을 클릭한 다음 **추가 기능 관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![추가 기능 관리 클릭](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="d8d90-130">이 대화 상자에서 **액세스 패널 확장**을 클릭하고 **사용** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![사용 클릭](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="d8d90-132">이러한 변경 내용을 저장하려면 모든 Internet Explorer 창을 닫은 다음 Internet Explorer를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="d8d90-133">InPrivate 브라우징에 확장 사용</span><span class="sxs-lookup"><span data-stu-id="d8d90-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="d8d90-134">InPrivate 브라우징 모드를 사용 중인 경우:</span><span class="sxs-lookup"><span data-stu-id="d8d90-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="d8d90-135">Internet Explorer에서 창 오른쪽 위 모퉁이에 있는 **기어 아이콘**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="d8d90-136">그런 다음 **인터넷 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="d8d90-137">이전 버전의 Internet Explorer에서는 **도구 > 인터넷 옵션** 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![진단 창 샘플](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="d8d90-139">**개인정보** 탭으로 이동한 다음 이름이 **InPrivate 브라우징 시작 시 도구 모음 및 확장 프로그램 사용 안 함** 확인란을 **선택 취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![InPrivate 브라우징 시작 시 도구 모음 및 확장 프로그램 사용 안 함](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="d8d90-141">이러한 변경 내용을 저장하려면 모든 Internet Explorer 창을 닫은 다음 Internet Explorer를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="d8d90-142">액세스 패널 확장 제거</span><span class="sxs-lookup"><span data-stu-id="d8d90-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="d8d90-143">컴퓨터에서 액세스 패널 확장을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="d8d90-144">키보드에서 **Windows 키** 를 눌러 시작 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="d8d90-145">메뉴를 열면 검색 작업에 아무 항목이나 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="d8d90-146">"제어판"을 입력한 다음 검색 결과에 표시되면 **제어판** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![제어판 검색](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="d8d90-148">제어판의 오른쪽 위 모퉁이에서 **보기** 옵션을 **큰 아이콘**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="d8d90-149">그런 다음 **프로그램 및 기능** 단추를 찾아 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![큰 아이콘을 표시하도록 보기 변경](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="d8d90-151">목록에서 **액세스 패널 확장**을 선택하고 **제거** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![제거 클릭](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="d8d90-153">그런 다음 확장을 다시 설치하여 문제가 해결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="d8d90-154">확장을 제거하는 데 문제가 있으면 [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) 도구를 사용하여 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d90-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d8d90-155">관련 문서</span><span class="sxs-lookup"><span data-stu-id="d8d90-155">Related Articles</span></span>
* [<span data-ttu-id="d8d90-156">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="d8d90-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d8d90-157">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8d90-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d8d90-158">그룹 정책을 사용하여 Internet Explorer용 액세스 패널 확장을 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8d90-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

