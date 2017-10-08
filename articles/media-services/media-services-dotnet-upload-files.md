---
title: ".NET을 사용 하 여 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "만들고 자산을 업로드 하 여 tooget 미디어를 미디어 서비스 콘텐츠 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="f1235-103">.NET을 사용하여 Media Services 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f1235-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1235-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f1235-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="f1235-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="f1235-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="f1235-106">포털</span><span class="sxs-lookup"><span data-stu-id="f1235-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="f1235-107">Media Services에서 자산에 디지털 파일을 업로드(수집)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="f1235-108">hello **자산** 엔터티 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터)를 포함할 수 있습니다  Hello 파일 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="f1235-109">hello 자산에 hello 파일 이라고 **자산 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="f1235-110">hello **AssetFile** 인스턴스와 hello 실제 미디어 파일에는 별개의 두 개체 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="f1235-111">hello AssetFile 인스턴스 hello 미디어 파일 hello 실제 미디어 콘텐츠가 포함 되어 있지만 hello 미디어 파일에 대 한 메타 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="f1235-112">hello 고려 사항에 따라 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="f1235-113">미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="f1235-114">값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="f1235-115">또한 하나만 있을 수 있습니다 하나 '.' hello 파일 이름 확장명에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="f1235-116">hello hello 이름 길이 260 자 보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="f1235-117">미디어 서비스에서 처리에 지원 되는 제한 toohello 최대 파일 크기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="f1235-118">참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="f1235-119">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f1235-120">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="f1235-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f1235-121">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1235-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="f1235-122">자산을 만들 때 hello 다음 암호화 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="f1235-123">**없음** - 암호화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-123">**None** - No encryption is used.</span></span> <span data-ttu-id="f1235-124">Hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-124">This is hello default value.</span></span> <span data-ttu-id="f1235-125">이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="f1235-126">Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="f1235-127">**CommonEncryption** - 일반적인 암호화 또는 PlayReady DRM(예: PlayReady DRM으로 보호되는 부드러운 스트리밍)으로 이미 보호된 콘텐츠를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="f1235-128">**EnvelopeEncrypted** – AES로 암호화된 HLS를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="f1235-129">참고 hello 파일을 인코딩된 있는지 및 Transform Manager를 통해 암호화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="f1235-130">**StorageEncrypted** -AES 256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 암호화 하 고 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="f1235-131">자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="f1235-132">강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일 디스크에 놓으면 toosecure를 원하는 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="f1235-133">미디어 서비스는 DRM(Digital Rights Manager)처럼 네트워크상이 아니라 자산에 대해 디스크상의 저장소 암호화 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="f1235-134">자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="f1235-135">자세한 내용은 [자산 배달 정책 구성](media-services-dotnet-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1235-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="f1235-136">사용 하 여 자산 toobe 암호화에 대해 지정 하는 경우는 **CommonEncrypted** 옵션을 또는 **EnvelopeEncypted** 옵션을 tooassociate 자산 사용 해야 합니다는 **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="f1235-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="f1235-137">자세한 내용은 참조 [어떻게 toocreate ContentKey](media-services-dotnet-create-contentkey.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="f1235-138">사용 하 여 자산 toobe 암호화에 대해 지정 하는 경우는 **StorageEncrypted** 옵션,.NET 만들어집니다에 대 한 미디어 서비스 SDK를 hello는 **StorateEncrypted** **ContentKey** 에 대 한 사용자 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="f1235-139">이 항목에서는 toouse 미디어 서비스 하는 방법을 보여 줍니다. 미디어 서비스 자산으로 미디어 서비스.NET SDK extensions tooupload 파일 뿐만 아니라.NET SDK.</span><span class="sxs-lookup"><span data-stu-id="f1235-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="f1235-140">미디어 서비스 .NET SDK를 사용하여 단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f1235-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="f1235-141">아래 샘플 코드 hello.NET SDK tooupload 단일 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="f1235-142">hello AccessPolicy와 Locator는 생성 되 고 hello 업로드 함수에 의해 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="f1235-143">미디어 서비스 .NET SDK를 사용하여 여러 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f1235-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="f1235-144">코드에서 보여 주는 방법을 다음 hello toocreate 자산 여러 파일을 업로드 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="f1235-145">hello 코드는 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="f1235-145">hello code does hello following:</span></span>

* <span data-ttu-id="f1235-146">Hello 이전 단계에서 정의 된 hello CreateEmptyAsset 메서드를 사용 하 여 빈 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="f1235-147">만듭니다는 **AccessPolicy** hello 권한 및 액세스 toohello 자산의 기간을 정의 하는 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f1235-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="f1235-148">만듭니다는 **로케이터** toohello 자산 액세스를 제공 하는 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f1235-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="f1235-149">**BlobTransferClient** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="f1235-150">이 형식은 hello Azure blob에 대해 작동 하는 클라이언트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="f1235-151">이 예에서는 hello 클라이언트 toomonitor hello 업로드 진행률을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="f1235-152">Hello 지정 된 디렉터리에 파일을 통해 열거 하 고 만듭니다는 **AssetFile** 각 파일에 대 한 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f1235-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="f1235-153">업로드 hello를 사용 하 여 미디어 서비스에 파일을 hello **UploadAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="f1235-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="f1235-154">Hello 호출이 차단 되지 않고 및 병렬로 hello 파일을 업로드 하는 hello UploadAsync 메서드 tooensure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="f1235-155">많은 자산을 업로드 하는 경우에 hello 다음 사항을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="f1235-156">스레드마다 새 **CloudMediaContext** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="f1235-157">hello **CloudMediaContext** 클래스는 스레드로부터 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="f1235-158">5와 2 tooa 더 높은 값의 hello 기본값에서 NumberOfConcurrentTransfers를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="f1235-159">이 자산을 설정하면 **CloudMediaContext**의 모든 인스턴스에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="f1235-160">Hello 기본값 10에 ParallelTransferThreadCount를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="f1235-161"><a id="ingest_in_bulk"></a>미디어 서비스 .NET SDK를 사용하여 대량으로 자산 수집</span><span class="sxs-lookup"><span data-stu-id="f1235-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="f1235-162">큰 자산 파일을 업로드하면 자산을 만드는 동안 병목 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="f1235-163">대량 또는 "대량 수집"에 자산을 수집, hello 업로드 프로세스에서 자산 만들기를 분리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="f1235-164">대량 수집 하는 방법 방식을 toouse hello 자산 및 관련된 파일을 설명 하는 매니페스트 (IngestManifest)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="f1235-165">사용자 선택 tooupload hello 관련된 파일 toohello 매니페스트의 blob 컨테이너의 hello 업로드 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="f1235-166">Microsoft Azure 미디어 서비스는 hello 매니페스트와 연결 된 hello blob 컨테이너를 감시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="f1235-167">파일 업로드 toohello blob 컨테이너를 Microsoft Azure 미디어 서비스는 hello 매니페스트에 (IngestManifestAsset) hello 자산의 hello 구성에 따라 hello 자산 만들기를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="f1235-168">새 IngestManifest toocreate hello IngestManifests 컬렉션 CloudMediaContext hello에 의해 노출 되는 hello Create 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="f1235-169">이 방법을 제공 하는 hello 매니페스트 이름의 새 IngestManifest 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="f1235-170">Hello 대량 IngestManifest와 연결 될 hello 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="f1235-171">Hello 대량 수집할 자산에서 원하는 hello 암호화 옵션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="f1235-172">IngestManifestAsset는 대량 수집을 위한 대량 IngestManifest와 자산을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="f1235-173">또한 각 자산을 구성할 Assetfile hello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="f1235-174">IngestManifestAsset toocreate hello 서버 컨텍스트에서 hello Create 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="f1235-175">hello 다음 예제에서는 이전에 만든 toohello 대량 hello 두 개의 자산에 연결 하는 추가 두 개의 새 Ingestmanifestasset 수집 매니페스트</span><span class="sxs-lookup"><span data-stu-id="f1235-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="f1235-176">각각의 IngestManifestAsset는 대량 수집 중에 각각의 자산에 업로드할 파일 집합도 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="f1235-177">Hello 자산 파일 toohello blob 저장소 컨테이너에서 hello 제공 하는 URI를 업로드할 수 있는 고속 클라이언트 응용 프로그램을 사용할 수 있습니다 **IIngestManifest.BlobStorageUriForUpload** hello IngestManifest의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="f1235-178">주목할 만한 고속 업로드 서비스 중 하나는 [Azure 응용 프로그램용 Aspera On Demand](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="f1235-179">작성할 수도 있습니다 코드 tooupload hello 자산 파일 hello 다음 코드 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="f1235-180">이 항목에서 사용 하는 hello 샘플에 대 한 hello 자산 파일을 업로드 하기 위한 hello 코드는 다음 코드 예제는 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="f1235-181">연결 된 모든 자산에 대 한 hello 대량 수집의 hello 진행률을 확인할 수 있습니다는 **IngestManifest** hello의 hello 통계 속성을 폴링하여 **IngestManifest**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="f1235-182">주문 tooupdate 진행률 정보를 사용 해야 하는 새 **CloudMediaContext** hello 통계 속성을 폴링할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="f1235-183">hello 다음 예제에서는 여는 IngestManifest 폴링 해당 **Id**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="f1235-184">.NET SDK Extensions를 사용하여 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f1235-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="f1235-185">아래 hello 예제는 단일 tooupload 파일.NET SDK Extensions를 사용 하 여 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="f1235-186">이 경우 hello **CreateFromFile** 메서드는 사용 되지 않지만 hello 비동기 버전도 있습니다 (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="f1235-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="f1235-187">hello **CreateFromFile** 메서드를 사용 하면 hello 파일 이름, 암호화 옵션 및 순서 tooreport hello에서 콜백을 업로드 진행률 hello 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

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

<span data-ttu-id="f1235-188">hello 다음 UploadFile 함수를 호출 하 고 저장소 암호화 hello 자산 만들기 옵션으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="f1235-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1235-189">Next steps</span></span>

<span data-ttu-id="f1235-190">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="f1235-191">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1235-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="f1235-192">또한 Azure 함수 tootrigger hello 구성 컨테이너에 도착 하는 파일을 기반으로 하는 인코딩 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="f1235-193">자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1235-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f1235-194">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f1235-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f1235-195">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f1235-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="f1235-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1235-196">Next step</span></span>
<span data-ttu-id="f1235-197">자산에 업로드 했으므로 tooMedia 서비스 이동 toohello [어떻게 tooGet 미디어 프로세서] [ How tooGet a Media Processor] 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f1235-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

