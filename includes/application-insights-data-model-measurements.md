<span data-ttu-id="f9ad3-101">사용자 지정 측정값 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-101">Collection of custom measurements.</span></span> <span data-ttu-id="f9ad3-102">이 컬렉션 tooreport 라는 hello 원격 분석 항목에 연결 된 측정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="f9ad3-103">일반적인 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-103">Typical use cases are:</span></span>
- <span data-ttu-id="f9ad3-104">종속성 원격 분석 페이로드의 hello 크기</span><span class="sxs-lookup"><span data-stu-id="f9ad3-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="f9ad3-105">hello 요청 원격 분석에서 처리 하는 큐 항목 수</span><span class="sxs-lookup"><span data-stu-id="f9ad3-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="f9ad3-106">해당 고객의 마법사 단계 완료 이벤트 원격 분석 toocomplete hello 단계는 데 걸린 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="f9ad3-107">응용 프로그램 분석에서 [사용자 지정 측정값](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H)을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="f9ad3-108">사용자 지정 측정 하는 것에 속해 hello 원격 분석 항목에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="f9ad3-109">이러한 측정값을 포함 하는 hello 원격 분석 항목 제목 toosampling 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="f9ad3-110">tootrack 측정을 사용 하 여 다른 원격 분석 형식에서 독립적인 값이 있는 [메트릭 원격 분석](../articles/application-insights/app-insights-api-custom-events-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ad3-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="f9ad3-111">최대 키 길이: 150</span><span class="sxs-lookup"><span data-stu-id="f9ad3-111">Max key length: 150</span></span>
