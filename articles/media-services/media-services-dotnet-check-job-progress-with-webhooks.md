---
title: ".net aaaUse Azure Webhook toomonitor 미디어 서비스 작업 알림 | Microsoft Docs"
description: "Toouse Azure Webhook toomonitor 미디어 서비스 알림 작업 하는 방법에 대해 알아봅니다. hello 코드 예제는 C#으로 작성 하 고 hello Media Services SDK for.NET 사용."
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
ms.openlocfilehash: b7df597da20e551cb2a02cd21c96c7bddf9e1a66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-webhooks-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="e1145-104">.NET과 함께 Azure Webhook toomonitor 미디어 서비스 작업 알림 사용</span><span class="sxs-lookup"><span data-stu-id="e1145-104">Use Azure WebHooks toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="e1145-105">작업을 실행 하면 일반적 방법을 tootrack 작업 진행 상황을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-105">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="e1145-106">Azure Webhooks 또는 [Azure Queue Storage](media-services-dotnet-check-job-progress-with-queues.md)를 사용하여 Media Services 작업 알림을 모니터링할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="e1145-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span></span> <span data-ttu-id="e1145-107">이 항목에서는 방법을 toowork Webhook 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-107">This topic shows how toowork with Webhooks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1145-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e1145-108">Prerequisites</span></span>

<span data-ttu-id="e1145-109">hello 다음은 필요한 toocomplete hello 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="e1145-110">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="e1145-110">An Azure account.</span></span> <span data-ttu-id="e1145-111">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1145-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e1145-112">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="e1145-112">A Media Services account.</span></span> <span data-ttu-id="e1145-113">미디어 서비스 계정 toocreate 참조 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e1145-114">이해 [어떻게 toouse Azure 함수](../azure-functions/functions-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-114">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="e1145-115">또한 [Azure Functions HTTP 및 WebHook 바인딩](../azure-functions/functions-bindings-http-webhook.md)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-115">Also, review [Azure functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md).</span></span>

<span data-ttu-id="e1145-116">이 항목에서는 다음을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-116">This topic shows how to</span></span>

*  <span data-ttu-id="e1145-117">사용자 지정 된 toorespond toowebhooks Azure 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-117">Define an Azure Function that is customized toorespond toowebhooks.</span></span> 
    
    <span data-ttu-id="e1145-118">이 경우 hello webhook 인코딩 작업 상태를 변경 하는 경우 미디어 서비스에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-118">In this case, hello webhook is triggered by Media Services when your encoding job changes status.</span></span> <span data-ttu-id="e1145-119">미디어 서비스 알림에서 hello webhook 호출에 대 한 수신 하 고 hello 작업이 완료 되 면 hello 출력 자산을 게시 하는 hello 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-119">hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="e1145-120">계속 진행하기 전에 [Azure Functions HTTP 및 Webhook 바인딩](../azure-functions/functions-bindings-http-webhook.md) 작동 방법에 대해 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-120">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md) work.</span></span>
    >
    
* <span data-ttu-id="e1145-121">Webhook tooyour 인코딩 태스크를 추가 하 고 hello webhook URL 및이 webhook이 응답 하는 비밀 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-121">Add a webhook tooyour encoding task and specify hello webhook URL and secret key that this webhook responds to.</span></span> <span data-ttu-id="e1145-122">Hello 예에서 여기에 표시 된 hello를 만드는 코드를 hello 인코딩 작업은 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-122">In hello example shown here, hello code that creates hello encoding task is a console app.</span></span>

## <a name="setting-up-webhook-notification-azure-functions"></a><span data-ttu-id="e1145-123">“웹후크 알림" Azure 기능 설정</span><span class="sxs-lookup"><span data-stu-id="e1145-123">Setting up "webhook notification" Azure functions</span></span>

<span data-ttu-id="e1145-124">이 섹션의 hello 코드는 webhook은 Azure 함수의 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-124">hello code in this section shows an implementation of an Azure function that is a webhook.</span></span> <span data-ttu-id="e1145-125">이 샘플에서는 hello 함수 미디어 서비스 알림에서 hello webhook 호출에 대 한 수신 대기 하 고 hello 작업이 완료 되 면 hello 출력 자산을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-125">In this sample, hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span>

<span data-ttu-id="e1145-126">hello webhook에서는 서명 키 (자격 증명) toomatch hello 하나 hello 알림 끝점을 구성 하는 때를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-126">hello webhook expects a signing key (credential) toomatch hello one you pass when you configure hello notification endpoint.</span></span> <span data-ttu-id="e1145-127">서명 키 hello는 사용 되는 tooprotect 되며 Webhook 콜백을 Azure 미디어 서비스에서 보안 된 hello 64 바이트 Base64 인코딩 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-127">hello signing key is hello 64-byte Base64 encoded value that is used tooprotect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

<span data-ttu-id="e1145-128">코드 다음 hello, hello **VerifyWebHookRequestSignature** 메서드 확인 hello 알림 메시지에 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-128">In hello following code, hello **VerifyWebHookRequestSignature** method does hello verification on hello notification message.</span></span> <span data-ttu-id="e1145-129">hello이 유효성이 검사의 목적은 환영 메시지가 tooensure Azure 미디어 서비스에서 보낸 및 손상 되지 않았음을입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-129">hello purpose of this validation is tooensure that hello message was sent by Azure Media Services and hasn’t been tampered with.</span></span> <span data-ttu-id="e1145-130">hello가 hello 서명을 Azure 기능에 대 한 선택 사항 **코드** 값으로 쿼리 매개 변수를 통해 보안 TLS (전송 계층).</span><span class="sxs-lookup"><span data-stu-id="e1145-130">hello signature is optional for Azure functions as it has hello **Code** value as a query parameter over Transport Layer Security (TLS).</span></span> 

<span data-ttu-id="e1145-131">다양 한 미디어 서비스.NET Azure 함수 (이 항목의 뒤에 하나 hello 포함)의 hello 정의 찾을 수 있습니다 [여기](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-131">You can find hello definition of various Media Services .NET Azure functions (including hello one shown in this topic) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>

<span data-ttu-id="e1145-132">hello 다음 코드 목록 정의 보여 줍니다 hello Azure 함수 매개 변수 및 Azure 함수 hello와 관련 된 세 개의 파일의: function.json, project.json, 및 run.csx 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-132">hello following code listing shows hello definitions of Azure function parameters and three files that are associated with hello Azure function: function.json, project.json, and run.csx.</span></span>

### <a name="application-settings"></a><span data-ttu-id="e1145-133">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="e1145-133">Application settings</span></span> 

<span data-ttu-id="e1145-134">hello 다음 표에 hello이이 섹션에 정의 된 Azure 함수에서 사용 되는 hello 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-134">hello following table shows hello parameters that are used by hello Azure function defined in this section.</span></span> 

|<span data-ttu-id="e1145-135">이름</span><span class="sxs-lookup"><span data-stu-id="e1145-135">Name</span></span>|<span data-ttu-id="e1145-136">정의</span><span class="sxs-lookup"><span data-stu-id="e1145-136">Definition</span></span>|<span data-ttu-id="e1145-137">예</span><span class="sxs-lookup"><span data-stu-id="e1145-137">Example</span></span>| 
|---|---|---|
|<span data-ttu-id="e1145-138">AMSAccount</span><span class="sxs-lookup"><span data-stu-id="e1145-138">AMSAccount</span></span>|<span data-ttu-id="e1145-139">AMS 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-139">Your AMS account name.</span></span> |<span data-ttu-id="e1145-140">juliakomediaservices</span><span class="sxs-lookup"><span data-stu-id="e1145-140">juliakomediaservices</span></span>|
|<span data-ttu-id="e1145-141">AMSKey</span><span class="sxs-lookup"><span data-stu-id="e1145-141">AMSKey</span></span> |<span data-ttu-id="e1145-142">AMS 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-142">Your AMS account key.</span></span> | <span data-ttu-id="e1145-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span><span class="sxs-lookup"><span data-stu-id="e1145-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span></span>|
|<span data-ttu-id="e1145-144">MediaServicesStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="e1145-144">MediaServicesStorageAccountName</span></span> |<span data-ttu-id="e1145-145">AMS 계정과 연결 된 hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-145">A name of hello storage account that is associated with your AMS account.</span></span>| <span data-ttu-id="e1145-146">storagepkeewmg5c3peq</span><span class="sxs-lookup"><span data-stu-id="e1145-146">storagepkeewmg5c3peq</span></span>|
|<span data-ttu-id="e1145-147">MediaServicesStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="e1145-147">MediaServicesStorageAccountKey</span></span> |<span data-ttu-id="e1145-148">AMS 계정과 연결 된 hello 저장소 계정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-148">A key of hello storage account that is associated with your AMS account.</span></span>|
|<span data-ttu-id="e1145-149">SigningKey</span><span class="sxs-lookup"><span data-stu-id="e1145-149">SigningKey</span></span> |<span data-ttu-id="e1145-150">서명 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-150">A signing key.</span></span>| <span data-ttu-id="e1145-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span><span class="sxs-lookup"><span data-stu-id="e1145-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span></span>|
|<span data-ttu-id="e1145-152">WebHookEndpoint</span><span class="sxs-lookup"><span data-stu-id="e1145-152">WebHookEndpoint</span></span> | <span data-ttu-id="e1145-153">웹후크 끝점 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-153">A webhook endpoint address.</span></span> | <span data-ttu-id="e1145-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span><span class="sxs-lookup"><span data-stu-id="e1145-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span></span>|

### <a name="functionjson"></a><span data-ttu-id="e1145-155">function.json</span><span class="sxs-lookup"><span data-stu-id="e1145-155">function.json</span></span>

<span data-ttu-id="e1145-156">hello function.json 파일 hello 함수 바인딩 및 기타 구성 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="e1145-157">hello 런타임은이 파일 toodetermine hello 이벤트 toomonitor 및 toopass 데이터를 한 반환 데이터에서 실행이 작동 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> 

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
    
### <a name="projectjson"></a><span data-ttu-id="e1145-158">project.json</span><span class="sxs-lookup"><span data-stu-id="e1145-158">project.json</span></span>

<span data-ttu-id="e1145-159">hello project.json 파일 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-159">hello project.json file contains dependencies.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="e1145-160">run.csx</span><span class="sxs-lookup"><span data-stu-id="e1145-160">run.csx</span></span>

<span data-ttu-id="e1145-161">hello 다음 C# 코드를 보여 줍니다 여 webhook을 사용할지를 Azure 함수의 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-161">hello following C# code shows a definition of an Azure function that is a webhook.</span></span> <span data-ttu-id="e1145-162">미디어 서비스 알림에서 hello webhook 호출에 대 한 수신 하 고 hello 작업이 완료 되 면 hello 출력 자산을 게시 하는 hello 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-162">hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span> 


>[!NOTE]
><span data-ttu-id="e1145-163">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-163">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e1145-164">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="e1145-164">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e1145-165">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1145-165">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

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
                log.Info($"URL toohello manifest for client streaming using HLS protocol: {urlForClientStreaming}");
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

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy,
        DateTime.UtcNow.AddMinutes(-5));


        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                    EndsWith(".ism")).
                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
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
    /// Converts a <see cref="T:byte[]"/> tooa hex-encoded string.
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

### <a name="function-output"></a><span data-ttu-id="e1145-166">함수 출력</span><span class="sxs-lookup"><span data-stu-id="e1145-166">Function output</span></span>

<span data-ttu-id="e1145-167">위의 hello 예제 hello 다음 출력을 생성, 값이 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-167">hello example above produced hello following output, your values will vary.</span></span>

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
    
    URL toohello manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="adding-webhook-tooyour-encoding-task"></a><span data-ttu-id="e1145-168">Webhook tooyour 인코딩 태스크 추가</span><span class="sxs-lookup"><span data-stu-id="e1145-168">Adding Webhook tooyour encoding task</span></span>

<span data-ttu-id="e1145-169">이 섹션에서는 webhook 알림 tooa 작업을 추가 하는 hello 코드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-169">In this section, hello code that adds a webhook notification tooa Task is shown.</span></span> <span data-ttu-id="e1145-170">작업 수준 알림을 추가할 수도 있습니다. 그러면 연결된 태스크를 사용하여 작업에 더 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-170">You can also add a job level notification, which would be more useful for a job with chained tasks.</span></span>  

1. <span data-ttu-id="e1145-171">Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-171">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="e1145-172">Hello 이름, 위치 및 솔루션 이름을 입력 하 고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-172">Enter hello Name, Location, and Solution name, and then click OK.</span></span>
2. <span data-ttu-id="e1145-173">사용 하 여 [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall Azure 미디어 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-173">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall Azure Media Services.</span></span>
3. <span data-ttu-id="e1145-174">App.config 파일을 적절한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-174">Update App.config file with appropriate values:</span></span> 
    
    * <span data-ttu-id="e1145-175">알림을 전송하는 Azure Media Services 이름 및 키</span><span class="sxs-lookup"><span data-stu-id="e1145-175">Azure Media Services name and key that will be sending notifications,</span></span> 
    * <span data-ttu-id="e1145-176">tooget hello 알림의 가지는 webhook URL</span><span class="sxs-lookup"><span data-stu-id="e1145-176">webhook URL that expects tooget hello notifications,</span></span> 
    * <span data-ttu-id="e1145-177">서명 키 여 webhook을 가지는 hello 키와 일치 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-177">hello signing key that matches hello key that your webhook expects.</span></span> <span data-ttu-id="e1145-178">서명 키 hello는 사용 되는 tooprotect 되며 Webhook 콜백을 Azure 미디어 서비스에서 보안 된 hello 64 바이트 Base64 인코딩 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-178">hello signing key is hello 64-byte Base64 encoded value that is used tooprotect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

            <appSettings>
              <add key="MediaServicesAccountName" value="AMSAcctName" />
              <add key="MediaServicesAccountKey" value="AMSAcctKey" />
              <add key="WebhookURL" value="https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
            
4. <span data-ttu-id="e1145-179">코드 다음 hello로 Program.cs 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1145-179">Update your Program.cs file with hello following code:</span></span>

        using System;
        using System.Configuration;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace NotificationWebHook
        {
            class Program
            {
            // Read values from hello App.config file.
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

                // Used hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(new MediaServicesCredentials(
                        _mediaServicesAccountName,
                        _mediaServicesAccountKey));

                byte[] keyBytes = Convert.FromBase64String(_signingKey);

                IAsset newAsset = _context.Assets.FirstOrDefault();

                // Check for existing Notification Endpoint with hello name "FunctionWebHook"

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

                // Declare a new encoding job with hello Standard encoder
                IJob job = _context.Jobs.Create("MES Job");

                // Get a media processor reference, and pass tooit hello name of hello 
                // processor toouse for hello specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(newAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is not encrypted. 
                task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                // Add hello WebHook notification toothis Task and request all notification state changes.
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

                Console.WriteLine("Expect WebHook toobe triggered for hello Job ID: {0}", job.Id);
                Console.WriteLine("Expect WebHook toobe triggered for hello Task ID: {0}", task.Id);

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

## <a name="next-step"></a><span data-ttu-id="e1145-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1145-180">Next step</span></span>
<span data-ttu-id="e1145-181">미디어 서비스 학습 경로 검토</span><span class="sxs-lookup"><span data-stu-id="e1145-181">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e1145-182">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="e1145-182">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
