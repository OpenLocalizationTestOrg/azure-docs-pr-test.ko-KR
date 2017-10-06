---
title: "C#을 사용 하 여 Azure 시간 계열 Insights 환경에 의해 hello aaaQuery 데이터로 | Microsoft Docs"
description: "이 자습서에서는 tooquery 데이터를 C# 예제 코드와 함께 사용 하는 시간 시계열 Insights 환경은 hello 하는 방법을 설명 합니다."
keywords: 
services: tsi
documentationcenter: 
author: ankryach
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: ankryach
ms.openlocfilehash: 0ddec36b7f275f6de279948193e45f045d30b644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-data-from-hello-azure-time-series-insights-environment-using-c"></a><span data-ttu-id="51b20-103">C#을 사용 하 여 hello Azure 시간 계열 Insights 환경에서 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-103">Query data from hello Azure Time Series Insights environment using C#</span></span>

<span data-ttu-id="51b20-104">C# 예제 tooquery 데이터를 Azure 시간 계열 Insights 환경 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-104">This C# example demonstrates how tooquery data from hello Azure Time Series Insights environment.</span></span>
<span data-ttu-id="51b20-105">hello 예제 쿼리 API 사용법의 몇 가지 기본적인 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-105">hello sample shows several basic examples of Query API usage:</span></span>
1. <span data-ttu-id="51b20-106">준비 단계로 hello Azure Active Directory API를 통해 hello 액세스 토큰을 확보 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-106">As a preparation step, acquire hello access token through hello Azure Active Directory API.</span></span> <span data-ttu-id="51b20-107">이 토큰을 hello에 전달할 `Authorization` 모든 쿼리 API 요청의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-107">Pass this token in hello `Authorization` header of every Query API request.</span></span> <span data-ttu-id="51b20-108">비대화형 응용 프로그램을 설정하려면 [인증 및 권한 부여](time-series-insights-authentication-and-authorization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51b20-108">For setting up non-interactive applications, see [Authentication and authorization](time-series-insights-authentication-and-authorization.md).</span></span> <span data-ttu-id="51b20-109">Hello 샘플 hello 맨 앞에 정의 된 모든 hello 상수 올바르게 설정 되었는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="51b20-109">Also, ensure all hello constants defined at hello beginning of hello sample are correctly set.</span></span>
2. <span data-ttu-id="51b20-110">hello 사용자 환경의 hello 목록에는 액세스 toois 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-110">hello list of environments that hello user has access toois obtained.</span></span> <span data-ttu-id="51b20-111">Hello 환경 중 하나는 선택 관심 있는 hello 환경으로 및이 환경에 대 한 데이터를 쿼리 하는 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-111">One of hello environments is picked up as hello environment of interest, and further data is queried for this environment.</span></span>
3. <span data-ttu-id="51b20-112">가용성 데이터는 HTTPS 요청에의 한 예로 관심 있는 hello 환경에 대 한 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-112">As an example of HTTPS request, availability data is requested for hello environment of interest.</span></span>
4. <span data-ttu-id="51b20-113">웹 소켓 요청이의 예를 들어 이벤트 집계 데이터는 관심 있는 hello 환경에 대 한 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-113">As an example of web socket request, event aggregates data is requested for hello environment of interest.</span></span> <span data-ttu-id="51b20-114">Hello 전체 가용성 시간 범위에 대 한 데이터 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51b20-114">Data is requested for hello whole availability time range.</span></span>

## <a name="c-example"></a><span data-ttu-id="51b20-115">C# 예제</span><span class="sxs-lookup"><span data-stu-id="51b20-115">C# example</span></span>

```csharp
using System;
using System.Diagnostics;
using System.IO;
using System.Net;
using System.Net.WebSockets;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

namespace TimeSeriesInsightsQuerySample
{
    class Program
    {
        // For automated execution under application identity,
        // use application created in Active Directory.
        // toocreate hello application in AAD, follow hello steps provided here:
        // https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization

        // SET hello application ID of application registered in your Azure Active Directory
        private static string ApplicationClientId = "#DUMMY#";

        // SET hello application key of hello application registered in your Azure Active Directory
        private static string ApplicationClientSecret = "#DUMMY#";

        // SET hello Azure Active Directory tenant.
        private static string Tenant = "#DUMMY#.onmicrosoft.com";

        public static async Task SampleAsync()
        {
            // 1. Acquire an access token.
            string accessToken = await AcquireAccessTokenAsync();

            // 2. Obtain list of environments and get environment FQDN for hello environment of interest.
            string environmentFqdn;
            {
                Uri uri = new UriBuilder("https", "api.timeseries.azure.com")
                {
                    Path = "environments",
                    Query = "api-version=2016-12-12"
                }.Uri;
                HttpWebRequest request = WebRequest.CreateHttp(uri);
                request.Method = "GET";
                request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsQuerySample");
                request.Headers.Add("Authorization", "Bearer " + accessToken);

                using (WebResponse webResponse = await request.GetResponseAsync())
                using (var sr = new StreamReader(webResponse.GetResponseStream()))
                {
                    string responseJson = await sr.ReadToEndAsync();

                    JObject result = JsonConvert.DeserializeObject<JObject>(responseJson);
                    JArray environmentsList = (JArray)result["environments"];
                    if (environmentsList.Count == 0)
                    {
                        // List of user environments is empty, fallback toosample environment.
                        environmentFqdn = "10000000-0000-0000-0000-100000000108.env.timeseries.azure.com";
                    }
                    else
                    {
                        // Assume hello first environment is hello environment of interest.
                        JObject firstEnvironment = (JObject)environmentsList[0];
                        environmentFqdn = firstEnvironment["environmentFqdn"].Value<string>();
                    }
                }
            }
            Console.WriteLine("Using environment FQDN '{0}'", environmentFqdn);

            // 3. Obtain availability data for hello environment and get availability range.
            DateTime fromAvailabilityTimestamp;
            DateTime toAvailabilityTimestamp;
            {
                Uri uri = new UriBuilder("https", environmentFqdn)
                {
                    Path = "availability",
                    Query = "api-version=2016-12-12"
                }.Uri;
                HttpWebRequest request = WebRequest.CreateHttp(uri);
                request.Method = "GET";
                request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsQuerySample");
                request.Headers.Add("Authorization", "Bearer " + accessToken);

                using (WebResponse webResponse = await request.GetResponseAsync())
                using (var sr = new StreamReader(webResponse.GetResponseStream()))
                {
                    string responseJson = await sr.ReadToEndAsync();

                    JObject result = JsonConvert.DeserializeObject<JObject>(responseJson);
                    JObject range = (JObject)result["range"];
                    fromAvailabilityTimestamp = range["from"].Value<DateTime>();
                    toAvailabilityTimestamp = range["to"].Value<DateTime>();
                }
            }
            Console.WriteLine(
                "Obtained availability range [{0}, {1}]",
                fromAvailabilityTimestamp,
                toAvailabilityTimestamp);

            // 4. Get aggregates for hello environment:
            //    group by Event Source Name and calculate number of events in each group.
            {
                // Assume data for hello whole availablility range is requested.
                DateTime from = fromAvailabilityTimestamp;
                DateTime too= toAvailabilityTimestamp;

                JObject inputPayload = new JObject(
                    // Send HTTP headers as a part of hello message since .NET WebSocket does not support
                    // sending custom headers on HTTP GET upgrade request tooWebSocket protocol request.
                    new JProperty("headers", new JObject(
                        new JProperty("x-ms-client-application-name", "TimeSeriesInsightsQuerySample"),
                        new JProperty("Authorization", "Bearer " + accessToken))),
                    new JProperty("content", new JObject(
                        new JProperty("aggregates", new JArray(new JObject(
                            new JProperty("dimension", new JObject(
                                new JProperty("uniqueValues", new JObject(
                                    new JProperty("input", new JObject(
                                        new JProperty("builtInProperty", "$esn"))),
                                    new JProperty("take", 1000))))),
                            new JProperty("measures", new JArray(new JObject(
                                new JProperty("count", new JObject()))))))),
                        new JProperty("searchSpan", new JObject(
                            new JProperty("from", from),
                            new JProperty("to", to))))));

                var webSocket = new ClientWebSocket();

                // Establish web socket connection.
                Uri uri = new UriBuilder("wss", environmentFqdn)
                {
                    Path = "aggregates",
                    Query = "api-version=2016-12-12"
                }.Uri;
                await webSocket.ConnectAsync(uri, CancellationToken.None);

                // Send input payload.
                byte[] inputPayloadBytes = Encoding.UTF8.GetBytes(inputPayload.ToString());
                await webSocket.SendAsync(
                    new ArraySegment<byte>(inputPayloadBytes),
                    WebSocketMessageType.Text,
                    endOfMessage: true,
                    cancellationToken: CancellationToken.None);

                // Read response messages from web socket.
                JObject responseContent = null;
                using (webSocket)
                {
                    while (true)
                    {
                        string message;
                        using (var ms = new MemoryStream())
                        {
                            // Write from socket toomemory stream.
                            const int bufferSize = 16 * 1024;
                            var temporaryBuffer = new byte[bufferSize];
                            while (true)
                            {
                                WebSocketReceiveResult response = await webSocket.ReceiveAsync(
                                    new ArraySegment<byte>(temporaryBuffer),
                                    CancellationToken.None);

                                ms.Write(temporaryBuffer, 0, response.Count);
                                if (response.EndOfMessage)
                                {
                                    break;
                                }
                            }

                            // Reset position toohello beginning tooallow reads.
                            ms.Position = 0;

                            using (var sr = new StreamReader(ms))
                            {
                                message = sr.ReadToEnd();
                            }
                        }

                        JObject messageObj = JsonConvert.DeserializeObject<JObject>(message);

                        // Stop reading if error is emitted.
                        if (messageObj["error"] != null)
                        {
                            break;
                        }

                        // Number of items corresponds toonumber of aggregates in input payload
                        JArray currentContents = (JArray)messageObj["content"];

                        // In this sample list of aggregates in input payload contains
                        // only 1 item since request contains 1 aggregate.
                        responseContent = (JObject)currentContents[0];

                        // Stop reading if 100% of completeness is reached.
                        if (messageObj["percentCompleted"] != null &&
                            Math.Abs((double)messageObj["percentCompleted"] - 100d) < 0.01)
                        {
                            break;
                        }
                    }

                    // Close web socket connection.
                    if (webSocket.State == WebSocketState.Open)
                    {
                        await webSocket.CloseAsync(
                            WebSocketCloseStatus.NormalClosure,
                            "CompletedByClient",
                            CancellationToken.None);
                    }
                }

                Console.WriteLine("Dimension Value\t\tCount");
                JArray dimensionValues = (JArray)responseContent["dimension"];
                JArray measures = (JArray)responseContent["measures"];
                Debug.Assert(
                    dimensionValues.Count == measures.Count,
                    "Number of measures and dimensions should match.");
                for (int i = 0; i < dimensionValues.Count; i++)
                {
                    string currentDimensionValue = (string)dimensionValues[i];
                    JArray currentMeasureValues = (JArray)measures[i];
                    double currentCount = (double)currentMeasureValues[0];

                    Console.WriteLine("{0}\t\t{1}", currentDimensionValue, currentCount);
                }
            }
        }

        private static async Task<string> AcquireAccessTokenAsync()
        {
            if (ApplicationClientId == "#DUMMY#" || ApplicationClientSecret == "#DUMMY#" || Tenant.StartsWith("#DUMMY#"))
            {
                throw new Exception(
                    $"Use hello link {"https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization"} tooupdate hello values of 'ApplicationClientId', 'ApplicationClientSecret' and 'Tenant'.");
            }

            var authenticationContext = new AuthenticationContext(
                $"https://login.windows.net/{Tenant}",
                TokenCache.DefaultShared);

            AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
                resource: "https://api.timeseries.azure.com/",
                clientCredential: new ClientCredential(
                    clientId: ApplicationClientId,
                    clientSecret: ApplicationClientSecret));

            // Show interactive logon dialog tooacquire token on behalf of hello user.
            // Suitable for native apps, and not on server-side of a web application.
            //AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
            //    resource: "https://api.timeseries.azure.com/",
            //    // Set well-known client ID for Azure PowerShell
            //    clientId: "1950a258-227b-4e31-a9cf-717495945fc2",
            //    // Set redirect URI for Azure PowerShell
            //    redirectUri: new Uri("urn:ietf:wg:oauth:2.0:oob"),
            //    parameters: new PlatformParameters(PromptBehavior.Auto));

            return token.AccessToken;
        }

        static void Main(string[] args)
        {
            Task.Run(async () => await SampleAsync()).Wait();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="51b20-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51b20-116">Next steps</span></span>

<span data-ttu-id="51b20-117">전체 쿼리 API 참조 hello에 대 한 참조 hello [쿼리 API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) 문서.</span><span class="sxs-lookup"><span data-stu-id="51b20-117">For hello full Query API reference, see hello [Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) document.</span></span>
