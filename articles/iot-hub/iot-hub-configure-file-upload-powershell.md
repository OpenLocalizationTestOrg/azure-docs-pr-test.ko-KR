---
title: "Azure PowerShell을 사용하여 파일 업로드 구성 | Microsoft Docs"
description: "Azure PowerShell cmdlet을 사용하여 연결된 장치에서 파일 업로드를 사용하도록 IoT Hub를 구성하는 방법입니다. 대상 Azure Storage 계정 구성에 대한 정보가 포함됩니다."
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="42f29-104">Azure PowerShell을 사용하여 IoT Hub 파일 업로드 구성</span><span class="sxs-lookup"><span data-stu-id="42f29-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="42f29-105">[IoT Hub의 파일 업로드 기능][lnk-upload]을 사용하려면 먼저 Azure 저장소 계정을 IoT Hub에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="42f29-106">기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="42f29-107">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="42f29-108">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="42f29-108">An active Azure account.</span></span> <span data-ttu-id="42f29-109">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="42f29-110">[Azure PowerShell cmdlet][lnk-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="42f29-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="42f29-111">Azure IoT Hub -</span><span class="sxs-lookup"><span data-stu-id="42f29-111">An Azure IoT hub.</span></span> <span data-ttu-id="42f29-112">IoT Hub가 없는 경우 [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub]을 사용하여 IoT Hub를 만들거나, 포털을 사용하여[IoT Hub를 만들][lnk-portal-hub] 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="42f29-113">Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="42f29-113">An Azure storage account.</span></span> <span data-ttu-id="42f29-114">Azure 저장소 계정이 없는 경우 [Azure Storage PowerShell cmdlet][lnk-powershell-storage]을 사용하여 저장소 계정을 만들거나, 포털을 사용하여[저장소 계정을 만들][lnk-portal-storage] 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="42f29-115">Azure 계정 로그인 및 설정</span><span class="sxs-lookup"><span data-stu-id="42f29-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="42f29-116">Azure 계정에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="42f29-117">PowerShell 프롬프트에서 **Login-AzureRmAccount** cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="42f29-118">Azure 구독이 여러 개 있는 경우 Azure에 로그인하면 자격 증명과 연결된 모든 Azure 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="42f29-119">다음 명령을 사용하여 사용할 수 있는 Azure 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="42f29-120">다음 명령을 사용하여 IoT Hub를 관리하는 명령을 실행하는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="42f29-121">이전 명령의 출력에서 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="42f29-122">저장소 계정 세부 정보 검색</span><span class="sxs-lookup"><span data-stu-id="42f29-122">Retrieve your storage account details</span></span>

<span data-ttu-id="42f29-123">다음 단계에서는 **클래식** 배포 모델이 아니라 **Resource Manager** 배포 모델을 사용하여 저장소 계정을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="42f29-124">장치에서 파일 업로드를 구성하려면 Azure 저장소 계정에 대한 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="42f29-125">저장소 계정은 IoT Hub와 동일한 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="42f29-126">또한 저장소 계정에 Blob 컨테이너의 이름도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="42f29-127">다음 명령을 사용하여 저장소 계정 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="42f29-128">**key1** 저장소 계정 키 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="42f29-129">다음 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-129">You need it in the following steps.</span></span>

<span data-ttu-id="42f29-130">파일 업로드에 기존 Blob 컨테이너를 사용하거나 새 Blob 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="42f29-131">저장소 계정의 기존 Blob 컨테이너를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="42f29-132">저장소 계정에 Blob 컨테이너를 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="42f29-133">IoT Hub 구성</span><span class="sxs-lookup"><span data-stu-id="42f29-133">Configure your IoT hub</span></span>

<span data-ttu-id="42f29-134">이제 저장소 계정 세부 정보를 사용하여 [파일 업로드 기능][lnk-upload]을 사용하도록 IoT Hub를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="42f29-135">구성에는 다음 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-135">The configuration requires the following values:</span></span>

<span data-ttu-id="42f29-136">**저장소 컨테이너**: 현재 Azure 구독에 있는 Azure 저장소 계정의 Blob 컨테이너로 IoT Hub와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="42f29-137">이전 섹션에서 필요한 저장소 계정 정보를 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="42f29-138">IoT Hub는 파일을 업로드하는 경우에 사용할 장치에 대한 이 Blob 컨테이너에 쓰기 권한이 있는 SAS URI를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="42f29-139">**업로드된 파일에 대한 알림 받기**: 파일 업로드 알림을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="42f29-140">**SAS TTL**: 이 설정은 IoT Hub에서 장치로 반환하는 SAS URI의 TTL(Time-to-Live)입니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="42f29-141">기본적으로 1시간으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-141">Set to one hour by default.</span></span>

<span data-ttu-id="42f29-142">**파일 알림 설정 기본 TTL**: 만료되기 전의 파일 업로드 알림 TTL입니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="42f29-143">기본적으로 1일로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-143">Set to one day by default.</span></span>

<span data-ttu-id="42f29-144">**파일 알림 최대 배달 횟수**: IoT Hub가 파일 업로드 알림 배달을 시도하는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="42f29-145">기본적으로 10으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-145">Set to 10 by default.</span></span>

<span data-ttu-id="42f29-146">다음 PowerShell cmdlet을 사용하여 IoT Hub의 파일 업로드 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="42f29-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a><span data-ttu-id="42f29-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42f29-147">Next steps</span></span>

<span data-ttu-id="42f29-148">IoT Hub의 파일 업로드 기능에 대한 자세한 내용은 [장치에서 파일 업로드][lnk-upload]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42f29-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="42f29-149">Azure IoT Hub를 관리하는 방법에 대한 자세한 내용을 알아보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="42f29-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="42f29-150">[IoT 장치 대량 관리][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="42f29-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="42f29-151">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="42f29-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="42f29-152">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="42f29-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="42f29-153">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42f29-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="42f29-154">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="42f29-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="42f29-155">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="42f29-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="42f29-156">[처음부터 IoT 솔루션 보안 유지][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="42f29-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md