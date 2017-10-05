---
title: " Azure 포털을 사용하여 미디어 서비스 계정에 파일 업로드 | Microsoft Docs"
description: "이 자습서에서는 Azure 포털을 사용하여 미디어 서비스 계정에 파일을 업로드하는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 3a1dd7470f940da839687478b636464d930d8ab7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-azure-portal"></a><span data-ttu-id="1f70e-103">Azure 포털을 사용하여 미디어 서비스 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="1f70e-103">Upload files into a Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f70e-104">포털</span><span class="sxs-lookup"><span data-stu-id="1f70e-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="1f70e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1f70e-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="1f70e-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="1f70e-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="1f70e-107">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="1f70e-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f70e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="1f70e-109">미디어 서비스에서 자산에 디지털 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="1f70e-110">자산에는 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택 자막 파일(및 이러한 파일에 대한 메타데이터)이 포함될 수 있습니다. 파일이 업로드되면 이후 처리 및 스트리밍을 위해 콘텐츠가 클라우드에 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="1f70e-111">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="1f70e-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="1f70e-112">Media Services에서 처리를 위해 지원되는 최대 파일 크기에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-112">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="1f70e-113">파일 크기 제한에 대한 세부 정보는 [이](media-services-quotas-and-limitations.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f70e-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

1. <span data-ttu-id="1f70e-114">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="1f70e-115">**설정** 블레이드에서 **자산**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-115">On the **Settings** blade, click **Assets**.</span></span>
   
    ![파일 업로드](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="1f70e-117">**업로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-117">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="1f70e-118">**비디오 자산 업로드** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-118">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1f70e-119">파일 크기에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="1f70e-120">컴퓨터에 원하는 비디오를 찾아 선택하고 확인을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-120">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="1f70e-121">업로드가 시작되고 파일 이름 아래에 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-121">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="1f70e-122">업로드가 완료되면 **자산** 창에 새 자산이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-122">Once the upload completes, you will see the new asset listed in the **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1f70e-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f70e-123">Next steps</span></span>
<span data-ttu-id="1f70e-124">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="1f70e-125">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f70e-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="1f70e-126">또한 Azure Functions를 사용하여 구성된 컨테이너에 도착하는 파일에 따라 인코딩 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70e-126">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="1f70e-127">자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f70e-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1f70e-128">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="1f70e-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1f70e-129">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="1f70e-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

