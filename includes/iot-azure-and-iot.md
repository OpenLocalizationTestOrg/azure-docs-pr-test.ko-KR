
# <a name="azure-and-internet-of-things"></a>Azure 및 사물 인터넷

Microsoft Azure 및 IoT(사물 인터넷)를 시작합니다. 이 문서에서는 Azure 서비스를 사용하여 배포할 수 있는 IoT 솔루션의 공통된 특성을 설명하는 IoT 솔루션 아키텍처를 소개합니다. IoT 솔루션은 수백만 대에 이르는 장치 및 솔루션 백 엔드 사이의 안전한, 양방향 통신을 필요로 합니다. 예를 들어, 솔루션 백 엔드는 장치-클라우드 이벤트 스트림으로부터 새로운 정보를 발견하기 위하여 자동화된 예측 분석을 사용할 수 있습니다.

Azure IoT Hub는 Azure 서비스를 사용하여 이러한 IoT 솔루션 아키텍처를 구현하는 경우에 주요한 구성 요소입니다. IoT Suite는 특정 IoT 시나리오에 이 아키텍처의 완전한 종단 간 구현을 제공합니다. 예:

* *원격 모니터링* 솔루션은 자동 판매기와 같은 장치의 상태를 모니터링할 수 있도록 해 줍니다.
* *예측 유지 관리* 솔루션은 원격 펌핑 스테이션과 같은 장치에 대한 유지 관리 요구를 예측하여 예정에 없는 가동 중지 시간을 피하는 데 도움을 줍니다.
* *연결된 팩터리* 솔루션을 사용하면 산업용 장치를 연결하고 모니터링할 수 있습니다.

## <a name="iot-solution-architecture"></a>IoT 솔루션 아키텍처

다음의 다이어그램에서는 일반적인 IoT 솔루션 아키텍처를 보여줍니다. 다이어그램은 특정 Azure 서비스의 이름을 포함하지 않지만 제네릭 IoT 솔루션 아키텍처의 주요 요소를 설명합니다. 이 아키텍처에서 IoT 장치는 클라우드 게이트웨이로 보내는 데이터를 수집합니다. 클라우드 게이트웨이를 사용하면 대시보드나 기타 프레젠테이션 장치를 통해 운영자 또는 다른 기간 업무 응용 프로그램에 데이터를 전달하는 다른 백 엔드 서비스에서 처리하기 위한 데이터를 사용할 수 있습니다.

![IoT 솔루션 아키텍처][img-solution-architecture]

> [!NOTE]
> IoT 아키텍처에 대한 자세한 설명은 [Microsoft Azure IoT 참조 아키텍처][lnk-refarch]를 참조하세요.

### <a name="device-connectivity"></a>장치 연결

이 IoT 솔루션 아키텍처에서 장치는 저장소 및 처리를 위한 클라우드 끝점에 펌핑 스테이션의 센서 판독값과 같은 원격 분석을 보냅니다. 예측 유지 관리 시나리오에서는 솔루션 백 엔드에서 센서 데이터 스트림을 사용하여 특정 펌프에 유지 관리가 필요한 시기를 결정할 수 있습니다. 또한 장치는 클라우드 끝점에서 메시지를 읽어 수신하고 클라우드-장치 메시지에 응답할 수 있습니다. 예를 들어 예측 유지 관리 시나리오에서 솔루션 백 엔드는 펌핑 스테이션의 다른 펌프로 메시지를 보내서 유지 관리가 시작되기 바로 전에 흐름을 다시 라우팅할 수 있습니다. 이 프로시저를 통해 유지 관리 엔지니어가 도착하는 즉시 작업을 시작할 수 있도록 합니다.

IoT 프로젝트의 가장 큰 당면 과제 중 하나는 장치를 안정적이고 안전하게 솔루션 백 엔드에 연결하는 방법입니다. IoT 장치는 브라우저 및 모바일 앱 등 다른 클라이언트에 비해 다른 특징을 가집니다. IoT 장치:

* 운영자가 없는 내장 시스템인 경우가 많습니다.
* 물리적 액세스에 많은 비용이 드는 원격 위치에 배포될 수 있습니다.
* 솔루션 백 엔드를 통해서만 연결 가능합니다. 장치와 상호 작용하는 다른 방법이 없습니다.
* 전원 및 리소스 처리 제한이 있을 수 있습니다.
* 일시적이거나 느리거나 비용이 많이 드는 네트워크 연결이 있을 수 있습니다.
* 독점, 사용자 지정 또는 업계 특정 응용 프로그램 프로토콜을 사용해야 할 수 있습니다.
* 널리 사용되는 다양한 하드웨어 및 소프트웨어 플랫폼을 사용하여 만들 수 있습니다.

위의 요구 사항 외에도 모든 IoT 솔루션은 크기 조정, 보안 및 안정성을 제공해야 합니다. 연결 요구 사항의 결과 집합은 웹 컨테이너 및 메시징 브로커와 같은 기존 기술을 사용하여 구현하는데 어렵고 많은 시간이 소요됩니다. Azure IoT Hub 및 Azure IoT 장치 SDK를 사용하여 이러한 요구 사항을 충족하는 솔루션을 보다 쉽게 구현할 수 있습니다.

장치는 클라우드 게이트웨이 끝점과 직접 통신하거나 장치가 클라우드 게이트웨이가 지원하는 통신 프로토콜을 사용할 수 없는 경우, 중간 게이트웨이를 통해 연결할 수 있습니다. 예를 들어 IoT Hub가 지원하는 프로토콜을 장치에서 사용할 수 없으면 [Azure IoT 프로토콜 게이트웨이][lnk-protocol-gateway]가 프로토콜 변환을 수행할 수 있습니다.

### <a name="data-processing-and-analytics"></a>데이터 처리 및 분석

클라우드의 IoT 솔루션 백 엔드는 원격 분석을 필터링하고 집계하여 다른 서버로 라우팅하는 등의 데이터 처리 작업 대부분이 이루어지는 곳입니다. IoT 솔루션 백 엔드:

* 사용 중인 장치로부터 대규모로 원격 분석을 수신하고 해당 데이터를 처리하고 저장하는 방법을 결정합니다. 
* 명령을 클라우드에서 특정 장치로 보내는 데 사용할 수 있습니다.
* 장치를 프로비전하고 인프라 연결을 허용할 장치를 제어하도록 하는 장치 등록 기능을 제공합니다.
* 장치 상태를 추적하고 해당 작업을 모니터링할 수 있습니다.

예측 유지 관리 시나리오에서 솔루션 백 엔드는 원격 분석 데이터 기록을 저장합니다. 솔루션 백 엔드는 이 데이터를 사용하여 특정 펌프에 대한 유지 관리 기한이 임박하다는 것을 나타내는 패턴을 파악할 수 있습니다.

IoT 솔루션은 자동 피드백 루프를 포함할 수 있습니다. 예를 들어 솔루션 백 엔드의 분석 모듈은 원격 분석을 통해 특정 장치의 온도가 정상 작동 수준보다 높다는 것을 파악할 수 있습니다. 그런 다음 솔루션이 장치에 명령을 보내서 시정 조치를 취하도록 지시할 수 있습니다.

### <a name="presentation-and-business-connectivity"></a>프레젠테이션 및 Business Connectivity

프레젠테이션 및 Business Connectivity 계층을 통해 최종 사용자가 IoT 솔루션 및 장치를 조작할 수 있습니다. 이를 통해 사용자가 해당 장치에서 수집된 데이터를 보고 분석할 수 있습니다. 이러한 보기는 기록 데이터와 거의 실시간 데이터를 모두 표시할 수 있는 대시보드 또는 BI 보고서 형식일 수 있습니다. 예를 들어 운영자는 특정 펌핑 스테이션의 상태를 검사하고 시스템에서 발생한 경고를 확인할 수 있습니다. 또한 이 계층을 통해 IoT 솔루션 백 엔드와 기존 기간 업무 응용 프로그램을 통합하여 엔터프라이즈 비즈니스 프로세스 또는 워크플로와 연계시킬 수 있습니다. 예를 들어 예측 유지 관리 솔루션은 유지 관리가 필요한 펌프를 식별한 경우 엔지니어의 펌핑 스테이션 방문 일정을 예약하는 예약 시스템과 통합될 수 있습니다.

![IoT 솔루션 대시보드][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf