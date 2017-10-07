---
title: "Azure IoT Hub 보안 aaaUnderstand | Microsoft Docs"
description: "개발자 가이드-toocontrol 장치 앱과 백 엔드에 대 한 허브 tooIoT를 액세스 하는 방법입니다. 보안 토큰 및 X.509 인증서에 대한 지원 관련 정보가 포함됩니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>컨트롤 액세스 tooIoT 허브

이 문서는 IoT 허브를 보호 하기 위한 hello 옵션에 설명 합니다. IoT Hub 사용 하 여 *권한을* toogrant 액세스 tooeach IoT hub 끝점입니다. 사용 권한 hello 액세스 tooan IoT 허브 기능에 따라 제한 합니다.

이 문서에서는 다음을 설명합니다.

* hello 서로 다른 사용 권한을 있습니다 부여할 수 있는 tooa 장치 또는 백 엔드 응용 프로그램 tooaccess IoT 허브입니다.
* hello tooverify 사용 권한을 사용 하 여 인증 프로세스와 hello 토큰입니다.
* 어떻게 tooscope toolimit toospecific 리소스에 액세스 자격 증명입니다.
* X.509 인증서에 대한 IoT Hub 지원.
* 기존 장치 ID 레지스트리 또는 인증 체계를 사용하는 사용자 지정 장치 인증 메커니즘.

### <a name="when-toouse"></a>때 toouse

적절 한 사용 권한을 tooaccess는 hello IoT Hub 끝점 중 하나 있어야 합니다. 예를 들어 장치 tooIoT 허브 보내는 모든 메시지와 함께 보안 자격 증명을 포함 하는 토큰을 포함 해야 합니다.

## <a name="access-control-and-permissions"></a>액세스 제어 및 권한

권한을 부여할 수 [권한을](#iot-hub-permissions) hello 같은 방법으로 다음에서:

* **IoT hub 수준 공유 액세스 정책**. 공유 액세스 정책은 모든 조합의 [권한](#iot-hub-permissions)을 부여할 수 있습니다. Hello에 정책을 정의할 수 있습니다 [Azure 포털][lnk-management-portal], 또는 hello를 사용 하 여 프로그래밍 방식으로 [IoT 허브 리소스 공급자 REST Api][lnk-resource-provider-apis]합니다. 새로 만든된 IoT 허브에는 다음 기본 정책 hello에 있습니다.

  * **iothubowner**: 모든 사용 권한이 있는 정책입니다.
  * **service**: **ServiceConnect** 사용 권한이 있는 정책입니다.
  * **device**: **DeviceConnect** 권한이 있는 정책입니다.
  * **registryRead**: **RegistryRead** 권한이 있는 정책입니다.
  * **registryReadWrite**: **RegistryRead** 및 RegistryWrite 권한이 있는 정책입니다.
  * **장치 단위 보안 자격 증명**. 각 IoT Hub는 [ID 레지스트리][lnk-identity-registry]를 포함합니다. 이 id 레지스트리에 각 장치에 대 한 권한을 부여 하는 보안 자격 증명을 구성할 수 있습니다 **DeviceConnect** 사용 권한 범위 toohello 해당 장치 끝점을 지정 합니다.

예를 들어 일반적인 IoT 솔루션에서는 다음이 적용됩니다.

* hello 장치 관리 구성 요소가 hello를 사용 하 여 *registryReadWrite* 정책입니다.
* hello 이벤트 프로세서 구성 요소 hello를 사용 하 여 *서비스* 정책입니다.
* hello 런타임에 장치 비즈니스 논리 구성 요소 hello를 사용 하 여 *서비스* 정책입니다.
* 개별 장치에 hello IoT hub id 레지스트리에 저장 된 자격 증명을 사용 하 여 연결 합니다.

> [!NOTE]
> 자세한 내용은 [사용 권한](#iot-hub-permissions)을 참조하세요.

## <a name="authentication"></a>인증

Azure IoT Hub hello 공유 액세스 정책 및 id 레지스트리 보안 자격 증명에 대 한 토큰을 확인 하 여 tooendpoints 액세스를 부여 합니다.

대칭 키와 같은 보안 자격 증명 hello 유선으로 전송 되지 됩니다.

> [!NOTE]
> hello Azure IoT 허브 리소스 공급자 때까지 보호 Azure 구독을 통해 hello에서 모든 공급자가 [Azure 리소스 관리자][lnk-azure-resource-manager]합니다.

방법에 대 한 자세한 내용은 tooconstruct 및 사용 하 여 보안 토큰 참조 [IoT Hub 보안 토큰][lnk-sas-tokens]합니다.

### <a name="protocol-specifics"></a>프로토콜 세부 사항

지원되는 각 프로토콜(예: MQTT, AMQP 및 HTTP)은 다양한 방식으로 토큰을 전송합니다.

MQTT를 사용할 때는 hello 연결 패킷 같습니다 hello deviceId hello ClientId, {iothubhostname} / {deviceId} hello 사용자 이름 필드 및 hello 암호 필드에는 SAS 토큰에 있습니다. {iothubhostname}는 hello IoT 허브 (예를 들어 contoso.azure devices.net)의 전체 CName hello 해야 합니다.

[AMQP][lnk-amqp]을 사용하는 경우 IoT Hub는 [SASL PLAIN][lnk-sasl-plain] 및 [AMQP 클레임 기반-보안][lnk-cbs]을 지원합니다.

표준 hello를 지정 하는 경우 AMQP 클레임 기반-보안에서는 어떻게 tootransmit 이러한 토큰입니다.

SASL 일반 hello **username** 될 수 있습니다.

* `{policyName}@sas.root.{iothubName}` IoT Hub 수준 토큰을 사용하는 경우입니다.
* `{deviceId}@sas.{iothubname}` 장치 범위 토큰을 사용하는 경우입니다.

두 경우 모두 hello 암호 필드가 hello 토큰에 설명 된 대로 [IoT Hub 보안 토큰][lnk-sas-tokens]합니다.

Hello에 유효한 토큰을 포함 하 여 인증을 구현 하는 HTTP **권한 부여** 요청 헤더입니다.

#### <a name="example"></a>예제

사용자 이름(DeviceId는 대/소문자 구분): `iothubname.azure-devices.net/DeviceId`

암호 (hello로 생성 SAS 토큰 [장치 탐색기] [ lnk-device-explorer] 도구):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> hello [Azure IoT Sdk] [ lnk-sdks] toohello 서비스에 연결할 때 토큰을 자동으로 생성 합니다. 경우에 따라 Azure IoT Sdk hello 모든 hello 프로토콜 또는 hello 인증 방법을 모두 지원 하지 않습니다.

### <a name="special-considerations-for-sasl-plain"></a>SASL PLAIN에 대한 특별 고려 사항

SASL 일반 AMQP를 사용할 경우 tooan IoT 허브를 연결 하는 클라이언트 각 TCP 연결에 대 한 단일 토큰을 사용할 수 있습니다. Hello 토큰이 만료 되 면 hello TCP 연결 hello 서비스에서 연결을 해제 하 고 다시 연결을 트리거합니다. 이 동작을 하지는 백 엔드 응용 프로그램에 대 한 문제가 발생 하는 동안 다음 이유로 hello에 대 한 장치 응용 프로그램에 대 한 손상을:

* 게이트웨이가 일반적으로 많은 장치를 대신하여 연결됩니다. SASL 일반을 사용 하 여, tooan IoT 허브 연결 하는 각 장치에 대 한 별도 TCP 연결 toocreate 유지 됩니다. 이 시나리오는 상당히 hello 전원 및 네트워킹 리소스 사용을 증가 하 고 각 장치 연결의 hello 대기 시간을 늘립니다.
* 리소스 제한 된 장치는 부정적인 영향을 줄 리소스 tooreconnect 증가 hello 사용 하 여 각 토큰 만료 된 후입니다.

## <a name="scope-iot-hub-level-credentials"></a>IoT Hub 수준 자격 증명의 범위 지정

제한된 리소스 URI로 토큰을 만들어 IoT Hub 수준 보안 정책의 범위를 지정할 수 있습니다. 장치에서 hello toosend 장치-클라우드 메시지를 끝점은 예를 들어 **/devices/ {deviceId} / 메시지/이벤트**합니다. IoT 허브 수준 공유 액세스 정책으로 사용할 수도 있습니다 **DeviceConnect** 권한 toosign 인 resourceURI은 토큰 **/devices/ {deviceId}**합니다. 이 방법은 장치를 대신 하 여 사용 가능한 toosend 메시지만 있는 토큰을 만드는 데 **deviceId**합니다.

이 메커니즘은 유사한 toohello [이벤트 허브 게시자 정책][lnk-event-hubs-publisher-policy], tooimplement 사용자 지정 인증 방법 수 있도록 합니다.

## <a name="security-tokens"></a>보안 토큰

보안을 사용 하는 IoT Hub tooauthenticate 장치 토큰 및 hello 통신 중에 키 보내기 tooavoid를 서비스 합니다. 또한 보안 토큰은 유효 기간 및 범위가 제한됩니다. [Azure IoT SDK][lnk-sdks]는 특별한 구성이 필요하지 않고 토큰을 자동으로 생성합니다. 일부 시나리오는 toogenerate 요구 하 고 직접 보안 토큰을 사용 하 여 수행 합니다. 이 시나리오에는 다음이 포함됩니다.

* hello MQTT, AMQP 또는 HTTP 표면 hello 직접 사용 합니다.
* 에 설명 된 대로 구현 hello 토큰 서비스 패턴 hello [사용자 지정 장치 인증][lnk-custom-auth]합니다.

IoT Hub에서는 장치 tooauthenticate IoT 허브를 사용 하 여 [X.509 인증서][lnk-x509]합니다.

### <a name="security-token-structure"></a>보안 토큰 구조

IoT 허브에서 보안 토큰 toogrant 액세스 시간 제한 toodevices 및 서비스 toospecific 기능을 사용합니다. tooget 권한 부여 tooconnect tooIoT 허브, 장치 및 서비스는 공유 액세스 또는 대칭 키로 서명 하는 보안 토큰을 전송 해야 합니다. 이러한 키는 hello id 레지스트리에에서 장치 id로 저장 됩니다.

공유 액세스 키 부여 액세스 tooall hello 관련 된 기능 hello 공유 액세스 정책 권한과로 토큰에 서명 합니다. 장치 id의 대칭 키에 부여 hello로 토큰에 서명 **DeviceConnect** 연결 된 장치 id hello에 대 한 사용 권한이 있습니다.

hello 보안 토큰 형식에 따라 hello에 있습니다.

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

다음은 hello 예상 되는 값입니다.

| 값 | 설명 |
| --- | --- |
| {signature} |hmac-sha256 서명 문자열 hello 폼의: `{URL-encoded-resourceURI} + "\n" + expiry`합니다. **중요 한**: hello 키는에서 base64 디코딩된 이며 키 tooperform hello hmac-sha256 계산으로 사용 합니다. |
| {resourceURI} |접두사 (세그먼트)에 의해 hello IoT 허브 (프로토콜 제외)의 호스트 이름으로 시작이 토큰으로 액세스할 수 있는 hello 끝점의 URI입니다. 예를 들어 `myHub.azure-devices.net/devices/device1` |
| {expiry} |1970 년 1 월 1에 hello epoch 00시: 00 UTC 이후의 초 수에 대 한 문자열을 u t f 8입니다. |
| {URL-encoded-resourceURI} |Hello 소문자 리소스 URI의 URL 인코딩을 이하인 경우 |
| {policyName} |이 토큰이 참조 하는 hello 공유 액세스 정책 toowhich의 hello 이름입니다. 경우 hello 토큰 toodevice 레지스트리 자격 증명을 참조합니다. |

**접두사에 대 한 참고**: hello URI 접두사 문자가 아닌에 세그먼트에 의해 계산 됩니다. 예를 들어 `/a/b`는 `/a/b/c`에 대한 접두사이지만 `/a/bc`에 대한 접두사는 아닙니다.

hello 다음 Node.js 조각 표시 호출 하는 함수 **generateSasToken** 계산 hello hello 입력에서 토큰을 `resourceUri, signingKey, policyName, expiresInMins`합니다. 다음 섹션에서는 hello tooinitialize hello hello 다른 토큰에 대 한 서로 다른 입력 사례를 사용 하는 방법을 자세히 설명 합니다.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

비교로 보안 토큰은 해당 하는 Python 코드 toogenerate hello:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Hello hello 토큰의 유효 기간 IoT Hub 컴퓨터에서 유효성을 검사 하므로 hello 토큰을 생성 하는 hello 컴퓨터의 hello 클록에 hello 드리프트 최소화 해야 합니다.

### <a name="use-sas-tokens-in-a-device-app"></a>장치 앱에서 SAS 토큰 사용

두 가지 방법으로 tooobtain **DeviceConnect** IoT Hub와 보안 토큰 사용 권한: 사용 하 여는 [hello identity 레지스트리에서 대칭 장치 키](#use-a-symmetric-key-in-the-identity-registry), 사용 또는 [공유액세스키](#use-a-shared-access-policy).

장치에서 액세스할 수 있는 모든 기능이 `/devices/{deviceId}` 접두사가 있는 끝점에서 의도적으로 노출된다는 것을 기억하십시오.

> [!IMPORTANT]
> IoT Hub 특정 장치를 인증 하는 hello 유일한 방법은 hello 장치 id 대칭 키를 사용 중입니다. 경우 공유 액세스 정책을 사용 하는 tooaccess 장치 기능 때 hello 솔루션으로 신뢰할 수 있는 하위 구성 요소일 hello 보안 토큰을 발급 하는 hello 구성 요소를 고려해 야 합니다.

hello 장치 연결 끝점 (관계 없이 hello 프로토콜)은:

| 끝점 | 기능 |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |장치-클라우드 메시지를 보냅니다. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |클라우드-장치 메시지를 받습니다. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Hello id 레지스트리에에서 대칭 키를 사용 합니다.

장치 id를 대칭 키 toogenerate 토큰을 사용할 경우 hello policyName (`skn`) hello 토큰의 요소가 생략 됩니다.

예를 들어 토큰 생성 tooaccess 모든 장치 기능 매개 변수 뒤 hello 있어야 합니다.

* 리소스 URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* 서명 키: hello에 대 한 모든 대칭 키 `{device id}` id
* 정책 이름 없음,
* 임의의 만료 시간.

Node.js 함수 앞에 오는 hello를 사용 하는 예제는 다음과 같습니다.

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

장치 1에 대 한 액세스 tooall 기능 권한을 부여 하는 hello 결과 다음과 같습니다.

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> 것은 가능한 toogenerate hello.NET을 사용 하 여 SAS 토큰 [장치 탐색기] [ lnk-device-explorer] 도구 또는 플랫폼 간 노드 기반 환영 [iothub 탐색기] [ lnk-iothub-explorer] 명령줄 유틸리티입니다.

### <a name="use-a-shared-access-policy"></a>공유 액세스 정책 사용

공유 액세스 정책에서 토큰을 만들 때 설정 hello `skn` hello 정책 필드 toohello 이름입니다. 이 정책은 hello 권한을 부여 해야 **DeviceConnect** 권한.

공유 액세스 정책 tooaccess 장치 기능을 사용 하기 위한 두 가지 주요 시나리오를 hello는:

* [클라우드 프로토콜 게이트웨이][lnk-endpoints]
* [토큰 서비스] [ lnk-custom-auth] tooimplement 사용자 지정 인증 체계를 사용 합니다.

Hello 이후 공유 액세스 정책 잠재적으로 권한을 부여할 수 액세스 tooconnect 모든 장치로 보안 토큰을 만드는 경우 중요 한 toouse hello 올바른 리소스 URI에는. 이 설정은 tooscope hello 토큰 tooa 특정 장치 hello 리소스 URI를 사용 하 여를 포함 하는 토큰 서비스에 대 한 특히 유용 합니다. 프로토콜 게이트웨이는 모든 장치에 대한 트래픽을 이미 조정하므로 관련성이 떨어집니다.

예를 들어 미리 만든 hello를 사용 하 여 토큰 서비스 공유 액세스 정책 이라는 **장치** 매개 변수 뒤 hello를 사용 하 여 토큰을 만듭니다.

* 리소스 URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* 서명 키: hello의 hello 키 중 하나 `device` 정책
* 정책 이름: `device`,
* 임의의 만료 시간.

Node.js 함수 앞에 오는 hello를 사용 하는 예제는 다음과 같습니다.

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

장치 1에 대 한 액세스 tooall 기능 권한을 부여 하는 hello 결과 다음과 같습니다.

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

프로토콜 게이트웨이 수 설정 하면 모든 장치 리소스 URI를 너무 hello에 대 한 토큰 같은 hello를 사용 하 여`myhub.azure-devices.net/devices`합니다.

### <a name="use-security-tokens-from-service-components"></a>서비스 구성 요소에서 보안 토큰 사용

서비스 구성 요소 수만 이전에 설명한 대로 hello 적절 한 사용 권한을 부여 하는 공유 액세스 정책을 사용 하 여 보안 토큰을 생성할 수 있습니다.

다음은 hello 끝점에서 노출 하는 hello 서비스 기능입니다.

| 끝점 | 기능 |
| --- | --- |
| `{iot hub host name}/devices` |장치 ID를 만들기, 업데이트, 검색 및 삭제합니다. |
| `{iot hub host name}/messages/events` |장치-클라우드 메시지를 받습니다. |
| `{iot hub host name}/servicebound/feedback` |클라우드-장치 메시지에 대한 피드백을 받습니다. |
| `{iot hub host name}/devicebound` |클라우드-장치 메시지를 보냅니다. |

예를 들어 미리 만든 hello를 사용 하 여 생성 하는 서비스 공유 액세스 정책 이라는 **registryRead** 매개 변수 뒤 hello를 사용 하 여 토큰을 만듭니다.

* 리소스 URI: `{IoT hub name}.azure-devices.net/devices`,
* 서명 키: hello의 hello 키 중 하나 `registryRead` 정책
* 정책 이름: `registryRead`,
* 임의의 만료 시간.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

계정이 나 부여 액세스 tooread 모든 장치 id, 인 hello 결과 다음과 같습니다.

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>지원되는 X.509 인증서

IoT Hub와 모든 X.509 인증서 tooauthenticate 장치를 사용할 수 있습니다. 인증서는 다음을 포함합니다.

* **기존 X.509 인증서**. 장치에 X.509 인증서가 이미 연결되어 있을 수 있습니다. hello 장치에서이 인증서 tooauthenticate IoT Hub와 사용할 수 있습니다.
* **자체 생성 및 자체 서명 X-509 인증서**. 장치 제조업체 또는 사내 deployer 수 이러한 인증서를 생성 하 고 hello 장치의 hello 해당 개인 키 (및 인증서)를 저장 합니다. 이 목적을 위해 [OpenSSL][lnk-openssl] 및 [Windows SelfSignedCertificate][lnk-selfsigned] 유틸리티와 같은 도구를 사용할 수 있습니다.
* **CA 서명 X.509 인증서**. 장치 tooidentify IoT Hub와 인증 하 고, 생성 및 서명 인증 기관 (CA)에서 X.509 인증서를 사용할 수 있습니다. IoT Hub에만 표시 해당 hello 지문을 확인 hello 구성 된 지문과 일치 합니다. IotHub은 hello 인증서 체인 유효성을 검사 하지 않습니다.

장치는 인증을 위해 X.509 인증서 또는 보안 토큰 중 하나만 사용할 수 있습니다.

### <a name="register-an-x509-certificate-for-a-device"></a>장치에 대해 X.509 인증서 등록

hello [C#에 대 한 Azure IoT 서비스 SDK] [ lnk-service-sdk] (버전 1.0.8+) 인증을 위해 X.509 인증서를 사용 하는 장치 등록을 지원 합니다. 장치 가져오기/내보내기 같은 기타 API에서도 X.509 인증서를 지원합니다.

### <a name="c-support"></a>C\# 지원

hello **RegistryManager** 클래스는 프로그래밍 방식으로 tooregister 장치를 제공 합니다. 특히 hello **AddDeviceAsync** 및 **UpdateDeviceAsync** 메서드를 사용 하면 tooregister 및 hello id 레지스트리에 IoT Hub에서에서 장치를 업데이트 합니다. 이러한 두 메서드는 입력으로 **Device** 인스턴스를 수락합니다. hello **장치** 클래스를 포함 한 **인증** toospecify 기본 및 보조 X.509 인증서 지문을 지정할 수 있는 속성입니다. hello 지문 (DER 이진 인코딩을 사용 하 여 저장) hello X.509 인증서의 sha-1 해시를 나타냅니다. 기본 지문 또는 보조 지문 또는 둘 다 지정 하는 hello 선택할을 수 있습니다. 기본 및 보조 지문이 지원 되는 toohandle 인증서 롤오버 시나리오입니다.

> [!NOTE]
> IoT Hub 필요 하지 않거나 hello 전체 X.509 인증서를 hello 지문만 저장 합니다.

다음은 샘플 C\# 코드 조각 tooregister X.509 인증서를 사용 하는 장치:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>런타임 작업 중에 X.509 인증서 사용

hello [Azure IoT 장치 SDK for.net] [ lnk-client-sdk] (버전 1.0.11+) hello 사용 되는 X.509 인증서를 지원 합니다.

### <a name="c-support"></a>C\# 지원

클래스를 hello **DeviceAuthenticationWithX509Certificate** 지원 hello 생성 **DeviceClient** X.509 인증서를 사용 하 여 인스턴스. hello X.509 인증서 hello 개인 키를 포함 하는 hello PFX (PKCS #12) 형식 이어야 합니다.

다음은 샘플 코드 조각입니다.

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>사용자 지정 장치 인증

Hello IoT 허브를 사용할 수 있습니다 [id 레지스트리에] [ lnk-identity-registry] tooconfigure-장치 보안 자격 증명 및 액세스 제어를 사용 하 여 [토큰] [ lnk-sas-tokens] . IoT 솔루션 이미 있으면 레지스트리 및/또는 인증 구성표를 사용자 지정 id를 만드는 것이 좋습니다는 *토큰 서비스* toointegrate IoT Hub와이 인프라입니다. 이러한 방식으로 솔루션에서 다른 IoT 기능을 사용할 수 있습니다.

토큰 서비스는 사용자 지정 클라우드 서비스입니다. IoT Hub 사용 하 여 *공유 액세스 정책* 와 **DeviceConnect** 권한 toocreate *장치 범위* 토큰입니다. 이러한 토큰을 장치 tooconnect tooyour IoT 허브를 사용 하도록 설정 합니다.

![Hello 토큰 서비스 패턴의 단계][img-tokenservice]

Hello hello 토큰 서비스 패턴의 주요 단계는 다음과 같습니다.

1. IoT Hub에 대한 **DeviceConnect** 권한으로 IoT Hub 공유 액세스 정책을 만듭니다. Hello에이 정책을 만들 수 있습니다 [Azure 포털] [ lnk-management-portal] 또는 프로그래밍 방식으로 합니다. hello 토큰 서비스를 만들이 정책 toosign hello 토큰을 사용 합니다.
1. 장치가 IoT hub tooaccess를 필요한 토큰 서비스에서 서명 된 토큰을 요청 합니다. hello 장치 hello 토큰 서비스 toocreate hello 토큰을 사용 하도록 사용자 지정 id 레지스트리/인증 체계 toodetermine hello 장치 id와 인증할 수 있습니다.
1. hello 토큰 서비스는 토큰을 반환합니다. hello 토큰은 사용 하 여 만든 `/devices/{deviceId}` 으로 `resourceURI`와 `deviceId` 인증 된 hello 장치로 합니다. hello 토큰 서비스는 hello 공유 액세스 정책 tooconstruct hello 토큰을 사용합니다.
1. hello 장치 hello IoT 허브를 사용 하 여 직접 hello 토큰을 사용합니다.

> [!NOTE]
> Hello.NET 클래스를 사용할 수 [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] Java 클래스 hello 또는 [IotHubServiceSasToken] [ lnk-java-sas] toocreate 토큰 토큰 서비스입니다.

hello 토큰 서비스는 원하는 대로 hello 토큰 만료를 설정할 수 있습니다. Hello 토큰이 만료 되 면 hello IoT hub 서버 hello 장치 연결 합니다. 그런 다음 hello 장치 hello 토큰 서비스에서 새 토큰을 요청 해야 합니다. 짧은 만료 시간 hello 장치와 hello 토큰 서비스에서 hello 부하를 증가합니다.

장치 tooconnect tooyour 허브에 대 한 계속 추가 해야 toohello IoT Hub id 레지스트리에-토큰과 장치 키 tooconnect 하지 hello 장치가 사용 하는 경우에 합니다. 따라서 hello에서 장치 id를 사용 하지 않도록 설정 하거나 설정 하 여 toouse 장치 액세스 제어를 계속할 수 있습니다 [id 레지스트리에][lnk-identity-registry]합니다. 이 방법은 토큰을 사용 하 여 긴 만료 시간을 유지 하면서 hello 위험을 완화 합니다.

### <a name="comparison-with-a-custom-gateway"></a>사용자 지정 게이트웨이와 비교

hello 토큰 서비스 패턴은 hello 권장 방법은 tooimplement IoT Hub와 사용자 지정 id 레지스트리/인증 체계입니다. IoT Hub toohandle 계속 하기 때문에이 패턴은 권장 hello 솔루션 트래픽의 대부분 합니다. 그러나 hello 사용자 지정 인증 스키마는 hello 프로토콜 얽혀 하므로, 경우 필요할 수 있습니다는 *사용자 지정 게이트웨이* tooprocess 트래픽 hello 모든 합니다. 이러한 시나리오의 예는 [TLS(전송 계층 보안) 및 PSK(미리 공유한 키)][lnk-tls-psk]를 사용합니다. 자세한 내용은 참조 hello [프로토콜 게이트웨이] [ lnk-protocols] 항목입니다.

## <a name="reference-topics"></a>참조 항목:

hello 다음 참조 항목 제공 제어 액세스 tooyour IoT 허브에 대 한 자세한 내용은 합니다.

## <a name="iot-hub-permissions"></a>IoT Hub 권한

hello 다음 표에서 hello 사용 권한을 나열 toocontrol 액세스 tooyour IoT 허브를 사용할 수 있습니다.

| 사용 권한 | 참고 사항 |
| --- | --- |
| **RegistryRead** |읽기 toohello id 레지스트리에 대 한 액세스를 부여 합니다. 자세한 내용은 [ID 레지스트리][lnk-identity-registry]를 참조하세요. <br/>이 사용 권한은 백 엔드 클라우드 서비스에서 사용됩니다. |
| **RegistryReadWrite** |부여 읽기 및 쓰기 액세스 toohello id 레지스트리 자세한 내용은 [ID 레지스트리][lnk-identity-registry]를 참조하세요. <br/>이 사용 권한은 백 엔드 클라우드 서비스에서 사용됩니다. |
| **ServiceConnect** |서비스 지향 통신 toocloud 및 끝점을 모니터링 액세스를 부여 합니다. <br/>Tooreceive 장치-클라우드 메시지를 권한 부여 클라우드-장치 메시지 및 검색 hello 해당 배달 승인을 보냅니다. <br/>파일에 대 한 부여 권한 tooretrieve 배달 승인을 업로드 합니다. <br/>권한 부여 권한 tooaccess 장치 트윈스 tooupdate 태그 및 해당된 속성에 보고 된 속성을 검색 하 고 쿼리를 실행 합니다. <br/>이 사용 권한은 백 엔드 클라우드 서비스에서 사용됩니다. |
| **DeviceConnect** |부여는 toodevice 연결 끝점에 액세스 합니다. <br/>권한 부여 권한 toosend 장치-클라우드 메시지 및 클라우드-장치 메시지를 수신 합니다. <br/>사용 권한 tooperform 파일 업로드 장치에서 부여 하 고 있습니다. <br/>권한 부여 권한 tooreceive 장치 원하는 이중 속성 알림 및 업데이트 장치로 이중 보고 된 속성입니다. <br/>권한 부여 권한 tooperform 파일을 업로드합니다. <br/>이 권한은 장치에서 사용됩니다. |

## <a name="additional-reference-material"></a>추가 참조 자료

Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.

* [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.
* [제한 및 할당량] [ lnk-quotas] hello 할당량을 설명 하 고 toohello IoT 허브 서비스에 적용 되는 동작을 조정 합니다.
* [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.
* [IoT Hub 쿼리 언어] [ lnk-query] 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용할 수는 hello 쿼리 언어에 설명 합니다.
* [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계

Toocontrol IoT Hub를 액세스 하는 방법을 파악 했으므로, 이제 hello 다음 IoT 허브 개발자 가이드 항목에에서 관심이 있을 수 있습니다.

* [장치 트윈스 toosynchronize 상태 및 구성 사용][lnk-devguide-device-twins]
* [장치에서 직접 메서드 호출][lnk-devguide-directmethods]
* [여러 장치에서 jobs 예약][lnk-devguide-jobs]

이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서를 따라 hello에 관심이 있을 수 있습니다.

* [Azure IoT Hub 시작][lnk-getstarted-tutorial]
* [IoT Hub와 toosend 클라우드-장치 메시지 하는 방법][lnk-c2d-tutorial]
* [어떻게 tooprocess IoT Hub 장치-클라우드 메시지][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
