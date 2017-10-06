---
title: ".NET을 사용 하 여 필요에 따라 콘텐츠를 배달 aaaGet 시작 | Microsoft Docs"
description: "이 자습서의.NET을 사용 하 여 Azure 미디어 서비스에 요청 콘텐츠 배달 응용 프로그램을 구현할 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="ad81b-103">.NET SDK를 사용한 주문형 콘텐츠 제공 시작</span><span class="sxs-lookup"><span data-stu-id="ad81b-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="ad81b-104">이 자습서는 hello Azure 미디어 서비스.NET SDK를 사용 하 여 Azure 미디어 서비스 (AMS) 응용 프로그램과 함께 기본 VoD ()를 주문형 비디오 콘텐츠 배달 서비스 구현의 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad81b-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ad81b-105">Prerequisites</span></span>

<span data-ttu-id="ad81b-106">hello 다음은 필요한 toocomplete hello 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="ad81b-107">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="ad81b-107">An Azure account.</span></span> <span data-ttu-id="ad81b-108">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad81b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ad81b-109">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="ad81b-109">A Media Services account.</span></span> <span data-ttu-id="ad81b-110">미디어 서비스 계정 toocreate 참조 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ad81b-111">.NET Framework 4.0 이상.</span><span class="sxs-lookup"><span data-stu-id="ad81b-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="ad81b-112">있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-112">Visual Studio.</span></span>

<span data-ttu-id="ad81b-113">이 자습서에는 작업을 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="ad81b-114">스트리밍 끝점 (hello Azure 포털을 사용 하 여)을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="ad81b-115">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="ad81b-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="ad81b-116">Toohello 미디어 서비스 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad81b-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="ad81b-117">비디오 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-117">Upload a video file.</span></span>
3. <span data-ttu-id="ad81b-118">Hello 소스 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="ad81b-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="ad81b-119">Hello 및 get 스트리밍 자산과 점진적 다운로드 Url을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="ad81b-120">콘텐츠를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="ad81b-121">개요</span><span class="sxs-lookup"><span data-stu-id="ad81b-121">Overview</span></span>
<span data-ttu-id="ad81b-122">이 자습서는 Azure 미디어 서비스 (AMS) SDK를 사용 하 여.NET에 대 한 주문형 비디오 (VoD) 콘텐츠 배달 응용 프로그램을 구현 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="ad81b-123">hello 자습서에서는 기본 미디어 서비스 워크플로 hello hello 가장 일반적인 프로그래밍 개체 및 미디어 서비스 개발에 필요한 작업을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="ad81b-124">Hello 자습서를 완료 한 hello 시점에서 있습니다 수 toostream 되거나 될 점진적으로 업로드, 인코딩, 다운로드 한 샘플 미디어 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="ad81b-125">AMS 모델</span><span class="sxs-lookup"><span data-stu-id="ad81b-125">AMS model</span></span>

<span data-ttu-id="ad81b-126">hello 다음 이미지에서는 가장 일반적으로 사용 하는 hello 개체 중 일부를 hello 미디어 서비스 OData 모델에 대 한 VoD 응용 프로그램을 개발 하는 경우</span><span class="sxs-lookup"><span data-stu-id="ad81b-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="ad81b-127">전체 크기로 hello 이미지 tooview를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="ad81b-128">Hello 전체 모델을 볼 수 있습니다 [여기](https://media.windows.net/API/$metadata?api-version=2.15)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="ad81b-129">Hello Azure 포털을 사용 하 여 끝점을 스트리밍 시작</span><span class="sxs-lookup"><span data-stu-id="ad81b-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="ad81b-130">Azure 미디어 서비스를 통해 적응 비트 전송률 스트리밍 비디오를 제공 하는 hello 가장 일반적인 시나리오 중 하나 작업할 때는입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="ad81b-131">미디어 서비스는 적응 비트 전송률 사전 패키지 toostore 필요 없이 (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 적시에서 지 원하는 형식 스트리밍을에 인코딩된 MP4 콘텐츠 toodeliver 수 있는 동적 패키징 제공 각각의 형식 스트리밍을 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="ad81b-132">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ad81b-133">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="ad81b-134">toostart hello 스트리밍 끝점을 다음 hello 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="ad81b-135">Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ad81b-136">Hello 설정 창에서 스트리밍 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="ad81b-137">Hello 기본 스트리밍 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="ad81b-138">hello 스트리밍 끝점 세부 정보 기본 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="ad81b-139">Hello 시작 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="ad81b-140">변경 내용을 저장 단추 toosave hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ad81b-141">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="ad81b-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="ad81b-142">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="ad81b-143">새 폴더를 만듭니다 (폴더는 로컬 드라이브에 아무 곳 이나 수 있음) 원하는 tooencode 및 스트림 하거나 점진적으로 다운로드 하는.mp4 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="ad81b-144">이 예제에서는 hello "C:\VideoFiles" 경로가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="ad81b-145">Toohello 미디어 서비스 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad81b-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="ad81b-146">미디어 서비스.net을 사용할 경우 hello를 사용 해야 **CloudMediaContext** 프로그래밍 작업 대부분 미디어 서비스에 대 한 클래스: tooMedia 서비스 계정 연결; 만들기, 업데이트, 액세스 및 hello 다음 삭제 개체: 자산, 자산 파일, 작업, 액세스 정책, 로케이터, 등입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="ad81b-147">Hello 코드 다음으로 hello 기본 프로그램 클래스를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="ad81b-148">hello 보여 주는 코드 tooread hello 연결 hello App.config 파일에서 값의 방식과 toocreate hello **CloudMediaContext** 순서 tooconnect tooMedia에서 개체를 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="ad81b-149">자세한 내용은 참조 [toohello 미디어 서비스 API 연결](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="ad81b-150">있는지 tooupdate hello 파일 이름 및 경로 toowhere 있는 미디어 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="ad81b-151">hello **Main** 함수 정의 하는 메서드를 호출 합니다.이 섹션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="ad81b-152">가져오는 것은 컴파일 오류가 모든 hello 함수에 대 한 정의 추가할 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="ad81b-153">새 자산 만들기 및 비디오 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ad81b-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="ad81b-154">Media Services에서 자산에 디지털 파일을 업로드(수집)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="ad81b-155">hello **자산** 엔터티 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터)를 포함할 수 있습니다  Hello 파일 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="ad81b-156">hello 자산에 hello 파일 이라고 **자산 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="ad81b-157">hello **UploadFile** 메서드 호출 아래에 정의 된 **CreateFromFile** (.NET SDK Extensions에 정의 됨).</span><span class="sxs-lookup"><span data-stu-id="ad81b-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="ad81b-158">**CreateFromFile** 는 hello에 지정 된 소스 파일을 업로드 하는 새 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="ad81b-159">hello **CreateFromFile** 메서드 **AssetCreationOptions** hello 자산 만들기 옵션을 다음 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="ad81b-160">**없음** - 암호화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-160">**None** - No encryption is used.</span></span> <span data-ttu-id="ad81b-161">Hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-161">This is hello default value.</span></span> <span data-ttu-id="ad81b-162">이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="ad81b-163">Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="ad81b-164">**StorageEncrypted** -이 옵션 tooencrypt tooAzure 암호화 된 상태로 저장 된 저장소 업로드 하는 표준 AES (고급 암호화)-256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ad81b-165">자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="ad81b-166">toosecure 디스크에 저장 된 상태의 강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일을 사용할 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="ad81b-167">**CommonEncryptionProtected** - 이미 암호화되어 일반적인 암호화 또는 PlayReady DRM(예: PlayReady DRM으로 보호되는 부드러운 스트리밍)으로 보호된 콘텐츠를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="ad81b-168">**EnvelopeEncryptionProtected** - AES로 암호화된 HLS를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="ad81b-169">참고 hello 파일을 인코딩된 있는지 및 Transform Manager를 통해 암호화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="ad81b-170">hello **CreateFromFile** 메서드 수도 있습니다 hello 파일의 순서 tooreport hello 업로드 프로세스에는 콜백을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="ad81b-171">다음 예제는 hello, 지정 **None** hello 자산 옵션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="ad81b-172">Hello toohello 프로그램 클래스 메서드를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-172">Add hello following method toohello Program class.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="ad81b-173">Hello 소스 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩</span><span class="sxs-lookup"><span data-stu-id="ad81b-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="ad81b-174">수 미디어 후 미디어 서비스 자산을 수집, 인코딩, 워터 transmuxed 등과 tooclients 전달 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="ad81b-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="ad81b-175">이러한 활동은 예약 되 고 여러 백그라운드 역할 인스턴스 tooensure 고성능 및 가용성에 대해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="ad81b-176">이러한 활동 작업을 호출 하 고 각 작업 hello 자산 파일에서 실제 작업 hello 수행 하는 원자성 작업으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="ad81b-177">위에 언급 한, Azure 미디어 서비스를 사용 하는 경우, 적응 비트 전송률 스트리밍 tooyour 클라이언트를 제공 하는 hello 가장 일반적인 시나리오 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="ad81b-178">미디어 서비스 hello 다음 형식 중 하나로 적응 비트 전송률 MP4 파일 집합이 동적으로 패키징할 수: HTTP 라이브 스트리밍 (HLS), 부드러운 스트리밍 및 MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="ad81b-179">tootake 이점은 동적 패키징을 tooencode 또는 필요한 코드 변환 중 2 층 (원본) 파일의 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="ad81b-180">hello 코드 다음 인코딩을 toosubmit 작업 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="ad81b-181">hello 작업에 포함 된 tootranscode hello 중 2 층 파일을 사용 하 여 적응 비트 전송률 mp4 집합으로 지정 하는 하나 이상의 태스크 **미디어 인코더 표준**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="ad81b-182">hello 코드 완료 될 때까지 hello 작업 및 대기를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="ad81b-183">Hello 작업이 완료 되 면 수 toostream 자산인 될 거 나 점진적으로 코드 변환의 결과로 생성 된 MP4 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="ad81b-184">Hello toohello 프로그램 클래스 메서드를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-184">Add hello following method toohello Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="ad81b-185">Hello 자산을 게시 하 고 스트리밍 및 점진적 다운로드에 대 한 Url 가져오기</span><span class="sxs-lookup"><span data-stu-id="ad81b-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="ad81b-186">toostream 또는 다운로드 자산 먼저 필요한 너무 "" 하 여 게시 한 로케이터를 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="ad81b-187">로케이터는 hello 자산에 포함 된 액세스 toofiles를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="ad81b-188">미디어 서비스는 두 가지 로케이터 유형을 지원: OnDemandOrigin 로케이터를 사용 하는 toostream 미디어 (예를 들어, MPEG DASH, HLS 또는 부드러운 스트리밍) 및 SAS (액세스 서명) locator toodownload 미디어 파일 ( SAS로케이터참조에대한자세한내용은사용[이](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) 블로그).</span><span class="sxs-lookup"><span data-stu-id="ad81b-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="ad81b-189">URL 형식에 대한 일부 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ad81b-189">Some details about URL formats</span></span>

<span data-ttu-id="ad81b-190">Hello 로케이터를 만든 후 거 사용된 toostream 나 파일을 다운로드 하는 hello Url을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="ad81b-191">이 자습서에서는 hello 예제는 적절 한 브라우저에 붙여 넣을 수 있는 Url을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="ad81b-192">이 섹션에서는 다양한 형식을 보여 주는 간단한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="ad81b-193">MPEG DASH에 대 한 스트리밍 URL 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="ad81b-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="ad81b-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="ad81b-195">HLS에 대 한 스트리밍 URL 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="ad81b-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="ad81b-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="ad81b-197">부드러운 스트리밍에 대 한 스트리밍 URL 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="ad81b-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="ad81b-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="ad81b-199">사용 되는 SAS URL toodownload 파일 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="ad81b-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span><span class="sxs-lookup"><span data-stu-id="ad81b-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="ad81b-201">미디어 서비스.NET SDK extensions는 게시 된 자산 반환 형식이 hello에 대 한 Url을 지정 하는 편리한 도우미 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="ad81b-202">hello 다음 코드에서는.NET SDK Extensions toocreate 로케이터 및 tooget 스트리밍과 점진적 다운로드 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="ad81b-203">또한 hello 코드 toodownload tooa 로컬 폴더를 파일 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="ad81b-204">Hello toohello 프로그램 클래스 메서드를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-204">Add hello following method toohello Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="ad81b-205">콘텐츠를 재생하여 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-205">Test by playing your content</span></span>

<span data-ttu-id="ad81b-206">Hello 이전 섹션에 정의 된 hello 프로그램을 실행 하면 되 면 hello Url 비슷한 toohello 다음 hello 콘솔 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="ad81b-207">적응 스트리밍 URL:</span><span class="sxs-lookup"><span data-stu-id="ad81b-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="ad81b-208">부드러운 스트리밍</span><span class="sxs-lookup"><span data-stu-id="ad81b-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="ad81b-209">HLS</span><span class="sxs-lookup"><span data-stu-id="ad81b-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="ad81b-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ad81b-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="ad81b-211">점진적 다운로드 URL(오디오 및 비디오)</span><span class="sxs-lookup"><span data-stu-id="ad81b-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="ad81b-212">toostream 비디오 hello에 hello URL 텍스트 상자에 URL을 붙여 [Azure 미디어 서비스 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="ad81b-213">tootest 점진적 다운로드 전용는 URL (예를 들어 Internet Explorer, Chrome 또는 Safari) 브라우저에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="ad81b-214">자세한 내용은 hello 다음 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad81b-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="ad81b-215">기존 플레이어를 사용하여 콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="ad81b-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="ad81b-216">비디오 플레이어 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="ad81b-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="ad81b-217">DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함</span><span class="sxs-lookup"><span data-stu-id="ad81b-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="ad81b-218">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="ad81b-218">Download sample</span></span>
<span data-ttu-id="ad81b-219">hello 다음 코드 샘플 코드가 포함 되어 hello이이 자습서에서 만든: [샘플](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad81b-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad81b-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad81b-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ad81b-221">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ad81b-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
