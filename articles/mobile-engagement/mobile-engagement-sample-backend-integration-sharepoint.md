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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement - API 통합
자동화 된 마케팅 시스템 만들기 hello도 마케팅 캠페인을 활성화 및 자동으로 발생 합니다. 이를 위해 Azure Mobile Engagement에서는 API를 사용하여 이런 자동화된 마케팅 캠페인을 만들 수 있습니다. 

일반적으로 고객의 마케팅 캠페인의 일환으로 hello Mobile Engagement 프런트 엔드 인터페이스 toocreate 알림/설문 등을 사용합니다. 마케팅 캠페인 수 발전 hello,으로 필요 하다는 있지만 캠페인 모바일에서 만듦 완전 자동화 된 파이프라인을 만들 수 있도록 tooleverage hello 데이터 (예: CRM 시스템 또는 SharePoint와 같은 CMS 시스템) hello 백 엔드 시스템에 고정 동적으로 데이터를 기반으로 hello hello 백 엔드 시스템에서 흐름에 참여 합니다. 

![][5]

이러한 시나리오를 SharePoint 비즈니스 사용자는 마케팅 데이터 인 SharePoint 목록을 채우고 hello 목록에서 항목을 선택 하 고 사용 하 여 hello Mobile Engagement 시스템으로 연결 하는 자동화 된 프로세스를 통해이 자습서 되 hello 사용할 수 있는 REST Api toocreate hello SharePoint 데이터에서 마케팅 캠페인입니다. 

> [!IMPORTANT]
> 일반적으로 어떻게 toocall 그대로 Mobile Engagement REST API에 자세히 설명 hello Api-인증 및 전달 매개 변수를 호출의 hello 두 가지 주요 측면을 이해 하기 위한 시작 지점으로이 샘플을 사용할 수 있습니다. 
> 
> 

## <a name="sharepoint-integration"></a>SharePoint 통합
1. 다음은 어떤 hello 샘플 SharePoint 목록은 같습니다. **제목**, **범주**, **NotificationTitle**, **메시지** 및 **URL** hello 알림이 만드는 데 사용 됩니다. 라는 열이 **IsProcessed** 콘솔 프로그램 hello 형태로 hello 샘플 자동화 프로세스에 의해 사용 되는 합니다. 하거나 직접 사용할 수 있습니다 hello SharePoint 워크플로 tooprogram 만들기 및 활성화 hello 알림이 hello SharePoint 목록에 항목이 삽입 될 때 하거나 예약할 수 있도록 Azure WebJob으로이 콘솔 프로그램을 실행할 수 있습니다. 이 샘플을 사용 하 여 SharePoint hello에 hello 항목을 나열 하 고 각각에 대 한 Azure Mobile Engagement에서 공지 만들기 이동한 다음 마지막 hello를 표시 하는 hello 콘솔 프로그램 **IsProcessed** 플래그 toobe true를 성공 알림 생성 합니다.
   
    ![][1]
2. Hello 코드 hello 샘플에서 사용 하 여 *hello 온라인 사용 하 여 SharePoint 클라이언트 개체 모델에서에서 원격 인증* [여기](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate hello SharePoint 목록 사용 합니다.
3. 새로 만든 항목 목록 항목 toofind hello 통해 루프를 실행 인증 되 면 (을 **IsProcessed** = false)입니다. 
   
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

## <a name="mobile-engagement-integration"></a>Mobile Engagement 통합
1. 처리를 필요로 하는 항목을 보면-필요한 hello 정보 추출할 되 면 hello에서 공지 toocreate 목록 항목 및이 호출 하는 `CreateAzMECampaign` toocreate 그 후 `ActivateAzMECampaign` tooactivate 것입니다. 이들은 기본적으로 toohello Mobile Engagement 백 엔드를 호출 하는 REST API 호출입니다. 
2. hello Mobile Engagement REST Api 필요는 **기본 인증 구성표가 HTTP 권한 부여 헤더** hello는 `ApplicationId` 및 hello `ApiKey` hello Azure 포털에서에서 얻을 합니다. Hello에서 키 hello를 사용 하 고 있는지 확인 **api 키** 섹션 및 *하지* hello에서 **sdk 키** 섹션. 
   
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
3. Hello 알림 형식을 만들기 위한 캠페인-toohello 참조 [설명서](https://msdn.microsoft.com/library/azure/mt683750.aspx)합니다. Toomake hello 캠페인을 지정 해야 할 `kind` 으로 *알림* 및 hello [페이로드](https://msdn.microsoft.com/library/azure/mt683751.aspx) FormUrlEncodedContent 서 전달 합니다. 
   
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
4. Hello hello Mobile Engagement 포털에 따라 같은 내용이 표시 됩니다 hello 알림이 생성 있으면 (해당 hello 상태 확인 = 초안 및 Activated = n/A)
   
    ![][3]
5. `CreateAzMECampaign`알림 캠페인을 만들고 해당 Id toohello 호출자를 반환 합니다. `ActivateAzMECampaign`hello 매개 변수 tooactivate hello 캠페인으로이 Id를 필요합니다. 
   
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
6. 활성화 hello 알림이 있는 hello 다음과 hello Mobile Engagement 포털에 표시 됩니다.
   
    ![][4]
7. Hello 캠페인이 활성화 되는 즉시 알림을 표시 hello 캠페인 hello 조건을 만족 하는 모든 장치 시작 됩니다. 
8. 해당 hello 목록 항목에 표시를 확인할 수도 있습니다 IsProcessed = false로 설정 된 tooTrue hello 알림 캠페인 만들어지면 합니다.  

이 샘플에는 주로 hello 필요한 속성을 지정 하는 간단한 알림 캠페인을 만들어졌습니다. 사용자 지정할 수 있습니다이 hello 정보를 사용 하 여 hello 포털에서 수 만큼 [여기](https://msdn.microsoft.com/library/azure/mt683751.aspx)합니다. 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



