---
title: "Mobile Engagement-백 엔드 통합 aaaAzure"
description: "SharePoint에서 SharePoint 백 엔드 toocreate 캠페인을 사용 하 여 Azure Mobile Engagement 연결"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="442f3-103">Azure Mobile Engagement - API 통합</span><span class="sxs-lookup"><span data-stu-id="442f3-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="442f3-104">자동화 된 마케팅 시스템 만들기 hello도 마케팅 캠페인을 활성화 및 자동으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="442f3-105">이를 위해 Azure Mobile Engagement에서는 API를 사용하여 이런 자동화된 마케팅 캠페인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="442f3-106">일반적으로 고객의 마케팅 캠페인의 일환으로 hello Mobile Engagement 프런트 엔드 인터페이스 toocreate 알림/설문 등을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="442f3-107">마케팅 캠페인 수 발전 hello,으로 필요 하다는 있지만 캠페인 모바일에서 만듦 완전 자동화 된 파이프라인을 만들 수 있도록 tooleverage hello 데이터 (예: CRM 시스템 또는 SharePoint와 같은 CMS 시스템) hello 백 엔드 시스템에 고정 동적으로 데이터를 기반으로 hello hello 백 엔드 시스템에서 흐름에 참여 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="442f3-108">이러한 시나리오를 SharePoint 비즈니스 사용자는 마케팅 데이터 인 SharePoint 목록을 채우고 hello 목록에서 항목을 선택 하 고 사용 하 여 hello Mobile Engagement 시스템으로 연결 하는 자동화 된 프로세스를 통해이 자습서 되 hello 사용할 수 있는 REST Api toocreate hello SharePoint 데이터에서 마케팅 캠페인입니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="442f3-109">일반적으로 어떻게 toocall 그대로 Mobile Engagement REST API에 자세히 설명 hello Api-인증 및 전달 매개 변수를 호출의 hello 두 가지 주요 측면을 이해 하기 위한 시작 지점으로이 샘플을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="442f3-110">SharePoint 통합</span><span class="sxs-lookup"><span data-stu-id="442f3-110">SharePoint integration</span></span>
1. <span data-ttu-id="442f3-111">다음은 어떤 hello 샘플 SharePoint 목록은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="442f3-112">**제목**, **범주**, **NotificationTitle**, **메시지** 및 **URL** hello 알림이 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="442f3-113">라는 열이 **IsProcessed** 콘솔 프로그램 hello 형태로 hello 샘플 자동화 프로세스에 의해 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="442f3-114">하거나 직접 사용할 수 있습니다 hello SharePoint 워크플로 tooprogram 만들기 및 활성화 hello 알림이 hello SharePoint 목록에 항목이 삽입 될 때 하거나 예약할 수 있도록 Azure WebJob으로이 콘솔 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="442f3-115">이 샘플을 사용 하 여 SharePoint hello에 hello 항목을 나열 하 고 각각에 대 한 Azure Mobile Engagement에서 공지 만들기 이동한 다음 마지막 hello를 표시 하는 hello 콘솔 프로그램 **IsProcessed** 플래그 toobe true를 성공 알림 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="442f3-116">Hello 코드 hello 샘플에서 사용 하 여 *hello 온라인 사용 하 여 SharePoint 클라이언트 개체 모델에서에서 원격 인증* [여기](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate hello SharePoint 목록 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="442f3-117">새로 만든 항목 목록 항목 toofind hello 통해 루프를 실행 인증 되 면 (을 **IsProcessed** = false)입니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="442f3-118">Mobile Engagement 통합</span><span class="sxs-lookup"><span data-stu-id="442f3-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="442f3-119">처리를 필요로 하는 항목을 보면-필요한 hello 정보 추출할 되 면 hello에서 공지 toocreate 목록 항목 및이 호출 하는 `CreateAzMECampaign` toocreate 그 후 `ActivateAzMECampaign` tooactivate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="442f3-120">이들은 기본적으로 toohello Mobile Engagement 백 엔드를 호출 하는 REST API 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="442f3-121">hello Mobile Engagement REST Api 필요는 **기본 인증 구성표가 HTTP 권한 부여 헤더** hello는 `ApplicationId` 및 hello `ApiKey` hello Azure 포털에서에서 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="442f3-122">Hello에서 키 hello를 사용 하 고 있는지 확인 **api 키** 섹션 및 *하지* hello에서 **sdk 키** 섹션.</span><span class="sxs-lookup"><span data-stu-id="442f3-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="442f3-123">Hello 알림 형식을 만들기 위한 캠페인-toohello 참조 [설명서](https://msdn.microsoft.com/library/azure/mt683750.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="442f3-124">Toomake hello 캠페인을 지정 해야 할 `kind` 으로 *알림* 및 hello [페이로드](https://msdn.microsoft.com/library/azure/mt683751.aspx) FormUrlEncodedContent 서 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="442f3-125">Hello hello Mobile Engagement 포털에 따라 같은 내용이 표시 됩니다 hello 알림이 생성 있으면 (해당 hello 상태 확인 = 초안 및 Activated = n/A)</span><span class="sxs-lookup"><span data-stu-id="442f3-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="442f3-126">`CreateAzMECampaign`알림 캠페인을 만들고 해당 Id toohello 호출자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="442f3-127">`ActivateAzMECampaign`hello 매개 변수 tooactivate hello 캠페인으로이 Id를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="442f3-128">활성화 hello 알림이 있는 hello 다음과 hello Mobile Engagement 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="442f3-129">Hello 캠페인이 활성화 되는 즉시 알림을 표시 hello 캠페인 hello 조건을 만족 하는 모든 장치 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="442f3-130">해당 hello 목록 항목에 표시를 확인할 수도 있습니다 IsProcessed = false로 설정 된 tooTrue hello 알림 캠페인 만들어지면 합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="442f3-131">이 샘플에는 주로 hello 필요한 속성을 지정 하는 간단한 알림 캠페인을 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="442f3-132">사용자 지정할 수 있습니다이 hello 정보를 사용 하 여 hello 포털에서 수 만큼 [여기](https://msdn.microsoft.com/library/azure/mt683751.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="442f3-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



