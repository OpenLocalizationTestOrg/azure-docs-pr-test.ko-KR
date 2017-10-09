# <a name="secure-your-iot-deployment"></a>IoT 배포 보안 유지
이 문서는 hello Azure IoT 기반 인터넷 IoT (사물) 인프라를 보호 하기 위한 hello 다음 수준의 세부 정보를 제공 합니다. 구성 하 고 각 구성 요소 배포에 대 한 tooimplementation 수준의 세부 정보를 연결 합니다. 그밖에도 다양한 경쟁 방법 간을 비교하고 선택 항목을 제공합니다.

Hello Azure IoT 배포 보안 hello 다음 세 가지 보안 영역으로 나눌 수 있습니다.

* **장치 보안**: hello 와일드 카드에 배포 되는 동안 고정 hello IoT 장치입니다.
* **연결 보안**: 기밀 및 무단은 hello IoT 장치와 IoT Hub 간에 전송 된 모든 데이터를 확인 합니다.
* **보안 클라우드**: 데이터를 제공 하는 수단 toosecure를 통해 이동 하 고 hello 클라우드에 저장 됩니다.

![세 가지 보안 영역][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>보안 장치를 프로비전 및 인증
다음 두 가지 방법을 hello 하 여 IoT 장치를 보호 하는 hello Azure IoT Suite:

* Hello 장치 toocommunicate hello IoT 허브로 사용할 수 있는 각 장치에 대해 고유한 id 키 (보안 토큰)를 제공 하 합니다.
* 장치를 사용 하 여 [X.509 인증서] [ lnk-x509] 와 수단 tooauthenticate hello 장치 toohello IoT 허브로 개인 키입니다. 이 인증 방법을 해당 hello를 사용 하면 hello 장치에서 개인 키가 알 수 없는 hello 장치 외부 언제 든 지 더 높은 수준의 보안을 제공 합니다.

보안 토큰 방법의 hello hello 대칭 키 tooeach 호출을 연결 하 여 hello 장치 tooIoT 허브 하 여 실행 한 각 호출에 대 한 인증을 제공 합니다. X.509 기반 인증 hello TLS 연결 설정의 일부로 hello 물리적 계층에서 IoT 장치 인증을 허용 합니다. 덜 안전한 패턴 hello X.509 인증 없이 hello 보안 토큰 기반 메서드를 사용할 수 있습니다. hello hello 두 메서드 중 하나를 선택은 주로 지정 방법도 hello에서 장치 인증 toobe와 hello 장치에서 보안 저장소의 가용성을 필요 (toostore 개인 키를 안전 하 게 hello 데 사용).

## <a name="iot-hub-security-tokens"></a>IoT Hub 보안 토큰
IoT Hub는 보안 토큰 tooauthenticate 장치 및 서비스 tooavoid hello 네트워크에서 키 보내기 사용 합니다. 또한 보안 토큰은 유효 기간 및 범위가 제한됩니다. Azure IoT SDK는 특별한 구성이 필요하지 않고 토큰을 자동으로 생성합니다. 그러나 일부 시나리오에서는 hello 사용자 toogenerate 필요 하 고 보안 토큰을 직접 사용 합니다. 여기에 hello hello MQTT, AMQP 또는 HTTP 표면을 직접 사용 또는 hello 토큰 서비스 패턴의 hello 구현을 포함 합니다.

Hello 보안 토큰 및 사용법의 hello 구조에 대 한 자세한 내용은 다음 문서는 hello에서 찾을 수 있습니다.

* [보안 토큰 구조][lnk-security-tokens]
* [장치로 SAS 토큰 사용][lnk-sas-tokens]

각 IoT 허브에는 [id 레지스트리에] [ lnk-identity-registry] tooallow 액세스 toohello 및 진행 중인 클라우드-장치 메시지를 포함 하는 큐와 같이 hello 서비스에서 사용 되는 toocreate 장치 단위 리소스 일 수 있는 장치 연결 끝점입니다. IoT Hub id 레지스트리에 hello 장치 id 및 솔루션에 대 한 보안 키의 안전한 저장소를 제공 합니다. 장치 id의 그룹이 나 개인을 추가할 수 있습니다 tooan 허용 목록 또는 차단 목록, 완벽 하 게 장치 액세스 제어를 사용 하도록 설정 합니다. hello 다음 문서를 더욱 자세히 hello identity 레지스트리 및 지원 되는 작업의 hello 구조에 있습니다.

[IoT Hub는 MQTT, AMQP 및 HTTP와 같은 프로토콜을 지원합니다][lnk-protocols]. 이러한 각 프로토콜 다르게 hello IoT 장치 tooIoT 허브의에서 보안 토큰을 사용 합니다.

* AMQP: SASL 일반 및 AMQP 클레임 기반 보안 ({policyName}@sas.root. { iothubName} IoT 허브 수준 토큰; hello 경우 {deviceId} 장치 범위 토큰의 경우).
* MQTT: hello {ClientId}, {IoThubhostname}로 패킷을 사용 하 여 {deviceId} 연결 / {deviceId} hello에 **Username** hello에서 필드와 SAS 토큰 **암호** 필드입니다.
* HTTP: hello 권한 부여 요청 헤더에 유효한 토큰이 되었습니다.

IoT Hub id 레지스트리에 액세스 제어 및 사용 되는 tooconfigure-장치 보안 자격 증명 일 수 있습니다. 그러나 [사용자 지정 장치 ID 레지스트리 및/또는 인증 체계][lnk-custom-auth]에 이미 상당한 투자를 한 IoT 솔루션의 경우 토큰 서비스를 만들어 IoT Hub가 있는 기존 인프라로 통합할 수 있습니다.

### <a name="x509-certificate-based-device-authentication"></a>X.509 인증서 기반 장치 인증
사용 하 여 hello는 [X.509 인증서 장치 기반] [ lnk-use-x509] 하 고 해당 연결 된 개인 및 공개 키 쌍 hello 물리적 계층에서 추가 인증을 허용 합니다. hello 개인 키 hello 장치에 안전 하 게 저장 되며 hello 장치 외부 검색할 수 없습니다. hello X.509 인증서에는 장치 ID와 같은 hello 장치에 대 한 정보 및 기타 조직 구성 세부 정보가 포함 되어 있습니다. Hello 인증서의 서명은 hello 개인 키를 사용 하 여 생성 됩니다.

고급 장치 프로비전 흐름:

* 식별자 tooa 물리적 장치는 대개 장치 id 및/또는 장치 제조 또는 위임 하는 동안 X.509 인증서 관련된 toohello 장치를 연결 합니다.
* IoT Hub-장치 id 및 hello id 레지스트리에 IoT 허브에에서 연결 된 장치 정보에에서 해당 id 항목을 만듭니다.
* X.509 인증서 지문을 IoT Hub ID 레지스트리에 안전하게 저장

### <a name="root-certificate-on-device"></a>장치의 루트 인증서
IoT Hub와의 보안 TLS 연결을 설정 하는 동안 hello IoT 장치 hello 장치 SDK에 포함 되어 있는 루트 인증서를 사용 하 여 IoT 허브를 인증 합니다. Hello C 클라이언트 SDK에 대 한 hello 인증서 아래에 있는 hello 폴더 "\\c\\인증서" hello 리 포 루트 hello 하위 합니다. 이러한 루트 인증서는 수명이 길지만 만료되거나 해지될 수 있습니다. 방법이 있으면 업데이트 하는 hello 장치의 hello 인증서 hello 장치 못할 경우 toosubsequently toohello IoT Hub (또는 다른 클라우드 서비스)를 연결 합니다. 수단 tooupdate hello 루트 인증서를 hello IoT 장치를 배포 하는 것이 위험 효과적으로 완화 됩니다.

## <a name="securing-hello-connection"></a>Hello 연결 보안
IoT Hub와 hello IoT 장치 간의 인터넷 연결이 hello 보안 TLS (전송 계층) 표준을 사용 하 여 보호 됩니다. Azure IoT는 [TLS 1.2][lnk-tls12], TLS 1.1 및 TLS 1.0을 순서대로 지원합니다. TLS 1.0에 대한 지원은 이전 버전과의 호환성을 위해서만 제공됩니다. Hello 최상의 보안을 제공 하므로 TLS 1.2 toouse를 좋습니다.

Azure IoT Suite hello 암호 그룹을이 순서에서 다음을 지원 합니다.

| 암호화 그룹 | 길이 |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. 7680 bits RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. 3072 bits RSA) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. 7680 bits RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. 3072 bits RSA) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Hello 클라우드 보안 설정
Azure IoT Hub에서는 각 보안 키에 대해 [액세스 제어 정책][lnk-protocols]을 정의할 수 있습니다. IoT Hub 끝점 사용 권한 toogrant 액세스 tooeach의 집합을 추적 하는 hello를 사용 합니다. 사용 권한 hello 액세스 tooan 기능에 따라 IoT Hub를 제한 합니다.

* **RegistryRead**. 읽기 toohello id 레지스트리에 대 한 액세스를 부여 합니다. 자세한 내용은 [ID 레지스트리][lnk-identity-registry]를 참조하세요.
* **RegistryReadWrite**. 부여 읽기 및 쓰기 액세스 toohello id 레지스트리 자세한 내용은 [ID 레지스트리][lnk-identity-registry]를 참조하세요.
* **ServiceConnect**. 서비스 지향 통신 toocloud 및 끝점을 모니터링 액세스를 부여 합니다. 예를 들어 부여 권한을 tooback 간 클라우드 서비스 tooreceive 장치-클라우드 메시지, 클라우드-장치 메시지를 보낼 하 고 해당 배달 승인을 hello를 검색 합니다.
* **DeviceConnect**. 부여는 toodevice 연결 끝점에 액세스 합니다. 예를 들어 toosend 장치-클라우드 메시지 사용 권한을 부여 하 고 클라우드-장치 메시지를 수신 합니다. 이 권한은 장치에서 사용됩니다.

두 가지 방법으로 tooobtain **DeviceConnect** 된 IoT 허브를 사용한 사용 권한 [보안 토큰][lnk-sas-tokens]: 장치 id 키 또는 공유 액세스 키를 사용 하 여 합니다. 또한 중요 한 toonote을은 장치에서 액세스할 수 있는 모든 기능 디자인 접두사가 포함 된 끝점에 의해 노출 되는 `/devices/{deviceId}`합니다.

[서비스 구성 요소는 보안 토큰을 생성만] [ lnk-service-tokens] 를 사용 하 여 공유 액세스 정책의 hello 적절 한 사용 권한을 부여 합니다.

Azure IoT Hub 및 hello 솔루션의 일부가 될 수 있는 다른 서비스 사용자가 Azure Active Directory hello를 사용 하 여 관리할을 수 있습니다.

Azure IoT Hub를 통해 수집된 데이터는 Azure Stream Analytics, Azure Blob Storage 등과 같은 다양한 서비스에서 사용될 수 있습니다. 이러한 서비스는 관리 액세스를 허용합니다. 아래에서 이러한 서비스 및 사용 가능한 옵션에 대해 읽어보세요.

* [Azure DocumentDB][lnk-docdb]: hello 장치에 대 한 메타 데이터를 관리 하는 반 구조화 된 데이터에 대 한 확장성, 완벽 하 게 인덱싱할 데이터베이스 서비스를 프로 비전 할 같은 특성, 구성 및 보안 속성입니다. DocumentDB는 높은 성능 및 처리량 처리, 데이터의 스키마와 관계 없는 인덱싱 및 풍부한 SQL 쿼리 인터페이스를 제공합니다.
* [Azure 스트림 분석][lnk-asa]: 개발 하 고는 저렴 한 비용 솔루션 toouncover 실시간에서 얻은 분석 통찰 장치, 센서, 배포 하는 실시간 스트림 toorapidly 있습니다 수 있도록 하는 hello 클라우드에서 처리 인프라 및 응용 프로그램입니다. hello 서비스에서에서 데이터를이 완전히 관리 되는 높은 처리량, 짧은 대기 시간 및 복원 력을 확보 tooany 볼륨을 확장할 수 있습니다.
* [Azure 앱 서비스][lnk-appservices]: 클라우드 플랫폼 toobuild 강력한 웹 및 모바일 앱 toodata 아무 곳 이나;에 연결 하는 hello 클라우드 또는 온-프레미스에 있습니다. iOS, Android 및 Windows를 위한 유용한 모바일 앱을 빌드하세요. 클라우드 기반 서비스의 기본 연결 toodozens로 응용 프로그램 및 엔터프라이즈 응용 프로그램 소프트웨어와 함께 Saas () 및 엔터프라이즈 통합 합니다. 즐겨 찾는 언어 및 IDE에서 코드 (.NET, Node.js, PHP, Python 또는 Java) toobuild 웹 앱 및 Api를 그 어느 때 보다 빠릅니다.
* [논리 앱][lnk-logicapps]: hello 논리 앱 Azure 앱 서비스의 기능은 IoT 솔루션 tooyour 기존 기간 업무 시스템 통합 및 워크플로 프로세스를 자동화 합니다. 응용 프로그램 논리는 트리거에서 시작 하 고 다음 일련의 단계를 실행 하는 개발자가 toodesign 워크플로 사용 하면-규칙 및 비즈니스 프로세스와 toointegrate 강력한 커넥터를 사용 하는 작업입니다. 논리 앱의 기본 연결 tooa vast 생태계 SaaS, 클라우드 기반을 제공 하며 온-프레미스 응용 프로그램.
* [Azure blob 저장소][lnk-blob]: 장치는 toohello 클라우드를 전송 하는 hello 데이터에 대 한 경제적이 고, 신뢰할 수 있는 클라우드 저장소입니다.

## <a name="conclusion"></a>결론
이 문서에서는 Azure IoT를 사용하여 IoT 인프라를 디자인 및 배포하기 위한 구현 수준 세부 정보의 개요를 제공합니다. 각 구성 요소 toobe 보안 구성은 보안에 대 한 키 hello 전체 IoT 인프라입니다. hello 설계 선택 사항은 Azure IoT에서 사용할 수 있는 유연성과 선택; 일정 수준의 제공합니다. 그러나 각 선택 사항 보안상 문제가 있을 수 있습니다. 위험/비용 평가를 통해 이러한 각 선택 옵션을 평가하는 것이 좋습니다.

[img-overview]: media/iot-secure-your-deployment/overview.png

[lnk-security-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../articles/iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-use-x509]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/
