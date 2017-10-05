---
title: "Azure 저장소 계정 목록"
description: "Eclipse용 Azure 도구 키트를 사용하여 저장소 계정 설정 관리"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="54113-103">Azure 저장소 계정 목록</span><span class="sxs-lookup"><span data-stu-id="54113-103">Azure Storage Account List</span></span>
<span data-ttu-id="54113-104">Azure 저장소 계정은 JDK, 응용 프로그램 서버, 임의 구성 요소뿐만 아니라 캐싱을 사용하는 경우 상태 저장을 위해 다운로드 위치를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="54113-105">Eclipse는 프로젝트에 사용할 수 있는 알려진 저장소 계정 목록을 사용자의 Eclipse 작업 공간에 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="54113-106">목록을 관리하는 데 사용되는 **저장소 계정** 대화 상자를 열려면, Eclipse에서 **창**, **기본 설정**을 차례로 클릭하고 **Azure**를 확장한 다음 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="54113-107">다음은 **Storage Accounts** 대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="54113-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="54113-108">이 대화 상자는 다음과 같이 저장소 계정을 사용하는 대화 상자의 **Accounts** 링크를 통해 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="54113-109">**서버 구성** 대화 상자의 **JDK** 탭</span><span class="sxs-lookup"><span data-stu-id="54113-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="54113-110">**서버 구성** 대화 상자의 **서버** 탭</span><span class="sxs-lookup"><span data-stu-id="54113-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="54113-111">**Add Component** 대화 상자</span><span class="sxs-lookup"><span data-stu-id="54113-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="54113-112">**Caching** 속성 대화 상자</span><span class="sxs-lookup"><span data-stu-id="54113-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="54113-113">게시 설정 파일을 사용하여 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="54113-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="54113-114">**저장소 계정** 대화 상자에서 **PUBLISH-SETTINGS 파일에서 가져오기**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="54113-115">(게시 설정 파일을 로컬 컴퓨터에 이미 저장한 경우에는 이 단계를 건너뜁니다.) **구독 정보 가져오기** 대화 상자에서 **PUBLISH-SETTINGS 파일 다운로드**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="54113-116">Azure 계정에 로그인하지 않은 경우에는 로그인을 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54113-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="54113-117">그 후 Azure 게시 설정 파일을 저장하도록 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54113-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="54113-118">(로그인 페이지에 이렇게 표시되는 지침은 무시할 수 있습니다. 이러한 지침은 Azure 포털에 의해 제공되며 Visual Studio 사용자를 위한 것입니다.) 로컬 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="54113-119">**구독 정보 가져오기** 대화 상자에서 **찾아보기** 단추를 클릭하고 이전에 로컬에 저장해 놓은 게시 설정 파일을 선택한 다음 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="54113-120">**확인**을 클릭하여 **구독 정보 가져오기** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="54113-121">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="54113-121">To create a new storage account</span></span>
1. <span data-ttu-id="54113-122">**저장소 계정** 대화 상자에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="54113-123">**저장소 계정 추가** 대화 상자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="54113-124">**New Storage Account** 대화 상자에서 다음 항목에 대한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="54113-125">저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="54113-125">Storage account name.</span></span>

   * <span data-ttu-id="54113-126">저장소 계정의 위치</span><span class="sxs-lookup"><span data-stu-id="54113-126">Location of the storage account.</span></span>

   * <span data-ttu-id="54113-127">저장소 계정에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="54113-127">Description of the storage account.</span></span>

   * <span data-ttu-id="54113-128">저장소 계정이 속해 있는 구독</span><span class="sxs-lookup"><span data-stu-id="54113-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="54113-129">**확인**를 클릭하여 **새 저장소 계정** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="54113-130">저장소 계정을 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="54113-131">계정이 생성된 후에 **확인**를 클릭하여 **저장소 계정 추가** 대화 상자를 닫으면, 새 저장소 계정이 사용 가능한 저장소 계정 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="54113-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="54113-132">기존 저장소 계정을 목록에 추가</span><span class="sxs-lookup"><span data-stu-id="54113-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="54113-133">Azure 저장소 계정이 없는 경우에는 위의 **새 저장소 계정 만들기 섹션** 에 나열된 단계에 따라서 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54113-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="54113-134">(또는 [Azure Management Portal][Azure Management Portal]에서 새 저장소 계정을 만들 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="54113-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="54113-135">**저장소 계정** 대화 상자에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="54113-136">**저장소 계정 추가** 대화 상자에서 **이름** 및 **선택키**의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="54113-137">계정 이름 및 액세스 키는 기존 Azure 저장소 계정에 대한 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="54113-138">저장소 계정 이름 및 키를 보려면 [Azure Management Portal][Azure Management Portal]의 **저장소** 섹션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="54113-139">**Add Storage Account** 대화 상자는 다음과 유사한 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="54113-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="54113-140">**확인**을 클릭하여 **저장소 계정 추가** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="54113-141">새 액세스 키를 사용하도록 저장소 계정 수정</span><span class="sxs-lookup"><span data-stu-id="54113-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="54113-142">**저장소 계정** 대화 상자에서 편집할 저장소 계정을 클릭한 후 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="54113-143">**저장소 계정 선택기 편집** 대화 상자에서 **선택키** 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="54113-144">**확인**을 클릭하고 **저장소 계정 선택기 편집** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="54113-145">Eclipse에 유지 관리되는 목록에서 저장소 계정 제거</span><span class="sxs-lookup"><span data-stu-id="54113-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="54113-146">**저장소 계정** 대화 상자에서 편집할 저장소 계정을 클릭한 후 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="54113-147">저장소 계정을 제거한다는 메시지가 표시되면 **OK** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54113-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="54113-148">**Storage Accounts** 대화 상자를 통해 저장소 계정을 제거하면, 계정은 Eclipse 내에서 볼 수 있는 저장소 계정 목록에서만 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="54113-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="54113-149">Azure 구독에서 저장소 계정을 제거하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="54113-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="54113-150">아울러 Eclipse에서 구독 세부 정보를 다시 로드한 후에 저장소 계정이 다시 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54113-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="54113-151">참고 항목</span><span class="sxs-lookup"><span data-stu-id="54113-151">See Also</span></span>
<span data-ttu-id="54113-152">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="54113-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="54113-153">[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="54113-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="54113-154">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="54113-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="54113-155">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54113-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
