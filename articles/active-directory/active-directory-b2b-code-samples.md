---
title: "aaaAzure Active Directory B2B 공동 작업 코드 및 PowerShell 샘플 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업을 위한 코드 및 PowerShell 샘플"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 8e4f66fcb50d190899304831ea7ccd2203c5468c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a>Azure Active Directory B2B 공동 작업 코드 및 PowerShell 샘플

## <a name="powershell-example"></a>PowerShell 예제
있습니다 수 대량-초대에 저장 된 전자 메일 주소에서 tooan 조직 외부 사용자가 합니다. CSV 파일입니다.

1. Hello를 준비 합니다. CSV 파일 새로운 CSV 파일을 만들기 및 invitations.csv 라는 이름을 지정 합니다. 이 예제에서는 hello 파일 C:\data에 저장 되 고 hello 다음 정보를 포함 합니다.
  
  이름                  |  InvitedUserEmailAddress
  --------------------- | --------------------------
  Gmail B2B 초대 대상자     | b2binvitee@gmail.com
  Outlook B2B 초대 대상자   | b2binvitee@outlook.com


2. 최신 Azure AD PowerShell toouse hello 가져오기 hello 새로운 cmdlet에서 다운로드할 수 있는 업데이트 hello Azure AD PowerShell 모듈을 설치 해야 [hello Powershell 모듈의 릴리스 페이지](https://www.powershellgallery.com/packages/AzureADPreview)

3. Tooyour 테 넌 트에 로그인

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. Hello PowerShell cmdlet을 실행

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

이 cmdlet invitations.csv에 초대 toohello 전자 메일 주소를 보냅니다. 이 cmdlet의 추가 기능은 다음과 같습니다.
- Hello 전자 메일 메시지에 사용자 지정 된 텍스트
- 사용자 초대 hello에 대 한 표시 이름을 포함 하 여
- 메시지 tooCCs 보내거나 완전히 전자 메일 메시지를 표시 하지 않음

## <a name="code-sample"></a>코드 샘플
여기서 "응용 프로그램 전용" 모드로 toocall hello 초대 API, 초대할 hello 리소스 toowhich tooget hello 상환 URL B2B 사용자 hello 방법을 설명 합니다. hello 목표는 사용자 지정 초대 메일 toosend입니다. hello 전자 메일 모양을 사용자 지정할 수 있으며 Graph API를 통해 메시지를 보낼 수 있도록 HTTP 클라이언트를 구성할 수 있습니다.

```
namespace SampleInviteApp
{
    using System;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    class Program
    {
        /// <summary>
        /// Microsoft graph resource.
        /// </summary>
        static readonly string GraphResource = "https://graph.microsoft.com";
 
        /// <summary>
        /// Microsoft graph invite endpoint.
        /// </summary>
        static readonly string InviteEndPoint = "https://graph.microsoft.com/v1.0/invitations";
 
        /// <summary>
        ///  Authentication endpoint tooget token.
        /// </summary>
        static readonly string EstsLoginEndpoint = "https://login.microsoftonline.com";
 
        /// <summary>
        /// This is hello tenantid of hello tenant you want tooinvite users to.
        /// </summary>
        private static readonly string TenantID = "";
 
        /// <summary>
        /// This is hello application id of hello application that is registered in hello above tenant.
        /// hello required scopes are available in hello below link.
        /// https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/invitation_post
        /// </summary>
        private static readonly string TestAppClientId = "";
 
        /// <summary>
        /// Client secret of hello application.
        /// </summary>
        private static readonly string TestAppClientSecret = @"
 
        /// <summary>
        /// This is hello email address of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserEmailAddress = @"";
 
        /// <summary>
        /// This is hello display name of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserDisplayName = @"";
 
        /// <summary>
        /// Main method.
        /// </summary>
        /// <param name="args">Optional arguments</param>
        static void Main(string[] args)
        {
            Invitation invitation = CreateInvitation();
            SendInvitation(invitation);
        }
 
        /// <summary>
        /// Create hello invitation object.
        /// </summary>
        /// <returns>Returns hello invitation object.</returns>
        private static Invitation CreateInvitation()
        {
            // Set hello invitation object.
            Invitation invitation = new Invitation();
            invitation.InvitedUserDisplayName = InvitedUserDisplayName;
            invitation.InvitedUserEmailAddress = InvitedUserEmailAddress;
            invitation.InviteRedirectUrl = "https://www.microsoft.com";
            invitation.SendInvitationMessage = true;
            return invitation;
        }
 
        /// <summary>
        /// Send hello guest user invite request.
        /// </summary>
        /// <param name="invitation">Invitation object.</param>
        private static void SendInvitation(Invitation invitation)
        {
            string accessToken = GetAccessToken();
 
            HttpClient httpClient = GetHttpClient(accessToken);
 
            // Make hello invite call. 
            HttpContent content = new StringContent(JsonConvert.SerializeObject(invitation));
            content.Headers.Add("ContentType", "application/json");
            var postResponse = httpClient.PostAsync(InviteEndPoint, content).Result;
            string serverResponse = postResponse.Content.ReadAsStringAsync().Result;
            Console.WriteLine(serverResponse);
        }
 
        /// <summary>
        /// Get hello HTTP client.
        /// </summary>
        /// <param name="accessToken">Access token</param>
        /// <returns>Returns hello Http Client.</returns>
        private static HttpClient GetHttpClient(string accessToken)
        {
            // setup http client.
            HttpClient httpClient = new HttpClient();
            httpClient.Timeout = TimeSpan.FromSeconds(300);
            httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
            httpClient.DefaultRequestHeaders.Add("client-request-id", Guid.NewGuid().ToString());
            Console.WriteLine(
                "CorrelationID for hello request: {0}",
                httpClient.DefaultRequestHeaders.GetValues("client-request-id").Single());
            return httpClient;
        }
 
        /// <summary>
        /// Get hello access token for our application tootalk toomicrosoft graph.
        /// </summary>
        /// <returns>Returns hello access token for our application tootalk toomicrosoft graph.</returns>
        private static string GetAccessToken()
        {
            string accessToken = null;
 
            // Get hello access token for our application tootalk toomicrosoft graph.
            try
            {
                AuthenticationContext testAuthContext =
                    new AuthenticationContext(string.Format("{0}/{1}", EstsLoginEndpoint, TenantID));
                AuthenticationResult testAuthResult = testAuthContext.AcquireTokenAsync(
                    GraphResource,
                    new ClientCredential(TestAppClientId, TestAppClientSecret)).Result;
                accessToken = testAuthResult.AccessToken;
            }
            catch (AdalException ex)
            {
                Console.WriteLine("An exception was thrown while fetching hello token: {0}.", ex);
                throw;
            }
 
            return accessToken;
        }
 
        /// <summary>
        /// Invitation class.
        /// </summary>
        public class Invitation
        {
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserDisplayName { get; set; }
 
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserEmailAddress { get; set; }
 
            /// <summary>
            /// Gets or sets a value indicating whether Invitation Manager should send hello email tooInvitedUser.
            /// </summary>
            public bool SendInvitationMessage { get; set; }
 
            /// <summary>
            /// Gets or sets invitation redirect URL
            /// </summary>
            public string InviteRedirectUrl { get; set; }
        }
    }
}
```


## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업용 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
