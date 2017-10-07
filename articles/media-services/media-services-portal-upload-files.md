---
title: "aaa\"hello Azure 포털을 사용 하 여 미디어 서비스 계정에 파일을 업로드 | \"Microsoft Docs"
description: "이 자습서에서는 업로드 파일의 hello 단계 hello Azure 포털을 사용 하 여 미디어 서비스 계정에"
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
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="ae85d-103">Hello Azure 포털을 사용 하 여 미디어 서비스 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ae85d-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae85d-104">포털</span><span class="sxs-lookup"><span data-stu-id="ae85d-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="ae85d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ae85d-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="ae85d-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="ae85d-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="ae85d-107">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="ae85d-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae85d-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="ae85d-109">미디어 서비스에서 자산에 디지털 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="ae85d-110">비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터) hello 자산 포함 될 수 있습니다. Hello 파일 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="ae85d-111">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ae85d-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="ae85d-112">미디어 서비스에서 처리에 지원 되는 제한 toohello 최대 파일 크기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="ae85d-113">참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="ae85d-114">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="ae85d-115">Hello에 **설정** 블레이드에서 클릭 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![파일 업로드](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="ae85d-117">Hello 클릭 **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="ae85d-118">hello **비디오 자산을 업로드** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae85d-119">파일 크기에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="ae85d-120">컴퓨터에 필요한 toohello 비디오 찾아보기 선택한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="ae85d-121">hello 업로드 시작 하 고 hello 파일 이름에서 hello 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="ae85d-122">Hello에 나열 된 hello 새 자산을 보게 hello 업로드가 완료 되 면 **자산** 창.</span><span class="sxs-lookup"><span data-stu-id="ae85d-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ae85d-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae85d-123">Next steps</span></span>
<span data-ttu-id="ae85d-124">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="ae85d-125">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae85d-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="ae85d-126">또한 Azure 함수 tootrigger hello 구성 컨테이너에 도착 하는 파일을 기반으로 하는 인코딩 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae85d-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="ae85d-127">자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae85d-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ae85d-128">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ae85d-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ae85d-129">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ae85d-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

