---
title: "Java 통해 Azure IoT 지 모듈 aaaCreate | Microsoft Docs"
description: "이 자습서는 배포용 데이터 변환기 사용 하 여 모듈 toowrite 최신 Azure IoT 가장자리 Maven 패키지 hello 하는 방법을 보여줍니다."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a>Java를 사용하여 Azure IoT Edge 모듈 만들기

이 자습서는 Java에서 Azure IoT Edge에 대한 모듈을 빌드하는 방법을 소개합니다.

이 자습서에서는 단계별로 환경 설정 방법과 toowrite는 [배포용](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) hello 최신 Azure IoT 가장자리 Maven 패키지를 사용 하 여 데이터 변환기 모듈입니다.

## <a name="prerequisites"></a>필수 조건

이 섹션에서는 IoT Edge 모듈 개발을 위한 환경을 설정하게 됩니다. Tooboth 적용 *64 비트 Windows* 및 *64 비트 Linux (Debian Ubuntu/8)* 운영 체제.

hello 소프트웨어 다음이 필요 합니다.

* [Git 클라이언트](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html)

명령줄 터미널 창 및 복제 hello를 다음 저장소를 엽니다.

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>전체 아키텍처

hello Azure IoT 가장자리 플랫폼 hello을 과도 하 게 채택 [본 Neumann 아키텍처](https://en.wikipedia.org/wiki/Von_Neumann_architecture)합니다. 즉, hello 전체 Azure IoT 가장자리 아키텍처에는 입력을 처리 하 고 출력을 생성 하는 시스템 및 각 개별 모듈 아주 작은 입력-출력 하위 시스템 이기도 합니다. 이 자습서에서는 다음 두 개의 모듈 hello를 소개 합니다.

1. 시뮬레이션된 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 신호를 수신하여 형식이 지정된 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지로 변환하는 모듈입니다.
2. 받은 hello 출력 하는 모듈 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지입니다.

hello 다음 이미지가 표시 hello 일반적인이 프로젝트에 대 한 종단 간 데이터 흐름:

![3개의 모듈 간의 데이터 흐름](media/iot-hub-iot-edge-create-module/dataflow.png "입력: 시뮬레이션된 BLE 모듈, 프로세서: 변환기 모듈, 출력: 프린터 모듈")

## <a name="understanding-hello-code"></a>Hello 코드 이해

### <a name="maven-project-structure"></a>Maven 프로젝트 구조

Azure IoT 가장자리 패키지 Maven을 기반으로 하기 원하므로 해야 toocreate 포함 하는 일반적인 Maven 프로젝트 구조는 `pom.xml` 파일입니다.

hello POM에서에서 상속 hello `com.microsoft.azure.gateway.gateway-module-base` hello 런타임 이진 파일, hello 게이트웨이 구성 파일 경로 및 hello 실행 동작을 포함 하는 모듈 프로젝트에 필요한 hello 종속성의 모든 선언 하는 패키지입니다. 이 많은 시간을 구성할 필요가 및 hello 필요 toowrite 제거 및 반복 해 서 수백 줄의 코드를 다시 작성 해야 합니다.

필요한 hello 종속성/플러그 인 및 hello 다음 코드 조각에에서 나와 있는 것 처럼 모듈에서 사용 하는 hello 구성 파일 toobe의 hello 이름을 선언 하 여 tooupdate pom.xml 파일 필요 합니다.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Azure IoT Edge 모듈에 대한 기본적인 이해

Azure IoT Edge 모듈을 입력을 수신하고, 처리하며, 출력을 생성하는 작업을 수행하는 데이터 프로세서로 간주할 수 있습니다.

하드웨어 (예: 동작 탐지기) 데이터, 다른 모듈 또는 (예: 타이머가 정기적으로 생성 된 난수) 다른 작업에서 메시지 hello 입력 수 있습니다.

비슷한 toohello 입력이 출력을 hello, 하드웨어 동작 (예: led가 깜박입니다.이 hello) 메시지 tooother 모듈, 기타 (예: 인쇄 toohello 콘솔)를 트리거할 수 있습니다.

모듈은 `com.microsoft.azure.gateway.messaging.Message` 클래스를 사용하여 서로 통신합니다. hello **콘텐츠** 의 `Message` 는 모든 종류의 원하는 데이터를 표시할 수 있는 바이트 배열입니다. **속성** hello에 사용할 수 있습니다 `Message` 되며 문자열을 문자열 매핑 하기만 합니다. 으로 생각할 수 **속성** HTTP 요청 또는 파일의 hello 메타 데이터에 대 한 hello 머리글로 합니다.

Toocreate 새 모듈 클래스에서 상속 하는 순서 toodevelop Java에 대 한 Azure IoT 가장자리 모듈에에서 필요한 `com.microsoft.azure.gateway.core.GatewayModule` hello 필요한 추상 메서드를 구현 하 고 `receive()` 및 `destroy()`합니다. 이 시점에서 선택할 수도 있습니다 (옵션) tooimplement hello `start()` 또는 `create()` 메서드 뿐입니다. 다음 코드 조각 hello tooget 시작 Azure IoT 지 모듈을 작성 하는 방법을 보여 줍니다.

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a>변환기 모듈

| 입력                    | 프로세서                              | 출력                 | 원본 파일            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| 온도 데이터 메시지 | 새 JSON 메시지의 구문 분석 및 생성 | JSON 메시지 구조 | `ConverterModule.java` |

이 모듈은 일반적인 Azure IoT Edge 모듈입니다. 다른 모듈에서 온도 메시지를 수락 하기 (하드웨어 모듈의 경우,이 경우에 시뮬레이트된 배포용 모듈 또는); 다음 구조화 tooa JSON 메시지 (hello 메시지 ID, tootrigger hello 온도 경고 해야 하는지 여부의 hello 속성을 설정 추가 및 포함 등)에 hello 온도 메시지를 정규화 합니다.

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a>프린터 모듈

| 입력                          | 프로세서 | 출력                     | 원본 파일          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| 다른 모듈의 모든 메시지 | 해당 없음       | Hello 메시지 tooconsole 로그 | `PrinterModule.java` |

이것이 받은 hello 메시지 toohello 터미널 윈도우를 출력 하는 간단 하 고 자체 설명 모듈입니다.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Azure IoT Edge 구성

hello 모듈을 실행 하기 전에 hello 마지막 단계에는 Azure IoT 가장자리 tooconfigure hello 및 모듈 간에 tooestablish hello 연결입니다.

먼저 다음 해야 toodeclare에서 참조 될 수 있는 (다른 언어의 Azure IoT 가장자리 지원 로더)부터 우리의 Java 로더 해당 `name` hello 단원의 나중에 있습니다.

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

우리의 로더를 선언 했습니다 되 면 필요 합니다 toodeclare 뿐 우리 모듈입니다. 비슷한 toodeclaring hello 로더도 참조할 수 하 여 자신의 `name` 특성입니다. Toospecify hello 로더 사용 해야 (있어야 하 고 hello 하나 앞에 정의) 필요한 모듈을 선언할 때 진입점 (모듈의 hello 정규화 된 클래스 이름 이어야 함) 각 모듈에 대 한 hello 및 합니다. hello `simulated_device` hello Azure IoT 가장자리 코어 런타임 패키지에 포함 된 네이티브 모듈입니다. 항상 포함할지 `args` hello 경우에 JSON 파일에서 `null`합니다.

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

Hello 구성의 hello 끝 hello 연결을 설정 합니다. 각 연결은 `source` 및 `sink`로 표현됩니다. 미리 정의된 모듈을 모두 참조해야 합니다. hello 출력 메시지의 `source` 모듈의 toohello 입력 전달 `sink` 모듈입니다.

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a>Hello 모듈을 실행합니다.

사용 하 여 `mvn package` toobuild hello에 모든 `target/` 폴더입니다. `mvn clean package`도 클린 빌드에 좋습니다.

사용 하 여 `mvn exec:exec` toorun hello Azure IoT 가장자리 하 고 hello 온도 데이터와 모든 hello 속성은 고정 된 요금이 인쇄 toohello 콘솔을 준수 해야 합니다.

Tooterminate hello 응용 프로그램을 사용 하도록 하려는 경우 키를 눌러 `<Enter>` 키입니다.

> [!IMPORTANT]
> 좋지 toouse Ctrl + C tooterminate hello IoT 가장자리 게이트웨이 응용 프로그램입니다. Hello 프로세스 tooterminate 비정상적으로 생길 수 있습니다.

