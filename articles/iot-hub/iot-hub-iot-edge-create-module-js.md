---
title: "Node.js와 함께 Azure IoT 지 모듈 aaaCreate | Microsoft Docs"
description: "이 자습서에서는 toowrite는 배포용 데이터 변환기 사용 하 여 모듈의 최신 Azure IoT 가장자리 NPM 패키지 및 Yeoman hello 어떻게 생성기입니다."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="792d8-103">Node.js를 사용하여 Azure IoT Edge 모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="792d8-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="792d8-104">이 자습서에서는 어떻게 toocreate j에서 Azure IoT 가장자리에 대 한 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="792d8-105">이 자습서에서는 연습 환경 설정 방법과 toowrite는 [배포용](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) hello 최신 Azure IoT 가장자리 NPM 패키지를 사용 하 여 데이터 변환기 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="792d8-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="792d8-106">Prerequisites</span></span>

<span data-ttu-id="792d8-107">이 섹션에서는 IoT Edge 모듈 개발을 위한 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="792d8-108">Tooboth 적용 *64 비트 Windows* 및 *64 비트 Linux (Ubuntu 14 +)* 운영 체제.</span><span class="sxs-lookup"><span data-stu-id="792d8-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="792d8-109">hello 소프트웨어 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-109">hello following software is required:</span></span>
* <span data-ttu-id="792d8-110">[Git 클라이언트](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="792d8-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="792d8-111">[노드 LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="792d8-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="792d8-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="792d8-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="792d8-113">아키텍처</span><span class="sxs-lookup"><span data-stu-id="792d8-113">Architecture</span></span>

<span data-ttu-id="792d8-114">hello Azure IoT 가장자리 플랫폼 hello을 과도 하 게 채택 [본 Neumann 아키텍처](https://en.wikipedia.org/wiki/Von_Neumann_architecture)합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="792d8-115">즉, hello 전체 Azure IoT 가장자리 아키텍처에는 입력을 처리 하 고 출력을 생성 하는 시스템 및 각 개별 모듈 아주 작은 입력-출력 하위 시스템 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="792d8-116">이 자습서에서는 다음 두 개의 모듈 hello 유도:</span><span class="sxs-lookup"><span data-stu-id="792d8-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="792d8-117">시뮬레이션된 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 신호를 수신하여 형식이 지정된 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지로 변환하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="792d8-118">받은 hello 출력 하는 모듈 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="792d8-119">hello 다음 이미지가 표시 hello tooend dataflow이이 프로젝트에 대 한 일반적인 끝:</span><span class="sxs-lookup"><span data-stu-id="792d8-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="792d8-120">![3개의 모듈 간의 데이터 흐름](media/iot-hub-iot-edge-create-module/dataflow.png "입력: 시뮬레이션된 BLE 모듈, 프로세서: 변환기 모듈, 출력: 프린터 모듈")</span><span class="sxs-lookup"><span data-stu-id="792d8-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="792d8-121">Hello 환경 설정</span><span class="sxs-lookup"><span data-stu-id="792d8-121">Set up hello environment</span></span>
<span data-ttu-id="792d8-122">아래 보여줍니다 tooquickly 설정 방법 환경 toostart toowrite JS와 첫 번째 배포용 변환기 모듈.</span><span class="sxs-lookup"><span data-stu-id="792d8-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="792d8-123">모듈 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="792d8-123">Create module project</span></span>
1. <span data-ttu-id="792d8-124">명령줄 창을 열고 `yo az-iot-gw-module`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="792d8-125">모듈 프로젝트의 hello 화면 toofinish hello 초기화 시 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="792d8-126">프로젝트 구조</span><span class="sxs-lookup"><span data-stu-id="792d8-126">Project structure</span></span>
<span data-ttu-id="792d8-127">JS 모듈 프로젝트 hello 다음과 같은 구성 요소가 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="792d8-128">`modules`-hello JS 모듈 소스 파일을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="792d8-129">Hello 기본 대체 `sensor.js` 및 `printer.js` 모듈 파일을 직접 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="792d8-130">`app.js`-hello 항목 파일 toostart hello 가장자리 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="792d8-131">`gw.config.json`-hello 구성 파일 toocustomize hello 모듈 toobe 가장자리에서 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="792d8-132">`package.json`-hello 모듈 프로젝트에 대 한 메타 데이터 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="792d8-133">`README.md`-hello 모듈 프로젝트에 대 한 기본 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="792d8-134">패키지 파일</span><span class="sxs-lookup"><span data-stu-id="792d8-134">Package file</span></span>

<span data-ttu-id="792d8-135">이 `package.json` hello 이름, 버전, 항목, 스크립트, 런타임 및 개발 종속성을 포함 하는 모듈 프로젝트에 필요한 모든 hello 메타 데이터 정보를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="792d8-136">코드 조각에 나와 있는 다음 방법을 tooconfigure 배포용 변환기에 대 한 샘플 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a><span data-ttu-id="792d8-137">입력 파일</span><span class="sxs-lookup"><span data-stu-id="792d8-137">Entry file</span></span>
<span data-ttu-id="792d8-138">hello `app.js` hello 방식으로 tooinitialize hello 가장자리 인스턴스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="792d8-139">여기 필요 하지 않습니다 toomake 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-139">Here we don't need toomake any change.</span></span>

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a><span data-ttu-id="792d8-140">모듈의 인터페이스</span><span class="sxs-lookup"><span data-stu-id="792d8-140">Interface of module</span></span>
<span data-ttu-id="792d8-141">Azure IoT Edge 모듈을 입력을 수신하고, 처리하며, 출력을 생성하는 작업을 수행하는 데이터 프로세서로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="792d8-142">하드웨어 (예: 동작 탐지기) 데이터, 다른 모듈 또는 (예: 타이머가 정기적으로 생성 된 난수) 다른 작업에서 메시지 hello 입력 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="792d8-143">비슷한 toohello 입력이 출력을 hello, 하드웨어 동작 (예: led가 깜박입니다.이 hello) 메시지 tooother 모듈, 기타 (예: 인쇄 toohello 콘솔)를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="792d8-144">모듈은 `message` 개체를 사용하여 서로 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="792d8-145">hello **콘텐츠** 의 `message` 는 모든 종류의 원하는 데이터를 표시할 수 있는 바이트 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="792d8-146">**속성** hello에 사용할 수 있습니다 `message` 되며 문자열을 문자열 매핑 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="792d8-147">으로 생각할 수 **속성** HTTP 요청 또는 파일의 hello 메타 데이터에 대 한 hello 머리글로 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="792d8-148">Toocreate hello 필요한 메서드를 구현 하는 새 모듈 개체 순서 toodevelop JS에 대 한 Azure IoT 가장자리 모듈에에서 필요한 `receive()`합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="792d8-149">이 시점에서 선택할 수도 있습니다 (옵션) tooimplement hello `create()` 또는 `start()`, 또는 `destroy()` 메서드 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="792d8-150">다음 코드 조각 hello JS 모듈 개체의 스 캐 폴딩 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a><span data-ttu-id="792d8-151">변환기 모듈</span><span class="sxs-lookup"><span data-stu-id="792d8-151">Converter module</span></span>
| <span data-ttu-id="792d8-152">입력</span><span class="sxs-lookup"><span data-stu-id="792d8-152">Input</span></span>                    | <span data-ttu-id="792d8-153">프로세서</span><span class="sxs-lookup"><span data-stu-id="792d8-153">Processor</span></span>                              | <span data-ttu-id="792d8-154">출력</span><span class="sxs-lookup"><span data-stu-id="792d8-154">Output</span></span>                 | <span data-ttu-id="792d8-155">원본 파일</span><span class="sxs-lookup"><span data-stu-id="792d8-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="792d8-156">온도 데이터 메시지</span><span class="sxs-lookup"><span data-stu-id="792d8-156">Temperature data message</span></span> | <span data-ttu-id="792d8-157">새 JSON 메시지의 구문 분석 및 생성</span><span class="sxs-lookup"><span data-stu-id="792d8-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="792d8-158">JSON 메시지 구조</span><span class="sxs-lookup"><span data-stu-id="792d8-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="792d8-159">이 모듈은 일반적인 Azure IoT Edge 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="792d8-160">다른 모듈에서 온도 메시지를 수락 하기 (하드웨어 모듈의 경우,이 경우에 시뮬레이트된 배포용 모듈 또는); 다음 구조화 tooa JSON 메시지 (hello 메시지 ID, tootrigger hello 온도 경고 해야 하는지 여부의 hello 속성을 설정 추가 및 포함 등)에 hello 온도 메시지를 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="792d8-161">프린터 모듈</span><span class="sxs-lookup"><span data-stu-id="792d8-161">Printer module</span></span>
| <span data-ttu-id="792d8-162">입력</span><span class="sxs-lookup"><span data-stu-id="792d8-162">Input</span></span>                          | <span data-ttu-id="792d8-163">프로세서</span><span class="sxs-lookup"><span data-stu-id="792d8-163">Processor</span></span> | <span data-ttu-id="792d8-164">출력</span><span class="sxs-lookup"><span data-stu-id="792d8-164">Output</span></span>                     | <span data-ttu-id="792d8-165">원본 파일</span><span class="sxs-lookup"><span data-stu-id="792d8-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="792d8-166">다른 모듈의 모든 메시지</span><span class="sxs-lookup"><span data-stu-id="792d8-166">Any message from other modules</span></span> | <span data-ttu-id="792d8-167">해당 없음</span><span class="sxs-lookup"><span data-stu-id="792d8-167">N/A</span></span>       | <span data-ttu-id="792d8-168">Hello 메시지 tooconsole 로그</span><span class="sxs-lookup"><span data-stu-id="792d8-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="792d8-169">이 모듈은 간단 하 고 새로울 hello 받은 메시지 (속성, 콘텐츠) toohello 터미널 윈도우를 출력 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="792d8-170">구성</span><span class="sxs-lookup"><span data-stu-id="792d8-170">Configuration</span></span>
<span data-ttu-id="792d8-171">hello 모듈을 실행 하기 전에 hello 마지막 단계에는 Azure IoT 가장자리 tooconfigure hello 및 모듈 간에 tooestablish hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="792d8-172">먼저 toodeclare 해야 우리의 `node` 에서 참조 될 수 있는 (다른 언어의 Azure IoT 가장자리 지원 로더)부터 로더 해당 `name` hello 단원의 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="792d8-173">우리의 로더를 선언 했습니다 되 면도 필요 toodeclare 뿐 우리 모듈 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="792d8-174">비슷한 toodeclaring hello 로더도 참조할 수 하 여 자신의 `name` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="792d8-175">Toospecify hello 로더 사용 해야 (있어야 하 고 hello 하나 앞에 정의) 필요한 모듈을 선언할 때 진입점 (모듈의 hello 정규화 된 클래스 이름 이어야 함) 각 모듈에 대 한 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="792d8-176">hello `simulated_device` hello Azure IoT 가장자리 코어 런타임 패키지에 포함 된 네이티브 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="792d8-177">포함 `args` hello 경우에 JSON 파일에서 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="792d8-178">Hello 구성의 hello 끝 hello 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="792d8-179">각 연결은 `source` 및 `sink`로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="792d8-180">미리 정의된 모듈을 모두 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="792d8-181">hello 출력 메시지의 `source` 모듈의 toohello 입력 전달 `sink` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-hello-modules"></a><span data-ttu-id="792d8-182">Hello 모듈을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="792d8-183">Tooterminate hello 응용 프로그램을 사용 하도록 하려는 경우 키를 눌러 `<Enter>` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="792d8-184">좋지 toouse Ctrl + C tooterminate hello IoT 가장자리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="792d8-185">이러한 방식으로 hello 프로세스 tooterminate 비정상적으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="792d8-185">As this way may cause hello process tooterminate abnormally.</span></span>
