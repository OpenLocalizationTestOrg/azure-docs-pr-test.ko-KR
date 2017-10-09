---
title: "aaaUse hello Azure 포털 tooconfigure 파일 업로드 | Microsoft Docs"
description: "Toouse hello Azure 포털 tooconfigure 방법 IoT 허브 tooenable 파일에 연결 된 장치에서 업로드 합니다. Hello 대상 Azure 저장소 계정을 구성 하는 방법에 대 한 정보가 포함 됩니다."
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
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="e761b-104">IoT Hub 파일 업로드 hello Azure 포털을 사용 하 여 구성</span><span class="sxs-lookup"><span data-stu-id="e761b-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="e761b-105">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="e761b-105">File upload</span></span>

<span data-ttu-id="e761b-106">toouse hello [IoT 허브에서 파일을 업로드 기능][lnk-upload], 허브와 Azure 저장소 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="e761b-107">선택 **파일 업로드** toodisplay 수정 하는 hello IoT 허브에 대 한 파일 업로드 속성의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![IoT Hub 파일 보기 업로드 hello 포털에서 설정][13]

<span data-ttu-id="e761b-109">**저장소 컨테이너**: 사용 하 여 hello Azure 포털 tooselect IoT Hub와 현재 Azure 구독 tooassociate 프로그램의 Azure 저장소 계정에서 blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="e761b-110">경우 필요에 따라 만들 수 있습니다는 Azure 저장소 계정에 hello **저장소 계정은** 블레이드 및 blob 컨테이너에서 hello **컨테이너** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="e761b-111">IoT Hub 때 자동으로 생성 SAS Uri toouse 장치에 대 한 쓰기 권한 toothis blob 컨테이너로 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Hello 포털에서 파일 업로드에 대 한 저장소 컨테이너 보기][14]

<span data-ttu-id="e761b-113">**업로드 된 파일에 대 한 알림을 수신**: hello 토글을 통해 파일 업로드 알림을 설정 하거나 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="e761b-114">**SAS TTL**:이 설정은-time-to-live의 SAS Uri IoT 허브에서 toohello 장치를 반환 하는 hello hello입니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="e761b-115">기본적으로 tooone 시간 설정 되지만 사용자 지정 된 tooother 값을 사용할 수도 hello 슬라이더 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="e761b-116">**파일 설정을 기본 TTL 알림**: hello time-to-live 만료 되기 전에 파일 업로드 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="e761b-117">Tooone 일은 기본적으로 설정 되지만 사용자 지정 된 tooother 값을 사용할 수도 hello 슬라이더 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="e761b-118">**알림 최대 배달 횟수 파일**: hello 횟수입니다. IoT Hub 시도 toodeliver 파일 업로드 알림 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="e761b-119">Too10 기본적으로 설정 되지만 사용자 지정 된 tooother 값을 사용할 수도 hello 슬라이더 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![IoT Hub 파일 업로드 hello 포털에서 구성][15]

## <a name="next-steps"></a><span data-ttu-id="e761b-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e761b-121">Next steps</span></span>

<span data-ttu-id="e761b-122">IoT Hub hello 파일 업로드 기능에 대 한 자세한 내용은 참조 [장치에서 파일을 업로드] [ lnk-upload] hello IoT 허브 개발자 가이드에서에서.</span><span class="sxs-lookup"><span data-stu-id="e761b-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="e761b-123">이러한 링크 toolearn Azure IoT Hub를 관리 하는 방법에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e761b-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="e761b-124">[IoT 장치 대량 관리][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="e761b-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="e761b-125">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="e761b-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="e761b-126">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="e761b-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="e761b-127">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e761b-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e761b-128">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="e761b-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="e761b-129">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e761b-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="e761b-130">[Hello 접지에서 IoT 솔루션 보안][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="e761b-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
