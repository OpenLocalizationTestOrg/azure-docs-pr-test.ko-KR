
# <a name="azure-and-internet-of-things"></a>Azure 및 사물 인터넷

인터넷의 IoT (사물) hello 및 tooMicrosoft Azure를 시작 합니다. 이 문서에서는 Azure 서비스를 사용 하 여 배포할 수 있는 IoT 솔루션의 hello 일반적인 특징을 설명 하는 IoT 솔루션 아키텍처를 소개 합니다. IoT 솔루션 백만 hello 및 솔루션 백 엔드에 이르기 수 있는 장치 간의 양방향 통신을 보호에 필요 합니다. 예를 들어 솔루션 백 엔드 장치-클라우드 이벤트 스트림에서 자동화 되 고, 예측 분석 toouncover insights를 사용할 수 있습니다.

Azure IoT Hub는 Azure 서비스를 사용하여 이러한 IoT 솔루션 아키텍처를 구현하는 경우에 주요한 구성 요소입니다. IoT Suite는 특정 IoT 시나리오에 이 아키텍처의 완전한 종단 간 구현을 제공합니다. 예:

* hello *원격 모니터링* 솔루션 toomonitor hello 상태 건포도 컴퓨터 등의 장치를 사용 합니다.
* hello *예측 유지 관리* 솔루션에서는 tooanticipate 유지 관리가 필요한 펌프 대리 펌핑 원격 스테이션 및 tooavoid 예약 되지 않은 가동 중지 등의 장치입니다.
* hello *연결 된 팩터리* 솔루션 tooconnect 활용 하 고 산업 장치 모니터링 합니다.

## <a name="iot-solution-architecture"></a>IoT 솔루션 아키텍처

hello 다음 다이어그램에서는 일반적인 IoT 솔루션 아키텍처를 보여 줍니다. hello 다이어그램 모든 특정 Azure 서비스의 hello 이름이 포함 되어 있지 않으면이 열리지만, hello 제네릭 IoT 솔루션 아키텍처의 주요 요소에 설명 합니다. 이 아키텍처 IoT 장치 tooa 클라우드 게이트웨이 보내는 데이터를 수집 합니다. hello 클라우드 게이트웨이 hello 데이터를 사용할 수 있도록 tooother 기간 업무 응용 프로그램이 나 대시보드 또는 기타 프레젠테이션 장치를 통해 toohuman 연산자 데이터가 전달 되는 위치에서 다른 백 엔드 서비스에서 처리 합니다.

![IoT 솔루션 아키텍처][img-solution-architecture]

> [!NOTE]
> IoT 아키텍처는 대 한 자세한 내용은 참조 hello [Microsoft Azure IoT 참조 아키텍처][lnk-refarch]합니다.

### <a name="device-connectivity"></a>장치 연결

이 IoT 솔루션 아키텍처 장치 센서 판독값 대리 펌핑 스테이션, 저장소에 대 한 tooa 클라우드 끝점을 및 처리와 같은 원격 분석을 보냅니다. 예측 유지 관리 시나리오에서는 특정 펌프 유지 관리 해야 하는 경우 hello 솔루션 백 엔드 센서 데이터 toodetermine hello 스트림을 사용할 수 있습니다. 또한 장치 수신 하 고 toocloud-장치 메시지 클라우드 끝점에서 메시지를 참조 하 여 응답할 수 있습니다. 예를 들어 hello 예측 유지 관리 시나리오 hello 솔루션에서 백 엔드 보낼 수 있습니다 메시지 펌프 tooother hello 바로 전에 유지 관리 기간이 흐름 다시 라우팅할 경우 스테이션 toobegin 펌프에 toostart 합니다. 이 절차는 hello 유지 관리 엔지니어 메시지를 보내고 받이 되는 즉시 시작 하려면 수 있는지 확인 해야 합니다.

IoT 프로젝트 직면 hello 가장 큰 해결 과제 중 하나인 어떻게 tooreliably 장치 toohello 솔루션에 대 한 백 엔드를 안전 하 게 연결 합니다. IoT 장치 브라우저 및 모바일 앱과 같은 비교 tooother 클라이언트와 다른 특징을 갖습니다. IoT 장치:

* 운영자가 없는 내장 시스템인 경우가 많습니다.
* 물리적 액세스에 많은 비용이 드는 원격 위치에 배포될 수 있습니다.
* Hello 솔루션 백 엔드를 통해 도달할 수 있습니다. Hello 장치와 다른 방식으로 toointeract 되지 않습니다.
* 전원 및 리소스 처리 제한이 있을 수 있습니다.
* 일시적이거나 느리거나 비용이 많이 드는 네트워크 연결이 있을 수 있습니다.
* Toouse 소유, 사용자 지정 또는 업계 관련 응용 프로그램 프로토콜을 지정 해야 합니다.
* 널리 사용되는 다양한 하드웨어 및 소프트웨어 플랫폼을 사용하여 만들 수 있습니다.

또한 toohello 위의 요구 사항은, 모든 IoT 솔루션도 배달 해야 배율, 보안 및 안정성 합니다. hello 결과 집합의 연결 요구 사항은 하드 및 시간 소요 정도가 tooimplement 웹 컨테이너와 같은 기존 기술을 사용 하 여 및 브로커 메시징입니다. Azure IoT Hub 및 hello Azure IoT 장치 sdk에서는 이러한 요구 사항을 충족 하는 보다 쉽게 tooimplement 솔루션을 만듭니다.

장치는 클라우드 게이트웨이 끝점와 직접 통신할 수 또는 hello 장치 클라우드 게이트웨이 지원 hello hello 통신 프로토콜을 사용할 수 없습니다, 하는 경우 중간 게이트웨이 통해 연결할 수 있습니다. 예를 들어 hello [Azure IoT 프로토콜 게이트웨이] [ lnk-protocol-gateway] 장치에 hello 프로토콜을 지 원하는 IoT 허브를 사용할 수 없는 경우에 프로토콜 변환을 수행할 수 있습니다.

### <a name="data-processing-and-analytics"></a>데이터 처리 및 분석

Hello 클라우드 IoT 솔루션 백 엔드는 필터링 하 고 원격 분석 집계 및 라우팅 tooother 서비스 같은 대부분의 데이터 처리 hello 발생 합니다. IoT 솔루션 백 엔드 hello:

* 장치에서 규모에 원격 분석을 받아 결정 방법을 tooprocess 및 해당 데이터를 저장 합니다. 
* 사용 하면 hello 클라우드 toospecific 장치에서 toosend 명령 있습니다.
* Tooprovision 장치 및 장치는 tooconnect tooyour 인프라 허용 toocontrol 수 있도록 장치 등록 기능을 제공 합니다.
* Tootrack 있습니다 hello 장치 상태 및 해당 작업을 모니터링할 수 있습니다.

Hello 예측 유지 관리 시나리오에서는 hello 솔루션 백 엔드 기록 원격 분석 데이터를 저장합니다. hello 솔루션 백 엔드를 유지 관리 기간이 특정 펌프 나타내는이 데이터 toouse tooidentify 패턴을 사용할 수 있습니다.

IoT 솔루션은 자동 피드백 루프를 포함할 수 있습니다. 예를 들어 hello 솔루션 백 엔드에 대 한 분석 모듈 정상 작동 수준 위에 있는 hello 온도 특정 장치에 원격 분석에서 식별할 수 있습니다. hello 솔루션 tootake 수정 동작을 지정 하는 명령 toohello 장치를 보낼 수 있습니다.

### <a name="presentation-and-business-connectivity"></a>프레젠테이션 및 Business Connectivity

hello 프레젠테이션 및 비즈니스 연결 레이어 hello 장치와 toointeract IoT 솔루션 hello로 최종 사용자가 수 있습니다. 사용자가 tooview 있으며 자신의 장치에서 수집 된 hello 데이터를 분석 합니다. 이러한 뷰는 hello 형식 모두 기록 데이터를 표시할 수 있는 BI 보고서의 또는 거의 실시간 데이터를 사용할 수 있습니다. 예를 들어 운영자 특정 대리 펌핑 스테이션의 hello 상태에 확인 하 고 hello 시스템에 의해 발생 한 경고를 볼 수 있습니다. 이 계층에는 엔터프라이즈 비즈니스 프로세스 또는 워크플로가 hello IoT 솔루션 기존 기간 업무 응용 프로그램 tootie와 백 엔드의 통합 수 있습니다. 예를 들어 hello 예측 유지 관리 솔루션와 통합할 수 일정 시스템 해당 설명서 엔지니어 toovisit 대리 펌핑 스테이션 hello 솔루션 유지 관리가 필요한 펌프를 식별 하는 경우.

![IoT 솔루션 대시보드][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
