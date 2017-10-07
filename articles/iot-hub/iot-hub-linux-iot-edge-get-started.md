---
title: "Azure IoT 가장자리 (Linux) aaaGet 시작 | Microsoft Docs"
description: "어떻게 toobuild Linux에 게이트웨이 컴퓨터 고 모듈 및 JSON 구성 파일 등 Azure IoT 가장자리의 주요 개념에 알아봅니다."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="a0819-103">Linux에서 Azure IoT Edge 아키텍처 살펴보기</span><span class="sxs-lookup"><span data-stu-id="a0819-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="a0819-104">Toorun 샘플 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a0819-104">How toorun hello sample</span></span>

<span data-ttu-id="a0819-105">hello **build.sh** hello로 해당 출력을 생성 하는 스크립트 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="a0819-106">이 출력에는 hello이이 샘플에 사용 되는 두 개의 IoT 가장자리 모듈이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="a0819-107">빌드 스크립트 위치 hello **liblogger.so** hello에 **빌드/모듈/로 거/** 폴더 및 **libhello\_world.so** hello에 **빌드 / 모듈/hello_world/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="a0819-108">이러한 경로 사용 하 여 hello에 대 한 **모듈 경로** hello 다음 예제에서는 JSON 설정 파일에에서 표시 된 대로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="a0819-109">hello hello\_세계\_샘플 프로세스 hello tooa JSON 구성 파일 경로 명령줄 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="a0819-110">hello 다음 예제에서는 JSON 파일에에서 제공에서 hello SDK 리포지토리 **샘플/hello\_세계/src/hello\_세계\_lin.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="a0819-111">hello를 수정 하지 않는 한이 구성 파일 작동 스크립트 tooplace hello IoT 가장자리 모듈 빌드하거나 기본이 아닌 위치에서 실행 파일을 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="a0819-112">hello 모듈 경로 어디에서 현재 작업 디렉터리를 상대 toohello hello hello\_세계\_하지 hello 실행가 있는 디렉터리를 hello, 샘플 실행 파일이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="a0819-113">hello 예제 JSON 구성 파일 기본값 toowriting 'log.txt' 현재 작업 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. <span data-ttu-id="a0819-114">Toohello 이동 **빌드** hello의 로컬 복사본의 hello 루트에서 폴더 **iot 가장자리** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="a0819-115">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0819-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

