---
title: "저장소 계정 목록을 aaaAzure"
description: "저장소 계정 설정을 Eclipse 용 Azure 도구 키트 hello를 사용 하 여 관리"
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="215ec-103">Azure 저장소 계정 목록</span><span class="sxs-lookup"><span data-stu-id="215ec-103">Azure Storage Account List</span></span>
<span data-ttu-id="215ec-104">Azure 저장소 계정을 사용 하는 JDK, 응용 프로그램 서버 및 임의 구성 요소는 물론 캐싱을 사용할 때 상태를 저장 하는 데 사용 되는 위치 toobe를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="215ec-105">Eclipse는 Eclipse 작업 영역에서 사용할 수 있는 tooyour 프로젝트는 알려진된 저장소 계정 목록을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="215ec-106">tooopen hello **저장소 계정은** 대화 상자를 사용 하는 toomanage Eclipse 내에서 나열 하는 클릭 **창**, 클릭 **기본 설정**, 확장 **Azure** , 클릭 하 고 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="215ec-107">hello 다음 표시 되어 hello **저장소 계정은** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="215ec-108">이 대화 상자에서 열 수도 있습니다는 **계정** hello 다음과 같은 저장소 계정을 사용 하는 대화 상자에서 링크:</span><span class="sxs-lookup"><span data-stu-id="215ec-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="215ec-109">hello **JDK** hello 탭 **서버 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="215ec-110">hello **서버** hello 탭 **서버 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="215ec-111">hello **구성 요소 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="215ec-112">hello **캐싱** 속성 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="215ec-113">저장소를 사용 하 여 계정을 tooimport 게시 설정 파일</span><span class="sxs-lookup"><span data-stu-id="215ec-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="215ec-114">Hello 내 **저장소 계정은** 대화 상자에서 클릭 **게시 설정 파일에서 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="215ec-115">(이 단계는 이미 게시 설정 파일 tooyour 로컬 컴퓨터를 저장 하는 경우.) Hello에 **구독 정보 가져오기** 대화 상자를 클릭 하 여 **게시 설정 파일 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="215ec-116">아직 Azure 계정에 로그인 하지 않은 경우에 증명된 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="215ec-117">다음 메시지가 표시 됩니다 toosave Azure 게시 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="215ec-118">(Hello hello 로그온 페이지에 표시 되는 결과 지침을 무시할 수 hello Azure 포털에서 제공 하며 Visual Studio 사용자를 대상으로 합니다.) Tooyour 로컬 시스템으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="215ec-119">Hello에 여전히 **구독 정보 가져오기** 대화 상자에서 hello 클릭 **찾아보기** 단추, 선택 hello 설정을 저장 한 파일을 로컬에서 이전에 게시 하 고 클릭 **열**.</span><span class="sxs-lookup"><span data-stu-id="215ec-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="215ec-120">클릭 **확인** tooclose hello **구독 정보 가져오기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="215ec-121">toocreate 새 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="215ec-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="215ec-122">Hello 내 **저장소 계정은** 대화 상자에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="215ec-123">Hello 내 **저장소 계정 추가** 대화 상자를 클릭 하 여 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="215ec-124">Hello 내 **새 저장소 계정** 대화 상자에서 다음 hello에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="215ec-125">저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="215ec-125">Storage account name.</span></span>

   * <span data-ttu-id="215ec-126">Hello 저장소 계정의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="215ec-127">Hello 저장소 계정에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="215ec-128">hello 구독 toowhich hello 저장소 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="215ec-129">클릭 **확인** tooclose hello **새 저장소 계정** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="215ec-130">만든 저장소 계정 toobe 프로그램에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="215ec-131">를 만든 후 클릭 **확인** tooclose hello **저장소 계정 추가** 대화 상자에서 및 새로운 저장소 계정이 사용 가능한 저장소 계정 목록이 toohello 추가 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="215ec-132">기존 저장소 계정 toohello 목록 tooadd</span><span class="sxs-lookup"><span data-stu-id="215ec-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="215ec-133">Hello에 나열 된 hello 단계를 수행 하면 아직 없는 Azure 저장소 계정, 만들 경우 **toocreate 새 저장소 계정 섹션** 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="215ec-134">(새 저장소 계정을 hello에서 만들 수 있습니다 또는 [Azure 관리 포털][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="215ec-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="215ec-135">Hello 내 **저장소 계정은** 대화 상자에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="215ec-136">Hello 내 **저장소 계정 추가** 대화 상자에서 값을 입력 **이름** 및 **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="215ec-137">기존 Azure 저장소 계정에 대 한 hello 계정 이름과 액세스 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="215ec-138">사용 하 여 hello **저장소** hello 섹션 [Azure 관리 포털] [ Azure Management Portal] tooview 저장소 계정의 이름을 지정 하 고 키입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="215ec-139">프로그램 **저장소 계정 추가** 대화 상자가 유사 toohello 다음에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="215ec-140">클릭 **확인** tooclose hello **저장소 계정 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="215ec-141">toomodify 저장소 계정 toouse 새 액세스 키</span><span class="sxs-lookup"><span data-stu-id="215ec-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="215ec-142">Hello 내 **저장소 계정은** 대화 상자에서 tooedit 원하고 클릭 hello 저장소 계정을 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="215ec-143">Hello 내 **저장소 계정 액세스 키 편집** 대화 상자에서 hello 수정 **선택 키** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="215ec-144">클릭 **확인** tooclose hello **저장소 계정 액세스 키 편집** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="215ec-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="215ec-145">tooremove hello 목록에서 저장소 계정을 Eclipse에서 유지 관리</span><span class="sxs-lookup"><span data-stu-id="215ec-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="215ec-146">Hello 내 **저장소 계정은** 대화 상자에서 tooedit 원하고 클릭 hello 저장소 계정을 클릭 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="215ec-147">클릭 **확인** 때 메시지 표시 tooremove hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="215ec-148">Hello 통해 hello 저장소 계정을 제거 하는 **저장소 계정은** 대화만이 목록에서 제거 hello Eclipse 내에서 볼 수 있는 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="215ec-149">Azure 구독에서 저장소 계정을 hello를 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="215ec-150">또한 hello 저장소 계정 수 다시 목록에 표시 Eclipse 구독 hello 세부 정보를 다시 로드 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="215ec-151">참고 항목</span><span class="sxs-lookup"><span data-stu-id="215ec-151">See Also</span></span>
<span data-ttu-id="215ec-152">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="215ec-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="215ec-153">[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="215ec-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="215ec-154">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="215ec-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="215ec-155">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="215ec-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
