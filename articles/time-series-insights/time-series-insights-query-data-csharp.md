---
title: "C#을 사용하여 Azure Time Series Insights 환경에서 데이터 쿼리 | Microsoft 문서"
description: "이 자습서에서는 C#을 사용하여 Time Series Insights 환경에서 데이터를 쿼리하는 방법을 다루며 예제 코드를 제공합니다."
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
ms.openlocfilehash: 1444b517664355e8e240ea181d707c464d7ec5bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="query-data-from-the-azure-time-series-insights-environment-using-c"></a>C#을 사용하여 Azure Time Series Insights 환경에서 데이터 쿼리

이 C# 예제에서는 Azure Time Series Insights 환경에서 데이터를 쿼리하는 방법을 보여 줍니다.
이 샘플은 쿼리 API 사용의 몇 가지 기본 예제를 보여 줍니다.
1. 준비 단계로, Azure Active Directory API를 통해 액세스 토큰을 가져옵니다. 이 토큰을 모든 쿼리 API 요청의 `Authorization` 헤더에 전달합니다. 비대화형 응용 프로그램을 설정하려면 [인증 및 권한 부여](time-series-insights-authentication-and-authorization.md)를 참조하세요. 또한 샘플의 시작 부분에 정의된 모든 상수를 올바르게 설정합니다.
2. 사용자가 액세스 권한을 가진 환경 목록을 가져옵니다. 환경 중 하나를 관심 환경으로 선택하고 이 환경에 대해 추가 데이터를 쿼리합니다.
3. HTTPS 요청의 예로, 관심 환경에 대해 가용성 데이터를 요청합니다.
4. 웹 소켓 요청의 예로, 관심 환경에 대해 이벤트 집계 데이터를 요청합니다. 전체 가용성 시간 범위에 대한 데이터가 요청됩니다.

## <a name="c-example"></a>C# 예제

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
        // To create the application in AAD, follow the steps provided here:
        // https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization

        // SET the application ID of application registered in your Azure Active Directory
        private static string ApplicationClientId = "#DUMMY#";

        // SET the application key of the application registered in your Azure Active Directory
        private static string ApplicationClientSecret = "#DUMMY#";

        // SET the Azure Active Directory tenant.
        private static string Tenant = "#DUMMY#.onmicrosoft.com";

        public static async Task SampleAsync()
        {
            // 1. Acquire an access token.
            string accessToken = await AcquireAccessTokenAsync();

            // 2. Obtain list of environments and get environment FQDN for the environment of interest.
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
                        // List of user environments is empty, fallback to sample environment.
                        environmentFqdn = "10000000-0000-0000-0000-100000000108.env.timeseries.azure.com";
                    }
                    else
                    {
                        // Assume the first environment is the environment of interest.
                        JObject firstEnvironment = (JObject)environmentsList[0];
                        environmentFqdn = firstEnvironment["environmentFqdn"].Value<string>();
                    }
                }
            }
            Console.WriteLine("Using environment FQDN '{0}'", environmentFqdn);

            // 3. Obtain availability data for the environment and get availability range.
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

            // 4. Get aggregates for the environment:
            //    group by Event Source Name and calculate number of events in each group.
            {
                // Assume data for the whole availablility range is requested.
                DateTime from = fromAvailabilityTimestamp;
                DateTime to = toAvailabilityTimestamp;

                JObject inputPayload = new JObject(
                    // Send HTTP headers as a part of the message since .NET WebSocket does not support
                    // sending custom headers on HTTP GET upgrade request to WebSocket protocol request.
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
                            // Write from socket to memory stream.
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

                            // Reset position to the beginning to allow reads.
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

                        // Number of items corresponds to number of aggregates in input payload
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
                    $"Use the link {"https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization"} to update the values of 'ApplicationClientId', 'ApplicationClientSecret' and 'Tenant'.");
            }

            var authenticationContext = new AuthenticationContext(
                $"https://login.windows.net/{Tenant}",
                TokenCache.DefaultShared);

            AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
                resource: "https://api.timeseries.azure.com/",
                clientCredential: new ClientCredential(
                    clientId: ApplicationClientId,
                    clientSecret: ApplicationClientSecret));

            // Show interactive logon dialog to acquire token on behalf of the user.
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

## <a name="next-steps"></a>다음 단계

전체 쿼리 API 참조는 [쿼리 API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) 문서를 참조하세요.
