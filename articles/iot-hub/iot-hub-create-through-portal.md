---
title: "aaaUse hello Azure 포털 toocreate IoT Hub | Microsoft Docs"
description: "어떻게 toocreate, 관리 및 hello Azure 포털을 통해 Azure IoT 허브를 삭제 합니다. 가격 책정 계층, 보안, 배율 및 메시징 구성에 대한 정보가 포함됩니다."
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
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="f9616-104">Hello Azure 포털을 사용 하 여 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="f9616-105">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-105">This article describes:</span></span>

* <span data-ttu-id="f9616-106">어떻게 toofind hello hello Azure 포털에서에서 IoT Hub 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="f9616-107">어떻게 toocreate IoT 허브 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="f9616-108">여기서 toofind hello IoT 허브 서비스</span><span class="sxs-lookup"><span data-stu-id="f9616-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="f9616-109">다음 위치 hello 포털에서 hello에 hello IoT 허브 서비스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="f9616-110">**+새로 만들기**를 선택한 다음, **사물 인터넷**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="f9616-111">마켓플레이스 hello 선택 **사물 인터넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="f9616-112">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="f9616-112">Create an IoT hub</span></span>

<span data-ttu-id="f9616-113">메서드를 다음 hello를 사용 하 여 IoT hub를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="f9616-114">hello **+ 새로 만들기** 옵션 hello 스크린 샷 뒤에 표시 된 hello 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="f9616-115">이 메서드를 통해 및 hello marketplace를 통해 hello IoT 허브를 만드는 hello 단계는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="f9616-116">마켓플레이스 hello 선택 **만들기** tooopen hello 블레이드 hello 스크린 샷 뒤에 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="f9616-117">hello 다음 섹션에서는 설명 hello 몇 가지 단계 toocreate IoT hub:</span><span class="sxs-lookup"><span data-stu-id="f9616-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="f9616-118">Hello IoT 허브의 hello 이름 선택</span><span class="sxs-lookup"><span data-stu-id="f9616-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="f9616-119">IoT hub toocreate hello IoT 허브를 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="f9616-120">이 이름은 모든 IoT Hub에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="f9616-121">Hello 가격 책정 계층 선택</span><span class="sxs-lookup"><span data-stu-id="f9616-121">Choose hello pricing tier</span></span>

<span data-ttu-id="f9616-122">**무료**, **표준 1**, **표준 2**, **표준 S3**라는 네 개의 계층 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="f9616-123">hello 무료 계층에는 500 장치 toobe toohello IoT 허브 연결에 및 too8, 하루 000 메시지를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="f9616-124">**표준 S1**: 다 수의 각기 적은 양의 데이터를 생성 하는 장치를 사용 하 여 IoT 솔루션에 대 한 hello S1 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="f9616-125">각 단위 hello S1 버전의 too400, 연결 된 모든 장치에서 하루 000 메시지를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="f9616-126">**표준 S2**: IoT 솔루션에서 장치 생성 하는 많은 양의 데이터에 대 한 hello S2 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="f9616-127">각 단위 hello S2 버전에 연결 된 모든 장치 간의 하루 백만 메시지를 too6를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="f9616-128">**표준 S3**: 많은 양의 데이터를 생성 하는 IoT 솔루션에 대 한 hello S3 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="f9616-129">각 단위 hello S3 버전에 연결 된 모든 장치 간의 하루 백만 메시지를 too300를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="f9616-130">IoT Hub는 Azure 구독당 하나의 무료 허브만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="f9616-131">IoT Hub 단위</span><span class="sxs-lookup"><span data-stu-id="f9616-131">IoT hub units</span></span>

<span data-ttu-id="f9616-132">hello 하루 단위 당 허용 되는 메시지 수가 허브의 가격 책정 계층에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="f9616-133">예를 들어 hello 700, 000 메시지 IoT 허브 toosupport 수신 하려는 경우에 두 명의 S1 계층 단위 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="f9616-134">장치 toocloud 파티션 및 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f9616-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="f9616-135">Hello IoT 허브에 대 한 파티션 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="f9616-136">hello 기본 파티션 수는 4, hello 드롭 다운 목록에서 다른 숫자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="f9616-137">않아도 tooexplicitly 빈 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="f9616-138">리소스를 만들 때 기존 리소스 그룹을 사용 하 하거나 새 toocreate 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="f9616-139">구독 선택</span><span class="sxs-lookup"><span data-stu-id="f9616-139">Choose subscription</span></span>

<span data-ttu-id="f9616-140">Azure IoT Hub 자동으로 목록 hello hello 사용자 계정이 Azure 구독 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="f9616-141">Hello Azure 구독 tooassociate hello IoT 허브를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="f9616-142">Hello 위치 선택</span><span class="sxs-lookup"><span data-stu-id="f9616-142">Choose hello location</span></span>

<span data-ttu-id="f9616-143">hello 위치 옵션 IoT 허브를 사용할 수 있는 hello 지역 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="f9616-144">Hello IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-144">Create hello IoT hub</span></span>

<span data-ttu-id="f9616-145">위의 모든 단계 완료 되 면 hello IoT hub를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="f9616-146">클릭 **만들기** toostart 백 엔드 프로세스 toocreate hello 및 선택한 hello 옵션으로 hello IoT 허브를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="f9616-147">백 엔드 배포 toorun hello에 대 한 시간 hello 적절 한 위치 서버에는 몇 분 toocreate hello IoT hub을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="f9616-148">Hello IoT 허브의 hello 설정 변경</span><span class="sxs-lookup"><span data-stu-id="f9616-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="f9616-149">IoT Hub 블레이드 hello에서 만들어진 후 기존 IoT hub의 hello 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="f9616-150">**공유 액세스 정책의**:이 정책은 장치 및 서비스 tooconnect tooIoT 허브에 대 한 hello 권한을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="f9616-151">**일반**에서 **공유 액세스 정책**을 클릭하여 이러한 정책에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="f9616-152">이 블레이드에서 기존 정책을 수정하거나 새 정책을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="f9616-153">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="f9616-153">Create a policy</span></span>

* <span data-ttu-id="f9616-154">클릭 **추가** tooopen 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="f9616-155">여기서 hello 새 정책 이름을 입력할 수 있습니다 및 hello 다음과 같이 되도록이 정책 사용 하 여 tooassociate hello 권한을 그림:</span><span class="sxs-lookup"><span data-stu-id="f9616-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="f9616-156">이러한 공유 정책과 연결할 수 있는 몇 개의 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="f9616-157">hello **읽을 레지스트리** 및 **레지스트리 쓰기** 정책 읽기 및 쓰기 액세스 권한 toohello id 레지스트리에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="f9616-158">Hello 쓰기 옵션을 자동으로 선택 hello 읽을 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="f9616-159">hello **서비스 연결** 정책이 부여 권한을 tooaccess 서비스 끝점 등 **장치-클라우드 수신**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="f9616-160">hello **장치 연결** 정책이 hello 장치 측 IoT Hub 끝점을 사용 하 여 메시지 송수신에 대 한 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="f9616-161">클릭 **만들기** tooadd이 새로 생성 된 정책 toohello 기존 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="f9616-162">끝점</span><span class="sxs-lookup"><span data-stu-id="f9616-162">Endpoints</span></span>

<span data-ttu-id="f9616-163">클릭 **끝점** toodisplay 수정 하는 hello IoT 허브에 대 한 끝점의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="f9616-164">두 가지 방법으로 끝점의: hello IoT hub에 내장 된 끝점 및 끝점을 만든 후 toohello IoT 허브를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="f9616-165">기본 제공 끝점</span><span class="sxs-lookup"><span data-stu-id="f9616-165">Built-in endpoints</span></span>

<span data-ttu-id="f9616-166">두 개의 기본 제공 끝점이: **toodevice 피드백 클라우드** 및 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="f9616-167">**Toodevice 피드백 클라우드** 설정:이 설정은 아무런 두 하위 설정: **tooDevice TTL 클라우드** (-time-to-live) 및 **보존 시간** 시간에서 hello 메시지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="f9616-168">첫 번째 IoT 허브를 만들 때 이러한 두 설정 기본값이 hello 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="f9616-169">tooadjust 이러한 설정을 hello 슬라이더를 사용 하거나 hello 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="f9616-170">**이벤트** 설정: 이 설정에는 몇 가지 하위 설정이 있고 일부는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="f9616-171">hello 다음 목록에서는 이러한 설정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="f9616-172">**파티션**: hello IoT hub를 만들 때 기본값이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="f9616-173">이 설정을 통해 파티션의 hello 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="f9616-174">**이벤트 허브 호환 이름 및 끝점**: hello IoT hub를 만들면 이벤트 허브 만들어집니다 내부적으로 액세스할 수 있습니다 필요한 toounder 특정 상황입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="f9616-175">이벤트 허브 호환 hello 이름 및 끝점 값을 사용자 지정할 수 있지만 클릭 하 여 복사할 수 있습니다 **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="f9616-176">**보존 시간**: tooone 일은 기본적으로 설정 되지만 hello 드롭 다운 목록을 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="f9616-177">이 값은 hello 장치-클라우드 설정에 대 한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="f9616-178">**소비자 그룹**: 소비자 그룹을 여러 판독기 tooread 메시지 hello IoT 허브에서 독립적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="f9616-179">모든 IoT Hub가 기본 소비자 그룹으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="f9616-180">그러나 추가 하거나이 설정을 사용 하는 소비자 그룹 tooyour IoT 허브를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f9616-181">hello 기본 소비자 그룹을 편집 하거나 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="f9616-182">사용자 지정 끝점</span><span class="sxs-lookup"><span data-stu-id="f9616-182">Custom endpoints</span></span>

<span data-ttu-id="f9616-183">Hello 포털을 사용 하 여 IoT 허브에서 사용자 지정 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="f9616-184">Hello에서 **끝점** 블레이드에서 클릭 **추가** hello 상위 tooopen hello에 **끝점 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="f9616-185">Hello 필요한 정보를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="f9616-186">사용자 지정 끝점은 주 hello에 나열 된 이제 **끝점** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="f9616-187">[참조 - IoT Hub 끝점][lnk-devguide-endpoints]에서 사용자 지정 끝점에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="f9616-188">경로</span><span class="sxs-lookup"><span data-stu-id="f9616-188">Routes</span></span>

<span data-ttu-id="f9616-189">클릭 **경로** toomanage IoT Hub에서 장치-클라우드 메시지를 디스패치 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="f9616-190">클릭 하 여 경로 tooyour IoT hub를 추가할 수 있습니다 **추가** hello의 hello 위쪽 **경로*** hello 필요한 정보를 입력 하 고 클릭 하 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="f9616-191">경로 주 hello에 나열 된 다음 **경로** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="f9616-192">경로의 hello 목록에서 클릭 하 여 경로 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="f9616-193">tooenable 경로 경로의 hello 목록에서 클릭 하 고 hello 설정 **Enabled** 너무 설정/해제**오프**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="f9616-194">toosave hello 변경 클릭 **확인** hello hello 블레이드 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="f9616-195">가격 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f9616-195">Pricing and scale</span></span>

<span data-ttu-id="f9616-196">기존 IoT 허브의 가격 책정 hello hello 통해 변경할 수 있습니다 **가격 책정** 예외 다음 hello로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="f9616-197">IoT hub는 무료 SKU와의 유료 Sku를 hello 계층 tooone hello 현재 구현에서 변경할 수 없습니다 또는 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="f9616-198">만에 있을 수 있습니다 하나 무료 계층 IoT hub hello Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f9616-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="f9616-199">Hello 보낸 메시지 수 그 날 수행 hello 하위 계층에 대 한 hello 할당량을 초과 하는 경우에 높은 toolower 계층에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="f9616-200">예를 들어 hello 하루 메시지 수가 400, 000을 초과 하면 hello IoT 허브를 변경할 수 있습니다에 대 한 계층 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="f9616-201">그러나 toohello S1 계층을 변경 하는 경우 hello IoT hub 그 날에 대 한 제한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="f9616-202">Hello IoT 허브 삭제</span><span class="sxs-lookup"><span data-stu-id="f9616-202">Delete hello IoT hub</span></span>

<span data-ttu-id="f9616-203">Toodelete 클릭 하 여 원하는 toohello IoT hub를 찾아볼 수 **찾아보기**, 적절 한 허브 toodelete hello 다음을 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="f9616-204">toodelete IoT hub hello, hello 클릭 **삭제** hello IoT 허브 이름 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9616-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9616-205">Next steps</span></span>

<span data-ttu-id="f9616-206">이러한 링크 toolearn Azure IoT Hub를 관리 하는 방법에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9616-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="f9616-207">[IoT 장치 대량 관리][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="f9616-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="f9616-208">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="f9616-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="f9616-209">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="f9616-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="f9616-210">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f9616-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f9616-211">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="f9616-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="f9616-212">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f9616-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="f9616-213">[Hello 접지에서 IoT 솔루션 보안][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="f9616-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
