>[!NOTE]
>리소스를 수정 하지 않는 대 한 지원 티켓을 열어에 의해 발생 하는 hello 할당량 toobe 요청할 수 있습니다. 수행 **하지** tooobtain 더 높은 값 제한 시도 추가 Azure 미디어 서비스 계정을 만듭니다.

| 리소스 | 기본 제한 | 
| --- | --- | 
| 단일 구독의 Azure 미디어 서비스(AMS) 계정 | 25(고정) |
| AMS 계정당 미디어 RU(예약 단위) |25(S1, S2)<br/>10(S3)<sup>(1)</sup> | 
| AMS 계정당 작업 | 50,000<sup>(2)</sup> |
| 작업당 연결된 태스크 | 30(고정) |
| AMS 계정당 자산 | 1,000,000|
| 태스크당 자산 | 50 |
| 작업당 자산 | 100 |
| 한번에 자산과 연결된 고유 로케이터 | 5<sup>(4)</sup> |
| AMS 계정당 라이브 채널  |5|
| 채널당 중지 상태인 프로그램  |50|
| 채널당 실행 상태인 프로그램  |3|
| AMS 계정당 실행 상태인 스트리밍 끝점 |2|
| 스트리밍 끝점당 스트리밍 단위  |10 |
| 저장소 계정 | 1,000<sup>(5)</sup>(고정) |
| 정책 | 1,000,000<sup>(6)</sup> |
| 파일 크기| 일부 시나리오에서는 있는 미디어 서비스에서 처리를 위해 지원 되는 hello 최대 파일 크기에서 제한이 됩니다. <sup>7</sup> |
  
<sup>1</sup> S3 RU는 인도 서부에서 사용할 수 없습니다. hello max RU 제한 빨리 hello 고객 hello 형식 (예: S2 tooS1)에서 변경 되 면 다시 설정 합니다. 

<sup>2</sup> 이 번호에 대기 중, 완료, 활성 및 취소 된 작업도 포함 됩니다. 삭제된 작업은 포함 되지 않습니다. 사용 하 여 hello 오래 된 작업을 삭제할 수 있습니다 **IJob.Delete** 또는 hello **삭제** HTTP 요청입니다.

2017 년 4 월 1부터 90 일 보다 오래 된 계정에서 모든 작업 기록은 자동으로 함께 삭제 됩니다, 관련된 작업 레코드를 레코드의 총 수 hello hello 최대 할당량 미만인 경우에 합니다. 내용을 tooarchive hello 작업/태스크를 설명 하는 hello 코드를 사용할 수 있습니다 [여기](../articles/media-services/media-services-dotnet-manage-entities.md)합니다.

<sup>3</sup> toolist Job 엔터티 요청을 수행할 때는 최대 1000 개의 요청당 반환 됩니다. Tookeep를 추적 해야 할 경우 모든 작업을 제출에 설명 된 대로 top/skip을 사용할 수 있습니다 [OData 시스템 쿼리 옵션](http://msdn.microsoft.com/library/gg309461.aspx)합니다.

<sup>4</sup> 로케이터는 사용자별 액세스 제어를 관리하도록 설계되지 않았습니다. toogive 서로 다른 액세스 권한 tooindividual 사용자는 디지털 Rights Management (DRM) 솔루션을 사용 합니다. 자세한 내용은 [이](../articles/media-services/media-services-content-protection-overview.md) 섹션을 참조하세요.

<sup>5</sup> hello 저장소 계정은 hello에서 가져와야 합니다. 동일한 Azure 구독.

<sup>6</sup> 다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. 

>[!NOTE]
> Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 액세스 권한 / / 등입니다. 내용 및 예제는 [이](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) 섹션을 참조하세요.

<sup>7</sup>업로드 하는 경우 콘텐츠 tooan 자산 Azure 미디어에서 사용 하 여 서비스 hello 의도 tooprocess 사용 하 여 서비스의 hello 미디어 프로세서 중 하나 (예: 인코더 등의 미디어 인코더 표준 및 미디어 인코더 프리미엄 워크플로 또는 분석 엔진 Face 탐지기)와 같은 다음 수 hello 최대 크기에 hello 제약 조건입니다. 

2017 년 5 월 15부터 hello 단일 blob에 대해 지원 되는 최대 크기와이 제한 보다 파일 largers 195 t-B는 하 고 작업 실패 합니다. 작업 수정 tooaddress이 한이도입니다. 또한 hello hello의 최대 크기에 hello 제약 조건을 Asset은 다음과 같습니다.

| 미디어 예약 단위 유형 | 최대 입력 크기(GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
