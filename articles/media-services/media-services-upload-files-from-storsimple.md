---
title: "Azure StorSimple에서 Azure 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "이 문서에서는 Azure StorSimple 데이터 관리자를 간략하게 설명합니다. hello 문서는 방법을 보여 주는 tootutorials 링크도 StorSimple에서 tooextract 데이터 자산 tooan Azure 미디어 서비스 계정으로 업로드 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="a87c2-104">Azure StorSimple의 Azure Media Services 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="a87c2-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="a87c2-105">이 문서에서는 Azure StorSimple 데이터 관리자를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="a87c2-106">hello 문서는 방법을 보여 주는 tootutorials 링크도 StorSimple에서 tooextract 데이터 자산 tooan Azure 미디어 서비스 (AMS) 계정으로이 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="a87c2-107">현재 Azure StorSimple 데이터 관리자는 비공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="a87c2-108">개요</span><span class="sxs-lookup"><span data-stu-id="a87c2-108">Overview</span></span>

<span data-ttu-id="a87c2-109">미디어 서비스에서 자산에 디지털 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="a87c2-110">비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터) hello 자산 포함 될 수 있습니다. Hello 파일 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="a87c2-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) hello의 확장 온-프레미스 솔루션 고 hello 온-프레미스 저장소와 클라우드 저장소에서 데이터를 자동으로 눈금 클라우드 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="a87c2-112">hello StorSimple 장치 dedupes 및 큰 파일 toohello 클라우드를 보내기 위한 매우 효율적으로 만드는 toohello 클라우드를 보내기 전에 데이터를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="a87c2-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) 서비스는 StorSimple의 있습니다 tooextract 데이터를 사용 하 고 AMS 자산으로 제공 하는 Api를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="a87c2-114">시작</span><span class="sxs-lookup"><span data-stu-id="a87c2-114">Get started</span></span>

1. <span data-ttu-id="a87c2-115">[미디어 서비스 계정 만들기](media-services-portal-create-account.md) 넣을 tootransfer hello 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="a87c2-116">Hello에 설명 된 대로 데이터 관리자 미리 보기에 등록 [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a87c2-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="a87c2-117">StorSimple 데이터 관리자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="a87c2-118">데이터 변환 작업을 실행할 때 만들고 StorSimple 장치에서 데이터를 추출하고 AMS 계정에 자산으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="a87c2-119">Hello 작업 실행을 시작할 때 저장소 큐 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="a87c2-120">이 큐는 준비가 완료된 변환 Blob에 대한 메시지로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="a87c2-121">이 큐의 hello 이름 hello 작업 정의의 hello 이름과 달라 서 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="a87c2-122">이 큐 toodetermine를 사용할 수 있습니다 때 자산 그대로 준비를 호출 하 여 원하는 미디어 서비스 작업 toorun 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="a87c2-123">예를 들어이 큐 tootrigger hello 필요한 미디어 서비스 코드에 있는 Azure 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="a87c2-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a87c2-124">See also</span></span>

[<span data-ttu-id="a87c2-125">사용 하 여.Net SDK hello hello 데이터 관리자에서에서 tootrigger 작업</span><span class="sxs-lookup"><span data-stu-id="a87c2-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="a87c2-126">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a87c2-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a87c2-127">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a87c2-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a87c2-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a87c2-128">Next steps</span></span>

<span data-ttu-id="a87c2-129">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87c2-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="a87c2-130">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87c2-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
