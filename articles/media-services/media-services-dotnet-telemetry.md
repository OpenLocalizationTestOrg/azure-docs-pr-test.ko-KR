---
title: ".NET과 함께 Azure 미디어 서비스 원격 분석 aaaConfiguring | Microsoft Docs"
description: "이 문서 toouse.NET SDK를 사용 하 여 Azure 미디어 서비스 원격 분석을 hello 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 4019fa7d080ca3f8a8709bd1e666f7062b883954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="22479-103">.NET을 사용하여 Azure Media Services 원격 분석 구성</span><span class="sxs-lookup"><span data-stu-id="22479-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="22479-104">이 항목에서는.NET SDK를 사용 하 여 hello Azure 미디어 서비스 (AMS) 원격 분석을 구성할 때 사용할 수 있는 일반적인 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22479-104">This topic describes general steps that you might take when configuring hello Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="22479-105">방식에 대 한 hello 기능에 대해 상세히 AMS 원격 분석 및 tooconsume, hello 참조 [개요](media-services-telemetry-overview.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="22479-105">For hello detailed explanation of what is AMS telemetry and how tooconsume it, see hello [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="22479-106">Hello 같은 방법으로 다음 중 하나에 대 한 원격 분석 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22479-106">You can consume telemetry data in one of hello following ways:</span></span>

- <span data-ttu-id="22479-107">Azure 테이블 저장소 (예: hello 저장소 SDK 사용)에서 직접 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="22479-107">Read data directly from Azure Table Storage (e.g. using hello Storage SDK).</span></span> <span data-ttu-id="22479-108">원격 분석 저장소 테이블의 hello 설명 hello 참조 **원격 분석 정보를 사용해** 에 [이](https://msdn.microsoft.com/library/mt742089.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="22479-108">For hello description of telemetry storage tables, see hello **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="22479-109">또는</span><span class="sxs-lookup"><span data-stu-id="22479-109">Or</span></span>

- <span data-ttu-id="22479-110">저장소 데이터를 읽기 위한 hello 미디어 서비스.NET SDK에서에서 사용 하 여 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="22479-110">Use hello support in hello Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="22479-111">이 항목에서는 방법을 사용 하 여 tooquery hello 메트릭을 hello Azure 미디어 서비스.NET SDK 및 hello에 대 한 원격 분석 tooenable AMS 계정을 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22479-111">This topic shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="22479-112">미디어 서비스 계정에 대해 원격 분석 구성</span><span class="sxs-lookup"><span data-stu-id="22479-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="22479-113">hello 다음 단계는 필요한 tooenable 원격 분석.</span><span class="sxs-lookup"><span data-stu-id="22479-113">hello following steps are needed tooenable telemetry:</span></span>

- <span data-ttu-id="22479-114">Hello hello 저장소 계정 연결 toohello 미디어 서비스 계정 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22479-114">Get hello credentials of hello storage account attached toohello Media Services account.</span></span> 
- <span data-ttu-id="22479-115">알림 끝점을 만들 **이 나와** 도**AzureTable** 및 endPointAddress 가리키는 toohello 저장소 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="22479-115">Create a Notification Endpoint with **EndPointType** set too**AzureTable** and endPointAddress pointing toohello storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="22479-116">Hello 서비스에 대 한 모니터링 구성 설정 만들기 toomonitor 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="22479-116">Create a monitoring configuration settings for hello services you want toomonitor.</span></span> <span data-ttu-id="22479-117">한 개 이하의 모니터링 구성 설정이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22479-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="22479-118">이</span><span class="sxs-lookup"><span data-stu-id="22479-118">Consuming telemetry information</span></span>

<span data-ttu-id="22479-119">원격 분석 정보 사용에 대한 자세한 내용은 [이](media-services-telemetry-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22479-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="22479-120">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="22479-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="22479-121">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22479-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="22479-122">요소 다음에 오는 너무 hello 추가**appSettings** app.config 파일에 정의 된:</span><span class="sxs-lookup"><span data-stu-id="22479-122">Add hello following element too**appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="22479-123">예제</span><span class="sxs-lookup"><span data-stu-id="22479-123">Example</span></span>  
    
<span data-ttu-id="22479-124">다음 예제는 hello에 hello에 대 한 원격 분석 tooenable AMS 계정을 지정 하는 방법 및 tooquery hello 메트릭을 사용 하 여 Azure 미디어 서비스.NET SDK hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22479-124">hello following example shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print hello channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="22479-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22479-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="22479-126">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="22479-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
