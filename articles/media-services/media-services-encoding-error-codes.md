---
title: "오류 코드를 인코딩 aaaAzure 미디어 서비스 | Microsoft Docs"
description: "이 항목 hello 인코딩 작업을 실행 하는 동안 오류가 발생 했습니다 경우 반환 될 수 있는 오류 코드를 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="5f072-103">인코딩 오류 코드</span><span class="sxs-lookup"><span data-stu-id="5f072-103">Encoding error codes</span></span>

<span data-ttu-id="5f072-104">hello 다음 표 hello 인코딩 작업을 실행 하는 동안 오류가 발생 했습니다 경우 반환 될 수 있는 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="5f072-105">hello를 사용 하 여.NET 코드에 tooget 오류 세부 정보 [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="5f072-106">나머지 코드에서 오류 세부 정보 tooget hello를 사용 하 여 [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="5f072-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="5f072-107">ErrorDetail.Code</span></span> | <span data-ttu-id="5f072-108">가능한 오류 원인</span><span class="sxs-lookup"><span data-stu-id="5f072-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="5f072-109">알 수 없음</span><span class="sxs-lookup"><span data-stu-id="5f072-109">Unknown</span></span> |<span data-ttu-id="5f072-110">Hello 작업을 실행 하는 동안 알 수 없는 오류</span><span class="sxs-lookup"><span data-stu-id="5f072-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="5f072-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="5f072-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="5f072-112">잘못된 파일 이름, 길이가 0 인 파일, 잘못된 형식 등 입력 자산을 다운로드하는 동안 발생하는 오류를 포함하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="5f072-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="5f072-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="5f072-114">다운로드 하는 동안 네트워크 또는 저장소 오류의 예제에 대 한 hello 서비스 쪽-문제를 검사 하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="5f072-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="5f072-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="5f072-116">오류 범주에 작업 <see cref="MediaTask.PrivateData"/> 올바르지 않습니다 (구성), 예를 들어 hello 구성 아닙니다 유효한 시스템 사전 설정에 잘못 된 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="5f072-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="5f072-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="5f072-118">여기서 hello 내 문제 입력 미디어 파일에 오류가 발생 하는 hello 태스크의 hello 실행 동안 발생 한 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="5f072-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="5f072-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="5f072-120">여기서 hello 미디어 프로세서 제공 하는 hello 파일을 처리할 수 없습니다-미디어를 포맷할 오류 범주는 지원 되지 않거나 구성 hello와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="5f072-121">예를 들어 tooproduce 비디오가 유일한 자산에서 오디오 전용 출력 시도</span><span class="sxs-lookup"><span data-stu-id="5f072-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="5f072-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="5f072-122">ErrorProcessingTask</span></span> |<span data-ttu-id="5f072-123">미디어 프로세서 hello 다른 오류의 범주는 관련 없는 toocontent hello 작업의 hello 처리 하는 동안 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="5f072-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="5f072-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="5f072-125">Hello 출력 자산을 업로드 하는 경우 오류 범주</span><span class="sxs-lookup"><span data-stu-id="5f072-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="5f072-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="5f072-126">ErrorCancelingTask</span></span> |<span data-ttu-id="5f072-127">Toocancel hello 작업을 시도할 때 오류 toocover 오류의 범주</span><span class="sxs-lookup"><span data-stu-id="5f072-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="5f072-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="5f072-128">TransientError</span></span> |<span data-ttu-id="5f072-129">오류 toocover 일시적인 문제 (예:의 범주.</span><span class="sxs-lookup"><span data-stu-id="5f072-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="5f072-130">Azure Storage의 임시 네트워킹 문제)</span><span class="sxs-lookup"><span data-stu-id="5f072-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="5f072-131">hello에서 tooget 도움말 **미디어 서비스** 팀 열기는 [지원 티켓](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f072-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5f072-132">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="5f072-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5f072-133">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5f072-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="5f072-134">관련 문서</span><span class="sxs-lookup"><span data-stu-id="5f072-134">Related articles</span></span>
* [<span data-ttu-id="5f072-135">미디어 인코더 표준 사전 설정을 사용자 지정하여 고급 인코딩 작업 수행</span><span class="sxs-lookup"><span data-stu-id="5f072-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="5f072-136">할당량 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="5f072-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
