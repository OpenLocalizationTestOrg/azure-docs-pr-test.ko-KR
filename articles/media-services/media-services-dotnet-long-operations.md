---
title: "장기 실행 작업 aaaPolling | Microsoft Docs"
description: "이 항목에서는 방법을 toopoll 장기 실행 작업입니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a>Azure 미디어 서비스를 사용하여 라이브 스트리밍 제공

## <a name="overview"></a>개요

Microsoft Azure 미디어 서비스는 요청을 보내는 tooMedia Services toostart 작업 (예: 만들기, 시작, 중지 또는 채널을 삭제) 합니다. 이러한 작업은 장기 실행됩니다.

미디어 서비스.NET SDK hello hello 요청을 보내고 hello 작업 toocomplete (내부적으로 Api는 일정 간격 작업 진행률에 대 한 폴링 hello) 때까지 대기 하는 Api를 제공 합니다. 예를 들어, 채널을 호출 하는 경우. Start (), hello 메서드 hello 채널 시작 된 후 반환 합니다. Hello 비동기 버전을 사용할 수 있습니다: 채널을 기다립니다. StartAsync() (작업 기반 비동기 패턴에 대 한 정보를 참조 하십시오. [탭](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). 작업 요청을 보내고 hello 작업이 완료 될 때까지 다음 hello 상태에 대해 폴링하는 Api는 "폴링 메서드" 라고 합니다. 리치 클라이언트 응용 프로그램 및/또는 상태 저장 서비스에 대 한 이러한 메서드 (특히 hello 비동기 버전)를 사용 하는 것이 좋습니다.

하는 경우 응용 프로그램에서 장기 실행 http 요청을 기다릴 수 없는 수동으로 hello 작업 진행률에 대 한 toopoll가 있습니다. 일반적인 예로 상태 비저장 웹 서비스와 상호 작용 하는 브라우저 수: hello 브라우저 요청 toocreate 채널, hello 웹 서비스는 장기 실행 작업을 시작 하 고, 작업 ID toohello 브라우저를 hello 반환 합니다. hello 브라우저 hello 웹 서비스 tooget hello 작업 상태 hello ID를 기반 요청할 수 있습니다. 미디어 서비스.NET SDK hello이이 시나리오에 유용한 Api를 제공 합니다. 이 API를 “비 폴링 메서드”라고 합니다.
hello "비 폴링 메서드"가 명명 패턴을 따르는 hello: 보내기*OperationName*작업 (예를 들어 SendCreateOperation). 보내기*OperationName*hello를 반환 하는 작업 메서드가 **IOperation** ; hello 반환 된 개체 정보를 포함 사용된 tootrack hello 작업이 될 수 있는 개체입니다. hello 송신*OperationName*OperationAsync 메서드 반환 **작업<IOperation>**합니다.

현재 클래스 지원 비 폴링 메서드를 다음 hello: **채널**, **StreamingEndpoint**, 및 **프로그램**합니다.

hello 작업 상태를 사용 하 여 hello toopoll **GetOperation** 메서드 hello **OperationBaseCollection** 클래스입니다. 다음 간격 toocheck hello operationstatus hello를 사용 하 여:에 대 한 **채널** 및 **StreamingEndpoint** 작업을 사용 하 여 30 초;에 대 한 **프로그램** 10을 사용 하는 작업 시간 (초)입니다.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.

## <a name="example"></a>예제

hello 다음 예제에서는 클래스를 정의 **ChannelOperations**합니다. 이 클래스 정의는 웹 서비스 클래스 정의 시작 지점이 될 수 있습니다. 간단한 설명을 위해 hello 다음 예제에서는 메서드의 hello 비동기 버전입니다.

hello 예제에는 hello 클라이언트는이 클래스 사용 방법을 보여 줍니다.

### <a name="channeloperations-class-definition"></a>ChannelOperations 클래스 정의

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
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

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a>hello 클라이언트 코드
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

