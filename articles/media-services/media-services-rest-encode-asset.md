---
title: "Azure 미디어 인코더 표준를 사용 하 여 자산 aaaHow tooencode | Microsoft Docs"
description: "Azure 미디어 서비스에서 미디어 인코더 표준 tooencode 미디어 toouse 콘텐츠 하는 방법에 대해 알아봅니다. REST API를 사용하는 코드 샘플입니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="7d5f1-104">어떻게 tooencode 미디어 인코더 표준를 사용 하 여 자산</span><span class="sxs-lookup"><span data-stu-id="7d5f1-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d5f1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7d5f1-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="7d5f1-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="7d5f1-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="7d5f1-107">포털</span><span class="sxs-lookup"><span data-stu-id="7d5f1-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="7d5f1-108">개요</span><span class="sxs-lookup"><span data-stu-id="7d5f1-108">Overview</span></span>
<span data-ttu-id="7d5f1-109">hello 인터넷을 통해 디지털 비디오 toodeliver hello 미디어를 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="7d5f1-110">디지털 비디오 파일에는 큰 있으며 수 너무 큰 toodeliver hello 인터넷을 통해 또는 고객의 장치 toodisplay에 대 한 제대로.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="7d5f1-111">인코딩은 고객이 미디어를 볼 수 있도록 비디오 및 오디오를 압축의 hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="7d5f1-112">인코딩 작업은 Azure 미디어 서비스에서 hello 가장 일반적인 처리 작업 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="7d5f1-113">하나의 인코딩 tooanother에서 인코딩 작업 tooconvert 미디어 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="7d5f1-114">인코드할 때는 hello 미디어 서비스 기본 제공 인코더 (미디어 인코더 표준)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="7d5f1-115">또한 Media Services 파트너가 제공하는 인코더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="7d5f1-116">타사 인코더는 hello Azure 마켓플레이스를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="7d5f1-117">인코더에 대해 정의 된 사전 설정된 문자열을 사용 하 여 또는 미리 설정 된 구성 파일을 사용 하 여 인코딩 태스크의 hello 세부 정보를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="7d5f1-118">를 사용할 수 있는 사전 설정 toosee hello 유형을 참조 [미디어 인코더 표준의 태스크 사전 설정](http://msdn.microsoft.com/library/mt269960)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="7d5f1-119">각 작업 하나를 사용할 수 또는 더 많은 작업 하는 처리가 hello 유형에 따라 tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="7d5f1-120">Hello REST API를 통해 다음 두 가지 방법 중 하나에서 작업 및 관련된 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="7d5f1-121">작업에는 작업 엔터티에 대해 hello 작업 탐색 속성을 통해 인라인으로 정의할된 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="7d5f1-122">OData 배치 처리 사용.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-122">Use OData batch processing.</span></span>

<span data-ttu-id="7d5f1-123">항상 원본 파일을 적응 비트 전송률 MP4 집합을 인코딩한 다음 hello 집합 toohello 원하는 형식을 사용 하 여 변환 하는 것이 좋습니다 [동적 패키징](media-services-dynamic-packaging-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="7d5f1-124">출력 자산이 저장소 암호화 이면 hello 자산 배달 정책을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="7d5f1-125">자세한 내용은 [자산 배달 정책 구성](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="7d5f1-126">고려 사항</span><span class="sxs-lookup"><span data-stu-id="7d5f1-126">Considerations</span></span>

<span data-ttu-id="7d5f1-127">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="7d5f1-128">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="7d5f1-129">정확 하 게 미디어 프로세서의 id입니다.를 hello가 참조 하는 미디어 프로세서를 시작 하기 전에 확인</span><span class="sxs-lookup"><span data-stu-id="7d5f1-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="7d5f1-130">자세한 내용은 [미디어 프로세서 가져오기](media-services-rest-get-media-processor.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="7d5f1-131">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="7d5f1-131">Connect tooMedia Services</span></span>

<span data-ttu-id="7d5f1-132">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="7d5f1-133">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7d5f1-134">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="7d5f1-135">작업을 단일 인코딩 작업으로 만들기</span><span class="sxs-lookup"><span data-stu-id="7d5f1-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="7d5f1-136">미디어 서비스 REST API hello로 작업할 때 hello 다음 고려 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="7d5f1-137">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="7d5f1-138">자세한 내용은 [Media Services REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="7d5f1-139">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7d5f1-140">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="7d5f1-141">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="7d5f1-142">때 JSON를 사용 하 고 toouse hello 지정 **__metadata** hello를 설정 해야 합니다 (예를 들어 tooreferences 연결된 된 개체), hello 요청에는 키워드 **Accept** 헤더 너무[자세한 JSON 형식 ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): 수락: 응용 프로그램/json; odata = 세부 정보 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="7d5f1-143">다음 예제는 hello 있습니다 설정 방법을 보여 줍니다 toocreate 및 post 작업 인 작업 tooencode 비디오 특정 해상도 및 품질에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="7d5f1-144">Media Encoder Standard로 인코딩할 때 [여기](http://msdn.microsoft.com/library/mt269960)에 지정된 작업 구성 기본 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="7d5f1-145">요청:</span><span class="sxs-lookup"><span data-stu-id="7d5f1-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="7d5f1-146">응답:</span><span class="sxs-lookup"><span data-stu-id="7d5f1-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="7d5f1-147">Hello 출력 자산의 이름 설정</span><span class="sxs-lookup"><span data-stu-id="7d5f1-147">Set hello output asset's name</span></span>
<span data-ttu-id="7d5f1-148">다음 예제는 hello tooset assetName 특성을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="7d5f1-149">고려 사항</span><span class="sxs-lookup"><span data-stu-id="7d5f1-149">Considerations</span></span>
* <span data-ttu-id="7d5f1-150">TaskBody 속성, 입력 또는 출력 자산 hello 작업에서 사용 되는 리터럴 XML toodefine hello 번호를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="7d5f1-151">hello 작업 항목 XML hello에 대 한 hello XML 스키마 정의 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="7d5f1-152">TaskBody 정의 hello에 대 한 각 내부 값 <inputAsset> 및 <outputAsset> JobInputAsset(value) 또는 JobOutputAsset(value)로 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="7d5f1-153">작업 출력 자산은 여러 개일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-153">A task can have multiple output assets.</span></span> <span data-ttu-id="7d5f1-154">작업에서 하나의 JobOutputAsset(x)을 작업 출력으로 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="7d5f1-155">JobInputAsset 또는 JobOutputAsset을 작업의 입력 자산으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="7d5f1-156">작업은 주기를 형성해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="7d5f1-157">tooJobInputAsset 또는 JobOutputAsset을 전달 하는 hello value 매개 변수는 자산에 대 한 hello 인덱스 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="7d5f1-158">실제 자산은 hello hello InputMediaAssets 및 OutputMediaAssets 탐색 속성 hello job 엔터티 정의에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="7d5f1-159">미디어 서비스는 OData v 3에서 빌드되므로 hello 개별 자산은 hello InputMediaAssets 및 OutputMediaAssets 탐색 속성 컬렉션을 통해 참조 되는 "__metadata: uri" 이름-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="7d5f1-160">InputMediaAssets는 tooone 또는 미디어 서비스에서 만든 자세한 자산에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="7d5f1-161">Outputmediaasset은 hello 시스템에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="7d5f1-162">기존 자산을 참조하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="7d5f1-163">Outputmediaasset은 hello assetName 특성을 사용 하 여 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="7d5f1-164">이 특성이 없으면 경우 OutputMediaAsset hello의 hello 이름을 hello의 hello 내부 텍스트 값은 <outputAsset> 요소는 hello 작업 이름 값 또는 hello 작업 Id 값 (hello 경우 hello 이름 속성이 정의 되지 않습니다)의 접미사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="7d5f1-165">예를 들어 assetName에 대 한 값을 설정 하는 경우 너무 "Sample" 다음 hello OutputMediaAsset 이름 속성은 너무 "Sample."</span><span class="sxs-lookup"><span data-stu-id="7d5f1-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="7d5f1-166">그러나 assetName에 대 한 값을 설정 하지 않은 했지만 hello 작업 이름을 설정할가 너무 "NewJob" hello OutputMediaAsset 이름은 수 "JobOutputAsset (값) _NewJob"입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="7d5f1-167">연결된 작업으로 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="7d5f1-167">Create a job with chained tasks</span></span>
<span data-ttu-id="7d5f1-168">대부분의 응용 프로그램 시나리오에서 개발자는 toocreate 일련의 처리 작업을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="7d5f1-169">미디어 서비스에서 일련의 연결된 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="7d5f1-170">각 작업은 서로 다른 처리 단계를 수행하고 다양한 미디어 프로세서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="7d5f1-171">연결 된 hello 작업 hello 자산에 대해 작업의 선형 시퀀스를 수행 하는 하나 이상의 태스크 tooanother에서 자산을 전달 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="7d5f1-172">그러나 작업에서 수행 하는 hello 작업 시퀀스에 필요한 toobe 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="7d5f1-173">Hello에 연결 된 연결 된 작업을 만들 때 **ITask** 개체에는 단일 만들어집니다 **IJob** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="7d5f1-174">현재 작업은 작업당 30개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="7d5f1-175">30 개 이상의 작업 toochain 해야 할 경우 둘 이상의 작업 toocontain hello 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="7d5f1-176">고려 사항</span><span class="sxs-lookup"><span data-stu-id="7d5f1-176">Considerations</span></span>
<span data-ttu-id="7d5f1-177">tooenable 작업 체인:</span><span class="sxs-lookup"><span data-stu-id="7d5f1-177">tooenable task chaining:</span></span>

* <span data-ttu-id="7d5f1-178">작업에 작업이 2개 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="7d5f1-179">해당 입력이 hello 출력 hello 작업에서 다른 작업의 작업을 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="7d5f1-180">OData 배치 처리 사용</span><span class="sxs-lookup"><span data-stu-id="7d5f1-180">Use OData batch processing</span></span>
<span data-ttu-id="7d5f1-181">다음 예제는 hello 작업 및 작업 toouse OData 일괄 처리 toocreate 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="7d5f1-182">일괄 처리에 대한 정보는 [Open Data Protocol(OData) 일괄 처리](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="7d5f1-183">JobTemplate을 사용하여 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="7d5f1-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="7d5f1-184">작업, JobTemplate toospecify hello 기본 작업 사전 설정, 사용 또는 작업 tooset hello 순서의 공통 집합을 사용 하 여 여러 자산을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="7d5f1-185">다음 예제는 hello toocreate JobTemplate은 TaskTemplate와 인라인을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="7d5f1-186">TaskTemplate hello hello MediaProcessor tooencode hello 자산 파일으로 미디어 인코더 표준 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="7d5f1-187">그러나 다른 Mediaprocessor도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="7d5f1-188">다른 미디어 서비스 엔터티를 달리 각 TaskTemplate에 대 한 새 GUID 식별자를 정의 하 고 요청 본문에 hello taskTemplateId 및 Id 속성에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="7d5f1-189">hello 콘텐츠 식별 구성표 Azure 미디어 서비스 엔터티 식별에 설명 된 hello 체계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="7d5f1-190">또한 JobTemplates는 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="7d5f1-191">대신 업데이트된 변경 사항으로 새로운 템플릿을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="7d5f1-192">성공 하면 다음 응답 hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="7d5f1-193">hello 방법을 예제와 다음 toocreate JobTemplate Id를 참조 하는 작업:</span><span class="sxs-lookup"><span data-stu-id="7d5f1-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="7d5f1-194">성공 하면 다음 응답 hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="7d5f1-195">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="7d5f1-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7d5f1-196">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="7d5f1-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7d5f1-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d5f1-197">Next steps</span></span>
<span data-ttu-id="7d5f1-198">배웠으므로 toocreate 자산, 작업 tooencode 확인 하려면 어떻게 해야 [toocheck 미디어 서비스를 사용 하 여 진행률을 작업 하는 방법을](media-services-rest-check-job-progress.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5f1-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7d5f1-199">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7d5f1-199">See also</span></span>
[<span data-ttu-id="7d5f1-200">미디어 프로세서 가져오기</span><span class="sxs-lookup"><span data-stu-id="7d5f1-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
