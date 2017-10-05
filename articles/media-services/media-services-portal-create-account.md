---
title: "Azure 포털을 사용하여 Azure 미디어 서비스 계정 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure 포털을 사용하여 Azure 미디어 서비스 계정을 만드는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: 919a0b2f390bab353d24423d7f216e7031581aba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-media-services-account-using-the-azure-portal"></a><span data-ttu-id="812a8-103">Azure Portal을 사용하여 Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="812a8-103">Create an Azure Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="812a8-104">포털</span><span class="sxs-lookup"><span data-stu-id="812a8-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="812a8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="812a8-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="812a8-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="812a8-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="812a8-107">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="812a8-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="812a8-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="812a8-109">Azure 포털을 통해 AMS(Azure 미디어 서비스) 계정을 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-109">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="812a8-110">계정을 사용하여 Azure에서 미디어 콘텐츠를 저장, 암호화, 인코딩, 관리 및 스트리밍할 수 있는 미디어 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-110">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="812a8-111">미디어 서비스 계정을 만들 때 미디어 서비스 계정과 동일한 지역에 관련 저장소 계정도 만들거나 기존 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-111">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span></span>

<span data-ttu-id="812a8-112">이 문서에서는 몇 가지 일반적인 개념을 설명하고 Azure 포털을 사용하여 미디어 서비스 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-112">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="812a8-113">개념</span><span class="sxs-lookup"><span data-stu-id="812a8-113">Concepts</span></span>
<span data-ttu-id="812a8-114">미디어 서비스에 액세스하려면 다음 두 개의 관련 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="812a8-115">미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="812a8-115">A Media Services account.</span></span> <span data-ttu-id="812a8-116">계정을 통해 Azure에서 사용할 수 있는 클라우드 기반 미디어 서비스 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-116">Your account gives you access to a set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="812a8-117">미디어 서비스 계정은 실제 미디어 콘텐츠를 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="812a8-118">대신, 미디어 콘텐츠 및 미디어 처리 작업에 대한 메타데이터를 계정에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-118">Instead it stores metadata about the media content and media processing jobs in your account.</span></span> <span data-ttu-id="812a8-119">계정을 만들 때 사용 가능한 미디어 서비스 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-119">At the time you create the account, you select an available Media Services region.</span></span> <span data-ttu-id="812a8-120">선택한 영역은 계정에 대한 메타데이터 레코드를 저장하는 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-120">The region you select is a data center that stores the metadata records for your account.</span></span>
  
* <span data-ttu-id="812a8-121">Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="812a8-121">An Azure storage account.</span></span> <span data-ttu-id="812a8-122">저장소 계정은 Media Services 계정과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-122">Storage accounts must be located in the same geographic region as the Media Services account.</span></span> <span data-ttu-id="812a8-123">미디어 서비스 계정을 만들 때 동일한 지역의 기존 저장소 계정을 선택하거나 동일한 지역에 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-123">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span></span> <span data-ttu-id="812a8-124">미디어 서비스 계정을 삭제하는 경우 관련 저장소 계정의 Blob은 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-124">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="812a8-125">다른 지역에서 Azure Media Services 기능의 사용 가용성에 대한 정보는 [데이터 센터에서 AMS 기능의 사용 가용성](scenarios-and-availability.md#availability)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="812a8-125">For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="812a8-126">AMS 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="812a8-126">Create an AMS account</span></span>
<span data-ttu-id="812a8-127">이 섹션의 단계에서는 AMS 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-127">The steps in this section show how to create an AMS account.</span></span>

1. <span data-ttu-id="812a8-128">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-128">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="812a8-129">**+새로 만들기** > **웹 + 모바일** > **Media Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-129">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![미디어 서비스 만들기](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="812a8-131">**미디어 서비스 계정 만들기** 에 필요한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-131">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![미디어 서비스 만들기](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="812a8-133">**계정 이름**에 새 AMS 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-133">In **Account Name**, enter the name of the new AMS account.</span></span> <span data-ttu-id="812a8-134">Media Services 계정 이름은 공백 없이 모두 소문자로 이루어진 3-24자의 숫자 또는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-134">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span></span>
   2. <span data-ttu-id="812a8-135">구독에서 액세스할 수 있는 다양한 Azure 구독 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-135">In Subscription, select among the different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="812a8-136">**리소스 그룹**에서 새 또는 기존 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-136">In **Resource Group**, select the new or existing resource.</span></span>  <span data-ttu-id="812a8-137">리소스 그룹은 수명 주기, 권한 및 정책을 공유하는 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-137">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="812a8-138">[여기](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="812a8-138">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="812a8-139">**위치**에서 Media Services 계정에 대한 메타데이터 레코드 및 미디어를 저장하는 데 사용할 지리적 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-139">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span></span> <span data-ttu-id="812a8-140">이 지역은 미디어를 처리하고 스트림하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-140">This  region will be used to process and stream your media.</span></span> <span data-ttu-id="812a8-141">사용 가능한 미디어 서비스 지역만 드롭다운 목록 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-141">Only the available Media Services regions appear in the drop-down list box.</span></span> 
   5. <span data-ttu-id="812a8-142">**저장소 계정**에서 미디어 서비스 계정의 미디어 콘텐츠가 포함된 Blob 저장소를 제공할 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-142">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span></span> <span data-ttu-id="812a8-143">미디어 서비스 계정과 동일한 지역의 기존 저장소 계정을 선택하거나 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-143">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="812a8-144">동일한 지역에 새 저장소 계정이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-144">A new storage account is created in the same region.</span></span> <span data-ttu-id="812a8-145">저장소 계정 이름에 대한 규칙은 미디어 서비스 계정의 경우와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-145">The rules for storage account names are the same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="812a8-146">저장소에 대한 자세한 내용은 [여기](../storage/common/storage-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="812a8-146">Learn more about storage [here](../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="812a8-147">계정 배포 진행 상태를 보려면 **대시보드에 고정** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-147">Select **Pin to dashboard** to see the progress of the account deployment.</span></span>
4. <span data-ttu-id="812a8-148">양식 맨 아래에 있는 **만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-148">Click **Create** at the bottom of the form.</span></span>
   
    <span data-ttu-id="812a8-149">계정이 성공적으로 만들어지면 개요 페이지가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-149">Once the account is successfully created, overview page loads.</span></span> <span data-ttu-id="812a8-150">스트리밍 끝점 테이블에서 계정은 **중지됨** 상태에서 기본 스트리밍 끝점을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-150">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="812a8-151">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-151">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="812a8-152">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-152">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
   
## <a name="to-manage-your-ams-account"></a><span data-ttu-id="812a8-153">AMS 계정을 관리하려면</span><span class="sxs-lookup"><span data-stu-id="812a8-153">To manage your AMS account</span></span>

<span data-ttu-id="812a8-154">AMS 계정을 관리하려면(예: 프로그래밍 방식으로 AMS API에 연결, 비디오 업로드, 자산 인코딩, 콘텐츠 보호 구성, 작업 진행률 모니터링) 포털의 왼쪽에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-154">To manage your AMS account (for example, connect to the AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on the left side of the portal.</span></span> <span data-ttu-id="812a8-155">**설정**에서 사용할 수 있는 블레이드 중 하나로 이동합니다(예: **API 액세스**, **자산**, **작업**, **콘텐츠 보호**).</span><span class="sxs-lookup"><span data-stu-id="812a8-155">From the **Settings**, navigate to one of the available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="812a8-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="812a8-156">Next steps</span></span>

<span data-ttu-id="812a8-157">이제 AMS 계정에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="812a8-157">You can now upload files into your AMS account.</span></span> <span data-ttu-id="812a8-158">자세한 내용은 [파일 업로드](media-services-portal-upload-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="812a8-158">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="812a8-159">프로그래밍 방식으로 AMS API에 액세스하려는 경우 [Azure AD 인증을 사용하여 Azure Media Services API에 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="812a8-159">If you plan to access AMS API programmatically, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="812a8-160">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="812a8-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="812a8-161">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="812a8-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

