## <a name="create-a-simulated-device-app"></a><span data-ttu-id="0f1b4-101">시뮬레이션된 장치 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0f1b4-101">Create a simulated device app</span></span>
<span data-ttu-id="0f1b4-102">이 섹션에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-102">In this section, you:</span></span>

* <span data-ttu-id="0f1b4-103">응답 tooa 직접적인 방법 hello 클라우드에서 호출 하 여 Node.js 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0f1b4-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="0f1b4-104">시뮬레이션된 펌웨어 업데이트 트리거</span><span class="sxs-lookup"><span data-stu-id="0f1b4-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="0f1b4-105">사용 하 여 hello 속성 tooenable 장치로 이중 쿼리 tooidentify 장치 및 펌웨어 업데이트를 마지막 완료 하는 경우 보고</span><span class="sxs-lookup"><span data-stu-id="0f1b4-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="0f1b4-106">1단계: **manageddevice**라는 빈 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="0f1b4-107">Hello에 **manageddevice** 폴더를 다음 명령 프롬프트에서 명령을 hello를 사용 하 여 package.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="0f1b4-108">모든 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="0f1b4-109">2 단계: hello에서 명령 프롬프트에 **manageddevice** hello 명령 tooinstall hello 다음를 실행 하는 폴더 **azure iot 장치** 및 **azure iot-장치 mqtt** 장치 SDK 패키지:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="0f1b4-110">텍스트 편집기를 사용 하는 3 단계: 만들는 **dmpatterns_fwupdate_device.js** hello에 대 한 파일 **manageddevice** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="0f1b4-111">4 단계: hello 다음 '필요' hello hello 시작 부분에 설명 추가 **dmpatterns_fwupdate_device.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="0f1b4-112">5 단계: 추가 **connectionString** 변수 toocreate를 사용 하는 **클라이언트** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="0f1b4-113">Hello 대체 `{yourdeviceconnectionstring}` hello 연결 문자열에서 이전에 기록한는 hello "하 여 장치 id 만들기" 섹션에서 이전에 자리 표시자.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="0f1b4-114">6 단계: 추가 hello 다음 함수를 사용 하는 tooupdate 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

<span data-ttu-id="0f1b4-115">7 단계 다운로드 한 후 hello 펌웨어 이미지 적용을 시뮬레이션 하는 함수를 수행 하는 hello를 추가 합니다.:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

<span data-ttu-id="0f1b4-116">8 단계: 추가 hello 함수 hello 통해 업데이트 hello 펌웨어 업데이트 상태 보고 속성 너무 다음**대기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="0f1b4-117">일반적으로 정책 hello 장치 toostart 다운로드 하 고 hello 업데이트를 적용 하면 관리자가 정의한 및 사용 가능한 업데이트의 장치 정보.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="0f1b4-118">이 함수는 정책을 실행 해야 하는 논리 tooenable hello입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="0f1b4-119">간단한 설명을 위해 hello 샘플 toodownload hello 펌웨어 이미지를 계속 하기 전에 4 초 동안 대기:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

<span data-ttu-id="0f1b4-120">9 단계: 추가 hello 함수 hello 통해 업데이트 hello 펌웨어 업데이트 상태 보고 속성 너무 다음**다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="0f1b4-121">hello 함수 있으면에서 펌웨어 다운로드 하 고 마지막으로 업데이트 hello 펌웨어 업데이트 상태 tooeither **downloadFailed** 또는 **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

<span data-ttu-id="0f1b4-122">10 단계: 추가 hello 함수 hello 통해 업데이트 hello 펌웨어 업데이트 상태 보고 속성 너무 다음**적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="0f1b4-123">hello 함수 다음 시뮬레이션 hello 펌웨어 이미지를 적용 하 고 마지막으로 업데이트 hello 펌웨어 업데이트 상태 tooeither **applyFailed** 또는 **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

<span data-ttu-id="0f1b4-124">11 단계: 추가 hello 다음 함수는 해당 핸들 hello **firmwareUpdate** 직접적인 방법 및 시작 hello 여러 단계로 이루어진 펌웨어 업데이트 프로세스:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="0f1b4-125">마지막으로, 12 단계 hello 코드 tooyour IoT 허브를 연결 하는 다음을 추가 합니다.:</span><span class="sxs-lookup"><span data-stu-id="0f1b4-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="0f1b4-126">단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0f1b4-127">프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리](https://msdn.microsoft.com/library/hh675232.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 