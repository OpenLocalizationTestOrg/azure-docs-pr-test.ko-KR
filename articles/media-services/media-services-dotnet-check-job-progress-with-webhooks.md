---
title: "Azure WebHooks를 사용하여 .NET으로 Media Services 작업 알림 모니터링 | Microsoft Docs"
description: "Azure WebHooks를 사용하여 Media Services 작업 알림을 모니터링하는 방법에 대해 알아봅니다. 코드 샘플은 C#으로 작성되었으며 Media Services SDK for .NET을 사용합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a61fe157-81b1-45c1-89f2-224b7ef55869
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/06/2017
ms.author: juliako
ms.openlocfilehash: eaa875a7c78de0b69c81514ea023f9b8bceb2656
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-webhooks-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="4b89e-104">Azure WebHooks를 사용하여 .NET으로 Media Services 작업 알림 모니터링</span><span class="sxs-lookup"><span data-stu-id="4b89e-104">Use Azure WebHooks to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="4b89e-105">작업을 실행할 때 작업 진행 상태를 추적하는 방법이 종종 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-105">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="4b89e-106">Azure Webhooks 또는 [Azure Queue Storage](media-services-dotnet-check-job-progress-with-queues.md)를 사용하여 Media Services 작업 알림을 모니터링할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="4b89e-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span></span> <span data-ttu-id="4b89e-107">이 항목에서는 Webhook을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-107">This topic shows how to work with Webhooks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b89e-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4b89e-108">Prerequisites</span></span>

<span data-ttu-id="4b89e-109">자습서를 완료하는 데 필요한 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="4b89e-110">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4b89e-110">An Azure account.</span></span> <span data-ttu-id="4b89e-111">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b89e-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4b89e-112">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="4b89e-112">A Media Services account.</span></span> <span data-ttu-id="4b89e-113">Media Services 계정을 만들려면 [Media Services 계정을 만드는 방법](media-services-portal-create-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b89e-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="4b89e-114">[Azure Functions를 사용하는 방법](../azure-functions/functions-overview.md)을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-114">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="4b89e-115">또한 [Azure Functions HTTP 및 WebHook 바인딩](../azure-functions/functions-bindings-http-webhook.md)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-115">Also, review [Azure functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md).</span></span>

<span data-ttu-id="4b89e-116">이 항목에서는 다음을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-116">This topic shows how to</span></span>

*  <span data-ttu-id="4b89e-117">Webhook에 응답하도록 사용자 지정된 Azure Function을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-117">Define an Azure Function that is customized to respond to webhooks.</span></span> 
    
    <span data-ttu-id="4b89e-118">이 경우에 인코딩 작업이 상태를 변경하면 Webhook이 Media Services에서 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-118">In this case, the webhook is triggered by Media Services when your encoding job changes status.</span></span> <span data-ttu-id="4b89e-119">함수는 Media Services 알림의 Webhook 호출을 수신 대기하고 작업이 완료되면 출력 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-119">The function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="4b89e-120">계속 진행하기 전에 [Azure Functions HTTP 및 Webhook 바인딩](../azure-functions/functions-bindings-http-webhook.md) 작동 방법에 대해 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-120">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md) work.</span></span>
    >
    
* <span data-ttu-id="4b89e-121">인코딩 태스크에 Webhook을 추가하고 Webhook URL 및 이 Webhook이 응답하는 암호 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-121">Add a webhook to your encoding task and specify the webhook URL and secret key that this webhook responds to.</span></span> <span data-ttu-id="4b89e-122">여기에 표시된 예제에서 인코딩 태스크를 만드는 코드는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-122">In the example shown here, the code that creates the encoding task is a console app.</span></span>

## <a name="setting-up-webhook-notification-azure-functions"></a><span data-ttu-id="4b89e-123">“웹후크 알림" Azure 기능 설정</span><span class="sxs-lookup"><span data-stu-id="4b89e-123">Setting up "webhook notification" Azure functions</span></span>

<span data-ttu-id="4b89e-124">이 섹션의 코드는 Webhook에서 Azure Function의 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-124">The code in this section shows an implementation of an Azure function that is a webhook.</span></span> <span data-ttu-id="4b89e-125">이 샘플에서 함수는 Media Services 알림의 Webhook 호출을 수신 대기하고 작업이 완료되면 출력 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-125">In this sample, the function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span>

<span data-ttu-id="4b89e-126">Webhook은 알림 끝점을 구성하는 경우에 전달되는 것과 일치하는 서명 키(자격 증명)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-126">The webhook expects a signing key (credential) to match the one you pass when you configure the notification endpoint.</span></span> <span data-ttu-id="4b89e-127">서명 키는 Azure Media Services에서 Webhook 콜백을 보호하고 보안하는 데 사용되는 64바이트 Base64 인코딩 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-127">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

<span data-ttu-id="4b89e-128">다음 코드에서 **VerifyWebHookRequestSignature** 메서드는 알림 메시지에 대한 검증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-128">In the following code, the **VerifyWebHookRequestSignature** method does the verification on the notification message.</span></span> <span data-ttu-id="4b89e-129">이 유효성 검사는 메시지가 Azure Media Services에서 전송되었는지, 손상되지 않았는지 확인하기 위해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-129">The purpose of this validation is to ensure that the message was sent by Azure Media Services and hasn’t been tampered with.</span></span> <span data-ttu-id="4b89e-130">전송 계층 보안(TLS)에서 쿼리 매개 변수로 **코드** 값을 보유하는 것처럼 서명도 Azure Functions에 대해 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-130">The signature is optional for Azure functions as it has the **Code** value as a query parameter over Transport Layer Security (TLS).</span></span> 

<span data-ttu-id="4b89e-131">[여기](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)에서는 이 항목에 나와 있는 항목을 포함하여 다양한 Media Services .NET Azure Functions의 정의를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-131">You can find the definition of various Media Services .NET Azure functions (including the one shown in this topic) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>

<span data-ttu-id="4b89e-132">다음 코드 목록은 Azure Function 매개 변수 및 Azure Function과 관련된 function.json, project.json, run.csx라는 세 개 파일의 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-132">The following code listing shows the definitions of Azure function parameters and three files that are associated with the Azure function: function.json, project.json, and run.csx.</span></span>

### <a name="application-settings"></a><span data-ttu-id="4b89e-133">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="4b89e-133">Application settings</span></span> 

<span data-ttu-id="4b89e-134">다음 표에는 이 섹션에 정의된 Azure 함수에 사용되는 매개 변수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-134">The following table shows the parameters that are used by the Azure function defined in this section.</span></span> 

|<span data-ttu-id="4b89e-135">이름</span><span class="sxs-lookup"><span data-stu-id="4b89e-135">Name</span></span>|<span data-ttu-id="4b89e-136">정의</span><span class="sxs-lookup"><span data-stu-id="4b89e-136">Definition</span></span>|<span data-ttu-id="4b89e-137">예</span><span class="sxs-lookup"><span data-stu-id="4b89e-137">Example</span></span>| 
|---|---|---|
|<span data-ttu-id="4b89e-138">AMSAccount</span><span class="sxs-lookup"><span data-stu-id="4b89e-138">AMSAccount</span></span>|<span data-ttu-id="4b89e-139">AMS 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-139">Your AMS account name.</span></span> |<span data-ttu-id="4b89e-140">juliakomediaservices</span><span class="sxs-lookup"><span data-stu-id="4b89e-140">juliakomediaservices</span></span>|
|<span data-ttu-id="4b89e-141">AMSKey</span><span class="sxs-lookup"><span data-stu-id="4b89e-141">AMSKey</span></span> |<span data-ttu-id="4b89e-142">AMS 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-142">Your AMS account key.</span></span> | <span data-ttu-id="4b89e-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span><span class="sxs-lookup"><span data-stu-id="4b89e-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span></span>|
|<span data-ttu-id="4b89e-144">MediaServicesStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="4b89e-144">MediaServicesStorageAccountName</span></span> |<span data-ttu-id="4b89e-145">AMS 계정과 연결된 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-145">A name of the storage account that is associated with your AMS account.</span></span>| <span data-ttu-id="4b89e-146">storagepkeewmg5c3peq</span><span class="sxs-lookup"><span data-stu-id="4b89e-146">storagepkeewmg5c3peq</span></span>|
|<span data-ttu-id="4b89e-147">MediaServicesStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="4b89e-147">MediaServicesStorageAccountKey</span></span> |<span data-ttu-id="4b89e-148">AMS 계정과 연결된 저장소 계정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-148">A key of the storage account that is associated with your AMS account.</span></span>|
|<span data-ttu-id="4b89e-149">SigningKey</span><span class="sxs-lookup"><span data-stu-id="4b89e-149">SigningKey</span></span> |<span data-ttu-id="4b89e-150">서명 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-150">A signing key.</span></span>| <span data-ttu-id="4b89e-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span><span class="sxs-lookup"><span data-stu-id="4b89e-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span></span>|
|<span data-ttu-id="4b89e-152">WebHookEndpoint</span><span class="sxs-lookup"><span data-stu-id="4b89e-152">WebHookEndpoint</span></span> | <span data-ttu-id="4b89e-153">웹후크 끝점 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-153">A webhook endpoint address.</span></span> | <span data-ttu-id="4b89e-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span><span class="sxs-lookup"><span data-stu-id="4b89e-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span></span>|

### <a name="functionjson"></a><span data-ttu-id="4b89e-155">function.json</span><span class="sxs-lookup"><span data-stu-id="4b89e-155">function.json</span></span>

<span data-ttu-id="4b89e-156">function.json 파일은 함수 바인딩 및 기타 구성 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="4b89e-157">런타임은 이 파일을 사용하여 모니터링할 이벤트와 함수 실행에서 데이터를 전달하고 반환하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> 

    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [
        "post",
        "get",
        "put",
        "update",
        "patch"
          ]
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
    
### <a name="projectjson"></a><span data-ttu-id="4b89e-158">project.json</span><span class="sxs-lookup"><span data-stu-id="4b89e-158">project.json</span></span>

<span data-ttu-id="4b89e-159">project.json 파일은 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-159">The project.json file contains dependencies.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="4b89e-160">run.csx</span><span class="sxs-lookup"><span data-stu-id="4b89e-160">run.csx</span></span>

<span data-ttu-id="4b89e-161">다음 C# 코드는 Webhook인 Azure Function의 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-161">The following C# code shows a definition of an Azure function that is a webhook.</span></span> <span data-ttu-id="4b89e-162">함수는 Media Services 알림의 Webhook 호출을 수신 대기하고 작업이 완료되면 출력 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-162">The function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span> 


>[!NOTE]
><span data-ttu-id="4b89e-163">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-163">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="4b89e-164">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-164">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="4b89e-165">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b89e-165">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    ///////////////////////////////////////////////////
    #r "Newtonsoft.Json"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using System.Globalization;
    using Newtonsoft.Json;
    using Microsoft.Azure;
    using System.Net;
    using System.Security.Cryptography;

    internal const string SignatureHeaderKey = "sha256";
    internal const string SignatureHeaderValueTemplate = SignatureHeaderKey + "={0}";
    static string _webHookEndpoint = Environment.GetEnvironmentVariable("WebHookEndpoint");
    static string _signingKey = Environment.GetEnvironmentVariable("SigningKey");
    static string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    static string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static CloudMediaContext _context = null;

    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

        Task<byte[]> taskForRequestBody = req.Content.ReadAsByteArrayAsync();
        byte[] requestBody = await taskForRequestBody;

        string jsonContent = await req.Content.ReadAsStringAsync();
        log.Info($"Request Body = {jsonContent}");

        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-signature", out values))
        {
        byte[] signingKey = Convert.FromBase64String(_signingKey);
        string signatureFromHeader = values.FirstOrDefault();

        if (VerifyWebHookRequestSignature(requestBody, signatureFromHeader, signingKey))
        {
            string requestMessageContents = Encoding.UTF8.GetString(requestBody);

            NotificationMessage msg = JsonConvert.DeserializeObject<NotificationMessage>(requestMessageContents);

            if (VerifyHeaders(req, msg, log))
            { 
            string newJobStateStr = (string)msg.Properties.Where(j => j.Key == "NewState").FirstOrDefault().Value;
            if (newJobStateStr == "Finished")
            {
                _context = new CloudMediaContext(new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey));

                if(_context!=null)   
                {                        
                string urlForClientStreaming = PublishAndBuildStreamingURLs(msg.Properties["JobId"]);
                log.Info($"URL to the manifest for client streaming using HLS protocol: {urlForClientStreaming}");
                }
            }

            return req.CreateResponse(HttpStatusCode.OK, string.Empty);
            }
            else
            {
            log.Info($"VerifyHeaders failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyHeaders failed.");
            }
        }
        else
        {
            log.Info($"VerifyWebHookRequestSignature failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyWebHookRequestSignature failed.");
        }
        }

        return req.CreateResponse(HttpStatusCode.BadRequest, "Generic Error.");
    }

    private static string PublishAndBuildStreamingURLs(String jobID)
    {
        IJob job = _context.Jobs.Where(j => j.Id == jobID).FirstOrDefault();
        IAsset asset = job.OutputMediaAssets.FirstOrDefault();

        // Create a 30-day readonly access policy. 
        // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
        TimeSpan.FromDays(30),
        AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy,
        DateTime.UtcNow.AddMinutes(-5));


        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                    EndsWith(".ism")).
                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest" +  "(format=m3u8-aapl)";
        return urlForClientStreaming;

    }

    private static bool VerifyWebHookRequestSignature(byte[] data, string actualValue, byte[] verificationKey)
    {
        using (var hasher = new HMACSHA256(verificationKey))
        {
        byte[] sha256 = hasher.ComputeHash(data);
        string expectedValue = string.Format(CultureInfo.InvariantCulture, SignatureHeaderValueTemplate, ToHex(sha256));

        return (0 == String.Compare(actualValue, expectedValue, System.StringComparison.Ordinal));
        }
    }

    private static bool VerifyHeaders(HttpRequestMessage req, NotificationMessage msg, TraceWriter log)
    {
        bool headersVerified = false;

        try
        {
        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-mediaservices-accountid", out values))
        {
            string accountIdHeader = values.FirstOrDefault();
            string accountIdFromMessage = msg.Properties["AccountId"];

            if (0 == string.Compare(accountIdHeader, accountIdFromMessage, StringComparison.OrdinalIgnoreCase))
            {
            headersVerified = true;
            }
            else
            {
            log.Info($"accountIdHeader={accountIdHeader} does not match accountIdFromMessage={accountIdFromMessage}");
            }
        }
        else
        {
            log.Info($"Header ms-mediaservices-accountid not found.");
        }
        }
        catch (Exception e)
        {
        log.Info($"VerifyHeaders hit exception {e}");
        headersVerified = false;
        }

        return headersVerified;
    }

    private static readonly char[] HexLookup = new char[] { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };

    /// <summary>
    /// Converts a <see cref="T:byte[]"/> to a hex-encoded string.
    /// </summary>
    private static string ToHex(byte[] data)
    {
        if (data == null)
        {
        return string.Empty;
        }

        char[] content = new char[data.Length * 2];
        int output = 0;
        byte d;
        for (int input = 0; input < data.Length; input++)
        {
        d = data[input];
        content[output++] = HexLookup[d / 0x10];
        content[output++] = HexLookup[d % 0x10];
        }
        return new string(content);
    }

    internal enum NotificationEventType
    {
        None = 0,
        JobStateChange = 1,
        NotificationEndPointRegistration = 2,
        NotificationEndPointUnregistration = 3,
        TaskStateChange = 4,
        TaskProgress = 5
    }
    
    internal sealed class NotificationMessage
    {
        public string MessageVersion { get; set; }
        public string ETag { get; set; }
        public NotificationEventType EventType { get; set; }
        public DateTime TimeStamp { get; set; }
        public IDictionary<string, string> Properties { get; set; }
    }

### <a name="function-output"></a><span data-ttu-id="4b89e-166">함수 출력</span><span class="sxs-lookup"><span data-stu-id="4b89e-166">Function output</span></span>

<span data-ttu-id="4b89e-167">위의 예제는 다음과 같이 출력되고 사용자의 값이 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-167">The example above produced the following output, your values will vary.</span></span>

    C# HTTP trigger function processed a request. RequestUri=https://juliako001-functions.azurewebsites.net/api/Notification_Webhook_Function?code=9376d69kygoy49oft81nel8frty5cme8hb9xsjslxjhalwhfrqd79awz8ic4ieku74dvkdfgvi
    Request Body = {
      "MessageVersion": "1.1",
      "ETag": "b8977308f48858a8f224708bc963e1a09ff917ce730316b4e7ae9137f78f3b20",
      "EventType": 4,
      "TimeStamp": "2017-02-16T03:59:53.3041122Z",
      "Properties": {
        "JobId": "nb:jid:UUID:badd996c-8d7c-4ae0-9bc1-bd7f1902dbdd",
        "TaskId": "nb:tid:UUID:80e26fb9-ee04-4739-abd8-2555dc24639f",
        "NewState": "Finished",
        "OldState": "Processing",
        "AccountName": "mediapkeewmg5c3peq",
        "AccountId": "301912b0-659e-47e0-9bc4-6973f2be3424",
        "NotificationEndPointId": "nb:nepid:UUID:cb5d707b-4db8-45fe-a558-19f8d3306093"
      }
    }
    
    URL to the manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="adding-webhook-to-your-encoding-task"></a><span data-ttu-id="4b89e-168">인코딩 태스크에 Webhook 추가</span><span class="sxs-lookup"><span data-stu-id="4b89e-168">Adding Webhook to your encoding task</span></span>

<span data-ttu-id="4b89e-169">이 섹션에서는 태스크에 Webhook 알림을 추가하는 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-169">In this section, the code that adds a webhook notification to a Task is shown.</span></span> <span data-ttu-id="4b89e-170">작업 수준 알림을 추가할 수도 있습니다. 그러면 연결된 태스크를 사용하여 작업에 더 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-170">You can also add a job level notification, which would be more useful for a job with chained tasks.</span></span>  

1. <span data-ttu-id="4b89e-171">Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-171">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="4b89e-172">이름, 위치 및 솔루션 이름을 입력하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-172">Enter the Name, Location, and Solution name, and then click OK.</span></span>
2. <span data-ttu-id="4b89e-173">[NuGet](https://www.nuget.org/packages/windowsazure.mediaservices)을 사용하여 Azure Media Services를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-173">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) to install Azure Media Services.</span></span>
3. <span data-ttu-id="4b89e-174">App.config 파일을 적절한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-174">Update App.config file with appropriate values:</span></span> 
    
    * <span data-ttu-id="4b89e-175">알림을 전송하는 Azure Media Services 이름 및 키</span><span class="sxs-lookup"><span data-stu-id="4b89e-175">Azure Media Services name and key that will be sending notifications,</span></span> 
    * <span data-ttu-id="4b89e-176">알림을 가져오려는 Webhook URL</span><span class="sxs-lookup"><span data-stu-id="4b89e-176">webhook URL that expects to get the notifications,</span></span> 
    * <span data-ttu-id="4b89e-177">Webhook이 필요로 하는 키와 일치하는 서명 키</span><span class="sxs-lookup"><span data-stu-id="4b89e-177">the signing key that matches the key that your webhook expects.</span></span> <span data-ttu-id="4b89e-178">서명 키는 Azure Media Services에서 Webhook 콜백을 보호하고 보안하는 데 사용되는 64바이트 Base64 인코딩 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-178">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

            <appSettings>
              <add key="MediaServicesAccountName" value="AMSAcctName" />
              <add key="MediaServicesAccountKey" value="AMSAcctKey" />
              <add key="WebhookURL" value="https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
            
4. <span data-ttu-id="4b89e-179">Program.cs 파일을 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4b89e-179">Update your Program.cs file with the following code:</span></span>

        using System;
        using System.Configuration;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace NotificationWebHook
        {
            class Program
            {
            // Read values from the App.config file.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];
            private static readonly string _webHookEndpoint =
                ConfigurationManager.AppSettings["WebhookURL"];
            private static readonly string _signingKey =
                 ConfigurationManager.AppSettings["WebhookSigningKey"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {

                // Used the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(new MediaServicesCredentials(
                        _mediaServicesAccountName,
                        _mediaServicesAccountKey));

                byte[] keyBytes = Convert.FromBase64String(_signingKey);

                IAsset newAsset = _context.Assets.FirstOrDefault();

                // Check for existing Notification Endpoint with the name "FunctionWebHook"

                var existingEndpoint = _context.NotificationEndPoints.Where(e => e.Name == "FunctionWebHook").FirstOrDefault();
                INotificationEndPoint endpoint = null;

                if (existingEndpoint != null)
                {
                Console.WriteLine("webhook endpoint already exists");
                endpoint = (INotificationEndPoint)existingEndpoint;
                }
                else
                {
                endpoint = _context.NotificationEndPoints.Create("FunctionWebHook",
                    NotificationEndPointType.WebHook, _webHookEndpoint, keyBytes);
                Console.WriteLine("Notification Endpoint Created with Key : {0}", keyBytes.ToString());
                }

                // Declare a new encoding job with the Standard encoder
                IJob job = _context.Jobs.Create("MES Job");

                // Get a media processor reference, and pass to it the name of the 
                // processor to use for the specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

                // Specify the input asset to be encoded.
                task.InputAssets.Add(newAsset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is not encrypted. 
                task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                // Add the WebHook notification to this Task and request all notification state changes.
                // Note that you can also add a job level notification
                // which would be more useful for a job with chained tasks.  
                if (endpoint != null)
                {
                task.TaskNotificationSubscriptions.AddNew(NotificationJobState.All, endpoint, true);
                Console.WriteLine("Created Notification Subscription for endpoint: {0}", _webHookEndpoint);
                }
                else
                {
                Console.WriteLine("No Notification Endpoint is being used");
                }

                job.Submit();

                Console.WriteLine("Expect WebHook to be triggered for the Job ID: {0}", job.Id);
                Console.WriteLine("Expect WebHook to be triggered for the Task ID: {0}", task.Id);

                Console.WriteLine("Job Submitted");

            }
            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                return processor;
            }

            }
        }

## <a name="next-step"></a><span data-ttu-id="4b89e-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b89e-180">Next step</span></span>
<span data-ttu-id="4b89e-181">미디어 서비스 학습 경로 검토</span><span class="sxs-lookup"><span data-stu-id="4b89e-181">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4b89e-182">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="4b89e-182">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
