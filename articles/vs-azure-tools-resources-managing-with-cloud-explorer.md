---
title: "클라우드 탐색기를 사용하여 Azure 리소스 관리 | Microsoft Docs"
description: "클라우드 탐색기를 사용하여 Visual Studio 내에서 Azure 리소스를 검색 및 관리하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="0b6d2-103">Visual Studio 클라우드 탐색기에서 Azure 계정과 연결된 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="0b6d2-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="0b6d2-104">클라우드 탐색기를 사용하여 Azure 리소스 및 리소스 그룹을 보고, 해당 속성을 검사하고, Visual Studio 내에서 핵심 개발자 진단 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="0b6d2-105">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)에서와 마찬가지로 클라우드 탐색기는 Azure Resource Manager 스택을 토대로 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="0b6d2-106">따라서 클라우드 탐색기는 Azure 리소스 그룹과 같은 리소스 및 논리 앱과 API 앱과 같은 Azure 서비스를 이해하고 RBAC([역할 기반 액세스 제어](active-directory/role-based-access-control-configure.md))를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0b6d2-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0b6d2-107">Prerequisites</span></span>
- <span data-ttu-id="0b6d2-108">**Azure 워크로드**가 선택된 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 또는 [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657)가 있는 이전 버전의 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b6d2-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="0b6d2-109">Microsoft Azure 계정 - 계정이 없는 경우 [평가판을 등록](http://go.microsoft.com/fwlink/?LinkId=623901)하거나 [Visual Studio 구독자 혜택을 활성화](http://go.microsoft.com/fwlink/?LinkId=623901)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="0b6d2-110">클라우드 탐색기를 보려면 메뉴 모음에서 **보기** > **클라우드 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="0b6d2-111">클라우드 탐색기에 Azure 계정 추가</span><span class="sxs-lookup"><span data-stu-id="0b6d2-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="0b6d2-112">Azure 계정에 연결된 리소스를 보려면 먼저 클라우드 탐색기에 계정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="0b6d2-113">**클라우드 탐색기**에서 **Azure 계정 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![클라우드 탐색기 Azure 계정 설정 아이콘](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="0b6d2-115">**새 계정 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-115">Select **Add new account**.</span></span> 

    ![클라우드 탐색기 계정 추가 링크](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="0b6d2-117">해당 리소스를 검색하려는 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="0b6d2-118">Azure 계정에 로그인하면 해당 계정과 연결된 구독이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="0b6d2-119">탐색할 계정 구독에 대한 확인란을 선택한 다음 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![클라우드 탐색기: 표시할 Azure 구독 선택](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="0b6d2-121">해당 리소스를 검색하려는 구독을 선택하면 해당 구독 및 리소스가 클라우드 탐색기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Azure 계정에 대한 클라우드 탐색기 리소스 목록](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="0b6d2-123">클라우드 탐색기에서 Azure 계정 제거</span><span class="sxs-lookup"><span data-stu-id="0b6d2-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="0b6d2-124">**클라우드 탐색기**에서 **Azure 계정 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![클라우드 탐색기 Azure 계정 설정 아이콘](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="0b6d2-126">제거할 계정 옆에 있는 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![클라우드 탐색기 Azure 계정 설정 아이콘](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="0b6d2-128">리소스 종류 또는 리소스 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="0b6d2-128">View resource types or resource groups</span></span>
<span data-ttu-id="0b6d2-129">Azure 리소스를 보려면 **리소스 종류** 또는 **리소스 그룹** 보기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="0b6d2-130">**클라우드 탐색기**에서 리소스 보기 드롭다운을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![원하는 리소스 보기를 선택하기 위한 클라우드 탐색기 드롭다운 목록](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="0b6d2-132">상황에 맞는 메뉴에서 원하는 보기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="0b6d2-133">**리소스 종류** 보기 - [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)에서 사용되는 일반적인 보기로, 웹앱, 저장소 계정 및 가상 컴퓨터와 같은 형식으로 분류된 Azure 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="0b6d2-134">**리소스 그룹** 보기 - 연관된 Azure 리소스 그룹으로 Azure 리소스를 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="0b6d2-135">리소스 그룹은 일반적으로 특정 응용 프로그램에서 사용되는 Azure 리소스 번들입니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="0b6d2-136">Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](./azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="0b6d2-137">다음 이미지는 두 리소스 보기를 비교해서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-137">The following image shows a comparison of the two resource views:</span></span>

    ![클라우드 탐색기 리소스 보기 비교](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="0b6d2-139">클라우드 탐색기에서 리소스 보기 및 탐색</span><span class="sxs-lookup"><span data-stu-id="0b6d2-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="0b6d2-140">클라우드 탐색기에서 Azure 리소스를 탐색하고 정보를 보려면, 항목의 형식 또는 연결된 리소스 그룹을 확장한 다음 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="0b6d2-141">리소스를 선택하면 클라우드 탐색기의 아래쪽의 두 탭, 즉 **작업** 및 **속성**에 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="0b6d2-142">**작업** 탭 - 선택한 리소스에 대해 클라우드 탐색기에서 수행할 수 있는 동작을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="0b6d2-143">또한 리소스를 클릭하여 상황에 맞는 메뉴에서 이러한 옵션을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="0b6d2-144">**속성** 탭 - 해당 유형, 로캘 및 연관된 리소스 그룹과 같은 리소스의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="0b6d2-145">다음 이미지에는 App Service의 각 탭에 표시되는 내용을 비교한 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="0b6d2-146">모든 리소스에는 **포털에서 열기**작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="0b6d2-147">이 작업을 선택하면 클라우드 탐색기는 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에서 선택한 리소스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="0b6d2-148">**포털에서 열기** 기능은 여러 층으로 중첩된 리소스를 탐색하기에 더욱 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="0b6d2-149">추가 작업 및 속성 값은 Azure 리소스에 따라 다르게 나타날 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="0b6d2-150">예를 들어 웹앱 및 논리 앱에는 **포털에서 열기** 외에 **브라우저에서 열기** 및 **디버거 연결** 작업도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="0b6d2-151">저장소 계정 blob, 큐 또는 테이블을 선택하면 편집기를 열려는 작업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="0b6d2-152">Azure 앱에는 **URL** 및 **상태** 속성이 있으며, 저장소 리소스에는 키와 연결 문자열 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="0b6d2-153">클라우드 탐색기에서 리소스 찾기</span><span class="sxs-lookup"><span data-stu-id="0b6d2-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="0b6d2-154">Azure 계정 구독에서 특정 이름의 리소스를 찾으려면 클라우드 탐색기의 **검색** 상자에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![클라우드 탐색기에서 리소스 찾기](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="0b6d2-156">**검색** 상자에 문자를 입력하면 해당 문자와 일치하는 리소스만 리소스 트리에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0b6d2-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
