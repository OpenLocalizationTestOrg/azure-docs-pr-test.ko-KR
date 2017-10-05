---
title: "미디어 서비스.NET SDK를 사용하여 자산 및 관련 엔터티 관리"
description: "Media Services SDK for .NET을 사용하여 자산 및 관련 엔터티를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 5efe16a09808267d0797521f9e1df2b60aec9cbb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="87231-103">미디어 서비스.NET SDK를 사용하여 자산 및 관련 엔터티 관리</span><span class="sxs-lookup"><span data-stu-id="87231-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87231-104">.NET</span><span class="sxs-lookup"><span data-stu-id="87231-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="87231-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="87231-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="87231-106">이 항목에서는 .NET를 사용하여 Azure Media Services 엔터티를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-106">This topic shows how to manage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="87231-107">2017년 4월 1일부터 레코드의 총 수가 최고 할당량 미만인 경우에도 사용자 계정에 있는 90일이 지난 작업 레코드는 연결된 태스크 레코드와 함께 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="87231-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="87231-108">예를 들어, 2017년 4월 1일에는 계정에 있는 2016년 12월 31일 이전의 모든 작업 레코드가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="87231-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="87231-109">작업/태스크 정보를 보관해야 하는 경우에는 이 항목에 설명된 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-109">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87231-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="87231-110">Prerequisites</span></span>

<span data-ttu-id="87231-111">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="87231-111">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="87231-112">자산 참조 가져오기</span><span class="sxs-lookup"><span data-stu-id="87231-112">Get an Asset Reference</span></span>
<span data-ttu-id="87231-113">자주 수행하는 작업은 미디어 서비스에서 기존 자산에 대한 참조를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87231-113">A frequent task is to get a reference to an existing asset in Media Services.</span></span> <span data-ttu-id="87231-114">다음 코드 예제에서는 자산 ID를 기준으로 서버 컨텍스트 개체에 대한 Assets 컬렉션에서 자산 참조를 가져오는 방법을 보여 줍니다. 다음 코드 예제에서는 Linq 쿼리를 사용하여 기존 IAsset 개체에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="87231-114">The following code example shows how you can get an asset reference from the Assets collection on the server context object, based on an asset Id. The following code example uses a Linq query to get a reference to an existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query to get an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference the asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="87231-115">모든 자산 나열</span><span class="sxs-lookup"><span data-stu-id="87231-115">List All Assets</span></span>
<span data-ttu-id="87231-116">저장소에 포함된 자산 수가 증가하면 자산을 나열하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-116">As the number of assets you have in storage grows, it is helpful to list your assets.</span></span> <span data-ttu-id="87231-117">다음 코드 예제에서는 서버 컨텍스트 개체에 대한 Assets 컬렉션을 반복하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-117">The following code example shows how to iterate through the Assets collection on the server context object.</span></span> <span data-ttu-id="87231-118">각 자산이 포함된 코드 예제에서는 일부 속성 값을 콘솔에도 씁니다.</span><span class="sxs-lookup"><span data-stu-id="87231-118">With each asset, the code example also writes some of its property values to the console.</span></span> <span data-ttu-id="87231-119">예를 들어 각 자산에는 많은 미디어 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="87231-120">코드 예제에서는 각 자산과 관련된 모든 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="87231-120">The code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display the collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display the files associated with each asset. 
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

## <a name="get-a-job-reference"></a><span data-ttu-id="87231-121">작업 참조 가져오기</span><span class="sxs-lookup"><span data-stu-id="87231-121">Get a Job Reference</span></span>

<span data-ttu-id="87231-122">미디어 서비스 코드로 작업을 처리할 때 종종 ID에 따라 기존 작업에 대한 참조를 가져와야 합니다. 다음 코드 예제에서는 Jobs 컬렉션에서 IJob 개체에 대한 참조를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-122">When you work with processing tasks in Media Services code, you often need to get a reference to an existing job based on an Id. The following code example shows how to get a reference to an IJob object from the Jobs collection.</span></span>

<span data-ttu-id="87231-123">실행 시간이 긴 인코딩 작업을 시작할 때 작업 참조를 가져와야 하고 스레드에서 작업 상태를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-123">You may need to get a job reference when starting a long-running encoding job, and need to check the job status on a thread.</span></span> <span data-ttu-id="87231-124">이 경우 메서드가 스레드에서 반환될 때 작업에 대한 새로 고쳐진 참조를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-124">In cases like this, when the method returns from a thread, you need to retrieve a refreshed reference to a job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query to get an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return the job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="87231-125">작업 및 자산 나열</span><span class="sxs-lookup"><span data-stu-id="87231-125">List Jobs and Assets</span></span>
<span data-ttu-id="87231-126">중요한 관련 작업은 미디어 서비스에서 관련 작업이 있는 자산을 나열하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87231-126">An important related task is to list assets with their associated job in Media Services.</span></span> <span data-ttu-id="87231-127">다음 코드 예제에서는 각 IJob 개체를 나열하는 방법을 보여 주고, 각 작업에 대해 작업 관련 속성, 모든 관련 작업, 모든 입력 자산 및 모든 출력 자산을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-127">The following code example shows you how to list each IJob object, and then for each job, it displays properties about the job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="87231-128">이 예제의 코드는 다양한 다른 작업에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-128">The code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="87231-129">예를 들어 이전에 실행한 하나 이상의 인코딩 작업에서 출력 자산을 나열하려고 하면 이 코드에서는 출력 자산에 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-129">For example, if you want to list the output assets from one or more encoding jobs that you ran previously, this code shows how to access the output assets.</span></span> <span data-ttu-id="87231-130">출력 자산에 대한 참조가 있으면 콘텐츠를 다운로드하거나 URL을 제공하여 다른 사용자나 응용 프로그램에 콘텐츠를 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-130">When you have a reference to an output asset, you can then deliver the content to other users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="87231-131">자산 배달 옵션에 대한 자세한 내용은 [Media Services SDK for .NET을 사용하여 자산 배달](media-services-deliver-streaming-content.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87231-131">For more information on options for delivering assets, see [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on the server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display the collection of jobs on the server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display the associated tasks (a job  
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

            // For each job, display the list of input media assets.
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

            // For each job, display the list of output media assets.
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

## <a name="list-all-access-policies"></a><span data-ttu-id="87231-132">모든 액세스 정책 나열</span><span class="sxs-lookup"><span data-stu-id="87231-132">List all Access Policies</span></span>
<span data-ttu-id="87231-133">미디어 서비스에서 자산 또는 해당 파일에 대한 액세스 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="87231-134">액세스 정책은 파일 또는 자산에 대한 권한을 정의합니다(액세스 유형 및 기간).</span><span class="sxs-lookup"><span data-stu-id="87231-134">An access policy defines the permissions for a file or an asset (what type of access, and the duration).</span></span> <span data-ttu-id="87231-135">미디어 서비스 코드에서는 일반적으로 IAccessPolicy 개체를 만들고 기존 자산에 연결하여 액세스 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="87231-136">그다음에 미디어 서비스에서 자산에 직접 액세스할 수 있게 하는 ILocator 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87231-136">Then you create a ILocator object, which lets you provide direct access to assets in Media Services.</span></span> <span data-ttu-id="87231-137">이 설명서 시리즈와 함께 제공되는 Visual Studio 프로젝트에는 액세스 정책과 로케이터를 만들고 자산에 할당하는 방법을 보여 주는 몇 가지 코드 예제가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-137">The Visual Studio project that accompanies this documentation series contains several code examples that show how to create and assign access policies and locators to assets.</span></span>

<span data-ttu-id="87231-138">다음 코드 예제에서는 서버의 모든 액세스 정책을 나열하는 방법과 각 액세스 정책과 관련된 권한 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-138">The following code example shows how to list all access policies on the server, and shows the type of permissions associated with each.</span></span> <span data-ttu-id="87231-139">액세스 정책을 보는 또 다른 유용한 방법은 서버의 모든 ILocator 개체를 나열하는 것이고, 이렇게 하면 각 로케이터에 대해 AccessPolicy 속성을 사용하여 관련 액세스 정책을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-139">Another useful way to view access policies is to list all ILocator objects on the server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="87231-140">액세스 정책 제한</span><span class="sxs-lookup"><span data-stu-id="87231-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="87231-141">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="87231-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="87231-142">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-142">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="87231-143">예를 들어, 응용 프로그램에서 한 번만 실행하는 다음 코드와 일반 정책 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-143">For example, you can create a generic set of policies with the following code that would only run one time in your application.</span></span> <span data-ttu-id="87231-144">나중에 사용할 로그 파일에 ID를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-144">You can log IDs to a log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="87231-145">그런 다음 다음과 같이 코드에서 기존 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-145">Then, you can use the existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get the standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get the existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("The locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="87231-146">모든 로케이터 나열</span><span class="sxs-lookup"><span data-stu-id="87231-146">List All Locators</span></span>
<span data-ttu-id="87231-147">로케이터는 로케이터의 관련 액세스 정책에 정의된 대로 자산에 대한 권한과 함께 자산에 액세스하는 직접 경로를 제공하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="87231-147">A locator is a URL that provides a direct path to access an asset, along with permissions to the asset as defined by the locator's associated access policy.</span></span> <span data-ttu-id="87231-148">각 자산은 Locators 속성에서 자산과 연결된 ILocator 개체의 컬렉션을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="87231-149">서버 컨텍스트는 모든 로케이터가 포함된 Locators 컬렉션도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-149">The server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="87231-150">다음 코드 예제에서는 서버의 모든 로케이터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-150">The following code example lists all locators on the server.</span></span> <span data-ttu-id="87231-151">각 로케이터에 대해 관련 자산 및 액세스 정책에 대한 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-151">For each locator, it shows the Id for the related asset and access policy.</span></span> <span data-ttu-id="87231-152">또한 자산에 대한 전체 경로, 권한 유형 및 만료 날짜를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-152">It also displays the type of permissions, the expiration date, and the full path to the asset.</span></span>

<span data-ttu-id="87231-153">자산에 대한 로케이터 경로는 자산에 대한 기준 URL일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="87231-153">Note that a locator path to an asset is only a base URL to the asset.</span></span> <span data-ttu-id="87231-154">사용자 또는 응용 프로그램이 이동할 수 있는 개별 파일에 대한 직접 경로를 만들려면 코드에서 로케이터 경로에 특정 파일 경로를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-154">To create a direct path to individual files that a user or application could browse to, your code must add the specific file path to the locator path.</span></span> <span data-ttu-id="87231-155">이 작업을 수행하는 방법에 대한 자세한 내용은 [Media Services SDK for .NET을 사용하여 자산 배달](media-services-deliver-streaming-content.md)항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87231-155">For more information on how to do this, see the topic [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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
            // The locator path is the base or parent path (with included permissions) to access  
            // the media content of an asset. To create a full URL to a specific media file, take 
            // the locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="87231-156">대용량 엔터티 컬렉션 열거</span><span class="sxs-lookup"><span data-stu-id="87231-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="87231-157">엔터티를 쿼리할 때 한 번에 반환되는 엔터티 수는 최대 1000개입니다. 공용 REST v2에서는 쿼리 결과를 1000개로 제한하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="87231-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="87231-158">대용량 엔터티 컬렉션을 열거할 때 Skip 및 Take를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-158">You need to use Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="87231-159">다음 함수는 제공된 미디어 서비스 계정에서 모든 작업을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-159">The following function loops through all the jobs in the provided Media Services Account.</span></span> <span data-ttu-id="87231-160">미디어 서비스는 작업 컬렉션의 작업 1000개를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="87231-161">이 함수는 Skip 및 Take를 사용하여 모든 작업이 연결되었는지 확인합니다(계정에 1000개가 넘는 작업이 있는 경우).</span><span class="sxs-lookup"><span data-stu-id="87231-161">The function makes use of Skip and Take to make sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in the Media Services account
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

## <a name="delete-an-asset"></a><span data-ttu-id="87231-162">자산 삭제</span><span class="sxs-lookup"><span data-stu-id="87231-162">Delete an Asset</span></span>
<span data-ttu-id="87231-163">다음 예제에서는 자산을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-163">The following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete the asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted the Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="87231-164">작업 삭제</span><span class="sxs-lookup"><span data-stu-id="87231-164">Delete a Job</span></span>
<span data-ttu-id="87231-165">작업을 삭제하려면 State 속성에 표시된 작업의 상태를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-165">To delete a job, you must check the state of the job as indicated in the State property.</span></span> <span data-ttu-id="87231-166">완료되거나 취소된 작업을 삭제할 수 있지만, 큐에 대기됨, 예약됨 또는 처리 중 등의 특정 상태에 있는 작업을 먼저 취소해야 해당 작업을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87231-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="87231-167">다음 코드 예제에서는 작업 상태를 확인하고 상태가 완료됨 또는 취소됨일 때 삭제하는 방법으로 작업을 삭제하는 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-167">The following code example shows a method for deleting a job by checking job states and then deleting when the state is finished or canceled.</span></span> <span data-ttu-id="87231-168">이 코드에서는 작업에 대한 참조를 가져오는 방법에 대한 이 항목의 이전 섹션인 작업 참조 가져오기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87231-168">This code depends on the previous section in this topic for getting a reference to a job: Get a job reference.</span></span>

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
                    // You can also call job.DeleteAsync to do async deletes.
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


## <a name="delete-an-access-policy"></a><span data-ttu-id="87231-169">액세스 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="87231-169">Delete an Access Policy</span></span>
<span data-ttu-id="87231-170">다음 코드 예제에서는 정책 ID에 따라 액세스 정책에 대한 참조를 가져오고 정책을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87231-170">The following code example shows how to get a reference to an access policy based on a policy Id, and then to delete the policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // To delete a specific access policy, get a reference to the policy.  
        // based on the policy Id passed to the method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="87231-171">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="87231-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="87231-172">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="87231-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

