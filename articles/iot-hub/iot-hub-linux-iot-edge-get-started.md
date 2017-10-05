---
title: "Azure IoT Edge 시작(Linux) | Microsoft Docs"
description: "Linux 컴퓨터에서 게이트웨이를 빌드하는 방법 및 모듈과 JSON 구성 파일 등 Azure IoT Edge의 주요 개념에 대해 알아봅니다."
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="7a679-103">Linux에서 Azure IoT Edge 아키텍처 살펴보기</span><span class="sxs-lookup"><span data-stu-id="7a679-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="7a679-104">샘플을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="7a679-104">How to run the sample</span></span>

<span data-ttu-id="7a679-105">**build.sh** 스크립트는 **iot-edge** 리포지토리의 로컬 복사본에 있는 **build** 폴더에 해당 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="7a679-106">이 출력에는 이 샘플에서 사용된 두 개의 IoT Edge 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="7a679-107">빌드 스크립트는 **liblogger.so**를 **build/modules/logger/** 폴더에 배치하고 **libhello\_world.so**를 **build/modules/hello_world/** 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="7a679-108">다음 예제 JSON 설정 파일에 표시된 대로 **module path** 값에 이러한 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="7a679-109">hello\_world\_sample 프로세스는 JSON 구성 파일에 대한 경로를 명령줄 인수 형태로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="7a679-110">다음 예제 JSON 파일은 **samples/hello\_world/src/hello\_world\_lin.json**의 SDK 리포지토리에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="7a679-111">이 구성 파일은 빌드 스크립트를 수정하여 IoT Edge 모듈이나 샘플 실행 파일을 기본 위치가 아닌 위치에 배치한 경우 외에는 그대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="7a679-112">모듈 경로는 실행 파일이 있는 디렉터리가 아니라, hello\_world\_sample 실행 파일이 실행되는 위치의 현재 작업 디렉터리에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="7a679-113">샘플 JSON 구성 파일은 현재 작업 디렉터리에서 작성 중인 'log.txt'를 기본값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="7a679-114">**iot-edge** 리포지토리의 로컬 복사본에 있는 루트의 **build** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a679-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="7a679-115">다음 명령 실행:</span><span class="sxs-lookup"><span data-stu-id="7a679-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

