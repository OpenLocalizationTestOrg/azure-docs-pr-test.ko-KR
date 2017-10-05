---
title: "Azure IoT Hub 방법 | Microsoft Docs"
description: "개발자로서 다양한 IoT Hub 기능을 어떻게 사용합니까?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 786121ae249d69376b4be4c74000868cbb208989
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-iot-hub"></a><span data-ttu-id="3ac1b-103">Azure IoT Hub 사용 방법</span><span class="sxs-lookup"><span data-stu-id="3ac1b-103">How to use Azure IoT Hub</span></span>

<span data-ttu-id="3ac1b-104">IoT Hub 서비스를 개발하는 방법을 알아보는 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-104">You have various options to learn how to develop for the IoT Hub service:</span></span>

* <span data-ttu-id="3ac1b-105">IoT Hub의 기능을 자세히 설명하는 개념 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-105">Read the conceptual articles that describe the features of IoT Hub in detail.</span></span>
* <span data-ttu-id="3ac1b-106">IoT Hub의 다양한 기능을 다루는 자습서 중 하나를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-106">Follow one of the tutorials that cover the various features of IoT Hub.</span></span>

## <a name="developer-guide"></a><span data-ttu-id="3ac1b-107">개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="3ac1b-107">Developer guide</span></span>

<span data-ttu-id="3ac1b-108">개발자로서 [개발자 가이드][lnk-devguide]에서 IoT Hub에 대한 자세한 개념적 지침을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-108">As a developer, you can read detailed conceptual guidance about IoT Hub in the [Developer Guide][lnk-devguide].</span></span> <span data-ttu-id="3ac1b-109">이 가이드에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-109">This guide includes:</span></span>

* <span data-ttu-id="3ac1b-110">사용 방법을 배울 수 있는 모든 IoT Hub 기능에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="3ac1b-110">Detailed descriptions of all IoT Hub features that help you to learn how to use them.</span></span>
* <span data-ttu-id="3ac1b-111">여러 옵션을 사용할 수 있는 경우 선택하는 방법에 대한 지침</span><span class="sxs-lookup"><span data-stu-id="3ac1b-111">Guidance on how to choose when multiple options are available.</span></span>

## <a name="tutorials"></a><span data-ttu-id="3ac1b-112">자습서</span><span class="sxs-lookup"><span data-stu-id="3ac1b-112">Tutorials</span></span>

<span data-ttu-id="3ac1b-113">실습 연습을 통해 특정 IoT Hub 기능에 대해 자세히 알아보려는 경우 여러 자습서에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-113">If you prefer to learn about specific IoT Hub features by working through hands-on exercises, there are several tutorials to choose from.</span></span> <span data-ttu-id="3ac1b-114">대부분의 자습서는 여러 프로그래밍 언어로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-114">Many of these tutorials are available in multiple programming languages.</span></span> <span data-ttu-id="3ac1b-115">이 자습서는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-115">These tutorials include:</span></span>

- <span data-ttu-id="3ac1b-116">[경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리][lnk-routes-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-116">[Process IoT Hub device-to-cloud messages using routes][lnk-routes-tutorial].</span></span> <span data-ttu-id="3ac1b-117">이 자습서는 IoT Hub 라우팅 규칙을 사용하여 손쉬운 구성 기반 방식으로 장치-클라우드 메시지를 발송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-117">This tutorial shows you how to use IoT Hub routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>

- <span data-ttu-id="3ac1b-118">[IoT Hub를 사용하여 클라우드-장치 메시지 보내기][lnk-c2d-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-118">[Send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial].</span></span> <span data-ttu-id="3ac1b-119">이 자습서는 IoT Hub를 통해 클라우드-장치 메시지를 보내고 장치에서 클라우드-장치 메시지를 수신하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-119">This tutorial shows you how to send cloud-to-device messages through IoT Hub and receive cloud-to-device messages on a device.</span></span>

- <span data-ttu-id="3ac1b-120">[IoT Hub를 사용하여 장치에서 클라우드로 파일 업로드][lnk-upload-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-120">[Upload files from devices to the cloud with IoT Hub][lnk-upload-tutorial].</span></span> <span data-ttu-id="3ac1b-121">이 자습서는 IoT Hub의 파일 업로드 기능을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-121">This tutorial shows you how to use the file upload capabilities of IoT Hub.</span></span>

- <span data-ttu-id="3ac1b-122">[장치 쌍 시작][lnk-twin-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-122">[Get started with device twins][lnk-twin-tutorial].</span></span> <span data-ttu-id="3ac1b-123">이 자습서는 장치 쌍, reported 속성, desired 속성 및 태그를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-123">This tutorial introduces you to device twins, reported properties, desired properties, and tags.</span></span> <span data-ttu-id="3ac1b-124">장치 쌍을 사용하여 장치와 값을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-124">You use device twins to synchronize values with your devices.</span></span>

- <span data-ttu-id="3ac1b-125">[직접 메서드 사용][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-125">[Use direct methods][lnk-methods-tutorial].</span></span> <span data-ttu-id="3ac1b-126">이 자습서는 직접 메서드를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-126">This tutorial shows you how to use direct methods.</span></span> <span data-ttu-id="3ac1b-127">시뮬레이션된 장치에서 직접 메서드에 대한 처리기를 추가하고 IoT Hub에서 직접 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-127">You add a handler for a direct method in your simulated device and invoke the direct method from IoT Hub.</span></span>

- <span data-ttu-id="3ac1b-128">[장치 관리 시작][lnk-dm-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-128">[Get started with device management][lnk-dm-tutorial].</span></span> <span data-ttu-id="3ac1b-129">이 자습서는 쌍 및 직접 메서드와 같은 주요 장치 관리 기능을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-129">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="3ac1b-130">시뮬레이션된 장치를 원격으로 다시 부팅하는 데 이러한 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-130">You use these features to remotely reboot your simulated device.</span></span>

- <span data-ttu-id="3ac1b-131">[desired 속성을 사용하여 장치 구성][lnk-properties-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-131">[Use desired properties to configure devices][lnk-properties-tutorial].</span></span> <span data-ttu-id="3ac1b-132">이 자습서는 장치를 원격으로 구성하기 위해 장치 쌍의 desired 및 reported 속성을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-132">This tutorial shows you how to use the device twin's desired and reported properties, to remotely configure your device.</span></span>

- <span data-ttu-id="3ac1b-133">[장치 작업을 사용하여 장치 펌웨어 업데이트 시작][lnk-jobs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-133">[Use device jobs to initiate a device firmware update][lnk-jobs-tutorial].</span></span> <span data-ttu-id="3ac1b-134">이 자습서는 쌍 및 직접 메서드와 같은 주요 장치 관리 기능을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-134">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="3ac1b-135">이러한 기능을 사용하여 장치의 펌웨어를 원격으로 업데이트하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-135">You learn how to use these features to remotely update your device's firmware.</span></span>

- <span data-ttu-id="3ac1b-136">[작업 예약 및 브로드캐스트][lnk-schedule-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3ac1b-136">[Schedule and broadcast jobs][lnk-schedule-tutorial].</span></span> <span data-ttu-id="3ac1b-137">이 자습서는 예약된 시간에 여러 장치와 상호 작용하기 위해 desired 속성과 직접 메서드를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-137">This tutorial shows you how to use desired properties and direct methods to interact with multiple devices at a scheduled time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac1b-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ac1b-138">Next steps</span></span>

<span data-ttu-id="3ac1b-139">IoT Hub 서비스에 대한 자세한 내용을 보려면 [개발자 가이드][lnk-devguide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ac1b-139">To learn more about the IoT Hub service, see the [Developer Guide][lnk-devguide].</span></span>

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md