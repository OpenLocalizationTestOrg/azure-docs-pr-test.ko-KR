---
title: "aaaConfigure 파일 업로드 tooIoT Azure CLI (az.py)를 사용 하 여 허브 | Microsoft Docs"
description: "어떻게 tooconfigure fileuploads tooAzure IoT 허브를 사용 하 여 플랫폼 간 Azure CLI 2.0 (az.py) hello 합니다."
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
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="47aa5-103">Azure CLI를 사용하여 IoT Hub 파일 업로드 구성</span><span class="sxs-lookup"><span data-stu-id="47aa5-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="47aa5-104">toouse hello [IoT 허브에서 파일을 업로드 기능][lnk-upload], IoT hub와 Azure 저장소 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="47aa5-105">기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="47aa5-106">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="47aa5-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="47aa5-107">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="47aa5-107">An active Azure account.</span></span> <span data-ttu-id="47aa5-108">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="47aa5-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="47aa5-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="47aa5-110">Azure IoT Hub -</span><span class="sxs-lookup"><span data-stu-id="47aa5-110">An Azure IoT hub.</span></span> <span data-ttu-id="47aa5-111">IoT hub를 설정 하지 않은 경우에 hello을 사용할 수 있습니다 `az iot hub create` [명령] [ lnk-cli-create-iothub] toocreate 하나 또는 사용 하 여 hello 포털 너무 [IoT hub 만들기] [lnk 포털 허브].</span><span class="sxs-lookup"><span data-stu-id="47aa5-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="47aa5-112">Azure Storage 계정.</span><span class="sxs-lookup"><span data-stu-id="47aa5-112">An Azure Storage account.</span></span> <span data-ttu-id="47aa5-113">Azure 저장소 계정이 없으면 hello를 사용할 수 있습니다 [Azure CLI 2.0-저장소 계정 관리] [ lnk-manage-storage] toocreate 하나 또는 사용 하 여 hello 포털 너무[저장소 계정을 만드는] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="47aa5-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="47aa5-114">Azure 계정 로그인 및 설정</span><span class="sxs-lookup"><span data-stu-id="47aa5-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="47aa5-115">Azure 계정 tooyour 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="47aa5-116">Hello 명령 프롬프트에서 실행 hello [로그인 명령][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="47aa5-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="47aa5-117">Hello 코드를 사용 하 여 hello 지침 tooauthenticate 따르고 tooyour 웹 브라우저를 통해 Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="47aa5-118">TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="47aa5-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="47aa5-119">Hello 다음을 사용 하 여 [명령 toolist hello Azure 계정] [ lnk-az-account-command] toouse 있습니다 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="47aa5-120">다음 명령은 tooselect 구독 toouse toorun hello 명령을 toocreate IoT 허브를 지정 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="47aa5-121">Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="47aa5-122">저장소 계정 세부 정보 검색</span><span class="sxs-lookup"><span data-stu-id="47aa5-122">Retrieve your storage account details</span></span>

<span data-ttu-id="47aa5-123">hello 다음 단계에서는 가정 hello를 사용 하 여 저장소 계정을 만든 **리소스 관리자** 배포 모델 및 하지 hello **클래식** 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="47aa5-124">tooconfigure 파일을 업로드 하 여 장치에서 Azure 저장소 계정에 대 한 연결 문자열 hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="47aa5-125">저장소 계정 hello hello에 있어야 합니다. IoT hub와 같은 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="47aa5-126">Hello 저장소 계정에서 blob 컨테이너의 hello 이름도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="47aa5-127">다음 명령은 tooretrieve hello 저장소 계정 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="47aa5-128">Hello 메모 **connectionString** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="47aa5-129">단계를 수행 하는 hello에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-129">You need it in hello following steps.</span></span>

<span data-ttu-id="47aa5-130">파일 업로드에 기존 Blob 컨테이너를 사용하거나 새 Blob 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="47aa5-131">저장소 계정의 toolist hello 기존 blob 컨테이너 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="47aa5-132">다음 명령을 사용 하 여 hello 저장소 계정에서 blob 컨테이너 toocreate:</span><span class="sxs-lookup"><span data-stu-id="47aa5-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="47aa5-133">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="47aa5-133">File upload</span></span>

<span data-ttu-id="47aa5-134">IoT 허브 tooenable 구성할 수 있습니다 [파일 업로드 기능] [ lnk-upload] 저장소 계정 세부 정보를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="47aa5-135">hello 구성에는 다음 값에는 hello를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="47aa5-136">**저장소 컨테이너**: IoT hub와 현재 Azure 구독 tooassociate 프로그램의 Azure 저장소 계정에서 blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="47aa5-137">Hello 섹션 앞의 hello 필요한 저장소 계정 정보를 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="47aa5-138">IoT Hub 때 자동으로 생성 SAS Uri toouse 장치에 대 한 쓰기 권한 toothis blob 컨테이너로 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="47aa5-139">**업로드된 파일에 대한 알림 받기**: 파일 업로드 알림을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="47aa5-140">**SAS TTL**:이 설정은-time-to-live의 SAS Uri IoT 허브에서 toohello 장치를 반환 하는 hello hello입니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="47aa5-141">기본적으로 tooone 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-141">Set tooone hour by default.</span></span>

<span data-ttu-id="47aa5-142">**파일 설정을 기본 TTL 알림**: hello time-to-live 만료 되기 전에 파일 업로드 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="47aa5-143">기본적으로 tooone 하루를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-143">Set tooone day by default.</span></span>

<span data-ttu-id="47aa5-144">**알림 최대 배달 횟수 파일**: hello 횟수입니다. IoT Hub 시도 toodeliver 파일 업로드 알림 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="47aa5-145">기본적으로 too10를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-145">Set too10 by default.</span></span>

<span data-ttu-id="47aa5-146">Hello Azure CLI 명령을 tooconfigure hello 파일 업로드 설정 IoT 허브에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="47aa5-147">Bash 셸에서 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="47aa5-148">Windows 명령 프롬프트에서 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="47aa5-149">다음 명령을 hello를 사용 하 여 IoT 허브에서 파일 업로드 구성 hello를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="47aa5-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47aa5-150">Next steps</span></span>

<span data-ttu-id="47aa5-151">IoT Hub hello 파일 업로드 기능에 대 한 자세한 내용은 참조 [장치에서 파일을 업로드][lnk-upload]합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="47aa5-152">이러한 링크 toolearn Azure IoT Hub를 관리 하는 방법에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="47aa5-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="47aa5-153">[IoT 장치 대량 관리][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="47aa5-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="47aa5-154">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="47aa5-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="47aa5-155">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="47aa5-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="47aa5-156">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="47aa5-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="47aa5-157">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="47aa5-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="47aa5-158">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="47aa5-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="47aa5-159">[Hello 접지에서 IoT 솔루션 보안][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="47aa5-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create