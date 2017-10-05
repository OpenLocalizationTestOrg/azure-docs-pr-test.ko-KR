---
title: "C용 Azure IoT 장치 SDK - 직렬 변환기 | Microsoft Docs"
description: "C용 Azure IoT 장치 SDK에서 Serializer 라이브러리를 사용하여 IoT Hub와 통신하는 장치 앱을 만드는 방법입니다."
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
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="dacd5-103">C용 Azure IoT 장치 SDK - 직렬 변환기에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="dacd5-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="dacd5-104">이 시리즈의 [첫 번째 문서](iot-hub-device-sdk-c-intro.md)에서는 **C용 Azure IoT 장치 SDK**에 대해 소개했습니다. 다음 문서에서 [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md)에 대해 보다 자세히 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="dacd5-105">이 문서에서는 나머지 구성 요소인 **serializer** 라이브러리에 대한 보다 자세한 설명을 제공하여 SDK의 범위를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="dacd5-106">소개 자료에서 **serializer** 라이브러리를 사용하여 IoT Hub로 이벤트를 보내고 메시지를 받는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="dacd5-107">이 문서에서는 **serializer** 매크로 언어로 데이터를 모델링하는 방법에 대한 자세한 설명을 제공하여 논의를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="dacd5-108">또한 라이브러리에서 메시지를 직렬화하고 직렬화 동작을 제어하는 방법도 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="dacd5-109">사용자가 만드는 모델의 크기를 결정하는 일부 매개 변수를 수정하는 방법에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="dacd5-110">마지막으로 메시지 및 속성 처리와 같은 이전 문서에서 다루는 일부 항목을 다시 상기시키는 것으로 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="dacd5-111">알다시피, **IoTHubClient** 라이브러리로 작업할 때와 마찬가지로 **serializer** 라이브러리를 사용할 때 해당 기능이 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="dacd5-112">이 문서에 설명된 모든 내용은 **serializer** SDK 샘플을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="dacd5-113">따라하려면 C용 Azure IoT 장치 SDK에 포함된 **simplesample\_amqp** 및 **simplesample\_http** 응용 프로그램을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="dacd5-114">GitHub 리포지토리에서 [**C용 Azure IoT 장치 SDK**](https://github.com/Azure/azure-iot-sdk-c)를 찾고 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)에서 API의 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="dacd5-115">모델링 언어</span><span class="sxs-lookup"><span data-stu-id="dacd5-115">The modeling language</span></span>
<span data-ttu-id="dacd5-116">이 시리즈의 [소개 자료](iot-hub-device-sdk-c-intro.md)에서는 **simplesample\_amqp** 응용 프로그램에 제공된 예제를 통해 **C용 Azure IoT 장치 SDK** 모델링 언어를 소개했습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="dacd5-117">여기에서 볼 수 있듯이 모델링 언어는 C 매크로를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="dacd5-118">항상 **BEGIN\_NAMESPACE**로 사용자 정의를 시작하고 **END\_NAMESPACE**로 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="dacd5-119">회사에 해당하는 네임스페이스로 이름을 지정하는 것이 일반적입니다(이 예제에서는 작업 중인 프로젝트에 해당하는 이름을 지정).</span><span class="sxs-lookup"><span data-stu-id="dacd5-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="dacd5-120">네임스페이스 내부에는 모델 정의가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="dacd5-121">이 경우 풍력계에 대한 단일 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="dacd5-122">다시 한 번 언급하지만 모델에 아무 이름이나 지정할 수 있지만 일반적으로 장치 또는 IoT Hub와 교환하려는 데이터의 형식에 해당하는 이름으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="dacd5-123">모델에는 IoT Hub로 들어오는 이벤트(*데이터*)와 IoT Hub로부터 수신할 수 있는 메시지(*동작*)에 대한 정의가 포합됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="dacd5-124">예제에서 볼 수 있듯이, 이벤트에는 형식 및 이름이, 동작에는 이름 및 선택적 매개 변수(각각 형식 포함)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="dacd5-125">이 샘플에서는 SDK에서 지원되는 추가 데이터 형식은 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="dacd5-126">다음에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="dacd5-127">IoT Hub는 장치에서 보내는 데이터를 *이벤트*로 참조하는 반면 모델링 언어는 *데이터*(**WITH_DATA**를 사용하여 정의됨)로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="dacd5-128">마찬가지로 IoT Hub는 사용자가 장치로 보내는 데이터를 *메시지*로 참조하는 반면 모델링 언어는 *동작*(**WITH_ACTION**을 사용하여 정의됨)으로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="dacd5-129">이 문서에서는 이러한 용어가 같은 의미로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="dacd5-130">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="dacd5-130">Supported data types</span></span>
<span data-ttu-id="dacd5-131">**serializer** 라이브러리로 만든 모델에 다음 데이터 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="dacd5-132">형식</span><span class="sxs-lookup"><span data-stu-id="dacd5-132">Type</span></span> | <span data-ttu-id="dacd5-133">설명</span><span class="sxs-lookup"><span data-stu-id="dacd5-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dacd5-134">double</span><span class="sxs-lookup"><span data-stu-id="dacd5-134">double</span></span> |<span data-ttu-id="dacd5-135">배정밀도 부동 소수점 숫자</span><span class="sxs-lookup"><span data-stu-id="dacd5-135">double precision floating point number</span></span> |
| <span data-ttu-id="dacd5-136">int</span><span class="sxs-lookup"><span data-stu-id="dacd5-136">int</span></span> |<span data-ttu-id="dacd5-137">32비트 정수</span><span class="sxs-lookup"><span data-stu-id="dacd5-137">32 bit integer</span></span> |
| <span data-ttu-id="dacd5-138">float</span><span class="sxs-lookup"><span data-stu-id="dacd5-138">float</span></span> |<span data-ttu-id="dacd5-139">단정밀도 부동 소수점 숫자</span><span class="sxs-lookup"><span data-stu-id="dacd5-139">single precision floating point number</span></span> |
| <span data-ttu-id="dacd5-140">long</span><span class="sxs-lookup"><span data-stu-id="dacd5-140">long</span></span> |<span data-ttu-id="dacd5-141">정수(Long)</span><span class="sxs-lookup"><span data-stu-id="dacd5-141">long integer</span></span> |
| <span data-ttu-id="dacd5-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="dacd5-142">int8\_t</span></span> |<span data-ttu-id="dacd5-143">8비트 정수</span><span class="sxs-lookup"><span data-stu-id="dacd5-143">8 bit integer</span></span> |
| <span data-ttu-id="dacd5-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="dacd5-144">int16\_t</span></span> |<span data-ttu-id="dacd5-145">16비트 정수</span><span class="sxs-lookup"><span data-stu-id="dacd5-145">16 bit integer</span></span> |
| <span data-ttu-id="dacd5-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="dacd5-146">int32\_t</span></span> |<span data-ttu-id="dacd5-147">32비트 정수</span><span class="sxs-lookup"><span data-stu-id="dacd5-147">32 bit integer</span></span> |
| <span data-ttu-id="dacd5-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="dacd5-148">int64\_t</span></span> |<span data-ttu-id="dacd5-149">64비트 정수</span><span class="sxs-lookup"><span data-stu-id="dacd5-149">64 bit integer</span></span> |
| <span data-ttu-id="dacd5-150">bool</span><span class="sxs-lookup"><span data-stu-id="dacd5-150">bool</span></span> |<span data-ttu-id="dacd5-151">부울</span><span class="sxs-lookup"><span data-stu-id="dacd5-151">boolean</span></span> |
| <span data-ttu-id="dacd5-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="dacd5-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="dacd5-153">ASCII 문자열</span><span class="sxs-lookup"><span data-stu-id="dacd5-153">ASCII string</span></span> |
| <span data-ttu-id="dacd5-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="dacd5-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="dacd5-155">날짜 시간 오프셋</span><span class="sxs-lookup"><span data-stu-id="dacd5-155">date time offset</span></span> |
| <span data-ttu-id="dacd5-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="dacd5-156">EDM\_GUID</span></span> |<span data-ttu-id="dacd5-157">GUID</span><span class="sxs-lookup"><span data-stu-id="dacd5-157">GUID</span></span> |
| <span data-ttu-id="dacd5-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="dacd5-158">EDM\_BINARY</span></span> |<span data-ttu-id="dacd5-159">binary</span><span class="sxs-lookup"><span data-stu-id="dacd5-159">binary</span></span> |
| <span data-ttu-id="dacd5-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="dacd5-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="dacd5-161">복합 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="dacd5-161">complex data type</span></span> |

<span data-ttu-id="dacd5-162">마지막 데이터 형식부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-162">Let’s start with the last data type.</span></span> <span data-ttu-id="dacd5-163">**DECLARE\_STRUCT**로 기타 기본 형식의 그룹인 복합 데이터 형식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="dacd5-164">이러한 그룹을 통해 다음과 같은 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-164">These groupings allow us to define a model that looks like this:</span></span>

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

<span data-ttu-id="dacd5-165">이 모델은 **TestType**형식의 단일 데이터 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="dacd5-166">**TestType**은 여러 멤버를 포함하는 복합 형식이며 **serializer** 모델링 언어에서 지원되는 기본 형식을 총칭합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="dacd5-167">이와 같은 모델로 다음과 같이 데이터를 IoT Hub로 보내는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="dacd5-168">기본적으로 **Test** 구조체의 모든 멤버에 값을 할당한 후 **SendAsync**를 호출하여 **Test** 데이터 이벤트를 클라우드로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="dacd5-169">**SendAsync** 는 단일 데이터 이벤트를 IoT Hub로 보내는 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
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

<span data-ttu-id="dacd5-170">이 함수는 지정된 데이터 이벤트를 직렬화하고 **IoTHubClient\_SendEventAsync**를 사용하여 IoT Hub에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="dacd5-171">이전 문서에서 설명했던 것과 동일한 코드입니다(**SendAsync** 는 논리를 편리한 함수로 캡슐화함).</span><span class="sxs-lookup"><span data-stu-id="dacd5-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="dacd5-172">이전 코드에 사용된 다른 도우미 함수는 **GetDateTimeOffset**입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="dacd5-173">이 함수는 지정된 시간을 **EDM\_DATE\_TIME\_OFFSET** 형식 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="dacd5-174">이 코드를 실행하는 경우 다음과 같은 메시지가 IoT Hub로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="dacd5-175">직렬화는 **serializer** 라이브러리로 생성되는 형식의 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="dacd5-176">또한 직렬화된 JSON 개체의 각 멤버가 모델에 정의한 **TestType** 의 멤버와 일치하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="dacd5-177">이 값은 코드에 사용된 것과도 정확히 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="dacd5-178">그러나 이진 데이터는 base64 인코드되며 "AQID"는 {0x01, 0x02, 0x03}의 base64 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="dacd5-179">이 예제에서는 **serializer** 라이브러리 사용 시의 이점을 보여 줍니다. 응용 프로그램에서 직렬화를 명시적으로 처리하지 않고도 JSON을 클라우드로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="dacd5-180">모델에서 데이터 이벤트 값을 설정한 후 간단한 API를 호출하여 해당 이벤트를 클라우드로 전송할 수 있으므로 세세한 사항을 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="dacd5-181">이 정보로 복합 형식을 비롯하여 지원되는 데이터 형식의 범위를 포함하는 모델을 정의할 수 있습니다(다른 복합 형식 내에 복합 형식을 포함할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="dacd5-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="dacd5-182">하지만 위의 예제에서 생성된 직렬화된 JSON에 중요한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="dacd5-183">*serializer* 라이브러리로 데이터를 전송하는 **방식** 에 따라 JSON이 형성되는 방식이 정확히 결정된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="dacd5-184">이러한 특별한 내용은 다음에 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="dacd5-185">직렬화에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="dacd5-185">More about serialization</span></span>
<span data-ttu-id="dacd5-186">이전 섹션에서는 **serializer** 라이브러리에서 생성되는 출력의 예에 대해 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="dacd5-187">이 섹션에서는 라이브러리가 데이터를 직렬화하는 방식과 직렬화 API를 사용하여 동작을 제어하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="dacd5-188">직렬화에 대한 논의를 진행하기 위해 자동 온도 조절기를 기반으로 하는 새 모델로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="dacd5-189">먼저, 해결하려는 시나리오에 대한 몇 가지 배경 지식을 제공하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="dacd5-190">우리는 온도 및 습도를 측정하는 자동 온도 조절기를 모델링하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="dacd5-191">각 데이터 조각은 IoT Hub로 다르게 전송될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="dacd5-192">기본적으로 자동 온도 조절기는 온도 이벤트는 2분에 한 번, 습도 이벤트는 15분에 한 번 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="dacd5-193">이벤트를 수신할 때는 해당 온도 또는 습도가 측정된 시간을 보여 주는 타임스탬프를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="dacd5-194">이 시나리오에서는 데이터를 모델링하는 두 가지 다른 방법을 시연하며 모델링이 직렬화된 출력에 어떤 영향을 주는지를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="dacd5-195">모델 1</span><span class="sxs-lookup"><span data-stu-id="dacd5-195">Model 1</span></span>
<span data-ttu-id="dacd5-196">다음은 이전 시나리오를 지원하는 모델의 첫 번째 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-196">Here's the first version of a model that supports the previous scenario:</span></span>

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

<span data-ttu-id="dacd5-197">이 모델은 **온도** 및 **습도**라는 두 가지 데이터 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="dacd5-198">이전 예와 달리 각 이벤트의 형식은 **DECLARE\_STRUCT**를 사용하여 정의된 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="dacd5-199">**TemperatureEvent**는 온도 측정 및 타임스탬프를 포함하고 **HumidityEvent**는 습도 측정 및 타임스탬프를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="dacd5-200">이 모델은 위에 설명된 시나리오에 대한 데이터를 모델링하는 자연스러운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="dacd5-201">이벤트를 클라우드로 전송할 때 온도/타임스탬프 또는 습도/타임스탬프 쌍으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="dacd5-202">다음과 같은 코드를 사용하여 클라우드에 온도 이벤트를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-202">We can send a temperature event to the cloud using code such as the following:</span></span>

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

<span data-ttu-id="dacd5-203">여기서는 샘플 코드에 하드 코드된 온도 및 습도 값을 사용하지만 자동 온도 조절기의 해당 센서를 샘플링하여 이러한 값을 실제로 가져온다고 상상해 보세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="dacd5-204">위의 코드는 이전에 소개된 **GetDateTimeOffset** 도우미를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="dacd5-205">나중에 이해가 쉽도록 이 코드에서는 직렬화와 이벤트 전송 작업을 명시적으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="dacd5-206">이전 코드는 온도 이벤트를 버퍼로 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="dacd5-207">다음으로 이벤트를 IoT Hub로 보내는 **sendMessage** 도우미 함수(**simplesample\_amqp**에 포함됨)입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

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

<span data-ttu-id="dacd5-208">이 코드는 이전 섹션에 설명된 **SendAsync** 도우미의 하위 집합으로 여기에서 다시 다루지 않겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="dacd5-209">이전 코드를 실행하여 온도 이벤트를 전송하면 이 직렬화된 이벤트 양식이 IoT Hub로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="dacd5-210">**TemperatureEvent** 형식의 온도를 전송하고 해당 구조체에는 **Temperature** 및 **Time** 멤버가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="dacd5-211">직렬화된 데이터에 이 내용이 직접 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="dacd5-212">마찬가지로 이 코드로 습도 이벤트도 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="dacd5-213">IoT Hub로 전송되는 직렬화된 양식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="dacd5-214">역시, 예상대로 입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-214">Again, this is as expected.</span></span>

<span data-ttu-id="dacd5-215">이 모델로 추가 이벤트를 어떻게 쉽게 추가할 수 있는지 생각해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="dacd5-216">**DECLARE\_STRUCT**를 사용하여 보다 많은 구조체를 정의하고 **WITH\_DATA**를 사용하여 해당 이벤트를 모델에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="dacd5-217">이제 동일한 데이터를 포함하지만 다른 구조체를 사용하도록 모델을 수정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="dacd5-218">모델 2</span><span class="sxs-lookup"><span data-stu-id="dacd5-218">Model 2</span></span>
<span data-ttu-id="dacd5-219">위에 대해 다음 대체 모델을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="dacd5-220">이 경우 **DECLARE\_STRUCT** 매크로를 제거했고 시나리오에서 모델링 언어의 단순 형식을 사용해서 데이터 항목을 정의하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="dacd5-221">잠시 **시간** 이벤트를 무시하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="dacd5-222">이와 별개로 다음은 **온도**를 수신하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

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

<span data-ttu-id="dacd5-223">이 코드는 다음 직렬화된 이벤트를 IoT Hub로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="dacd5-224">습도 이벤트를 전송하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="dacd5-225">이 코드는 다음을 IoT Hub로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="dacd5-226">지금까지 특별한 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-226">So far there are still no surprises.</span></span> <span data-ttu-id="dacd5-227">이제 SERIALIZE 매크로를 사용하는 방법을 변경해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="dacd5-228">**SERIALIZE** 매크로는 여러 데이터 이벤트를 인수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="dacd5-229">이를 통해 **온도** 및 **습도** 이벤트를 함께 직렬화하고 한 번의 호출로 IoT Hub로 이를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="dacd5-230">이 코드의 결과, 두 데이터 이벤트가 IoT Hub로 전송된다고 추측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="dacd5-231">[</span><span class="sxs-lookup"><span data-stu-id="dacd5-231">[</span></span>

<span data-ttu-id="dacd5-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="dacd5-232">{"Temperature":75},</span></span>

<span data-ttu-id="dacd5-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="dacd5-233">{"Humidity":45}</span></span>

<span data-ttu-id="dacd5-234">]</span><span class="sxs-lookup"><span data-stu-id="dacd5-234">]</span></span>

<span data-ttu-id="dacd5-235">즉, 이 코드는 **온도** 및 **습도**를 별도로 전송하는 것과 같다고 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="dacd5-236">두 이벤트를 **SERIALIZE** 하기 위해 동일한 호출로 전달하는 것은 단지 편의를 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="dacd5-237">그러나 이 경우는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-237">However, that’s not the case.</span></span> <span data-ttu-id="dacd5-238">대신, 위의 코드는 IoT Hub에 단일 데이터 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="dacd5-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="dacd5-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="dacd5-240">모델에서 **온도** 및 **습도**를 두 개의 *별도* 이벤트로 정의하므로 이것이 이상하게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="dacd5-241">더 중요한 것은 **온도** 및 **습도**가 동일한 구조체에 있는 이벤트를 모델링하지 않았다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="dacd5-242">이 모델을 사용한 경우에 **온도** 및 **습도**가 동일한 직렬화된 메시지로 전송되는 방식을 보다 쉽게 이해하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="dacd5-243">하지만 두 데이터 이벤트를 모델 2를 사용하여 **SERIALIZE** 로 전달하는 경우 왜 그렇게 작동하는지 명확하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="dacd5-244">이 동작은 **serializer** 라이브러리의 가정 사항을 알고 있는 경우 보다 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="dacd5-245">이해를 위해 모델을 다시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="dacd5-246">이 모델을 개체 지향 용어로 생각해봅니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="dacd5-247">이 경우 실제 장치(자동 온도 조절기)를 모델링하고 해당 장치가 **온도** 및 **습도**와 같은 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="dacd5-248">다음과 같은 코드를 사용하여 모델의 전체 상태를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="dacd5-249">온도, 습도 및 시간 값이 설정되어 있다고 가정하면 이와 같은 이벤트가 IoT Hub로 전송되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="dacd5-250">*일부* 속성만 클라우드로 전송하고 싶을 때가 많습니다(모델에 대량의 데이터 이벤트가 포함된 경우 특히 그러함).</span><span class="sxs-lookup"><span data-stu-id="dacd5-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="dacd5-251">이전 예제처럼 데이터 이벤트의 하위 집합만 전송하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="dacd5-252">그러면 **Temperature** 및 **Time** 멤버를 포함하는 **TemperatureEvent**를 정의한 것처럼 정확히 같은 직렬화된 이벤트를 생성합니다. 이것은 모델 1에서 진행했습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="dacd5-253">이 경우 **직렬화**를 다른 방식으로 호출했으므로 다른 모델(모델 2)을 사용하여 정확히 같은 직렬화된 이벤트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="dacd5-254">중요한 사항은 여러 데이터 이벤트를 **SERIALIZE** 로 전달하면 각 이벤트가 단일 JSON 개체의 속성인 것으로 가정한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="dacd5-255">최적의 접근 방식은 사용자와 사용자가 모델에 대해 어떻게 생각하는지에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="dacd5-256">"이벤트"를 클라우드로 전송하고 각 이벤트에 정의된 속성 집합이 있다면 첫 번째 접근 방식이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="dacd5-257">이 경우 **DECLARE\_STRUCT**를 사용하여 각 이벤트의 구조체를 정의한 후 **WITH\_DATA** 매크로를 사용하여 이를 모델에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="dacd5-258">그런 다음 위의 첫 번째 예에서 했던 것처럼 각 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="dacd5-259">이 접근 방식에서는 **SERIALIZER**로 단일 데이터 이벤트만 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="dacd5-260">모델을 개체 지향 방식으로 생각한다면 두 번째 접근 방식이 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="dacd5-261">이 경우에 **WITH\_DATA**를 사용하여 정의된 요소는 개체의 "속성"입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="dacd5-262">클라우드로 전송하려는 "개체" 상태의 양에 따라 이벤트의 하위 집합을 원하는 대로 **SERIALIZE** 로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="dacd5-263">어떤 접근 방식이 옳거나 그르다고 말할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="dacd5-264">**serializer** 라이브러리가 작동하는 방식을 이해하고 사용자의 요구에 가장 잘 맞는 모델링 접근 방식을 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="dacd5-265">메시지 처리</span><span class="sxs-lookup"><span data-stu-id="dacd5-265">Message handling</span></span>
<span data-ttu-id="dacd5-266">지금까지 이 문서에서는 이벤트를 IoT Hub에 전송하는 것에 대해서만 다루었으며 수신 메시지에 대해서는 다루지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="dacd5-267">수신 메시지에 대해 알아야 하는 내용을 [이전 문서](iot-hub-device-sdk-c-intro.md)에서 폭넓게 다뤘기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="dacd5-268">메시지 콜백 함수를 등록하여 메시지를 처리하는 문서를 상기해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="dacd5-269">그런 다음 메시지를 수신할 때 호출되는 호출 함수를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="dacd5-270">**IoTHubMessage** 구현에서는 모델의 각 작업에 대해 특정 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="dacd5-271">예를 들어 모델에서 다음 동작을 정의하는 경우:</span><span class="sxs-lookup"><span data-stu-id="dacd5-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="dacd5-272">다음 서명과 함께 함수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="dacd5-273">**SetAirResistance** 가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="dacd5-274">직렬화된 버전의 메시지가 어떤 모습인지는 아직 설명하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="dacd5-275">즉, **SetAirResistance** 메시지를 장치로 전송하는 경우 어떤 모습일까요?</span><span class="sxs-lookup"><span data-stu-id="dacd5-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="dacd5-276">메시지를 장치로 전송하는 경우 Azure IoT 서비스 SDK를 통해 수행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="dacd5-277">특정 동작을 호출하기 위해 어떤 문자열을 전송하는지 여전히 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="dacd5-278">메시지 전송을 위한 일반적인 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="dacd5-279">다음 두 속성으로 직렬화된 JSON 개체를 전송합니다. **Name**은 작업(메시지)의 이름이고 **Parameters**는 해당 작업의 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="dacd5-280">예를 들어 **SetAirResistance** 를 호출하려면 다음 메시지를 장치에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="dacd5-281">동작 이름은 모델에 정의된 동작과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="dacd5-282">매개 변수 이름도 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-282">The parameter names must match as well.</span></span> <span data-ttu-id="dacd5-283">또한 대/소문자 구분 여부도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-283">Also note case sensitivity.</span></span> <span data-ttu-id="dacd5-284">**Name** 및 **Parameters**는 항상 대문자입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="dacd5-285">모델에서 동작 이름 및 매개 변수의 대/소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="dacd5-286">이 예에서 동작 이름은 "setairresistance"가 아닌, "SetAirResistance"입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="dacd5-287">두 가지 작업 **TurnFanOn** 및 **TurnFanOff**는 장치에 다음 메시지를 전송하여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="dacd5-288">이 섹션에서는 **serializer** 라이브러리로 이벤트를 전송하고 메시지를 수신할 때 알아야 할 모든 내용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="dacd5-289">설명을 진행하기 전에, 모델의 크기를 제어하기 위해 구성할 수 있는 몇 가지 매개 변수에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="dacd5-290">매크로 구성</span><span class="sxs-lookup"><span data-stu-id="dacd5-290">Macro configuration</span></span>
<span data-ttu-id="dacd5-291">**Serializer** 라이브러리를 사용하는 경우 알아야 할 SDK의 중요한 내용은 azure-c-shared-utility 라이브러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="dacd5-292">--recursive 옵션을 사용하여 GitHub에서 Azure-iot-sdk-c 리포지토리를 복제한 경우 이 공유 유틸리티 라이브러리를 다음에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="dacd5-293">라이브러리를 복제하지 않은 경우 [여기](https://github.com/Azure/azure-c-shared-utility)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="dacd5-294">공유 유틸리티 라이브러리 내에서 다음 폴더를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="dacd5-295">이 폴더에는 **macro\_utils\_h\_generator.sln**이라는 Visual Studio 솔루션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="dacd5-296">이 솔루션의 프로그램은 **macro\_utils.h** 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="dacd5-297">SDK에 포함된 기본 macro\_utils.h 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="dacd5-298">이 솔루션을 사용하면 일부 매개 변수를 수정하고 이러한 매개 변수를 기반으로 헤더 파일을 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="dacd5-299">여기서 고려할 두 가지 핵심 매개 변수는 **nArithmetic** 및 **nMacroParameters**이며 macro\_utils.tt에 있는 다음 두 줄로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="dacd5-300">이러한 값은 SDK에 포함된 기본 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="dacd5-301">각 매개 변수는 다음과 같은 의미를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="dacd5-302">nMacroParameters – 하나의 DECLARE\_MODEL 매크로 정의에 포함할 수 있는 매개 변수 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="dacd5-303">nArithmetic – 모델에 허용되는 총 멤버 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="dacd5-304">이러한 매개 변수는 모델이 얼마나 큰지를 제어하기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="dacd5-305">예를 들어 다음 모델 정의를 고려해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="dacd5-306">이전에 설명한 것처럼 **DECLARE\_MODEL**은 C 매크로입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="dacd5-307">모델 및 **WITH\_DATA** 문(아직 다른 매크로)의 이름은 **DECLARE\_MODEL**의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="dacd5-308">**nMacroParameters**는 **DECLARE\_MODEL**에 포함할 수 있는 매개 변수 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="dacd5-309">이러한 매개 변수는 포함할 수 있는 데이터 이벤트 및 동작 선언 수를 효과적으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="dacd5-310">이와 같이 기본 제한 124를 사용하면 약 60개의 동작과 데이터 이벤트 조합을 포함하는 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="dacd5-311">이 제한을 초과하려고 하는 경우 다음과 같은 컴파일러 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="dacd5-312">**nArithmetic** 매개 변수는 응용 프로그램보다는 매크로 언어의 내부 작업에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="dacd5-313">**DECLARE_STRUCT** 매크로를 비롯하여 모델에 포함할 수 있는 총 멤버 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="dacd5-314">다음과 같은 컴파일러 오류가 표시되면 **nArithmetic**을 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="dacd5-315">이러한 매개 변수를 변경하려는 경우 macro\_utils.tt 파일의 값을 수정하고 macro\_utils\_h\_generator.sln 솔루션을 다시 컴파일하고 컴파일한 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="dacd5-316">이렇게 하면 새 macro\_utils.h 파일이 생성되고 .\\common\\inc 디렉터리에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="dacd5-317">새 버전의 macro\_utils.h를 사용하려면 솔루션에서 **serializer** NuGet 패키지를 제거하고 대신 그 자리에 **serializer** Visual Studio 프로젝트를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="dacd5-318">이렇게 하면 serializer 라이브러리의 소스 코드에 대해 코드를 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="dacd5-319">여기에는 업데이트된 macro\_utils.h가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="dacd5-320">**simplesample\_amqp**에 대해 이 작업을 수행하려면 먼저 솔루션에서 serializer 라이브러리에 대해 NuGet 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="dacd5-321">그런 다음 Visual Studio 솔루션에 이 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="dacd5-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="dacd5-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="dacd5-323">완료되면 다음과 같이 솔루션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="dacd5-324">이제 솔루션을 컴파일할 때 업데이트된 macro\_utils.h가 라이브러리에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="dacd5-325">이 값을 너무 높게 늘리면 컴파일러 한계를 초과할 수 있음에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="dacd5-326">이 시점까지 **nMacroParameters** 가 고려해야 할 주요 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="dacd5-327">C99 사양에서는 매크로 정의에서 최소 127개의 매개 변수를 허용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="dacd5-328">Microsoft 컴파일러는 이 사양을 정확히 따르므로(127개의 제한) **nMacroParameters** 를 기본값을 초과하도록 늘릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="dacd5-329">다른 컴파일러에서는 허용될 수도 있습니다(예를 들어 GNU 컴파일러는 보다 높은 제한 지원).</span><span class="sxs-lookup"><span data-stu-id="dacd5-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="dacd5-330">지금까지 **serializer** 라이브러리로 코드를 작성하는 방법에 대해 알아야 하는 모든 내용을 살펴봤습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="dacd5-331">마무리하기 전에 궁금해할 수 있는 이전 문서의 일부 항목을 다시 확인해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="dacd5-332">하위 수준 API</span><span class="sxs-lookup"><span data-stu-id="dacd5-332">The lower-level APIs</span></span>
<span data-ttu-id="dacd5-333">이 문서에서 집중적으로 다룬 응용 프로그램 예제는 **simplesample\_amqp**입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="dacd5-334">이 샘플에서는 상위 수준(비-"LL") API를 사용하여 이벤트를 보내고 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="dacd5-335">이러한 API를 사용하는 경우 이벤트 전송 및 메시지 수신을 모두 처리하는 백그라운드 스레드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="dacd5-336">그러나 LL(하위 수준) API를 사용하여 이 백그라운드 스레드를 제거하고 이벤트를 전송하거나 클라우드에서 메시지를 수신하는 경우 명시적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="dacd5-337">설명한 대로 [이전 문서](iot-hub-device-sdk-c-iothubclient.md)에서 설명한 것처럼 상위 수준 API로 구성된 함수 집합이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="dacd5-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="dacd5-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="dacd5-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="dacd5-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="dacd5-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="dacd5-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="dacd5-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="dacd5-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="dacd5-342">이러한 API는 **simplesample\_amqp**에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="dacd5-343">유사한 하위 수준 API 집합도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="dacd5-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="dacd5-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="dacd5-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="dacd5-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="dacd5-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="dacd5-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="dacd5-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="dacd5-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="dacd5-348">하위 수준 API가 이전 문서에서 설명한 것과 정확히 동일하게 작동한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="dacd5-349">백그라운드 스레드에서 이벤트 전송 및 메시지 수신을 처리하도록 하려면 첫 번째 API 집합을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="dacd5-350">IoT Hub에서 데이터를 전송 및 수신할 때 명시적으로 제어하려면 두 번째 API 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="dacd5-351">어떤 API 집합을 사용하든 **serializer** 라이브러리에서 모두 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="dacd5-352">**serializer** 라이브러리와 하위 수준 API를 사용하는 방법에 대한 예제는 **simplesample\_http** 응용 프로그램을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="dacd5-353">추가 항목</span><span class="sxs-lookup"><span data-stu-id="dacd5-353">Additional topics</span></span>
<span data-ttu-id="dacd5-354">속성 처리, 대체 장치 자격 증명 사용 및 구성 옵션은 다시 강조할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="dacd5-355">이러한 모든 항목은 [이전 문서](iot-hub-device-sdk-c-iothubclient.md)에서 다뤘습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="dacd5-356">중요한 점은 **IoTHubClient** 라이브러리로 작업할 때와 마찬가지로 **serializer** 라이브러리를 사용할 때 해당 기능이 동일하게 작동한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="dacd5-357">예를 들어 모델에서 이벤트에 속성을 첨부하려는 경우 **IoTHubMessage\_Properties** 및 **Map**\_**AddorUpdate**는 이전에 설명한 것과 동일한 방식으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="dacd5-358">이벤트가 **serializer** 라이브러리에서 생성되었든, 직접 작성되었든, **IoTHubClient** 라이브러리 사용은 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="dacd5-359">대체 장치 자격 증명의 경우 **IoTHubClient\_LL\_Create**를 사용하는 것은 **IOTHUB\_CLIENT\_HANDLE**을 할당하기 위한 **IoTHubClient\_CreateFromConnectionString** 만큼이나 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="dacd5-360">마지막으로, **serializer** 라이브러리를 사용하는 경우 **IoTHubClient** 라이브러리를 사용할 때 했던 것처럼 **IoTHubClient\_LL\_SetOption**으로 구성 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="dacd5-361">**serializer** 라이브러리에서 기능은 초기화 API입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="dacd5-362">라이브러리 작업을 시작하기 전에 **serializer\_init**를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="dacd5-363">**IoTHubClient\_CreateFromConnectionString**을 호출하기 바로 전에 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="dacd5-364">마찬가지로 라이브러리 작업을 완료한 후 마지막 호출은 **serializer\_deinit**입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="dacd5-365">이 밖의 위에 나열된 기타 모든 기능은 **serializer** 라이브러리에서 **IoTHubClient** 라이브러리와 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="dacd5-366">이러한 항목에 대한 자세한 내용은 이 시리즈의 [이전 문서](iot-hub-device-sdk-c-iothubclient.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dacd5-367">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dacd5-367">Next steps</span></span>
<span data-ttu-id="dacd5-368">이 문서는 **C용 Azure IoT 장치 SDK**에 포함된 **serializer** 라이브러리의 고유한 측면에 대해 자세히 설명합니다. 제공된 정보로 모델을 사용하여 이벤트를 전송하고 IoT Hub에서 메시지를 수신하는 방법을 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="dacd5-369">또한 **C용 Azure IoT 장치 SDK**로 응용 프로그램을 개발하는 방법에 대한 3부로 구성된 시리즈를 완료합니다. API를 시작하는 방법뿐만 아니라 API의 작동 방식을 매우 정확하게 이해할 수 있는 충분한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="dacd5-370">자세한 정보를 위해 여기에서 다루지 않은 몇 가지 샘플이 SDK에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="dacd5-371">또는 [SDK 설명서](https://github.com/Azure/azure-iot-sdk-c) 가 추가 정보를 얻을 수 있는 훌륭한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="dacd5-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="dacd5-372">IoT Hub를 개발하는 방법에 대한 자세한 내용은 [Azure IoT SDK][lnk-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="dacd5-373">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dacd5-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="dacd5-374">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="dacd5-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
