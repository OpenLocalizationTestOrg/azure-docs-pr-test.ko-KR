---
title: "Aspera를 사용 하 여 Azure 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "이 자습서에서는 예제 hello를 사용 하 여 미디어 서비스 계정에 연결 된 저장소 계정에 파일을 업로드 hello 단계 * * Aspera 서버에서 요청 시 * * Azure 서비스입니다."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="61ef9-103">Hello Aspera Server On Demand 서비스를 사용 하 여 Azure에서 미디어 서비스 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="61ef9-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="61ef9-104">개요</span><span class="sxs-lookup"><span data-stu-id="61ef9-104">Overview</span></span>

<span data-ttu-id="61ef9-105">**Aspera** 는 고속 파일 전송 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="61ef9-106">Azure용 **Aspera Server On Demand**는 Azure BLOB 개체 저장소에 직접 대용량 파일을 고속으로 업로드 및 다운로드할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="61ef9-107">에 대 한 내용은 **Aspera On Demand**, hello 참조 [Aspera 클라우드](http://cloud.asperasoft.com/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="61ef9-108">**Aspera Server On Demand** Azure hello에서 구입할 수에 대 한 [Azure 마켓플레이스](https://azure.microsoft.com/en-us/marketplace/)합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="61ef9-109">순서로 toocomplete의 구매 **Aspera Server On Demand** Azure에 로그인 한 다음 Windows Live id를 사용 하 여 Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="61ef9-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="61ef9-110">이 자습서에서는 예제 hello를 사용 하 여 미디어 서비스 계정에 연결 된 저장소 계정에 파일을 업로드 hello 단계 **Aspera Server On Demand** Azure에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="61ef9-111">Azure toouse Aspera 및 미디어 서비스와 작동 하는 방법을 보여 주는 예제를 찾을 수 있습니다 [여기](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest)합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="61ef9-112">Azure 미디어 서비스로 미디어 프로세서 (Mp) 처리에 지원 제한 toohello 최대 파일 크기를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="61ef9-113">참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="61ef9-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="61ef9-114">Prerequisites</span></span> 

<span data-ttu-id="61ef9-115">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="61ef9-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="61ef9-116">Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="61ef9-116">A Windows Live ID</span></span>
* <span data-ttu-id="61ef9-117">[Azure 계정](https://azure.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="61ef9-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="61ef9-118">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61ef9-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="61ef9-119">[Azure Media Services 계정](media-services-portal-create-account.md)</span><span class="sxs-lookup"><span data-stu-id="61ef9-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="61ef9-120">Azure용 Aspera On Demand 구매</span><span class="sxs-lookup"><span data-stu-id="61ef9-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="61ef9-121">Azure Marketplace에 로그인 하면 이러한 기본 단계 toocomplete Aspera On Demand for Azure의 구입을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="61ef9-122">Aspera를 검색하고 'Server On Demand'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="61ef9-124">Hello 구독 계획을 검토 하 고 ' 등록 ' 클릭</span><span class="sxs-lookup"><span data-stu-id="61ef9-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="61ef9-126">요청 시 구독에서 서버에 대 한 hello 고유 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="61ef9-128">Hello 클릭 **가격 책정 계층** hello sub 패널에서 원하는 월별 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="61ef9-129">Hello에 **세부 정보를 계획** 패널에서 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="61ef9-130">그런 다음, hello **가격 책정 계층 선택** 에서 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="61ef9-132">클릭 **약관** tooview hello hello sub 패널의 법적 조항에 동의 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="61ef9-133">Hello 약관을 검토 한 후 클릭 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="61ef9-135">클릭 하 여 hello 구매를 완료 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="61ef9-137">Azure 대시보드 hello 공지 hello 서비스 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="61ef9-138">프로비저닝 완료 되 면 hello hello 서비스 이름에 대 한 리소스를 검색 하 여 hello 새 구독을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="61ef9-139">발견 하면 hello 서비스를 두 번 클릭 toolaunch hello 서비스 관리 포털.</span><span class="sxs-lookup"><span data-stu-id="61ef9-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="61ef9-141">Hello Aspera 관리 포털을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="61ef9-142">새 Aspera 서비스를 발견 하면 hello 서비스를 클릭 하 여 액세스 toohello 관리 포털을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="61ef9-143">새 패널이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-143">A new panel will be launched.</span></span> <span data-ttu-id="61ef9-144">새 해당 패널 내에서 필요한 hello에 tooclick **리소스 이름** 새 서비스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="61ef9-145">다음 스크린 샷 hello, hello 리소스 이름은 'AsperaTransferDemo'입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="61ef9-146">Hello 리소스 이름을 클릭 한 후 다른 패널 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="61ef9-147">새로 시작된 패널에 '관리' 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="61ef9-148">'관리' 링크 toolaunch hello Aspera 관리 포털 hello 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="61ef9-150">Hello를 클릭 하 여 관리 링크, 필요한 toohello 등록 페이지를 얻게 됩니다 tooaccess hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="61ef9-152">이 시점에서 액세스 toohello Aspera 서비스 관리 포털 수 선택 키 만들기, 다운로드 Aspera 클라이언트 및 라이선스, 사용법을 참조 하 고 있는 hello Api에 대 한 자세한 내용은 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="61ef9-153">hello 다음 스크린샷은 hello 액세스 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="61ef9-155">hello 다음 스크린샷은 hello 사용 hello 포털에서 인터페이스를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="61ef9-157">Aspera를 사용하여 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="61ef9-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="61ef9-158">다운로드 하 고 hello Aspera 클라이언트 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="61ef9-159">브라우저 플러그 인</span><span class="sxs-lookup"><span data-stu-id="61ef9-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="61ef9-160">리치 클라이언트</span><span class="sxs-lookup"><span data-stu-id="61ef9-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="61ef9-161">첫 번째 전송을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="61ef9-161">Make your first transfer.</span></span> <span data-ttu-id="61ef9-162">순서 toouse hello Aspera 클라이언트 tootransfer hello Aspera 전송 서비스와, toocomplete hello 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="61ef9-163">Hello Aspera 포털을 사용 하는 액세스 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="61ef9-164">다운로드, 설치 및 라이선스 hello Aspera 클라이언트 (소프트웨어 hello Aspera 포털에서 확인할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="61ef9-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="61ef9-165">구성 정보에 대 한 hello Aspera 클라이언트 가이드를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="61ef9-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="61ef9-166">Hello를 사용 하 여 Azure 미디어 계정와 연결 된 저장소 계정의 일부 정보를 검색할 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="61ef9-167">특히, 이름 및 키 및 hello 저장소 blob 컨테이너 이름에서 toowhich 원하는 tooplace 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="61ef9-168">hello 포털에서 tooget hello 저장소 정보: 저장소 계정의 찾을 hello 액세스 키 및 복사 사용자의 계정 이름 및 hello 키 hello 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="61ef9-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="61ef9-169">tooget hello 컨테이너 이름: 저장소 계정 선택 찾기 **Blob**선택, tooupload hello 콘텐츠를 원하는 hello 컨테이너의 hello 이름.</span><span class="sxs-lookup"><span data-stu-id="61ef9-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="61ef9-170">다음은 이러한 hello Aspera 클라이언트의 hello 스크린 샷 **연결 관리자** hello 'Azure' 저장소 유형 및 자격 증명으로 hello blob 컨테이너를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="61ef9-172">리소스</span><span class="sxs-lookup"><span data-stu-id="61ef9-172">Resources</span></span>

<span data-ttu-id="61ef9-173">다음 리소스는 hello 된이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="61ef9-174">브라우저 플러그 인 연결</span><span class="sxs-lookup"><span data-stu-id="61ef9-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="61ef9-175">가이드 연결</span><span class="sxs-lookup"><span data-stu-id="61ef9-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="61ef9-176">Aspera 클라이언트</span><span class="sxs-lookup"><span data-stu-id="61ef9-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="61ef9-177">클라이언트 가이드</span><span class="sxs-lookup"><span data-stu-id="61ef9-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="61ef9-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61ef9-178">Next steps</span></span>

<span data-ttu-id="61ef9-179">이제 [Blob을 저장소 계정에서 AMS 계정으로 복사](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61ef9-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="61ef9-180">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="61ef9-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61ef9-181">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="61ef9-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

