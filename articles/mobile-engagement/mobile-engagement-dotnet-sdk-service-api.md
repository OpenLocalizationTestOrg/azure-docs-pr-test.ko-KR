---
title: "aaaUsing.NET SDK tooaccess Azure Mobile Engagement 서비스 Api"
description: "Toouse Mobile Engagement.NET SDK tooaccess Azure Mobile Engagement 서비스 Api hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="f0578-103">.NET SDK tooaccess Azure Mobile Engagement 서비스 Api를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f0578-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="f0578-104">집합을 노출 하는 azure Mobile Engagement toomanage 장치 수, Api의 도달 범위/푸시 캠페인 등 toointeract 이러한 Api와,도 제공 하는 [Swagger 파일](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) 사용자 기본 설정에 대 한 toogenerate Sdk 도구를 사용할 수 있습니다 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="f0578-105">Hello를 사용 하는 것이 좋습니다 [AutoRest](https://github.com/Azure/AutoRest) toogenerate 쿼리하여 Swagger 파일에서 SDK 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="f0578-106">hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="f0578-107">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0578-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="f0578-108">수 있는 toointeract 이러한 Api와 C# 래퍼를 사용 하 여 비슷한 방식으로.NET SDK 만들어져 및 toodo hello 인증 토큰 협상 하 고 사용자가 직접를 새로 고칠 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="f0578-109">이 샘플 hello 집합이 단계 toofollow toouse hello.NET SDK을 통해 처리.</span><span class="sxs-lookup"><span data-stu-id="f0578-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="f0578-110">Api를 사용 하 여 설명 된 대로 Azure Active Directory hello에 대 한 toosetup hello 인증 필요 우선, [여기](mobile-engagement-api-authentication.md#authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="f0578-111">이러한 단계의 hello 끝은 유효한 있어야 **SubscriptionId**, **TenantId**, **ApplicationId** 및 **비밀**합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="f0578-112">알림 캠페인을 만드는의 hello 시나리오와 hello.NET SDK를 사용 하는 간단한 Windows 콘솔 앱 toodemonstrate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="f0578-113">따라서 Visual Studio를 열고 **콘솔 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="f0578-114">다음으로 사용할 수 있는.NET SDK toodownload hello 해야 **Microsoft Azure 서비스 관리 라이브러리** hello Nuget 갤러리에서 [여기](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="f0578-115">확인 표시가 hello 있는지 tooensure Visual Studio에서 Nuget hello를 설치 하는 경우 필요한 **Include 시험판** hello 패키지에 대 한 검색 하는 동안 옵션:</span><span class="sxs-lookup"><span data-stu-id="f0578-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="f0578-116">Hello에 `Program.cs` 파일, 네임 스페이스 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="f0578-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="f0578-117">다음 toodefine hello 인증에 사용할 상수를 따르고 hello 알림 캠페인 만들려는 hello Mobile Engagement 앱과 상호 작용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="f0578-118">Hello 정의 `EngagementManagementClient` 변수를 사용 하 여 toocall hello Mobile Engagement SDK 메서드:</span><span class="sxs-lookup"><span data-stu-id="f0578-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="f0578-119">Hello tooyour 다음 추가 `Main` 메서드:</span><span class="sxs-lookup"><span data-stu-id="f0578-119">Add hello following tooyour `Main` method:</span></span>
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="f0578-120">Hello hello를 초기화 하는 메서드를 다음 정의 `EngagementManagementClient` 먼저 인증 하 고 다음 toocreate hello 알림 캠페인을 계획 하는 hello Mobile Engagement 앱 자체 연결 하 여:</span><span class="sxs-lookup"><span data-stu-id="f0578-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="f0578-121">Toouse hello 해야 하는 참고 **응용 프로그램 리소스 이름** hello 응용 프로그램 이름 매개 변수에 대 한 hello Azure 관리 포털에 정의 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0578-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="f0578-122">마지막으로, 하므로 이전에 초기화 hello EngagementClient toocreate 간단한을 사용 하 여 hello CreateCampaign 메서드를 정의 **언제 든 지** & **알림 전용** 캠페인 제목 및 메시지:</span><span class="sxs-lookup"><span data-stu-id="f0578-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="f0578-123">콘솔 응용 프로그램 실행된 hello 볼 수 있습니다 hello 다음 hello 캠페인을 성공적으로 만들기에서:</span><span class="sxs-lookup"><span data-stu-id="f0578-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="f0578-124">**캠페인 ID '159'가 성공적으로 만들어졌으며 '초안' 상태입니다**</span><span class="sxs-lookup"><span data-stu-id="f0578-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
