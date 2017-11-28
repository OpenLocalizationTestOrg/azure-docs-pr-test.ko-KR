---
title: "aaaManaging 자산 및 미디어 서비스.NET SDK와 관련 엔터티"
description: "어떻게 toomanage 자산과 관련된 엔터티에 hello Media Services SDK for.NET에 알아봅니다."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="872dc-103">미디어 서비스.NET SDK를 사용하여 자산 및 관련 엔터티 관리</span><span class="sxs-lookup"><span data-stu-id="872dc-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="872dc-104">.NET</span><span class="sxs-lookup"><span data-stu-id="872dc-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="872dc-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="872dc-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="872dc-106">이 항목에서는 방법을 toomanage Azure 미디어 서비스.net 엔터티.</span><span class="sxs-lookup"><span data-stu-id="872dc-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="872dc-107">2017 년 4 월 1부터 90 일 보다 오래 된 계정에서 모든 작업 기록은 자동으로 함께 삭제 됩니다, 관련된 작업 레코드를 레코드의 총 수 hello hello 최대 할당량 미만인 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="872dc-108">예를 들어, 2017년 4월 1일에는 계정에 있는 2016년 12월 31일 이전의 모든 작업 레코드가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="872dc-109">Tooarchive hello 작업/태스크 정보가 필요 하면이 항목에서 설명 하는 hello 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="872dc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="872dc-110">Prerequisites</span></span>

<span data-ttu-id="872dc-111">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="872dc-112">자산 참조 가져오기</span><span class="sxs-lookup"><span data-stu-id="872dc-112">Get an Asset Reference</span></span>
<span data-ttu-id="872dc-113">자주 작업은 미디어 서비스에서 참조 tooan 기존 자산 tooget.</span><span class="sxs-lookup"><span data-stu-id="872dc-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="872dc-114">다음 코드 예제에서 사용 하는 자산 id입니다. hello에 따라 Linq 쿼리 tooget 참조 tooan 기존 IAsset 개체를 다음 코드 예제는 hello를 가져오는 방법을 자산 참조 hello 서버 hello 자산 컬렉션에서 컨텍스트 개체 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="872dc-115">모든 자산 나열</span><span class="sxs-lookup"><span data-stu-id="872dc-115">List All Assets</span></span>
<span data-ttu-id="872dc-116">Hello 저장소에 보유 한 자산의 수가 증가 하면 때 유용한 toolist 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="872dc-117">다음 코드 예제는 hello를 통해 tooiterate 자산 컬렉션 hello 서버 컨텍스트 개체에 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="872dc-118">각 자산에서 코드 예제에서는 hello를 기록 하는 속성 값 toohello 콘솔의 일부도 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="872dc-119">예를 들어 각 자산에는 많은 미디어 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="872dc-120">hello 코드 예제에서는 각 자산과 관련 된 모든 파일을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-120">hello code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a><span data-ttu-id="872dc-121">작업 참조 가져오기</span><span class="sxs-lookup"><span data-stu-id="872dc-121">Get a Job Reference</span></span>

<span data-ttu-id="872dc-122">미디어 서비스 코드에서 처리 태스크를 사용 하는 경우 다음 코드 예제는 id입니다. hello에 따라 참조 tooan 기존 작업 hello 작업 컬렉션에서 tooget 참조 tooan IJob 개체 하는 방법을 보여 줍니다. tooget이 필요한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="872dc-123">있습니다 수 tooget 작업 참조 인코딩 장기 실행 작업을 시작할 때 하며, 필요 스레드에 toocheck hello 작업 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="872dc-124">다음과 같은 경우에 스레드에서 hello 메서드가 반환 될 때 tooretrieve 새로 고친된 참조 tooa 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="872dc-125">작업 및 자산 나열</span><span class="sxs-lookup"><span data-stu-id="872dc-125">List Jobs and Assets</span></span>
<span data-ttu-id="872dc-126">중요 한 관련된 작업에는 미디어 서비스에서 관련된 작업을 사용 하 여 toolist 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="872dc-127">hello 다음 코드 예제에서는 방법을 보여 줍니다 toolist 각 IJob 개체 및 다음 hello 작업, 모든 관련된 작업, 모든 입력된 자산에 대 한 속성이 표시 각 작업에 대 한 모든 출력 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="872dc-128">이 예제의 hello 코드는 다른 여러 작업 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="872dc-129">예를 들어 이전에 실행 된 하나 이상의 인코딩 작업에서 toolist hello 출력 자산을 원하는 경우이 코드 tooaccess hello 자산을 출력 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="872dc-130">참조 tooan 출력 자산을 사용 하는 경우에 hello 콘텐츠 tooother 사용자 또는 응용 프로그램 다운로드 하거나 Url을 제공 하 여 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="872dc-131">자산을 배달 하기 위한 옵션에 대 한 자세한 내용은 참조 하십시오. [hello Media Services SDK for.NET을 사용 하 여 자산 제공](media-services-deliver-streaming-content.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a><span data-ttu-id="872dc-132">모든 액세스 정책 나열</span><span class="sxs-lookup"><span data-stu-id="872dc-132">List all Access Policies</span></span>
<span data-ttu-id="872dc-133">미디어 서비스에서 자산 또는 해당 파일에 대한 액세스 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="872dc-134">액세스 정책은 파일이 나 자산 (어떤 유형의 액세스 및 hello 기간)에 대 한 hello 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="872dc-135">미디어 서비스 코드에서는 일반적으로 IAccessPolicy 개체를 만들고 기존 자산에 연결하여 액세스 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="872dc-136">그런 다음 미디어 서비스에 대 한 직접 액세스 tooassets 제공할 수 있도록 ILocator 개체를 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="872dc-137">이 문서 시리즈와 함께 제공 되는 hello Visual Studio 프로젝트 toocreate 및 할당 액세스 정책 및 로케이터 tooassets 방법을 보여 주는 몇 가지 코드 예제가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="872dc-138">코드 예제에서 보여 주는 방법을 다음 hello toolist 각각와 연관 된 모든 액세스 정책을 hello 서버 및 사용 권한의 hello 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="872dc-139">또 다른 유용한 방법은 tooview 액세스 정책을 toolist hello 서버에서 모든 ILocator 개체 수 있으며, 그런 다음 각 로케이터에 대 한 관련된 액세스 정책을 해당 AccessPolicy 속성을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a><span data-ttu-id="872dc-140">액세스 정책 제한</span><span class="sxs-lookup"><span data-stu-id="872dc-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="872dc-141">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="872dc-142">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="872dc-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="872dc-143">예를 들어 응용 프로그램에 한 번 실행 되는 코드 다음 hello로 일반 정책 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="872dc-144">나중에 사용할 Id tooa 로그 파일을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="872dc-145">그런 다음 다음과 같이 코드의 Id를 기존 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-145">Then, you can use hello existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="872dc-146">모든 로케이터 나열</span><span class="sxs-lookup"><span data-stu-id="872dc-146">List All Locators</span></span>
<span data-ttu-id="872dc-147">로케이터는 hello 로케이터의 관련된 액세스 정책에 의해 정의 된 대로 직접 경로 tooaccess 권한 toohello 자산 함께 자산을 제공 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="872dc-148">각 자산은 Locators 속성에서 자산과 연결된 ILocator 개체의 컬렉션을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="872dc-149">hello 서버 컨텍스트에 모든 로케이터를 포함 하는 Locator 컬렉션을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="872dc-150">hello 다음 코드 예제에서는 모든 로케이터를 나열 hello 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="872dc-151">각 로케이터에 대 한 관련된 자산 hello 및 액세스 정책에 대 한 Id hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="872dc-152">또한 hello 유형 사용 권한, hello 만료 날짜 및 hello 전체 경로 toohello 자산을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="872dc-153">로케이터 경로 tooan 자산은 기본 URL toohello 자산만 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="872dc-154">직접 경로 tooindividual 파일을 사용자 또는 응용 프로그램을 찾아 수 toocreate, 코드 hello 특정 파일 경로 toohello 로케이터 경로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="872dc-155">방법에 대 한 자세한 내용은 toodo이,이 참조 hello 항목 [hello Media Services SDK for.NET을 사용 하 여 자산 제공](media-services-deliver-streaming-content.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="872dc-156">대용량 엔터티 컬렉션 열거</span><span class="sxs-lookup"><span data-stu-id="872dc-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="872dc-157">엔터티를 쿼리할 때 공용 REST v2 쿼리 결과 too1000 결과 제한 하기 때문에 한 번에 반환 된 1000 엔터티 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="872dc-158">큰 엔터티 컬렉션을 열거 하는 경우 toouse Skip 및 Take 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="872dc-159">hello hello에서 모든 hello 작업을 통해 다음 함수 루프 미디어 서비스 계정을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="872dc-160">미디어 서비스는 작업 컬렉션의 작업 1000개를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="872dc-161">hello 함수는 Skip을 사용 하 고 있는지 toomake을 수행 (있을 경우 1000 개 이상의 작업 계정에) 모든 작업 열거 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a><span data-ttu-id="872dc-162">자산 삭제</span><span class="sxs-lookup"><span data-stu-id="872dc-162">Delete an Asset</span></span>
<span data-ttu-id="872dc-163">다음 예에서는 hello 자산을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="872dc-164">작업 삭제</span><span class="sxs-lookup"><span data-stu-id="872dc-164">Delete a Job</span></span>
<span data-ttu-id="872dc-165">작업 toodelete hello State 속성에 표시 된 대로 hello 작업의 hello 상태를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="872dc-166">완료되거나 취소된 작업을 삭제할 수 있지만, 큐에 대기됨, 예약됨 또는 처리 중 등의 특정 상태에 있는 작업을 먼저 취소해야 해당 작업을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872dc-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="872dc-167">hello 다음 코드 예제에서는 작업 상태를 확인 한 후 hello 상태가 완료 또는 취소 하는 경우를 삭제 한 작업을 삭제 하기 위한 메서드</span><span class="sxs-lookup"><span data-stu-id="872dc-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="872dc-168">이 코드 hello 참조 tooa 작업을 가져오기 위한이 항목의 이전 섹션에 따라 다릅니다: 작업 참조 가져오기.</span><span class="sxs-lookup"><span data-stu-id="872dc-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a><span data-ttu-id="872dc-169">액세스 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="872dc-169">Delete an Access Policy</span></span>
<span data-ttu-id="872dc-170">hello 다음 코드 예제에서는 tooget 참조 tooan 액세스 정책에 따라 방법 정책 Id 및 다음 toodelete hello 정책</span><span class="sxs-lookup"><span data-stu-id="872dc-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="872dc-171">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="872dc-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="872dc-172">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="872dc-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

