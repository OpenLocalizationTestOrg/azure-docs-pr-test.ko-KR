---
title: "Node.js를 사용하여 Azure IoT Edge 모듈 만들기 | Microsoft Docs"
description: "이 자습서에서는 최신 Azure IoT Edge NPM 패키지 및 Yeoman 생성기를 사용하여 BLE 데이터 변환기 모듈을 작성하는 방법을 소개합니다."
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
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="1512e-103">Node.js를 사용하여 Azure IoT Edge 모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="1512e-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="1512e-104">이 자습서에서는 JS에서 Azure IoT Edge에 대한 모듈을 만드는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="1512e-105">이 자습서에서는 최신 Azure IoT Edge NPM 패키지를 사용하여 환경 설정 및 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 데이터 변환기 모듈을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1512e-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1512e-106">Prerequisites</span></span>

<span data-ttu-id="1512e-107">이 섹션에서는 IoT Edge 모듈 개발을 위한 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="1512e-108">*64비트 Windows* 및 *64비트 Linux(Ubuntu 14 이상)* 운영 체제 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="1512e-109">다음과 같은 소프트웨어가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-109">The following software is required:</span></span>
* <span data-ttu-id="1512e-110">[Git 클라이언트](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1512e-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="1512e-111">[노드 LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="1512e-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="1512e-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="1512e-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="1512e-113">아키텍처</span><span class="sxs-lookup"><span data-stu-id="1512e-113">Architecture</span></span>

<span data-ttu-id="1512e-114">Azure IoT Edge 플랫폼은 [Von Neumann 아키텍처](https://en.wikipedia.org/wiki/Von_Neumann_architecture)를 중요하게 채택합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="1512e-115">전체 Azure IoT Edge 아키텍처는 입력을 처리하고 출력을 생성하는 시스템이며 각 개별 모듈은 아주 작은 입력-출력 하위 시스템이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="1512e-116">이 자습서에서는 다음 두 개의 모듈을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="1512e-117">시뮬레이션된 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 신호를 수신하여 형식이 지정된 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지로 변환하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="1512e-118">수신한 [JSON](https://en.wikipedia.org/wiki/JSON) 메시지를 인쇄하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="1512e-119">다음 이미지는 이 프로젝트에 대한 일반적인 종단 간 데이터 흐름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="1512e-120">![3개의 모듈 간의 데이터 흐름](media/iot-hub-iot-edge-create-module/dataflow.png "입력: 시뮬레이션된 BLE 모듈, 프로세서: 변환기 모듈, 출력: 프린터 모듈")</span><span class="sxs-lookup"><span data-stu-id="1512e-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="1512e-121">환경 설정</span><span class="sxs-lookup"><span data-stu-id="1512e-121">Set up the environment</span></span>
<span data-ttu-id="1512e-122">다음은 JS를 사용하여 첫 번째 BLE 변환기 모듈을 작성할 수 있는 환경을 신속하게 설정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="1512e-123">모듈 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1512e-123">Create module project</span></span>
1. <span data-ttu-id="1512e-124">명령줄 창을 열고 `yo az-iot-gw-module`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="1512e-125">화면에 나타난 단계에 따라 모듈 프로젝트의 초기화를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="1512e-126">프로젝트 구조</span><span class="sxs-lookup"><span data-stu-id="1512e-126">Project structure</span></span>
<span data-ttu-id="1512e-127">JS 모듈 프로젝트는 다음 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="1512e-128">`modules` - 사용자 지정된 JS 모듈 원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="1512e-129">기본 `sensor.js` 및 `printer.js`를 사용자 고유의 모듈 파일로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="1512e-130">`app.js` - Edge 인스턴스를 시작하기 위한 항목 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="1512e-131">`gw.config.json` - Edge에서 로드할 모듈을 사용자 지정하는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="1512e-132">`package.json` - 모듈 프로젝트에 대한 메타데이터 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="1512e-133">`README.md` - 모듈 프로젝트에 대한 기본 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="1512e-134">패키지 파일</span><span class="sxs-lookup"><span data-stu-id="1512e-134">Package file</span></span>

<span data-ttu-id="1512e-135">이 `package.json`은 이름, 버전, 항목, 스크립트, 런타임 및 개발 종속성을 포함하는 모듈 프로젝트에 필요한 모든 메타데이터 정보를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="1512e-136">다음 코드 조각은 BLE 변환기 샘플 프로젝트를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="1512e-137">입력 파일</span><span class="sxs-lookup"><span data-stu-id="1512e-137">Entry file</span></span>
<span data-ttu-id="1512e-138">`app.js`는 에지 인스턴스를 초기화하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="1512e-139">여기에 대해 어떠한 변경도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-139">Here we don't need to make any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="1512e-140">모듈의 인터페이스</span><span class="sxs-lookup"><span data-stu-id="1512e-140">Interface of module</span></span>
<span data-ttu-id="1512e-141">Azure IoT Edge 모듈을 입력을 수신하고, 처리하며, 출력을 생성하는 작업을 수행하는 데이터 프로세서로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="1512e-142">입력은 하드웨어(예: 동작 탐지기)의 데이터, 다른 모듈의 메시지 또는 그밖에 무엇(예: 타이머에 의해 정기적으로 생성된 난수)이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="1512e-143">출력은 입력과 유사하게, 하드웨어 동작(예: 깜박이는 LED), 다른 모듈로 보내는 메시지 또는 그밖에 무엇(예: 콘솔에 인쇄)을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="1512e-144">모듈은 `message` 개체를 사용하여 서로 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="1512e-145">`message`의 **콘텐츠**는 사용자가 선호하는 모든 종류의 데이터를 표시할 수 있는 바이트 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="1512e-146">**속성**은 `message`에서 사용할 수 있으며 단순히 문자열-문자열 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="1512e-147">**속성**을 HTTP 요청의 헤더 또는 파일의 메타데이터로 생각할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="1512e-148">JS에서 Azure IoT Edge 모듈을 개발하려면 필요한 메서드 `receive()`를 구현하는 새 모듈 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="1512e-149">이 시점에서 선택적 `create()` 또는 `start()`나 `destroy()` 메서드를 구현하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="1512e-150">다음 코드 조각에서는 JS 모듈 개체의 스캐폴딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="1512e-151">변환기 모듈</span><span class="sxs-lookup"><span data-stu-id="1512e-151">Converter module</span></span>
| <span data-ttu-id="1512e-152">입력</span><span class="sxs-lookup"><span data-stu-id="1512e-152">Input</span></span>                    | <span data-ttu-id="1512e-153">프로세서</span><span class="sxs-lookup"><span data-stu-id="1512e-153">Processor</span></span>                              | <span data-ttu-id="1512e-154">출력</span><span class="sxs-lookup"><span data-stu-id="1512e-154">Output</span></span>                 | <span data-ttu-id="1512e-155">원본 파일</span><span class="sxs-lookup"><span data-stu-id="1512e-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="1512e-156">온도 데이터 메시지</span><span class="sxs-lookup"><span data-stu-id="1512e-156">Temperature data message</span></span> | <span data-ttu-id="1512e-157">새 JSON 메시지의 구문 분석 및 생성</span><span class="sxs-lookup"><span data-stu-id="1512e-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="1512e-158">JSON 메시지 구조</span><span class="sxs-lookup"><span data-stu-id="1512e-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="1512e-159">이 모듈은 일반적인 Azure IoT Edge 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="1512e-160">다른 모듈에서 온도 메시지를 수락하고(하드웨어 모듈 또는 이 경우 시뮬레이션된 BLE 모듈), 구조적 JSON 메시지로 온도 메시지를 정규화합니다(메시지 ID 첨부, 온도 경고를 트리거해야 하는지 여부의 속성 설정 등 포함).</span><span class="sxs-lookup"><span data-stu-id="1512e-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
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

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="1512e-161">프린터 모듈</span><span class="sxs-lookup"><span data-stu-id="1512e-161">Printer module</span></span>
| <span data-ttu-id="1512e-162">입력</span><span class="sxs-lookup"><span data-stu-id="1512e-162">Input</span></span>                          | <span data-ttu-id="1512e-163">프로세서</span><span class="sxs-lookup"><span data-stu-id="1512e-163">Processor</span></span> | <span data-ttu-id="1512e-164">출력</span><span class="sxs-lookup"><span data-stu-id="1512e-164">Output</span></span>                     | <span data-ttu-id="1512e-165">원본 파일</span><span class="sxs-lookup"><span data-stu-id="1512e-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="1512e-166">다른 모듈의 모든 메시지</span><span class="sxs-lookup"><span data-stu-id="1512e-166">Any message from other modules</span></span> | <span data-ttu-id="1512e-167">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1512e-167">N/A</span></span>       | <span data-ttu-id="1512e-168">콘솔에 메시지 로그</span><span class="sxs-lookup"><span data-stu-id="1512e-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="1512e-169">이 모듈은 간단하고 설명이 따로 필요 없으며, 수신한 메시지(속성, 콘텐츠)를 터미널 창으로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="1512e-170">구성</span><span class="sxs-lookup"><span data-stu-id="1512e-170">Configuration</span></span>
<span data-ttu-id="1512e-171">모듈을 실행하기 전 마지막 단계는 Azure IoT Edge를 구성하고 모듈 간 연결을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="1512e-172">첫 번째로, 나중에 섹션에서 자체 `name`에 의해 참조될 수 있는 `node` 로더를 선언해야 합니다(Azure IoT Edge가 다른 언어의 로더를 지원하기 때문).</span><span class="sxs-lookup"><span data-stu-id="1512e-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="1512e-173">로더를 선언하고 나면, 모듈도 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="1512e-174">로더 선언과 마찬가지로 모듈도 `name` 특성에 의해 참조될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="1512e-175">모듈을 선언할 때 각 모듈에 대해 사용해야 하는 로더(앞서 정의한 것 중 하나여야 함) 및 진입점(모듈의 정규화된 클래스 이름이어야 함)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="1512e-176">`simulated_device` 모듈은 Azure IoT Edge 코어 런타임 패키지에 포함되는 네이티브 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="1512e-177">`args`를 JSON 파일에 `null`인 경우라도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-177">Include `args` in the JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="1512e-178">구성 마지막에 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="1512e-179">각 연결은 `source` 및 `sink`로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="1512e-180">미리 정의된 모듈을 모두 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="1512e-181">`source` 모듈의 출력 메시지는 `sink` 모듈의 입력으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

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

## <a name="running-the-modules"></a><span data-ttu-id="1512e-182">모듈 실행</span><span class="sxs-lookup"><span data-stu-id="1512e-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="1512e-183">응용 프로그램을 종료하려면 `<Enter>` 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1512e-184">Ctrl + C를 사용하여 IoT Edge 응용 프로그램을 종료하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="1512e-185">이 방법은 프로세스를 비정상적으로 종료할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1512e-185">As this way may cause the process to terminate abnormally.</span></span>
