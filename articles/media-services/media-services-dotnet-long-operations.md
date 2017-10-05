---
title: "폴링 장기 실행 작업 | Microsoft 문서"
description: "이 토픽에서는 장기 실행 작업을 폴링하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="b1678-103">Azure 미디어 서비스를 사용하여 라이브 스트리밍 제공</span><span class="sxs-lookup"><span data-stu-id="b1678-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="b1678-104">개요</span><span class="sxs-lookup"><span data-stu-id="b1678-104">Overview</span></span>

<span data-ttu-id="b1678-105">Microsoft Azure 미디어 서비스는 작업(예: 채널 만들기, 시작, 중지 또는 삭제)을 시작하도록 미디어 서비스에 요청을 보내는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="b1678-106">이러한 작업은 장기 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-106">These operations are long-running.</span></span>

<span data-ttu-id="b1678-107">미디어 서비스 .NET SDK는 요청을 보내고 작업이 완료되기를 기다리는 API를 제공합니다(내부적으로 API는 일정 간격으로 작업 진행을 폴링함).</span><span class="sxs-lookup"><span data-stu-id="b1678-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="b1678-108">예를 들어 channel.Start()를 호출하면, 채널이 시작된 후 메서드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="b1678-109">비동기 버전: await channel.StartAsync()를 사용할 수도 있습니다(작업 기반 비동기 패턴에 대한 내용은 [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx) 참조).</span><span class="sxs-lookup"><span data-stu-id="b1678-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="b1678-110">작업 요청을 보낸 다음 작업이 완료될 때까지 상태에 대해 폴링하는 API를 "폴링 메서드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="b1678-111">리치 클라이언트 응용 프로그램 및/또는 상태 저장 서비스에 이 메서드 (특히 비동기 버전)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="b1678-112">응용 프로그램이 장기 실행하는 http 요청을 기다릴 수 없는 시나리오가 있으며 수동으로 작업 진행 상태를 폴링하려는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="b1678-113">전형적인 예는 상태 비저장 웹 서비스와 상호작용하는 브라우저입니다. 브라우저가 채널을 만들도록 요청하면 웹 서비스는 장기 실행 작업을 시작하고 브라우저에 작업 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="b1678-114">브라우저는 ID에 따라 작업 상태를 가져오도록 웹 서비스에 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="b1678-115">미디어 서비스 .NET SDK는 이 시나리오에 유용한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="b1678-116">이 API를 “비 폴링 메서드”라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="b1678-117">"비 폴링 메서드"에는 Send*OperationName*Operation(예: SendCreateOperation)과 같은 이름 지정 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="b1678-118">Send*OperationName*Operation 메서드는 **IOperation** 개체를 반환합니다. 반환된 개체는 작업을 추적하는 데 사용할 수 있는 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="b1678-119">Send*OperationName*OperationAsync 메서드는 **Task<IOperation>**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="b1678-120">현재 **Channel**, **StreamingEndpoint** 및 **Program** 클래스가 비 폴링 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="b1678-121">작업 상태에 대해 폴링하려면 **GetOperation** 메서드를 **OperationBaseCollection** 클래스에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="b1678-122">**Channel** 및 **StreamingEndpoint** 작업에 대한 작업 상태를 다음 간격으로 확인하려면, 30초를 사용합니다. **Program** 작업에 대해서는 10초를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b1678-123">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="b1678-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b1678-124">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="b1678-125">예제</span><span class="sxs-lookup"><span data-stu-id="b1678-125">Example</span></span>

<span data-ttu-id="b1678-126">다음 예제에서는 **ChannelOperations**라는 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="b1678-127">이 클래스 정의는 웹 서비스 클래스 정의 시작 지점이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="b1678-128">간단히 하기 위해 다음 예제에서는 메서드의 비동기 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="b1678-129">또한 이 예제에서는 클라이언트에서 이 클래스를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1678-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="b1678-130">ChannelOperations 클래스 정의</span><span class="sxs-lookup"><span data-stu-id="b1678-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
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
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
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
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
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

### <a name="the-client-code"></a><span data-ttu-id="b1678-131">The client code</span><span class="sxs-lookup"><span data-stu-id="b1678-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="b1678-132">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b1678-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b1678-133">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b1678-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

