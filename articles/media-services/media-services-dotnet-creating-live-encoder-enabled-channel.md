---
title: "aaaHow tooperform 라이브 스트리밍을 toocreate 다중 비트 전송률 스트림을 Azure 미디어 서비스를 사용 하 여.net | Microsoft Docs"
description: "이 자습서에서는 단일 비트 전송률 라이브 스트림을 수신 채널을 만드는 단계 hello 및.NET SDK를 사용 하 여 toomulti 비트 전송률 스트림으로 인코딩합니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a>.NET 어떻게 스트리밍하 tooperform 라이브 스트리밍을 Azure 미디어 서비스 toocreate 다중 비트 전송률을 사용 하 여
> [!div class="op_single_selector"]
> * [포털](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요.
> 
> 

## <a name="overview"></a>개요
이 자습서에서는 hello 만드는 단계는 **채널** 단일 비트 전송률 라이브 스트림을 수신 하 고 toomulti 비트 전송률 스트림으로 인코딩합니다.

자세한 개념 정보에 대 한 라이브 인코딩이 관련된 tooChannels 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.

## <a name="common-live-streaming-scenario"></a>일반적인 라이브 스트리밍 시나리오
단계를 수행 하는 hello 일반적인 라이브 스트리밍 응용 프로그램 만들기와 관련 된 작업에 설명 합니다.

> [!NOTE]
> 현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다. 오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.
> 
> 

1. 비디오 카메라 tooa 컴퓨터에 연결 합니다. 시작 하 고 hello 다음 프로토콜 중 하나에 단일 비트 전송률 스트림을 출력 하는 온-프레미스 라이브 인코더 구성: RTMP, 부드러운 스트리밍 또는 RTP (MPEG-TS). 자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.

    이 단계는 채널을 만든 후에도 수행할 수 있습니다.

2. 채널을 만들고 시작합니다.
3. 검색 hello 채널 수집 URL입니다.

    hello 수집 URL hello 라이브 인코더 toosend hello 스트림 toohello 채널에서 사용 됩니다.

4. Hello 채널 미리 보기 URL을 검색 합니다.

    이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.

5. 자산을 만듭니다.
6. Hello 자산 toobe 재생 하는 동안 동적으로 암호화에 사용할 경우 다음 hello지 않습니다.
7. 콘텐츠 키를 만듭니다.
8. Hello 콘텐츠 키 권한 부여 정책을 구성 합니다.
9. 자산 배달 정책(동적 패키징 및 동적 암호화에서 사용)을 구성합니다.
10. 프로그램을 만들고 만든 toouse hello 자산을 지정 합니다.
11. OnDemand 로케이터를 만들어 hello 프로그램과 연결 된 hello 자산을 게시 합니다.

    >[!NOTE]
    >AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 대 한 toobe **실행** 상태입니다. 

12. 스트리밍 및 보관 준비 toostart 있을 때는 hello 프로그램을 시작 합니다.
13. 필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다. hello 광고 hello 출력 스트림에 삽입 됩니다.
14. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다.
15. Hello 프로그램을 삭제 합니다 (한 필요에 따라 hello 자산을 삭제) 합니다.

## <a name="what-youll-learn"></a>학습할 내용
이 항목에서는 채널 및 미디어 서비스.NET SDK를 사용 하 여 프로그램에 대 한 tooexecute 다른 작업입니다. 많은 작업이 오래 실행되기 때문에 오래 실행되는 작업을 관리하는 .NET API가 사용됩니다.

항목에서는 hello 방법을 toodo hello 다음:

1. 채널을 만들고 시작합니다. 오래 실행되는 API가 사용됩니다.
2. 가져오기 hello 채널 수집 (입력된) 끝점입니다. 이 끝점은 단일 비트 전송률 라이브 스트림을 보낼 수 있는 toohello 인코더를 제공 되어야 합니다.
3. Hello 미리 보기 끝점을 가져옵니다. 이 끝점은 사용 되는 toopreview 스트림을 합니다.
4. 콘텐츠 사용된 toostore 될 자산을 만듭니다. hello 자산 배달 정책은이 예제에 표시 된 대로 구성 되어야 합니다.
5. 프로그램을 만들고 이전에 생성 된 toouse hello 자산을 지정 합니다. Hello 프로그램을 시작 합니다. 오래 실행되는 API가 사용됩니다.
6. Hello 콘텐츠에 게시할 tooyour 클라이언트 스트리밍할 수 있도록 hello 자산에 대 한 로케이터를 만듭니다.
7. 슬레이트를 표시하고 숨깁니다. 광고를 시작하고 중지합니다. 오래 실행되는 API가 사용됩니다.
8. 채널을 정리 하 고 모든 관련된 리소스를 hello 합니다.

## <a name="prerequisites"></a>필수 조건
필요한 toocomplete hello 자습서는 hello 다음과가 같습니다.

* Azure 계정. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요. Azure 서비스를 유료 아웃 사용된 tootry 일 수 있는 크레딧을 얻게. Hello 크레딧을 모두 사용 된 후에 hello 계정을 보관 하 고 사용 가능한 Azure 서비스 및 Azure 앱 서비스의 hello 웹 응용 프로그램 기능 등의 기능을 사용 합니다.
* Media Services 계정. 미디어 서비스 계정 toocreate 참조 [계정 만들기](media-services-portal-create-account.md)합니다.
* Visual Studio 2010 SP1(Professional, Premium, Ultimate 또는 Express) 이상 버전.
* 미디어 서비스 .NET SDK 버전 3.2.0.0 이상을 사용해야 합니다.
* 단일 비트 전송률 라이브 스트림을 보낼 수 있는 웹캠 및 인코더.

## <a name="considerations"></a>고려 사항
* 현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다. 오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.
* 다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

## <a name="download-sample"></a>샘플 다운로드

이 항목에 설명 된 hello 샘플을 다운로드할 수 [여기](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)합니다.

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a>.NET용 미디어 서비스 SDK를 사용한 개발을 위한 설정

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

## <a name="code-example"></a>코드 예제

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

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

            IChannel channel = CreateAndStartChannel();

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


