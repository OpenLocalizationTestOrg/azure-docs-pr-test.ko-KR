---
title: "Azure Portal을 사용하여 파일 업로드 구성 | Microsoft Docs"
description: "Azure Portal을 사용하여 연결된 장치에서 파일 로드를 사용하도록 IoT Hub를 구성하는 방법입니다. 대상 Azure Storage 계정 구성에 대한 정보가 포함됩니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="0d85d-104">Azure Portal을 사용하여 IoT Hub 파일 업로드 구성</span><span class="sxs-lookup"><span data-stu-id="0d85d-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="0d85d-105">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="0d85d-105">File upload</span></span>

<span data-ttu-id="0d85d-106">[IoT Hub에서 파일 업로드 기능][lnk-upload]을 사용하려면 먼저 Azure Storage 계정을 허브에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="0d85d-107">**파일 업로드**를 선택하여 수정하려는 IoT hub에 대한 파일 업로드 속성의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![포털에서 IoT Hub 파일 보기 설정 보기][13]

<span data-ttu-id="0d85d-109">**저장소 컨테이너**: Azure Portal을 사용하여 현재 Azure 구독의 Azure Storage 계정에서 Blob 컨테이너를 선택하고 IoT Hub와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="0d85d-110">필요에 따라 **Storage 계정** 블레이드에 Azure Storage 계정을 만들고 **컨테이너** 블레이드에 Blob 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="0d85d-111">IoT Hub는 파일을 업로드하는 경우에 사용할 장치에 대한 이 Blob 컨테이너에 쓰기 권한이 있는 SAS URI를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![포털에서 파일 업로드에 대한 저장소 컨테이너 보기][14]

<span data-ttu-id="0d85d-113">**업로드된 파일에 대한 알림 받기**: 토글을 통해 파일 업로드 알림을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="0d85d-114">**SAS TTL**: 이 설정은 IoT Hub에서 장치로 반환하는 SAS URI의 TTL(Time-to-Live)입니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="0d85d-115">기본적으로 1시간으로 설정되지만 슬라이더를 사용하여 다른 값으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="0d85d-116">**파일 알림 설정 기본 TTL**: 만료되기 전의 파일 업로드 알림 TTL입니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="0d85d-117">기본적으로 1시간으로 설정되지만 슬라이더를 사용하여 다른 값으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="0d85d-118">**파일 알림 최대 배달 횟수**: IoT Hub가 파일 업로드 알림 배달을 시도하는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="0d85d-119">기본적으로 10으로 설정되지만 슬라이더를 사용하여 다른 값으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d85d-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![포털에서 IoT Hub 파일 업로드 구성][15]

## <a name="next-steps"></a><span data-ttu-id="0d85d-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d85d-121">Next steps</span></span>

<span data-ttu-id="0d85d-122">IoT Hub의 파일 업로드 기능에 대한 자세한 내용은 IoT Hub 개발자 가이드의 [장치에서 파일 업로드][lnk-upload]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d85d-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="0d85d-123">Azure IoT Hub를 관리하는 방법에 대한 자세한 내용을 알아보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="0d85d-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="0d85d-124">[IoT 장치 대량 관리][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="0d85d-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="0d85d-125">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="0d85d-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="0d85d-126">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="0d85d-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="0d85d-127">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d85d-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0d85d-128">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="0d85d-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="0d85d-129">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0d85d-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="0d85d-130">[처음부터 IoT 솔루션 보안 유지][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="0d85d-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
