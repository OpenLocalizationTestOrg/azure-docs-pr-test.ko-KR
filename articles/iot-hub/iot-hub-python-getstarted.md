---
title: "Azure IoT Hub (Python) aaaGet 시작 | Microsoft Docs"
description: "Toosend 장치-클라우드 tooAzure IoT Sdk를 사용 하 여 Python에 대 한 IoT Hub를 메시지 하는 방법을 알아봅니다. 시뮬레이션 된 장치 및 서비스 응용 프로그램 tooregister 장치, 메시지를 보낼 만들고 IoT 허브에서 메시지를 읽은 합니다."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="66e89-104">Python을 사용 하 여 시뮬레이션 된 장치 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="66e89-105">이 자습서의 hello 끝 두 Python 응용 프로그램 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="66e89-106">**CreateDeviceIdentity.py**, 장치 id를 만듦 및 연결 된 보안 키 tooconnect 시뮬레이션 된 장치 앱.</span><span class="sxs-lookup"><span data-stu-id="66e89-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="66e89-107">**SimulatedDevice.py**앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는, 및 원격 분석 전송할 hello MQTT 프로토콜을 사용 하 여 메시지 주기적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="66e89-108">hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="66e89-109">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="66e89-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="66e89-110">[Python 2.x 또는 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="66e89-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="66e89-111">있는지 toouse hello 32 비트 또는 64 비트 설치 프로그램 설치 프로그램에서 필요에 따라 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="66e89-112">Hello 설치 하는 동안 대화 상자가 나타나면 있는지 tooadd Python tooyour 플랫폼 특정 환경 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="66e89-113">Python을 사용 하는 경우 2.x를 할 수 있습니다 너무[설치 또는 업그레이드 *pip*, hello Python 패키지 관리 시스템][lnk-install-pip]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="66e89-114">다음 Windows 운영 체제를 사용 하는 경우 [Visual c + + 재배포 가능 패키지] [ lnk-visual-c-redist] Python에서 네이티브 Dll tooallow hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="66e89-115">[Node.js 4.0 이상][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="66e89-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="66e89-116">있는지 toouse hello 32 비트 또는 64 비트 설치 프로그램 설치 프로그램에서 필요에 따라 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="66e89-117">이 필요한 tooinstall hello [IoT 허브 탐색기 도구][lnk-iot-hub-explorer]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="66e89-118">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="66e89-118">An active Azure account.</span></span> <span data-ttu-id="66e89-119">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="66e89-120">hello *pip* 패키지로 `azure-iothub-service-client` 및 `azure-iothub-device-client` 현재 Windows 운영 체제에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="66e89-121">Linux/Mac OS hello에 toohello Linux 및 Mac OS 관련 섹션을 참조 하십시오 [Python에 대 한 개발 환경을 준비] [ lnk-python-devbox] 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="66e89-122">IoT Hub를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-122">You have now created your IoT hub.</span></span> <span data-ttu-id="66e89-123">이 자습서의 나머지 부분 hello hello IoT Hub 호스트 이름 및 hello IoT 허브 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="66e89-124">또한 또는 만들 수 있습니다 IoT hub 명령줄에서 Python hello를 사용 하 여 Node.js Azure CLI를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="66e89-125">hello 문서 [hello Azure CLI 2.0을 사용 하 여 IoT 허브를 만듭니다.] [ lnk-azure-cli-hub] toodo 빠른 단계를 따라서 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="66e89-126">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="66e89-126">Create a device identity</span></span>
<span data-ttu-id="66e89-127">이 섹션에서는 hello 단계 toocreate hello id 레지스트리에 IoT 허브에서 장치 id를 작성 하는 Python 콘솔 앱을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="66e89-128">장치는 hello identity 레지스트리에 항목을 설정한 경우에 tooIoT 허브를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="66e89-129">자세한 내용은 참조 hello **Id 레지스트리에** hello 섹션 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="66e89-130">이 콘솔 응용 프로그램을 실행 하면 고유한 장치 ID를 생성 및 메시지 tooIoT 허브를 키 장치-클라우드 보낼 때 장치가 tooidentify 자체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="66e89-131">명령 프롬프트를 열고 hello 설치 **Python 용 Azure IoT 허브 서비스 SDK**합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="66e89-132">Hello SDK를 설치한 후 hello 명령 프롬프트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="66e89-133">**CreateDeviceIdentity.py**라는 이름의 Python 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="66e89-134">열 [Python 편집기/IDE를 원하는][lnk-python-ide-list], 예를 들어 기본 hello [IDLE][lnk-idle]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="66e89-135">Hello 코드 tooimport hello 필요한 모듈 hello 서비스 SDK에서에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="66e89-136">추가 코드 다음, hello 자리 표시자에 대 한 대체 hello `[IoTHub Connection String]` hello 이전 섹션에서 만든 hello IoT 허브에 대 한 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="66e89-137">Hello로 모든 이름을 사용할 수 있습니다 `DEVICE_ID`합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="66e89-138">추가 함수 tooprint 다음 hello 장치 정보 중 일부 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-138">Add hello following function tooprint some of hello device information.</span></span>

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. <span data-ttu-id="66e89-139">Hello 함수 toocreate hello 장치 식별 hello 레지스트리 관리자를 사용 하 여 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. <span data-ttu-id="66e89-140">마지막으로 다음과 같이 hello main 함수를 추가 하 고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-140">Finally, add hello main function as follows and save hello file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="66e89-141">Hello 명령 프롬프트에서 실행 hello **CreateDeviceIdentity.py** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="66e89-142">만든 가져오는 hello 시뮬레이션 된 장치에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="66e89-143">Hello 기록해 **deviceId** 및 hello **primaryKey** 이 장치의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="66e89-144">이 값이 필요 하면 이러한 나중 tooIoT 장치로 허브를 연결 하는 응용 프로그램을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="66e89-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![장치 만들기 성공][1]

> [!NOTE]
> <span data-ttu-id="66e89-146">IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="66e89-147">장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="66e89-148">응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="66e89-149">자세한 내용은 참조 hello [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="66e89-150">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="66e89-150">Create a simulated device app</span></span>
<span data-ttu-id="66e89-151">이 섹션에는 hello 단계 toocreate 시뮬레이트하는 장치 및 장치-클라우드 메시지 tooyour IoT 허브를 전송 하는 Python 콘솔 앱, 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="66e89-152">새 명령 프롬프트를 열고 다음과 같이 Python에 대 한 hello Azure IoT 허브 장치 SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="66e89-153">Hello 설치 후 hello 명령 프롬프트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="66e89-154">**SimulatedDevice.py**라는 이름의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="66e89-155">원하는 Python 편집기/IDE(예: IDLE)에서 이 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="66e89-156">Hello 코드 tooimport hello 필요한 모듈 hello 장치 SDK에서에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="66e89-157">Hello 다음 코드로 바꾸고 hello 자리 표시자에 대 한 대체 추가 `[IoTHub Device Connection String]` 장치에 대 한 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="66e89-158">장치 연결 문자열 hello는 일반적으로의 hello 형식 `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="66e89-159">사용 하 여 hello **deviceId** 및 **primaryKey** hello 이전 섹션 tooreplace hello에서 만든 hello 장치의 `<deviceId>` 및 `<primaryKey>` 각각.</span><span class="sxs-lookup"><span data-stu-id="66e89-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="66e89-160">`<hostName>`을 IoT Hub의 호스트 이름으로 바꿉니다. 일반적으로 `<IoT hub name>.azure-devices.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="66e89-161">다음 코드 toodefine 송신 확인 콜백 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-161">Add hello following code toodefine a send confirmation callback.</span></span> 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. <span data-ttu-id="66e89-162">다음 코드 tooinitialize hello 장치 클라이언트 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="66e89-163">Hello 다음 tooformat 작동을 시뮬레이션 된 장치 tooyour IoT 허브에서 메시지를 보냅니다를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. <span data-ttu-id="66e89-164">마지막으로 hello main 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="66e89-165">저장 후 닫기 hello **SimulatedDevice.py** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="66e89-166">사용자는 이제 준비 toorun이 응용이 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="66e89-167">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="66e89-168">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="66e89-169">시뮬레이션된 장치에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="66e89-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="66e89-170">장치에서 원격 분석 메시지 tooreceive 해야 toouse는 [이벤트 허브][lnk-event-hubs-overview]-호환 되는 hello hello 장치-클라우드 메시지를 읽는 IoT 허브에 의해 노출 된 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="66e89-171">읽기 hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] IoT 허브의 이벤트 허브 호환 끝점에 대 한 이벤트 허브에서 메시지 tooprocess 방법을 대 한 정보에 대 한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="66e89-172">이벤트 허브 아직 지원 하지 않는 원격 분석에서 Python, 하거나 만들 수 있도록 한 [Node.js](iot-hub-node-node-getstarted.md#D2C_node) 또는 [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) IoT 허브에서 이벤트 허브 기반 콘솔 앱 tooread hello 장치-클라우드 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="66e89-173">Hello를 사용 하는 방법을 보여 주는이 자습서 [IoT 허브 탐색기 도구] [ lnk-iot-hub-explorer] tooread 이러한 장치 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="66e89-174">명령 프롬프트를 열고 hello IoT 허브 탐색기를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="66e89-175">Hello hello 명령 프롬프트에 다음 명령을 실행 하면 장치에서 장치-클라우드 메시지 hello toobegin 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="66e89-176">IoT 허브의 연결 문자열을 사용 하 여 후 hello 자리 표시자의 `--login`합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="66e89-177">새 명령 프롬프트를 열고 hello를 포함 하는 toohello 디렉터리 **SimulatedDevice.py** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="66e89-178">Hello 실행 **SimulatedDevice.py** 원격 분석 데이터 tooyour IoT 허브를 주기적으로 전송 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="66e89-179">Hello 이전 섹션에서 hello IoT 허브 탐색기를 실행 하는 hello 명령 프롬프트에 hello 장치 메시지를 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Python 장치-클라우드 메시지][2]

## <a name="next-steps"></a><span data-ttu-id="66e89-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66e89-181">Next steps</span></span>
<span data-ttu-id="66e89-182">이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="66e89-183">이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 toosend 장치-클라우드 메시지 toohello IoT 허브를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="66e89-184">Hello 메시지를 사용 하 여 hello hello IoT 허브 탐색기 도구 hello IoT 허브에서 받은 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="66e89-185">심층, Azure IoT Hub 사용에 대 한 Python SDK tooexplore hello 방문 [이 허브 Git 리포지토리에][lnk-python-github]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="66e89-186">hello Python 용 Azure IoT 허브 서비스 SDK의 tooreview hello의 메시징 기능을 다운로드 하 고 실행할 수 [iothub_messaging_sample.py][lnk-messaging-sample]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="66e89-187">Python 용 Azure IoT 허브 장치 SDK hello를 사용 하 여 장치 쪽 시뮬레이션에 대 한 다운로드 하 고 실행할 수 hello [iothub_client_sample.py][lnk-client-sample]합니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="66e89-188">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="66e89-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="66e89-189">[장치 연결][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="66e89-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="66e89-190">[장치 관리 시작][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="66e89-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="66e89-191">[Azure IoT Hub 시작][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="66e89-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="66e89-192">toolearn tooextend 배율 사용할 때 IoT 솔루션 및 프로세스 장치-클라우드 메시지를 확인 하려면 어떻게 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="66e89-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
