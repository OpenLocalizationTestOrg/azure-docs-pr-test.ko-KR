---
title: ".NET SDK를 사용하여 스트리밍 끝점을 관리합니다. | Microsoft Docs"
description: "이 항목에서는 Azure 포털을 사용하여 스트리밍 끝점을 관리하는 방법을 설명합니다."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="06e32-104">.NET SDK를 사용하여 스트리밍 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="06e32-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="06e32-105">[개요](media-services-streaming-endpoints-overview.md) 항목을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="06e32-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="06e32-106">또한 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)도 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="06e32-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="06e32-107">이 항목의 코드는 Azure Media Services .NET SDK를 사용하여 다음 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="06e32-108">기본 스트리밍 끝점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="06e32-109">새 스트리밍 끝점을 만들거나 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="06e32-110">다른 CDN 및 직접 액세스를 사용하려는 경우 여러 스트리밍 끝점을 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="06e32-111">스트리밍 끝점이 실행 중인 상태일 때만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="06e32-112">스트리밍 끝점을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="06e32-113">Update() 함수를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="06e32-114">스트리밍 끝점을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="06e32-115">기본 스트리밍 끝점은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="06e32-116">스트리밍 끝점의 크기를 조정하는 방법에 대한 자세한 내용은 [이 항목](media-services-portal-scale-streaming-endpoints.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06e32-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="06e32-117">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="06e32-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="06e32-118">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="06e32-119">스트리밍 끝점을 관리하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="06e32-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="06e32-120">Program.cs의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="06e32-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06e32-121">Next steps</span></span>
<span data-ttu-id="06e32-122">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="06e32-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="06e32-123">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="06e32-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

