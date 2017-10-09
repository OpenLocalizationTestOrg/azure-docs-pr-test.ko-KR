hello 작업이 검색 되 고 추적 된 글꼴에 대 한 메타 데이터를 포함 하는 JSON 출력 파일을 생성 합니다. hello 메타 데이터 나타내는 얼굴의 hello 위치 뿐만 아니라 글꼴 ID 번호 나타내는 hello 추적 해당 개인의 좌표가 포함 됩니다. 글꼴 ID 번호는 상황에서 발생 하기 쉬운 tooreset hello 전면 손실 되거나 hello 프레임에서 겹쳐진의 결과로 나타나는 일부 사용자를 가져오는 여러 Id를 할당 합니다.

hello 출력 JSON hello 다음 특성을 포함 합니다.

| 요소 | 설명 |
| --- | --- |
| 버전 |이 hello 비디오 API의 toohello 버전을 나타냅니다. |
| index | (TooAzure 미디어 Redactor 적용) hello 현재 이벤트의 hello 프레임 인덱스를 정의 합니다. |
| timescale |"틱" hello 비디오의 초 당 합니다. |
| offset |타임 스탬프에 대 한 hello 시간 오프셋입니다. 동영상 API 버전 1.0에서는 항상 0입니다. 향후 지원하는 시나리오에서는 이 값이 변경될 수 있습니다. |
| framerate |Hello 비디오의 초당 프레임 수입니다. |
| fragments |hello 메타 데이터를 조각 이라고 하는 서로 다른 세그먼트에 청크 분할 됩니다. 각 조각에는 시작, 기간, 간격 번호 및 이벤트가 포함됩니다. |
| start |hello 'ticks' hello 첫 번째 이벤트 시간을 시작 합니다. |
| duration |"틱" hello 조각의 hello 길이입니다. |
| interval |"틱" hello 조각 내에서 각 이벤트 엔트리의 hello 간격입니다. |
| events |각 이벤트는 hello 얼굴 감지 하 고 해당 기간 내에서 추적을 포함 합니다. 이벤트 배열입니다. hello 외부 배열에는 한 시간 간격을을 나타냅니다. 0 이나 더 많은 이벤트 시간에서 해당 시점에 발생 하는 hello 내부 배열은 구성 됩니다. 빈 대괄호 []는 검색된 얼굴이 없음을 의미합니다. |
| id |추적 되 고 hello 면의 hello ID입니다. 이 번호는 얼굴이 검색되지 않는 경우 실수로 변경될 수 있습니다. 지정 된 개별 hello 전체 비디오 전체 ID 같습니다 hello 있어야 합니다. 하지만이 보장 되 due toolimitations hello 검색 알고리즘 (폐색 등)에 |
| x, y |hello 홈페이지 X 및 Y 좌표가 hello 0.0 too1.0의 정규화 된 눈금의 경계 상자를 직면 했습니다. <br/>-X 및 Y 좌표는 상대 toolandscape 항상 세로 비디오 (또는 뒤집어 iOS의 경우 hello)를 사용 하도록 설정한 경우 볼 수 있도록 tootranspose hello 좌표 적절 하 게 합니다. |
| width, height |hello의 hello 너비와 높이 0.0 too1.0의 정규화 된 눈금의 경계 상자를 직면 했습니다. |
| facesDetected |이 hello JSON 결과의 hello 끝에서 발견 되 고 해당 hello 알고리즘 hello 비디오 하는 동안 검색 면 hello 수를 요약 합니다. Hello Id 수 수 다시 설정 때문에 실수로 얼굴 감지 되지 않은 경우 (예: 글꼴 중 화면에서 바로 찾습니다) 항상이 숫자 hello true 면 hello 비디오 수와 같지 않을 수 있습니다. |

