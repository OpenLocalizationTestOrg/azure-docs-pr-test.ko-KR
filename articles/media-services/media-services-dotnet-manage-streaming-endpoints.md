---
title: "스트리밍 끝점.NET SDK와 aaaManage 합니다. | Microsoft Docs"
description: "이 항목에서는 toomanage 스트리밍 끝점이 Azure 포털 hello 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="e25b7-104">.NET SDK를 사용하여 스트리밍 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="e25b7-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="e25b7-105">있는지 tooreview hello 확인 [개요](media-services-streaming-endpoints-overview.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="e25b7-106">또한 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)도 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="e25b7-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="e25b7-107">이 항목의 hello 코드 toodo hello를 사용 하 여 작업을 다음 Azure 미디어 서비스.NET SDK hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="e25b7-108">Hello 기본 스트리밍 끝점을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="e25b7-109">새 스트리밍 끝점을 만들거나 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="e25b7-110">할 수 있습니다 toohave 여러 개의 스트리밍 끝점이 toohave 하려는 경우 다른 Cdn 또는 CDN 및 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e25b7-111">스트리밍 끝점이 실행 중인 상태일 때만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="e25b7-112">Hello 스트리밍 끝점을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="e25b7-113">있는지 toocall hello update () 함수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="e25b7-114">Hello 스트리밍 끝점을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e25b7-115">hello 기본 스트리밍 끝점을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="e25b7-116">어떻게 tooscale hello 스트리밍 끝점에 대 한 정보를 참조 하십시오. [이](media-services-portal-scale-streaming-endpoints.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e25b7-117">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="e25b7-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e25b7-118">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="e25b7-119">스트리밍 끝점을 관리하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="e25b7-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="e25b7-120">코드 다음 hello hello Program.cs의에서 hello 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
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


## <a name="next-steps"></a><span data-ttu-id="e25b7-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e25b7-121">Next steps</span></span>
<span data-ttu-id="e25b7-122">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e25b7-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e25b7-123">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="e25b7-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

