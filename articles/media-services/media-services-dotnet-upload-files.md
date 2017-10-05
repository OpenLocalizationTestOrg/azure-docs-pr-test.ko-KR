---
title: ".NET을 사용하여 Media Services 계정에 파일 업로드 | Microsoft 문서"
description: "자산을 만들고 업로드하여 미디어 서비스에 미디어 콘텐츠를 가져오는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ec8c1da633374ba684f6a0a895c542ee76ef73b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="fe23e-103">.NET을 사용하여 Media Services 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="fe23e-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe23e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="fe23e-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="fe23e-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="fe23e-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="fe23e-106">포털</span><span class="sxs-lookup"><span data-stu-id="fe23e-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="fe23e-107">미디어 서비스에서 자산에 디지털 파일을 업로드(수집)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="fe23e-108">**자산** 엔터티에는 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택 자막 파일(및 이러한 파일에 대한 메타데이터)이 포함될 수 있습니다.  파일이 업로드되면 이후 처리 및 스트리밍을 위해 콘텐츠가 클라우드에 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="fe23e-109">자산에 포함된 파일을 **자산 파일**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="fe23e-110">**AssetFile** 인스턴스 및 실제 미디어 파일은 별개의 두 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="fe23e-111">AssetFile 인스턴스는 미디어 파일에 대한 메타데이터를 포함하는 반면 미디어 파일은 실제 미디어 콘텐츠를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="fe23e-112">고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-112">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="fe23e-113">Media Services는 스트리밍 콘텐츠(예: http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.)를 위해 URL을 작성할 때 IAssetFile.Name 속성 값을 사용합니다. 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-113">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="fe23e-114">**Name** 속성 값에는 !*'();:@&=+$,/?%#[]"와 같은 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-114">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="fe23e-115">또한 파일 이름 확장명에는 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-115">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="fe23e-116">이름 길이는 260자보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-116">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="fe23e-117">Media Services에서 처리를 위해 지원되는 최대 파일 크기에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-117">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="fe23e-118">파일 크기 제한에 대한 세부 정보는 [이](media-services-quotas-and-limitations.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> * <span data-ttu-id="fe23e-119">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="fe23e-120">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-120">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="fe23e-121">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="fe23e-122">자산을 만들 때 다음 암호화 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-122">When you create assets, you can specify the following encryption options.</span></span> 

* <span data-ttu-id="fe23e-123">**없음** - 암호화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-123">**None** - No encryption is used.</span></span> <span data-ttu-id="fe23e-124">기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-124">This is the default value.</span></span> <span data-ttu-id="fe23e-125">이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="fe23e-126">MP4를 배달하려는 경우 이 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-126">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="fe23e-127">**CommonEncryption** - 일반적인 암호화 또는 PlayReady DRM(예: PlayReady DRM으로 보호되는 부드러운 스트리밍)으로 이미 보호된 콘텐츠를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="fe23e-128">**EnvelopeEncrypted** – AES로 암호화된 HLS를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="fe23e-129">파일을 Transform Manager로 인코딩 및 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="fe23e-130">**StorageEncrypted** - AES-256 비트 암호화를 통해 보호되지 않은 콘텐츠를 로컬로 암호화한 후에 Azure Storage에 업로드하고 사용하지 않을 때 암호화하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="fe23e-131">저장소 암호화로 보호된 자산은 자동으로 암호 해제되어 인코딩되기 전에 암호화된 파일 시스템에 배치됩니다. 그리고 필요에 따라 새 출력 자산으로 다시 업로드되기 전에 다시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="fe23e-132">저장소 암호화를 사용하는 기본적인 사례는 디스크에 저장된 상태일 때 강력한 암호화로 고품질의 입력 미디어 파일을 보호하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-132">The primary use case for Storage Encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="fe23e-133">미디어 서비스는 DRM(Digital Rights Manager)처럼 네트워크상이 아니라 자산에 대해 디스크상의 저장소 암호화 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="fe23e-134">자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="fe23e-135">자세한 내용은 [자산 배달 정책 구성](media-services-dotnet-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="fe23e-136">**CommonEncrypted** 옵션 또는 **EnvelopeEncypted** 옵션으로 암호화할 자산을 지정하는 경우 **ContentKey**로 해당 자산을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="fe23e-137">자세한 내용은 [ContentKey를 만드는 방법](media-services-dotnet-create-contentkey.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="fe23e-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="fe23e-138">**StorageEncrypted** 옵션으로 암호화할 자산을 지정하는 경우 .NET용 Media Services SDK에서 자산에 대한 **StorateEncrypted** **ContentKey**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="fe23e-139">이 항목에서는 Media Services .NET SDK와 Media Services .NET SDK 확장을 사용하여 Media Services 자산으로 파일을 업로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-139">This topic shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="fe23e-140">미디어 서비스 .NET SDK를 사용하여 단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="fe23e-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="fe23e-141">아래 샘플 코드는 .NET SDK를 사용하여 단일 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-141">The sample code below uses .NET SDK to upload a single file.</span></span> <span data-ttu-id="fe23e-142">AccessPolicy와 로케이터는 업로드 함수에 의해 생성되고 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="fe23e-143">미디어 서비스 .NET SDK를 사용하여 여러 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="fe23e-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="fe23e-144">다음 코드는 자산을 만들고 여러 파일을 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="fe23e-145">코드는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-145">The code does the following:</span></span>

* <span data-ttu-id="fe23e-146">이전 단계에서 정의된 CreateEmptyAsset 메서드를 사용하여 빈 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="fe23e-147">자산에 액세스할 수 있는 권한 및 기간을 정의하는 **AccessPolicy** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="fe23e-148">자산에 액세스를 제공하는 **Locator** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="fe23e-149">**BlobTransferClient** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="fe23e-150">이 유형은 Azure blob에서 작동하는 클라이언트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="fe23e-151">이 예제에서는 업로드 진행 상태를 모니터링하기 위해 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-151">In this example we use the client to monitor the upload progress.</span></span> 
* <span data-ttu-id="fe23e-152">지정된 디렉터리에서 파일을 열거하고 각각의 파일에 **AssetFile** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="fe23e-153">**UploadAsync** 메서드를 사용하여 파일을 Media Services에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="fe23e-154">호출을 차단하지 않고 파일을 동시에 업로드하려면 UploadAsync 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-154">Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.</span></span>
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

                // It is recommended to validate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="fe23e-155">많은 수의 자산을 업로드할 때에는 다음 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-155">When uploading a large number of assets, consider the following.</span></span>

* <span data-ttu-id="fe23e-156">스레드마다 새 **CloudMediaContext** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="fe23e-157">**CloudMediaContext** 클래스는 스레드로부터 안전하게 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-157">The **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="fe23e-158">기본 값 2에서 5와 같이 더 높은 값으로 NumberOfConcurrentTransfers를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="fe23e-159">이 자산을 설정하면 **CloudMediaContext**의 모든 인스턴스에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="fe23e-160">기본 값 10으로 ParallelTransferThreadCount를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <span data-ttu-id="fe23e-161"><a id="ingest_in_bulk"></a>미디어 서비스 .NET SDK를 사용하여 대량으로 자산 수집</span><span class="sxs-lookup"><span data-stu-id="fe23e-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="fe23e-162">큰 자산 파일을 업로드하면 자산을 만드는 동안 병목 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="fe23e-163">대량 또는 “대량 수집”으로 자산을 수집하면 업로드 과정에서 자산 만들기를 분리하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="fe23e-164">대량 수집 방식을 사용하려면 자산 및 연결된 파일을 설명하는 매니페스트(IngestManifest)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="fe23e-165">그런 다음 매니페스트의 blob 컨테이너에 연결된 파일을 업로드하기 위해 선택한 업로드 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="fe23e-166">Microsoft Azure Media Services는 매니페스트와 연결된 blob 컨테이너를 감시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="fe23e-167">blob 컨테이너에 파일을 업로드하면, Microsoft Azure Media Services가 매니페스트(IngestManifestAsset)의 자산 구성에 기반하여 자산 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="fe23e-168">새 IngestManifest 호출을 만들기 위해 CloudMediaContext에서 IngestManifests 모음이 만들기 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-168">To create a new IngestManifest call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="fe23e-169">이 메서드는 사용자가 입력하는 매니페스트 이름으로 새 IngestManifest를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-169">This method will create a new IngestManifest with the manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="fe23e-170">대량 IngestManifest와 연결되는 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-170">Create the assets that will be associated with the bulk IngestManifest.</span></span> <span data-ttu-id="fe23e-171">대량 수집을 위해 자산에 원하는 암호화 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="fe23e-172">IngestManifestAsset는 대량 수집을 위한 대량 IngestManifest와 자산을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="fe23e-173">각각의 자산을 구성하는 AssetFiles도 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-173">It also associates the AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="fe23e-174">IngestManifestAsset를 만들려면 서버 컨텍스트에서 만들기 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="fe23e-175">다음 예제에서는 대량 수집 매니페스트에 이전에 만든 두 자산을 연결하는 두 개의 새 IngestManifestAssets를 추가하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="fe23e-176">각각의 IngestManifestAsset는 대량 수집 중에 각각의 자산에 업로드할 파일 집합도 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="fe23e-177">IngestManifest의 **IIngestManifest.BlobStorageUriForUpload** 속성이 제공하는 blob 저장소 컨테이너 URI에 자산 파일을 업로드할 수 있는 고속 클라이언트 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-177">You can use any high speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> <span data-ttu-id="fe23e-178">주목할 만한 고속 업로드 서비스 중 하나는 [Azure 응용 프로그램용 Aspera On Demand](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)입니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="fe23e-179">다음 코트 예제와 같이 코드를 작성하여 자산 파일을 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-179">You can also write code to upload the assets files as shown in the following code example.</span></span>

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

<span data-ttu-id="fe23e-180">이 항목에서 사용하는 샘플의 자산 파일을 업로드하는 코드는 다음 코드 예제에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-180">The code for uploading the asset files for the sample used in this topic is shown in the following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="fe23e-181">**IngestManifest**의 Statistics 속성을 폴링하여 **IngestManifest**에 연결된 모든 자산의 대량 수집 과정을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-181">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="fe23e-182">과정 정보를 업데이트하려면 통계 속성을 폴링할 때마다 새 **CloudMediaContext** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-182">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="fe23e-183">다음 예제는 해당 **Id**로 IngestManifest를 폴링하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-183">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="fe23e-184">.NET SDK Extensions를 사용하여 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="fe23e-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="fe23e-185">아래 예제는 .NET SDK Extensions를 사용하여 단일 파일을 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-185">The example below shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="fe23e-186">이 경우 **CreateFromFile** 메서드가 사용되지만 비동기 버전(**CreateFromFileAsync**)도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-186">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="fe23e-187">**CreateFromFile** 메서드를 사용하면 파일 이름, 암호화 옵션 및 파일의 업로드 과정을 보고하기 위한 콜백을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-187">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

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

<span data-ttu-id="fe23e-188">다음 예제는 UploadFile 함수를 호출하며 자산 만들기 옵션으로 저장소 암호화를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-188">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="fe23e-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe23e-189">Next steps</span></span>

<span data-ttu-id="fe23e-190">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="fe23e-191">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="fe23e-192">또한 Azure Functions를 사용하여 구성된 컨테이너에 도착하는 파일에 따라 인코딩 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe23e-192">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="fe23e-193">자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fe23e-194">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="fe23e-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fe23e-195">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="fe23e-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="fe23e-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe23e-196">Next step</span></span>
<span data-ttu-id="fe23e-197">이제 Media Services에 자산을 업로드했으므로 [미디어 프로세서를 가져오는 방법][How to Get a Media Processor] 항목으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="fe23e-197">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] topic.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

