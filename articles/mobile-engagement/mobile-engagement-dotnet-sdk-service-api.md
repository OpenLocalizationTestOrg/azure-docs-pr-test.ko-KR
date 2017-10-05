---
title: ".NET SDK를 사용하여 Azure Mobile Engagement 서비스 API에 액세스"
description: "Mobile Engagement .NET SDK를 사용하여 Azure Mobile Engagement 서비스 API에 액세스하는 방법을 설명합니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="2570e-103">.NET SDK를 사용하여 Azure Mobile Engagement 서비스 API에 액세스</span><span class="sxs-lookup"><span data-stu-id="2570e-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="2570e-104">장치, 도달률/푸시 캠페인 등을 관리하기 위해 Azure Mobile Engagement는 API 집합을 노출합니다. 또한 이러한 API와 상호 작용하기 위해 기본 설정 언어에 대한 SDK를 생성하는 도구와 함께 사용할 수 있는 [Swagger 파일](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="2570e-105">Swagger 파일에서 SDK를 생성하는 [AutoRest](https://github.com/Azure/AutoRest) 도구를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="2570e-106">Azure Mobile Engagement 서비스는 2018년 3월에 사용 중지되며 현재 기존 고객에게만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="2570e-107">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2570e-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="2570e-108">C# 래퍼를 사용하여 이러한 API와 상호 작용할 수 있는 유사한 방식으로 .NET SDK를 만들었으며 인증 토큰 협상을 수행하거나 새로 고칠 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="2570e-109">이 샘플에서는 .NET SDK를 사용하기 위해 일련의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="2570e-110">먼저 [여기](mobile-engagement-api-authentication.md#authentication)설명된 대로 Azure Active Directory를 사용하여 API에 대한 인증을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="2570e-111">마지막 단계에서는 유효한 **SubscriptionId**, **TenantId**, **ApplicationId** 및 **암호**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="2570e-112">간단한 Windows 콘솔 앱을 사용하여 알림 캠페인을 만드는 시나리오에서 .NET SDK를 사용하는 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="2570e-113">따라서 Visual Studio를 열고 **콘솔 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="2570e-114">다음으로 **여기** Nuget 갤러리에서 [Microsoft Azure Engagement 관리 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/)로 사용할 수 있는 .NET SDK를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="2570e-115">Visual Studio에서 Nuget을 설치하는 경우 패키지를 검색하는 동안 **시험판 포함** 옵션을 선택했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="2570e-116">`Program.cs` 파일에서 다음 네임스페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="2570e-117">다음으로 알림 캠페인을 만들 Mobile Engagement 앱을 인증하고 이 앱과 상호 작용하는 데 사용할 다음 상수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="2570e-118">Mobile Engagement SDK 메서드를 호출하는 데 사용할 `EngagementManagementClient` 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="2570e-119">`Main` 메서드에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="2570e-120">먼저 인증한 다음 알림 캠페인을 만들려는 Mobile Engagement 앱과 연결하여 `EngagementManagementClient` 를 초기화하는 다음 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="2570e-121">AppName 매개 변수에 대해 Azure 관리 포털에 정의된 **앱 리소스 이름**을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="2570e-122">마지막으로 제목 및 메시지로 간단한 **항상** & **알림 전용** 캠페인을 만들기 위해 이전에 초기화된 EngagementClient를 사용하는 CreateCampaign 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="2570e-123">콘솔 앱을 실행하면 캠페인이 성공적으로 만들어지고 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2570e-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="2570e-124">**캠페인 ID '159'가 성공적으로 만들어졌으며 '초안' 상태입니다**</span><span class="sxs-lookup"><span data-stu-id="2570e-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
