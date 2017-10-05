---
title: "Azure Portal을 사용하여 IoT Hub 만들기 | Microsoft 문서"
description: "Azure Portal을 통해 Azure IoT Hub를 만들고 관리하고 삭제하는 방법입니다. 가격 책정 계층, 보안, 배율 및 메시징 구성에 대한 정보가 포함됩니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="c3c9a-104">Azure Portal을 사용하여 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c3c9a-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="c3c9a-105">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-105">This article describes:</span></span>

* <span data-ttu-id="c3c9a-106">Azure Portal에서 IoT Hub 서비스를 찾는 방법.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="c3c9a-107">IoT Hub 만들기 및 관리 방법.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="c3c9a-108">IoT Hub 서비스를 찾을 위치.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="c3c9a-109">IoT Hub 서비스를 포털의 다음 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="c3c9a-110">**+새로 만들기**를 선택한 다음, **사물 인터넷**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="c3c9a-111">Marketplace에서 **사물 인터넷**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c3c9a-112">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c3c9a-112">Create an IoT hub</span></span>

<span data-ttu-id="c3c9a-113">다음 메서드를 통해 IoT Hub를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="c3c9a-114">**+ 새로 만들기** 옵션에서 다음 스크린 샷에 표시된 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="c3c9a-115">이 메서드는 Marketplace를 통해 IoT Hub를 만드는 단계와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="c3c9a-116">Marketplace에서 **만들기**를 선택하여 다음 스크린 샷에 표시된 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="c3c9a-117">다음 섹션에서는 IoT Hub를 만드는 몇 가지 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="c3c9a-118">IoT Hub 이름 선택</span><span class="sxs-lookup"><span data-stu-id="c3c9a-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="c3c9a-119">IoT Hub를 만들려면 IoT Hub의 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="c3c9a-120">이 이름은 모든 IoT Hub에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="c3c9a-121">가격 책정 계층 선택</span><span class="sxs-lookup"><span data-stu-id="c3c9a-121">Choose the pricing tier</span></span>

<span data-ttu-id="c3c9a-122">**무료**, **표준 1**, **표준 2**, **표준 S3**라는 네 개의 계층 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="c3c9a-123">무료 계층에서는 IoT Hub에 500개 장치만 연결할 수 있으며 하루에 8,000개 메시지까지 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="c3c9a-124">**표준 S1**: 각각 적은 양의 데이터를 생성하는 많은 장치의 IoT 솔루션을 위한 S1 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="c3c9a-125">S1 버전의 각 단위는 연결된 모든 장치에서 하루에 최대 400,000개의 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="c3c9a-126">**표준 S2**: 장치가 대량의 데이터를 생성하는 IoT 솔루션을 위한 S2 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="c3c9a-127">S2 버전의 각 단위를 통해 연결된 모든 장치 간에 하루에 최대 600만 개의 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="c3c9a-128">**표준 S3**: 대량의 데이터를 생성하는 IoT 솔루션을 위한 S3 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="c3c9a-129">S3 버전의 각 단위를 통해 연결된 모든 장치 간에 하루에 최대 300만 개의 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="c3c9a-130">IoT Hub는 Azure 구독당 하나의 무료 허브만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="c3c9a-131">IoT Hub 단위</span><span class="sxs-lookup"><span data-stu-id="c3c9a-131">IoT hub units</span></span>

<span data-ttu-id="c3c9a-132">하루 단위당 허용되는 메시지의 수는 허브의 가격 책정 계층에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="c3c9a-133">예를 들어 IoT Hub가 700,000개의 메시지 수신을 지원하려면 S1 계층 단위 2개를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="c3c9a-134">클라우드 파티션 및 리소스 그룹에 대한 장치</span><span class="sxs-lookup"><span data-stu-id="c3c9a-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="c3c9a-135">IoT Hub에 대한 파티션 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="c3c9a-136">기본 파티션 수는 4개로, 드롭다운 목록에서 다른 숫자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="c3c9a-137">빈 리소스 그룹을 명시적으로 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="c3c9a-138">리소스를 만들 때 기존 리소스 그룹을 사용하거나 새로 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="c3c9a-139">구독 선택</span><span class="sxs-lookup"><span data-stu-id="c3c9a-139">Choose subscription</span></span>

<span data-ttu-id="c3c9a-140">Azure IoT Hub에 사용자 계정을 연결할 Azure 구독 목록이 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="c3c9a-141">Azure 구독을 선택하여 IoT Hub를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="c3c9a-142">위치 선택</span><span class="sxs-lookup"><span data-stu-id="c3c9a-142">Choose the location</span></span>

<span data-ttu-id="c3c9a-143">위치 옵션은 IoT Hub가 제공되는 지역 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="c3c9a-144">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c3c9a-144">Create the IoT hub</span></span>

<span data-ttu-id="c3c9a-145">이전 단계를 모두 완료하면 IoT Hub를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="c3c9a-146">백 엔드 프로세스를 시작하도록 **만들기**를 클릭하여 선택한 옵션으로 IoT Hub를 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="c3c9a-147">적절한 위치 서버에서 백 엔드 배포가 실행되는 데 시간이 소요되므로 IoT Hub를 만드는 데 몇 분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="c3c9a-148">IoT Hub의 설정 변경</span><span class="sxs-lookup"><span data-stu-id="c3c9a-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="c3c9a-149">IoT Hub 블레이드에서 IoT Hub를 만든 후에 기존 IoT Hub의 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="c3c9a-150">**공유 액세스 정책**: IoT Hub에 연결할 장치 및 서비스에 대한 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="c3c9a-151">**일반**에서 **공유 액세스 정책**을 클릭하여 이러한 정책에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="c3c9a-152">이 블레이드에서 기존 정책을 수정하거나 새 정책을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="c3c9a-153">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c3c9a-153">Create a policy</span></span>

* <span data-ttu-id="c3c9a-154">**추가**를 클릭하여 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="c3c9a-155">여기에서 다음 그림에 표시된 것처럼 새 정책 이름과 이 정책과 연결할 권한을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="c3c9a-156">이러한 공유 정책과 연결할 수 있는 몇 개의 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="c3c9a-157">**레지스트리 읽기** 및 **레지스트리 쓰기** 정책은 ID 레지스트리에 대한 읽기 및 쓰기 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="c3c9a-158">쓰기 옵션을 선택하면 읽기 옵션도 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="c3c9a-159">**서비스 연결** 정책은 **장치-클라우드 수신**과 같은 서비스 끝점에 액세스할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="c3c9a-160">**장치 연결** 정책은 IoT Hub 장치 쪽 끝점을 사용하여 메시지를 주고받기 위한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="c3c9a-161">**만들기** 를 클릭하여 새로 만들어진 이 정책을 기존 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="c3c9a-162">끝점</span><span class="sxs-lookup"><span data-stu-id="c3c9a-162">Endpoints</span></span>

<span data-ttu-id="c3c9a-163">**끝점**을 클릭하여 수정하는 IoT Hub에 대한 끝점 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="c3c9a-164">끝점의 두 가지 유형은 IoT Hub에 기본 제공된 끝점 및 IoT Hub를 만든 후 여기에 추가된 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="c3c9a-165">기본 제공 끝점</span><span class="sxs-lookup"><span data-stu-id="c3c9a-165">Built-in endpoints</span></span>

<span data-ttu-id="c3c9a-166">두 가지 기본 제공 끝점인 **클라우드-장치 피드백** 및 **이벤트**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="c3c9a-167">**클라우드-장치 피드백** 설정: 이 설정에는 메시지에 대한 **클라우드-장치 TTL**(time-to-live) 및 **보존 시간**(시간 단위)의 두 가지 하위 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="c3c9a-168">IoT Hub를 처음 만들 때 이 두 가지 설정 모두 1시간이 기본값 입니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="c3c9a-169">이러한 설정을 조정하려면 슬라이더를 사용하거나 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="c3c9a-170">**이벤트** 설정: 이 설정에는 몇 가지 하위 설정이 있고 일부는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="c3c9a-171">다음 목록은 이러한 설정에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="c3c9a-172">**파티션**: IoT Hub가 만들어질 때 기본 값이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="c3c9a-173">이 설정을 통해 파티션 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="c3c9a-174">**이벤트 허브 호환 이름 및 끝점**: IoT Hub가 만들어질 때 특정 상황에서 사용자가 액세스해야 하는 이벤트 허브가 내부적으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="c3c9a-175">Event Hub 호환 이름 및 끝점 값을 사용자 지정할 수는 없지만 **복사**를 클릭하여 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="c3c9a-176">**보존 시간**: 기본적으로 1일로 설정되지만 드롭다운 목록을 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="c3c9a-177">이 값은 장치-클라우드 설정에 대한 일 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="c3c9a-178">**소비자 그룹**: 소비자 그룹은 여러 판독기에서 IoT Hub의 메시지를 독립적으로 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="c3c9a-179">모든 IoT Hub가 기본 소비자 그룹으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="c3c9a-180">그러나 이 설정을 사용하여 소비자 그룹을 IoT Hub에 추가 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c3c9a-181">기본 소비자 그룹을 편집하거나 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="c3c9a-182">사용자 지정 끝점</span><span class="sxs-lookup"><span data-stu-id="c3c9a-182">Custom endpoints</span></span>

<span data-ttu-id="c3c9a-183">포털을 사용하여 IoT Hub에 사용자 지정 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="c3c9a-184">**끝점** 블레이드에서 맨 위의 **추가**를 클릭하여 **끝점 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="c3c9a-185">필요한 정보를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="c3c9a-186">사용자 지정 끝점이 기본 **끝점** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="c3c9a-187">[참조 - IoT Hub 끝점][lnk-devguide-endpoints]에서 사용자 지정 끝점에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="c3c9a-188">경로</span><span class="sxs-lookup"><span data-stu-id="c3c9a-188">Routes</span></span>

<span data-ttu-id="c3c9a-189">**경로**를 클릭하여 IoT Hub가 장치-클라우드 메시지를 발송하는 방법을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="c3c9a-190">**경로** * 블레이드에서 맨 위의 **추가**를 클릭하여 필요한 정보를 입력하고 **확인** 을 클릭하여 IoT Hub에 경로를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="c3c9a-191">그러면 기본 **경로** 블레이드에 경로가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="c3c9a-192">경로 목록에서 경로를 클릭하면 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="c3c9a-193">경로를 사용하려면 경로 목록에서 경로를 클릭하고 **사용** 토글을 **해제**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="c3c9a-194">변경 내용을 저장하려면 블레이드의 맨 아래에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="c3c9a-195">가격 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c3c9a-195">Pricing and scale</span></span>

<span data-ttu-id="c3c9a-196">기존 IoT Hub의 가격 책정을 **가격 책정** 설정을 통해 변경할 수 있으며 단, 다음과 같은 예외가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="c3c9a-197">현재 구현에서는, 무료 SKU를 포함하는 IoT Hub는 계층을 유료 SKU 중 하나로 변경할 수 없으며 또는 그 반대도 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="c3c9a-198">Azure 구독에는 하나의 무료 계층 IoT Hub만 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="c3c9a-199">그 날 보낸 메시지 수가 하위 계층에 대한 할당량을 초과하는 경우에만 상위 계층에서 하위 계층으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="c3c9a-200">예를 들어 하루당 메시지 수가 400,000개를 초과하면 IoT Hub에 대한 계층을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="c3c9a-201">그러나 S1 계층으로 변경하면 해당 일에 IoT Hub가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="c3c9a-202">IoT Hub 삭제</span><span class="sxs-lookup"><span data-stu-id="c3c9a-202">Delete the IoT hub</span></span>

<span data-ttu-id="c3c9a-203">**찾아보기**를 클릭한 후 삭제할 해당 허브를 선택하여 삭제할 IoT Hub를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="c3c9a-204">IoT Hub를 삭제하려면 IoT Hub 이름 아래의 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3c9a-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3c9a-205">Next steps</span></span>

<span data-ttu-id="c3c9a-206">Azure IoT Hub를 관리하는 방법에 대한 자세한 내용을 알아보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="c3c9a-207">[IoT 장치 대량 관리][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="c3c9a-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="c3c9a-208">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="c3c9a-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="c3c9a-209">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="c3c9a-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="c3c9a-210">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3c9a-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c3c9a-211">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="c3c9a-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="c3c9a-212">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c3c9a-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="c3c9a-213">[처음부터 IoT 솔루션 보안 유지][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="c3c9a-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
