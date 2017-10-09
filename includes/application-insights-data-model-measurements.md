사용자 지정 측정값 컬렉션입니다. 이 컬렉션 tooreport 라는 hello 원격 분석 항목에 연결 된 측정을 사용 합니다. 일반적인 사용 사례는 다음과 같습니다.
- 종속성 원격 분석 페이로드의 hello 크기
- hello 요청 원격 분석에서 처리 하는 큐 항목 수
- 해당 고객의 마법사 단계 완료 이벤트 원격 분석 toocomplete hello 단계는 데 걸린 시간입니다.

응용 프로그램 분석에서 [사용자 지정 측정값](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H)을 쿼리할 수 있습니다.

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > 사용자 지정 측정 하는 것에 속해 hello 원격 분석 항목에 연결 합니다. 이러한 측정값을 포함 하는 hello 원격 분석 항목 제목 toosampling 됩니다. tootrack 측정을 사용 하 여 다른 원격 분석 형식에서 독립적인 값이 있는 [메트릭 원격 분석](../articles/application-insights/app-insights-api-custom-events-metrics.md)합니다.

최대 키 길이: 150
