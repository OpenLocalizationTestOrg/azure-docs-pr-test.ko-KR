---
title: "C-직렬 변환기에 대 한 IoT 장치 aaaAzure SDK | Microsoft Docs"
description: "어떻게 toouse hello Serializer 라이브러리 C toocreate 장치 앱에 대 한 hello Azure IoT 장치 SDK에서에서 통신 하는 IoT 허브를 사용 합니다."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="eeee1-103">C용 Azure IoT 장치 SDK - 직렬 변환기에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="eeee1-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="eeee1-104">hello [먼저 문서](iot-hub-device-sdk-c-intro.md) 이 도입 시리즈 hello에 **C에 대 한 Azure IoT 장치 SDK**. hello 다음 기사 hello의 더 자세한 설명을 제공 [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="eeee1-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="eeee1-105">이 문서 나머지 구성 요소는 hello의 더 자세한 설명을 제공 하 여 hello SDK의 적용 범위 완료: hello **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="eeee1-106">방법을 설명 하는 hello 소개 문서 toouse hello **serializer** 라이브러리 toosend 이벤트 tooand IoT 허브에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="eeee1-107">이 문서의 내용을 확장 하였습니다 그 토론 방법에 대 한 자세한 설명은 제공 하 여 toomodel hello 사용 하 여 데이터 **serializer** 매크로 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="eeee1-108">hello 문서 라이브러리 hello 메시지를 serialize 하는 방법에 대 한 자세한 내용은 포함 되어 (및 경우에 따라 제어 하는 방법을 hello serialization 동작).</span><span class="sxs-lookup"><span data-stu-id="eeee1-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="eeee1-109">일부 매개 변수를 수정할 수 있습니다 사용자가 만드는 hello 모델의 hello 크기를 결정 하는 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="eeee1-110">마지막으로, hello 문서 다시 메시지 및 속성 처리와 같은 이전 문서에서 다루는 몇 가지 항목을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="eeee1-111">살펴보겠습니다에서 이러한 기능이 작동 하는 대로 hello hello를 사용 하 여 동일한 **serializer** 라이브러리 hello와 마찬가지로 **IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="eeee1-112">이 문서에 설명 된 모든 내용을 기반으로 hello **serializer** SDK 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="eeee1-113">Toofollow을 따라 하려는 경우 참조 hello **simplesample\_amqp** 및 **simplesample\_http** C. 용 hello Azure IoT 장치 SDK에에서 포함 된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eeee1-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="eeee1-114">Hello를 찾을 수 있습니다 [ **C에 대 한 Azure IoT 장치 SDK** ](https://github.com/Azure/azure-iot-sdk-c) hello에 hello API의 GitHub 리포지토리 및 뷰 세부 정보 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="eeee1-115">hello 모델링 언어</span><span class="sxs-lookup"><span data-stu-id="eeee1-115">hello modeling language</span></span>
<span data-ttu-id="eeee1-116">hello [소개 문서](iot-hub-device-sdk-c-intro.md) 이 도입 시리즈 hello에 **C에 대 한 Azure IoT 장치 SDK** 모델링 언어 hello에서 제공 하는 hello 예제의 통해 **simplesample\_amqp**  응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="eeee1-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="eeee1-117">볼 수 있듯이 hello 모델링 언어는 C 매크로 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="eeee1-118">항상 **BEGIN\_NAMESPACE**로 사용자 정의를 시작하고 **END\_NAMESPACE**로 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="eeee1-119">일반적인 tooname hello 또는 네임 스페이스 귀사에 대 한,이 예제에서 작업 하는 hello 프로젝트와 같이 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="eeee1-120">Hello 네임 스페이스 내 항목의 적합 한는 모델 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="eeee1-121">이 경우 풍력계에 대한 단일 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="eeee1-122">다시 한 번, 아무것도 hello 모델을 이름을 지정할 수 있지만 라는 일반적으로 hello 장치 또는 데이터의 종류에 대 한 IoT Hub와 tooexchange 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="eeee1-123">모델 정의 포함 하면 수신 tooIoT 허브 hello 이벤트의 (hello *데이터*) hello 메시지 IoT 허브에서 받을 수 뿐만 아니라 (hello *동작*).</span><span class="sxs-lookup"><span data-stu-id="eeee1-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="eeee1-124">형식과 이름을; 이벤트에는 hello 예제에서 볼 수 있습니다, 작업 이름 및 선택적 매개 변수 (형식으로 각각) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="eeee1-125">이 샘플에서 설명 하지 않음 무엇은 hello SDK에서 지 원하는 추가 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="eeee1-126">다음에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="eeee1-127">IoT Hub tooit으로 전송 하는 한 장치 toohello 데이터 참조 *이벤트*, 모델링 언어 hello tooit으로 참조 하는 반면, *데이터* (사용 하 여 정의 **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="eeee1-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="eeee1-128">마찬가지로, IoT Hub 참조 toohello 보내는 데이터를로 toodevices *메시지*, 모델링 언어 hello tooit으로 참조 하는 반면, *동작* (사용 하 여 정의 **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="eeee1-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="eeee1-129">이 문서에서는 이러한 용어가 같은 의미로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="eeee1-130">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="eeee1-130">Supported data types</span></span>
<span data-ttu-id="eeee1-131">데이터 형식은 다음 hello는 hello를 사용 하 여 만든 모델에서 지원 **serializer** 라이브러리:</span><span class="sxs-lookup"><span data-stu-id="eeee1-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="eeee1-132">형식</span><span class="sxs-lookup"><span data-stu-id="eeee1-132">Type</span></span> | <span data-ttu-id="eeee1-133">설명</span><span class="sxs-lookup"><span data-stu-id="eeee1-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eeee1-134">double</span><span class="sxs-lookup"><span data-stu-id="eeee1-134">double</span></span> |<span data-ttu-id="eeee1-135">배정밀도 부동 소수점 숫자</span><span class="sxs-lookup"><span data-stu-id="eeee1-135">double precision floating point number</span></span> |
| <span data-ttu-id="eeee1-136">int</span><span class="sxs-lookup"><span data-stu-id="eeee1-136">int</span></span> |<span data-ttu-id="eeee1-137">32비트 정수</span><span class="sxs-lookup"><span data-stu-id="eeee1-137">32 bit integer</span></span> |
| <span data-ttu-id="eeee1-138">float</span><span class="sxs-lookup"><span data-stu-id="eeee1-138">float</span></span> |<span data-ttu-id="eeee1-139">단정밀도 부동 소수점 숫자</span><span class="sxs-lookup"><span data-stu-id="eeee1-139">single precision floating point number</span></span> |
| <span data-ttu-id="eeee1-140">long</span><span class="sxs-lookup"><span data-stu-id="eeee1-140">long</span></span> |<span data-ttu-id="eeee1-141">정수(Long)</span><span class="sxs-lookup"><span data-stu-id="eeee1-141">long integer</span></span> |
| <span data-ttu-id="eeee1-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="eeee1-142">int8\_t</span></span> |<span data-ttu-id="eeee1-143">8비트 정수</span><span class="sxs-lookup"><span data-stu-id="eeee1-143">8 bit integer</span></span> |
| <span data-ttu-id="eeee1-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="eeee1-144">int16\_t</span></span> |<span data-ttu-id="eeee1-145">16비트 정수</span><span class="sxs-lookup"><span data-stu-id="eeee1-145">16 bit integer</span></span> |
| <span data-ttu-id="eeee1-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="eeee1-146">int32\_t</span></span> |<span data-ttu-id="eeee1-147">32비트 정수</span><span class="sxs-lookup"><span data-stu-id="eeee1-147">32 bit integer</span></span> |
| <span data-ttu-id="eeee1-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="eeee1-148">int64\_t</span></span> |<span data-ttu-id="eeee1-149">64비트 정수</span><span class="sxs-lookup"><span data-stu-id="eeee1-149">64 bit integer</span></span> |
| <span data-ttu-id="eeee1-150">bool</span><span class="sxs-lookup"><span data-stu-id="eeee1-150">bool</span></span> |<span data-ttu-id="eeee1-151">부울</span><span class="sxs-lookup"><span data-stu-id="eeee1-151">boolean</span></span> |
| <span data-ttu-id="eeee1-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="eeee1-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="eeee1-153">ASCII 문자열</span><span class="sxs-lookup"><span data-stu-id="eeee1-153">ASCII string</span></span> |
| <span data-ttu-id="eeee1-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="eeee1-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="eeee1-155">날짜 시간 오프셋</span><span class="sxs-lookup"><span data-stu-id="eeee1-155">date time offset</span></span> |
| <span data-ttu-id="eeee1-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="eeee1-156">EDM\_GUID</span></span> |<span data-ttu-id="eeee1-157">GUID</span><span class="sxs-lookup"><span data-stu-id="eeee1-157">GUID</span></span> |
| <span data-ttu-id="eeee1-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="eeee1-158">EDM\_BINARY</span></span> |<span data-ttu-id="eeee1-159">binary</span><span class="sxs-lookup"><span data-stu-id="eeee1-159">binary</span></span> |
| <span data-ttu-id="eeee1-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="eeee1-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="eeee1-161">복합 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="eeee1-161">complex data type</span></span> |

<span data-ttu-id="eeee1-162">Hello 마지막 데이터 형식과 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="eeee1-163">hello **DECLARE\_구조체** 있습니다 hello의 그룹인 toodefine 복합 데이터 형식을 다른 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="eeee1-164">이러한 그룹화는 다음과 같은 모델 toodefine 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="eeee1-164">These groupings allow us toodefine a model that looks like this:</span></span>

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

<span data-ttu-id="eeee1-165">이 모델은 **TestType**형식의 단일 데이터 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="eeee1-166">**TestType** hello hello에서 지원 되는 기본 형식 전체적으로 보여 주는 여러 멤버를 포함 하는 복합 유형 **serializer** 모델링 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="eeee1-167">이와 같은 모델, 코드 toosend 데이터 tooIoT 다음과 같이 표시 되는 허브를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

<span data-ttu-id="eeee1-168">기본적으로,의 hello는 값 tooevery 멤버를 지정 하는 것 **테스트** 구조와 다음 호출 **SendAsync** toosend hello **테스트** 데이터 이벤트 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="eeee1-169">**SendAsync** 함수는 단일 데이터 이벤트 tooIoT 허브 전송 하는 도우미 함수:</span><span class="sxs-lookup"><span data-stu-id="eeee1-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

<span data-ttu-id="eeee1-170">이 함수는 데이터 이벤트를 지정 하는 hello 또는 그 반대로 serialize 하 고 tooIoT 허브 보냅니다를 사용 하 여 **IoTHubClient\_SendEventAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="eeee1-171">이 동일한 코드 이전 문서에서 설명 하는 hello (**SendAsync** 을 편리 하 게 함수로 hello 논리를 캡슐화).</span><span class="sxs-lookup"><span data-stu-id="eeee1-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="eeee1-172">Hello 이전 코드에서 사용 되는 한 도우미 함수는 **GetDateTimeOffset**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="eeee1-173">이 함수 형식의 값에 지정 된 시간 hello 변환 **EDM\_날짜\_시간\_오프셋**:</span><span class="sxs-lookup"><span data-stu-id="eeee1-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

<span data-ttu-id="eeee1-174">이 코드를 실행 하는 경우 메시지의 뒤에 hello tooIoT 허브 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="eeee1-175">Hello serialization hello 형식인 hello에 의해 생성 된 JSON은 **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="eeee1-176">또한 hello의 각 멤버는 serialize 된 JSON 개체 일치 hello의 hello 멤버 **TestType** 예제의 모델에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="eeee1-177">hello 값도 일치 hello 코드에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="eeee1-178">그러나 hello 이진 데이터가 base64 인코딩 인지를 확인: "AQID"의 base64 인코딩입니다 hello은 {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="eeee1-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="eeee1-179">이 예제는 hello를 사용 하 여 활용 하는 hello **serializer** 라이브러리-수 있도록 toosend JSON toohello 클라우드 응용 프로그램의 serialization을 다루는 tooexplicitly 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="eeee1-180">이제 다 tooworry에 대 한을 설정의 hello hello 값 데이터 이벤트 예제의 모델 및 해당 이벤트 toohello 클라우드 단순 Api toosend를 호출한 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="eeee1-181">이 정보를 통해 지원 되는 데이터 형식, 복합 형식 (다른 복합 형식 내에서 복합 형식을 포함도 수)를 포함 하 여 hello 범위를 포함 하는 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="eeee1-182">하지만 생성 된 JSON 직렬화 그 hello에서 위의 예제는 중요 한 점은를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="eeee1-183">*어떻게* hello 사용 하 여 데이터를 받으실 **serializer** 라이브러리 정확 하 게 hello JSON 형성 되는 방식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="eeee1-184">이러한 특별한 내용은 다음에 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="eeee1-185">직렬화에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="eeee1-185">More about serialization</span></span>
<span data-ttu-id="eeee1-186">hello 이전 섹션 강조 예제 hello에 의해 생성 된 hello 출력 **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="eeee1-187">이 섹션에서는 hello serialization Api를 사용 하 여 해당 동작을 제어 하는 방법 및 hello 라이브러리에서 데이터를 직렬화 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="eeee1-188">Serialization 중에 tooadvance hello 토론 순서에서는 서머 스 탯을 기반으로 새 모델와 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="eeee1-189">첫째, 몇 가지 배경 정보를 제공 하겠습니다 hello 시나리오에 tooaddress는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="eeee1-190">온도 및 습도 측정 하는 자동 온도 조절기 toomodel 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="eeee1-191">각 데이터 조각 toobe 다르게 tooIoT 허브 전송 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="eeee1-192">기본적으로 hello 자동 온도 조절기 ingresses 온도 이벤트 2 분 마다 한 번씩; 습도 이벤트는 15 분 마다 한 번씩 ingressed.</span><span class="sxs-lookup"><span data-stu-id="eeee1-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="eeee1-193">이 이벤트 중 하나 이면 ingressed hello 시간 해당 hello 해당 온도 보여 주는 타임 스탬프를 포함 해야 합니다 또는 습도 측정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="eeee1-194">이 시나리오를 매개 변수로 받아 보여 드립니다 두 가지 방법으로 toomodel hello 데이터 및 모델링에 hello에 직렬화 된 출력 hello 효과 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="eeee1-195">모델 1</span><span class="sxs-lookup"><span data-stu-id="eeee1-195">Model 1</span></span>
<span data-ttu-id="eeee1-196">Hello 첫 번째 모델의 버전 지원 hello 이전 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

<span data-ttu-id="eeee1-197">해당 hello 모델 두 개 데이터 이벤트를 포함 하는 참고: **온도** 및 **습도**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="eeee1-198">이전 예제에서와 달리 hello 유형의 각 이벤트는 사용 하 여 정의 하는 구조 **DECLARE\_구조체**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="eeee1-199">**TemperatureEvent**는 온도 측정 및 타임스탬프를 포함하고 **HumidityEvent**는 습도 측정 및 타임스탬프를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="eeee1-200">이 모델 위에 설명 된 hello 시나리오에 대 한 자연 스러운 방법 toomodel hello 데이터 목록 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="eeee1-201">이벤트 toohello 클라우드 म 보내면 온도/타임 스탬프 또는 습도/타임 스탬프 쌍 하거나 보내 드립니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="eeee1-202">Hello 다음과 같은 코드를 사용 하는 온도 이벤트 toohello 클라우드를 보내 드립니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="eeee1-203">온도 및 습도 hello 샘플 코드에서에 하드 코드 된 값을 사용 하지만 하에서는 실제로 읽어 들이는 이러한 값 hello 해당 센서 hello 자동 온도 조절기를 샘플링 하 여 가정해 보세요. 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="eeee1-204">위의 hello 코드 hello를 사용 하 여 **GetDateTimeOffset** 이전에 도입 된 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="eeee1-205">지우기 이상 될의 이유로이 코드 hello를 직렬화 하 고 작업을 hello 이벤트를 보내는 명시적으로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="eeee1-206">hello 이전 코드를 버퍼에 hello 온도 이벤트를 serialize합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="eeee1-207">그런 다음 **sendMessage** 도우미 함수 (에 포함 된 **simplesample\_amqp**) 보냅니다 hello tooIoT 이벤트 허브는:</span><span class="sxs-lookup"><span data-stu-id="eeee1-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

<span data-ttu-id="eeee1-208">이 코드는 hello의 하위 집합 **SendAsync** 있으므로 않습니다 위로 다시 여기 hello 이전 섹션에서 설명 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="eeee1-209">Hello 이전 코드 toosend hello 온도 이벤트를 실행 하면이 serialize 된 형태의 hello 이벤트 허브 tooIoT 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="eeee1-210">**TemperatureEvent** 형식의 온도를 전송하고 해당 구조체에는 **Temperature** 및 **Time** 멤버가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="eeee1-211">이 직접 hello serialize 된 데이터에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="eeee1-212">마찬가지로 이 코드로 습도 이벤트도 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="eeee1-213">serialize 된 hello 양식 tooIoT 허브 전송 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="eeee1-214">역시, 예상대로 입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-214">Again, this is as expected.</span></span>

<span data-ttu-id="eeee1-215">이 모델로 추가 이벤트를 어떻게 쉽게 추가할 수 있는지 생각해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="eeee1-216">사용 하 여 더 많은 구조체를 정의 **DECLARE\_구조체**를 사용 하 여 hello 모델에 hello 해당 이벤트를 포함 하 고 **WITH\_데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="eeee1-217">이제 hello 포함 되도록 hello 모델을 수정 해 보겠습니다 동일한 데이터 하지만 서로 다른 구조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="eeee1-218">모델 2</span><span class="sxs-lookup"><span data-stu-id="eeee1-218">Model 2</span></span>
<span data-ttu-id="eeee1-219">위의이 대체 모델 toohello 하나를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="eeee1-220">이 경우 hello 제거 했다고 해 **DECLARE\_구조체** 매크로 및 모델링 언어 hello 단순 형식을 사용 하 여이 시나리오에서 hello 데이터 항목 정의 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="eeee1-221">Hello 순간에 대 한 hello 보겠습니다 무시 **시간** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="eeee1-222">와 별개로 같습니다 hello 코드 tooingress **온도**:</span><span class="sxs-lookup"><span data-stu-id="eeee1-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="eeee1-223">이 코드는 hello 다음 직렬화 tooIoT 이벤트 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="eeee1-224">고 hello 습도 이벤트 보내기 위한 hello 코드는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="eeee1-225">이 코드에서는이 tooIoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="eeee1-226">지금까지 특별한 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-226">So far there are still no surprises.</span></span> <span data-ttu-id="eeee1-227">이제 hello SERIALIZE 매크로 사용 하는 방법을 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="eeee1-228">hello **SERIALIZE** 매크로 인수로 여러 데이터 이벤트 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="eeee1-229">이렇게 하면 수 tooserialize hello **온도** 및 **습도** 이벤트 함께 한 번의 호출 tooIoT 허브를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="eeee1-230">두 데이터 이벤트 허브 tooIoT 전송 되도록이 코드의 hello 결과 임을 추측할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="eeee1-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="eeee1-231">[</span><span class="sxs-lookup"><span data-stu-id="eeee1-231">[</span></span>

<span data-ttu-id="eeee1-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="eeee1-232">{"Temperature":75},</span></span>

<span data-ttu-id="eeee1-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="eeee1-233">{"Humidity":45}</span></span>

<span data-ttu-id="eeee1-234">]</span><span class="sxs-lookup"><span data-stu-id="eeee1-234">]</span></span>

<span data-ttu-id="eeee1-235">즉, 예상 대로이 코드는 hello 동일 보내는 것과 **온도** 및 **습도** 별도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="eeee1-236">방금 편의 toopass는 두 이벤트 모두 너무**SERIALIZE** hello에서는 동일한 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="eeee1-237">그러나 hello 대/소문자가 아닌.</span><span class="sxs-lookup"><span data-stu-id="eeee1-237">However, that’s not hello case.</span></span> <span data-ttu-id="eeee1-238">대신, 위의 hello 코드는이 단일 데이터 이벤트 tooIoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="eeee1-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="eeee1-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="eeee1-240">모델에서 **온도** 및 **습도**를 두 개의 *별도* 이벤트로 정의하므로 이것이 이상하게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="eeee1-241">이러한 이벤트 모델링 하지 않은 다른 toohello 점 위치 **온도** 및 **습도** hello에 동일한 구조:</span><span class="sxs-lookup"><span data-stu-id="eeee1-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="eeee1-242">이 모델을 사용한 경우에 것이 더 쉽게 toounderstand 어떻게 **온도** 및 **습도** 보낼 hello에 메시지를 직렬화 하는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="eeee1-243">그러나 아닐 지우기 너무 두 데이터 이벤트를 전달 하는 경우 이런 방식으로 작동 하는 이유**SERIALIZE** 2 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="eeee1-244">해당 hello hello 가정을 알고 있는 경우에이 동작은 쉽게 toounderstand **serializer** 라이브러리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="eeee1-245">이 toomake 의미 백 tooour 모델을 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="eeee1-246">이 모델을 개체 지향 용어로 생각해봅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="eeee1-247">이 경우 실제 장치(자동 온도 조절기)를 모델링하고 해당 장치가 **온도** 및 **습도**와 같은 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="eeee1-248">Hello hello 다음과 같은 코드와 함께 모델의 전체 상태를 보내 드립니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="eeee1-249">온도, 습도 시간과 hello 값이 설정 된 경우이 보낸된 tooIoT 허브와 같은 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="eeee1-250">Toosend만 필요 하기도 *일부* hello 모델 toohello 클라우드 (이 모델에 있는 데이터 이벤트 수가 많은 경우에 특히 그렇습니다)의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="eeee1-251">와 같은 데이터 이벤트의 하위 집합만 유용 toosend 이전 예에서:</span><span class="sxs-lookup"><span data-stu-id="eeee1-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="eeee1-252">Hello 정확 하 게 생성 동일한 이벤트 처럼 serialize 정의는 **TemperatureEvent** 와 **온도** 및 **시간** 않았습니다으로 모델링 1와 같은 방법으로 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="eeee1-253">이 경우 अ स म र 정확 하 게 hello 동일 직렬화 이벤트 호출 하기 때문에 다른 모델 (모델 2)를 사용 하 여 수 toogenerate **SERIALIZE** 를 다른 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="eeee1-254">hello 중요 한 점은 너무 여러 데이터 이벤트를 전달 하는 경우**SERIALIZE,** 각 이벤트는 단일 JSON 개체의 속성을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="eeee1-255">가장 좋은 방법이 hello 및 모델에 대 한 생각 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="eeee1-256">"이벤트" toohello 클라우드 보내는 각 이벤트에 정의 된 속성 집합을 포함 하는 경우 hello 첫 번째 방법은 큰 의미를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="eeee1-257">사용이 경우 **DECLARE\_구조체** toodefine hello 각 이벤트의 구조 및 다음 hello 사용 하 여 모델에 포함할 **WITH\_데이터** 매크로입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="eeee1-258">그런 다음 위의 hello 첫 번째 예제에서와 같이 각 이벤트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="eeee1-259">이 방법만 전달 하는 단일 데이터 이벤트 너무**SERIALIZER**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="eeee1-260">개체 지향 방식으로 모델에 대 한 생각 되 면 다음 hello 두 번째 방법을 사용할 수 있습니다 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="eeee1-261">이 예에서 사용 하 여 정의 된 요소를 hello **WITH\_데이터** 은 개체의 hello "속성이"입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="eeee1-262">이벤트의 모든 하위 집합을 너무 전달**SERIALIZE** 원하는, toosend toohello 클라우드 "개체의" 상태의 정도 따라 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="eeee1-263">어떤 접근 방식이 옳거나 그르다고 말할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="eeee1-264">어떻게 될 hello **serializer** 라이브러리 작동 하며, 요구 사항에 가장 잘 맞는 선택 hello 모델링 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="eeee1-265">메시지 처리</span><span class="sxs-lookup"><span data-stu-id="eeee1-265">Message handling</span></span>
<span data-ttu-id="eeee1-266">지금까지이 문서는 송신 이벤트 tooIoT 허브 설명만 하 고 메시지를 받는 주소를 지정 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="eeee1-267">이유 hello 메시지를 수신 하는 방법에 대 한 tooknow에서 다루는 크게 필요한 것은이 대 한 프로그램 [이전 문서](iot-hub-device-sdk-c-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="eeee1-268">메시지 콜백 함수를 등록하여 메시지를 처리하는 문서를 상기해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="eeee1-269">그런 다음 메시지를 받을 때 호출 되는 hello 콜백 함수를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-269">You then write hello callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="eeee1-270">이 구현 **IoTHubMessage** 호출 hello 모델의 각 작업에 특정 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="eeee1-271">예를 들어 모델에서 다음 동작을 정의하는 경우:</span><span class="sxs-lookup"><span data-stu-id="eeee1-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="eeee1-272">다음 서명과 함께 함수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="eeee1-273">**SetAirResistance** 그런 다음 해당 메시지를 tooyour 장치를 보낼 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="eeee1-274">설명 하지 않은 것 처럼 보이는 메시지의 직렬화 된 hello 버전 또 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="eeee1-275">즉, toosend 하려는 경우는 **SetAirResistance** 메시지 tooyour 장치, 내용에 해당 모양을?</span><span class="sxs-lookup"><span data-stu-id="eeee1-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="eeee1-276">메시지 tooa 장치를 보내는 경우 hello Azure IoT 서비스 SDK 통해 그렇게가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="eeee1-277">여전히 toosend tooinvoke에서 특정 동작 문자열 tooknow 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="eeee1-278">hello 메시지를 보내기 위한 일반 형식 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="eeee1-279">두 개의 속성이 있는 serialize 된 JSON 개체를 보낼 때: **이름** hello 동작 (메시지)의 hello 이름인 및 **매개 변수** 해당 동작의 hello 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="eeee1-280">예를 들어 tooinvoke **SetAirResistance** 이 메시지 tooa 장치를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="eeee1-281">hello 동작 이름은 모델에 정의 된 동작을 정확히 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="eeee1-282">hello 매개 변수 이름은 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-282">hello parameter names must match as well.</span></span> <span data-ttu-id="eeee1-283">또한 대/소문자 구분 여부도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-283">Also note case sensitivity.</span></span> <span data-ttu-id="eeee1-284">**Name** 및 **Parameters**는 항상 대문자입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="eeee1-285">모델의 작업 이름 및 매개 변수 있는지 toomatch hello 사례를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="eeee1-286">이 예제에서는 hello 작업 이름이 "SetAirResistance" 및 "setairresistance" 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="eeee1-287">다른 두 가지 동작 hello **TurnFanOn** 및 **TurnFanOff** 이러한 메시지 tooa 장치를 전송 하 여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="eeee1-288">이 여기서 설명한 hello 이벤트를 전송 및 메시지를 받을 때 tooknow 필요한 모든 **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="eeee1-289">설명을 진행하기 전에, 모델의 크기를 제어하기 위해 구성할 수 있는 몇 가지 매개 변수에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="eeee1-290">매크로 구성</span><span class="sxs-lookup"><span data-stu-id="eeee1-290">Macro configuration</span></span>
<span data-ttu-id="eeee1-291">Hello를 사용 하 여 **Serializer** hello SDK toobe 인식의 중요 한 부분이 hello azure-c-공유-유틸리티 라이브러리에서 발견 되는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="eeee1-292">Hello-클래스 옵션을 사용 하 여 GitHub에서 hello Azure iot-sdk c 리포지토리를 복제 하는 경우이 공유 유틸리티 라이브러리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="eeee1-293">Hello 라이브러리를 복제 하지 하는 경우 파일을 찾을 수 [여기](https://github.com/Azure/azure-c-shared-utility)합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="eeee1-294">Hello 공유 유틸리티 라이브러리 내의 폴더를 다음 hello를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="eeee1-295">이 폴더에는 **macro\_utils\_h\_generator.sln**이라는 Visual Studio 솔루션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="eeee1-296">이 솔루션에서는 hello 프로그램 생성 hello **매크로\_utils.h** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="eeee1-297">기본 매크로가\_hello SDK에 포함 된 utils.h 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="eeee1-298">이 솔루션에서는 일부 매개 변수 및 한 후 다시 만듭니다 hello 이러한 매개 변수를 기반으로 하는 헤더 파일 toomodify가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="eeee1-299">와 관련 된 toobe hello 두 키 매개 변수는 **nArithmetic** 및 **nMacroParameters** 매크로이 두 줄에 정의 되어 있는\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="eeee1-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="eeee1-300">이러한 값은 hello SDK에 포함 된 hello 기본 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="eeee1-301">각 매개 변수에 의미에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="eeee1-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="eeee1-302">nMacroParameters – 하나의 DECLARE\_MODEL 매크로 정의에 포함할 수 있는 매개 변수 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="eeee1-303">nArithmetic hello 컨트롤 모델에서 허용 되는 멤버의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="eeee1-304">이러한 매개 변수는 중요 한 hello 이유 제어 하기 때문에 크기 모델 수입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="eeee1-305">예를 들어 다음 모델 정의를 고려해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="eeee1-306">이전에 설명한 것처럼 **DECLARE\_MODEL**은 C 매크로입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="eeee1-307">hello 모델과 hello 형태의 hello **WITH\_데이터** 문 (아직 다른 매크로)는의 매개 변수 **DECLARE\_모델**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="eeee1-308">**nMacroParameters**는 **DECLARE\_MODEL**에 포함할 수 있는 매개 변수 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="eeee1-309">이러한 매개 변수는 포함할 수 있는 데이터 이벤트 및 동작 선언 수를 효과적으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="eeee1-310">따라서 124 hello 기본 제한 값으로 즉, 약 60 동작 및 데이터 이벤트를 조합 하 여 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="eeee1-311">이 제한을 tooexceed를 시도 하면 컴파일러 오류 비슷한 toothis을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="eeee1-312">hello **nArithmetic** 매개 변수는 hello 매크로 언어의 hello 내부 작업에 대 한 응용 프로그램 보다 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="eeee1-313">모델에 포함할 수 있습니다는 구성원의 hello 총 수를 제어 등 **DECLARE_STRUCT** 매크로입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="eeee1-314">다음과 같은 컴파일러 오류가 표시되면 **nArithmetic**을 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="eeee1-315">Hello 매크로 hello 값을 수정 하려는 경우 toochange 이러한 매개 변수,\_utils.tt 파일, recompile hello 매크로\_유틸리티\_h\_generator.sln 솔루션과 실행된 hello 컴파일된 프로그램.</span><span class="sxs-lookup"><span data-stu-id="eeee1-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="eeee1-316">이렇게 하려면 다음을 새 매크로\_utils.h 파일 생성 되 고 hello에 배치 됩니다.\\ 일반적인\\inc 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="eeee1-317">순서 toouse hello 매크로의 새 버전에\_utils.h, 제거 hello **serializer** NuGet 패키지를 솔루션에서와 그 자리에 포함 hello **serializer** Visual Studio 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="eeee1-318">따라서 hello serializer 라이브러리의 hello 소스 코드에 대해 프로그램 코드 toocompile를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="eeee1-319">여기에 업데이트 하는 hello 매크로\_utils.h 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="eeee1-320">에 대 한이 toodo 하려면 **simplesample\_amqp**, hello 솔루션에서 hello serializer 라이브러리에 대 한 hello NuGet 패키지를 제거 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="eeee1-321">이 프로젝트 tooyour Visual Studio 솔루션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="eeee1-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="eeee1-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="eeee1-323">완료되면 다음과 같이 솔루션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="eeee1-324">매크로 업데이트 컴파일하는 경우, 솔루션 hello 이제\_utils.h 이진 파일에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="eeee1-325">이 값을 너무 높게 늘리면 컴파일러 한계를 초과할 수 있음에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="eeee1-326">toothis 지점 hello **nMacroParameters** 은 관심된 있는 toobe hello 주 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="eeee1-327">hello C99 사양의 127 매개 변수의 최소값 매크로 정의에서 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="eeee1-328">hello Microsoft 컴파일러 정확히 hello 사양 뒤에 오는 (및 127 제한 되어) 수 tooincrease 되지 않으므로 **nMacroParameters** hello 기본값 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="eeee1-329">다른 컴파일러 수 있도록 toodo 있으므로 (예를 들어 hello GNU 컴파일러 지원 더 높은 한도).</span><span class="sxs-lookup"><span data-stu-id="eeee1-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="eeee1-330">지금까지 설명한 tooknow toowrite hello로 코드가 하는 방식에 대 한 필요한 모든 항목에 대 한 **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="eeee1-331">마무리하기 전에 궁금해할 수 있는 이전 문서의 일부 항목을 다시 확인해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="eeee1-332">hello 하위 수준 Api</span><span class="sxs-lookup"><span data-stu-id="eeee1-332">hello lower-level APIs</span></span>
<span data-ttu-id="eeee1-333">이 문서 포커스가 있는 hello 샘플 응용 프로그램은 **simplesample\_amqp**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="eeee1-334">이 샘플 이벤트 사용 하 여 hello 상위 수준 (hello 비-"LL") Api toosend 및 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="eeee1-335">이러한 API를 사용하는 경우 이벤트 전송 및 메시지 수신을 모두 처리하는 백그라운드 스레드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="eeee1-336">그러나 hello 하위 (LL) Api tooeliminate이 백그라운드 스레드를 사용할 수 있으며 이벤트를 보내는 또는 hello 클라우드에서 메시지를 받을 통해 명시적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="eeee1-337">에 설명 된 대로 [이전 문서](iot-hub-device-sdk-c-iothubclient.md), hello로 구성 된 기능 집합이 더 높은 수준의 Api:</span><span class="sxs-lookup"><span data-stu-id="eeee1-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="eeee1-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="eeee1-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="eeee1-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="eeee1-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="eeee1-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="eeee1-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="eeee1-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="eeee1-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="eeee1-342">이러한 API는 **simplesample\_amqp**에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="eeee1-343">유사한 하위 수준 API 집합도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="eeee1-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="eeee1-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="eeee1-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="eeee1-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="eeee1-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="eeee1-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="eeee1-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="eeee1-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="eeee1-348">참고는 hello 하위 수준 Api 작업 정확 하 게 hello hello 이전 문서에서 설명 하는 방식으로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="eeee1-349">백그라운드 스레드 toohandle 메시지 이벤트 보내기 및 받기를 원하면 hello 첫 번째 집합의 Api 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="eeee1-350">Hello Api의 두 번째 집합을 사용 하 여 명시적으로 제어할 보내고 IoT 허브에서 데이터를 수신 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="eeee1-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="eeee1-351">Api 작업의 집합 중 하나가 hello로 동일 하 게 제대로 **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="eeee1-352">방법의 예에 대 한 hello 하위 Api 사용 hello로 **serializer** 라이브러리 참조 hello **simplesample\_http** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="eeee1-353">추가 항목</span><span class="sxs-lookup"><span data-stu-id="eeee1-353">Additional topics</span></span>
<span data-ttu-id="eeee1-354">속성 처리, 대체 장치 자격 증명 사용 및 구성 옵션은 다시 강조할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="eeee1-355">이러한 모든 항목은 [이전 문서](iot-hub-device-sdk-c-iothubclient.md)에서 다뤘습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="eeee1-356">hello 핵심인은 이러한 모든 기능은 작업 한다는 hello에서 동일한 방식으로 hello로 **serializer** 라이브러리 hello와 마찬가지로 **IoTHubClient** 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="eeee1-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="eeee1-357">예를 들어 모델에서 tooattach 속성 tooan 이벤트를 하려는 경우 사용 **IoTHubMessage\_속성** 및 **지도**\_**AddorUpdate**, 같은 방식으로 앞에서 설명한 hello:</span><span class="sxs-lookup"><span data-stu-id="eeee1-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="eeee1-358">Hello에서 hello 이벤트가 생성 된 여부 **serializer** 라이브러리 hello를 사용 하 여 수동으로 만든 또는 **IoTHubClient** 라이브러리는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="eeee1-359">Hello에 대 한 장치 자격 증명을 사용 하 여 대체 **IoTHubClient\_LL\_만들기** 작업으로 **IoTHubClient\_CreateFromConnectionString** 에 대 한 할당 된 **IOTHUB\_클라이언트\_처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="eeee1-360">마지막으로, hello를 사용 하 여 **serializer** 라이브러리 구성 옵션을 설정할 수 있습니다 **IoTHubClient\_LL\_SetOption** hello를사용하는경우와같이방금**IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="eeee1-361">고유 toohello 기능 **serializer** 라이브러리 Api hello 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="eeee1-362">Hello 라이브러리 사용을 시작 하기 전에 호출 해야 **serializer\_init**:</span><span class="sxs-lookup"><span data-stu-id="eeee1-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="eeee1-363">**IoTHubClient\_CreateFromConnectionString**을 호출하기 바로 전에 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="eeee1-364">마찬가지로, 다 hello 라이브러리, 사용 할 hello 마지막 호출이 너무**serializer\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="eeee1-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="eeee1-365">위에 나열 된 기타 기능 모두 hello 그렇지 않으면 작업 hello에 동일 hello **serializer** 라이브러리 hello에서와 마찬가지로 **IoTHubClient** 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="eeee1-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="eeee1-366">다음이 항목 중 하나에 대 한 자세한 내용은 참조 hello [이전 문서](iot-hub-device-sdk-c-iothubclient.md) 이 시리즈의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeee1-367">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eeee1-367">Next steps</span></span>
<span data-ttu-id="eeee1-368">이 문서에서는 자세히 hello hello의 고유한 측면에서 설명 **serializer** hello에 포함 된 라이브러리 **C에 대 한 Azure IoT 장치 SDK**합니다. 제공 된 hello 정보를 toouse toosend 이벤트를 모델링 하는 방법에 대해 잘 알고 있어야를 IoT 허브에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="eeee1-369">Hello 세 부분으로 이루어진 계열 toodevelop 응용 프로그램을 hello 하는 방법에 마쳤습니다 **C에 대 한 Azure IoT 장치 SDK**합니다. 이 되어야 충분 한 정보 toonot get 시작 하지만 hello Api 어떻게 작동 하는지에 대 한 철저 한 이해를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="eeee1-370">추가 정보에 대 한 hello SDK에서 다루지 않는 여기에서 몇 가지 샘플 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="eeee1-371">그렇지 않으면 hello [SDK 설명서](https://github.com/Azure/azure-iot-sdk-c) 추가 정보에 대 한 좋은 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="eeee1-372">IoT 허브에 대 한 개발에 대 한 더 toolearn 참조 hello [Azure IoT Sdk][lnk-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="eeee1-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="eeee1-373">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="eeee1-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="eeee1-374">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="eeee1-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
