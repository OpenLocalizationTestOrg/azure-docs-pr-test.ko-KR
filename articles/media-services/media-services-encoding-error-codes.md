---
title: "Azure Media Services 인코딩 오류 코드 | Microsoft Docs"
description: "이 항목에는 인코딩 작업을 실행하는 동안 오류가 발생하는 경우 반환될 수 있는 오류 코드가 나열되어 있습니다."
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
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="1d29f-103">인코딩 오류 코드</span><span class="sxs-lookup"><span data-stu-id="1d29f-103">Encoding error codes</span></span>

<span data-ttu-id="1d29f-104">다음 표에서는 인코딩 작업을 실행하는 동안 오류가 발생한 경우 반환될 수 있는 오류 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="1d29f-105">.NET 코드에서 오류 세부 정보를 가져오려면 [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="1d29f-106">REST 코드에서 오류 세부 정보를 가져오려면 [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="1d29f-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="1d29f-107">ErrorDetail.Code</span></span> | <span data-ttu-id="1d29f-108">가능한 오류 원인</span><span class="sxs-lookup"><span data-stu-id="1d29f-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="1d29f-109">알 수 없음</span><span class="sxs-lookup"><span data-stu-id="1d29f-109">Unknown</span></span> |<span data-ttu-id="1d29f-110">작업을 실행하는 동안 알 수 없는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="1d29f-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="1d29f-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="1d29f-112">잘못된 파일 이름, 길이가 0 인 파일, 잘못된 형식 등 입력 자산을 다운로드하는 동안 발생하는 오류를 포함하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="1d29f-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="1d29f-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="1d29f-114">다운로드하는 동안 발생하는 네트워크 또는 저장소 오류 등 서비스 쪽의 문제를 포함하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="1d29f-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1d29f-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="1d29f-116">구성이 잘못된 시스템 기본 설정이거나 잘못된 XML이 포함된 경우 등 작업 <see cref="MediaTask.PrivateData"/>(구성)가 잘못된 경우의 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="1d29f-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="1d29f-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="1d29f-118">입력 미디어 파일 내의 문제로 인해 실패가 발생한 작업을 실행하는 동안 발생하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="1d29f-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="1d29f-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="1d29f-120">미디어 프로세서가 지정한 미디어 형식이 지원되지 않는 파일을 처리할 수 없거나 구성과 일치하지 않는 경우의 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="1d29f-121">예를 들어 비디오만 사용할 수 있는 자산에서 오디오 전용 출력을 생성하려고 하는 경우</span><span class="sxs-lookup"><span data-stu-id="1d29f-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="1d29f-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="1d29f-122">ErrorProcessingTask</span></span> |<span data-ttu-id="1d29f-123">콘텐츠와 관련되지 않은 작업을 처리하는 동안 미디어 프로세서에서 발생하는 기타 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="1d29f-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="1d29f-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="1d29f-125">출력 자산을 업로드할 때 발생하는 오류를 포함하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="1d29f-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="1d29f-126">ErrorCancelingTask</span></span> |<span data-ttu-id="1d29f-127">작업을 취소하려고 할 때 발생하는 오류를 포함하는 오류 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="1d29f-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="1d29f-128">TransientError</span></span> |<span data-ttu-id="1d29f-129">일시적인 문제를 포함하는 오류 범주(예:</span><span class="sxs-lookup"><span data-stu-id="1d29f-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="1d29f-130">Azure Storage의 임시 네트워킹 문제)</span><span class="sxs-lookup"><span data-stu-id="1d29f-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="1d29f-131">**미디어 서비스** 팀에 도움을 요청하려면 [지원 티켓](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d29f-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1d29f-132">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="1d29f-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1d29f-133">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="1d29f-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="1d29f-134">관련 문서</span><span class="sxs-lookup"><span data-stu-id="1d29f-134">Related articles</span></span>
* [<span data-ttu-id="1d29f-135">미디어 인코더 표준 사전 설정을 사용자 지정하여 고급 인코딩 작업 수행</span><span class="sxs-lookup"><span data-stu-id="1d29f-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="1d29f-136">할당량 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1d29f-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
