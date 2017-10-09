---
title: "OMS IT 서비스 관리 커넥터에서 aaaITSM 연결 | Microsoft Docs"
description: "IT 서비스 관리 커넥터와 함께 OMS toocentrally 모니터에서 ITSM 제품/서비스를 연결 하 고 hello ITSM 작업 항목을 관리 합니다."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a><span data-ttu-id="48a30-103">ITSM 제품/서비스를 IT Service Management Connector(미리 보기)에 연결</span><span class="sxs-lookup"><span data-stu-id="48a30-103">Connect ITSM products/services with IT Service Management Connector (Preview)</span></span>
<span data-ttu-id="48a30-104">이 문서는 방법에 대 한 정보를 제공 tooconnect ITSM 제품/서비스 tooIT 서비스 관리 커넥터 및 중앙 집중식으로 OMS에서 작업 항목을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-104">This article provides information about how tooconnect your ITSM product/service tooIT Service Management Connector in OMS and centrally manage your work items.</span></span> <span data-ttu-id="48a30-105">IT Service Management Connector에 대한 자세한 내용은 [개요](log-analytics-itsmc-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48a30-105">More information about IT Service Management Connector, see [Overview](log-analytics-itsmc-overview.md).</span></span>

<span data-ttu-id="48a30-106">다음 제품/서비스는 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-106">hello following products/services are supported:</span></span>

- [<span data-ttu-id="48a30-107">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="48a30-107">System Center Service Manager</span></span>](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="48a30-108">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="48a30-108">ServiceNow</span></span>](#connect-servicenow-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="48a30-109">Provance</span><span class="sxs-lookup"><span data-stu-id="48a30-109">Provance</span></span>](#connect-provance-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="48a30-110">Cherwell</span><span class="sxs-lookup"><span data-stu-id="48a30-110">Cherwell</span></span>](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a><span data-ttu-id="48a30-111">System Center Service Manager tooIT OMS에서 서비스 관리 커넥터 연결</span><span class="sxs-lookup"><span data-stu-id="48a30-111">Connect System Center Service Manager tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="48a30-112">hello 다음 섹션에서는 방법에 대 한 tooconnect System Center Service Manager 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-112">hello following sections provide details about how tooconnect your System Center Service Manager product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48a30-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48a30-113">Prerequisites</span></span>

<span data-ttu-id="48a30-114">다음 필수 구성 요소가 충족 하는 hello 있는지 확인.</span><span class="sxs-lookup"><span data-stu-id="48a30-114">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="48a30-115">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-115">IT Service Management Connector installed.</span></span>
<span data-ttu-id="48a30-116">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="48a30-116">More information:  [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="48a30-117">hello 서비스 관리자 웹 응용 프로그램 (웹 앱) 배포 및 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-117">hello Service Manager Web application (Web app) is deployed and configured.</span></span> <span data-ttu-id="48a30-118">웹앱에 대한 정보는 [여기](#create-and-deploy-service-manager-web-app-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48a30-118">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
- <span data-ttu-id="48a30-119">하이브리드 연결이 생성 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-119">Hybrid connection created and configured.</span></span> <span data-ttu-id="48a30-120">자세한 내용은: [구성 hello 하이브리드 연결](#configure-the-hybrid-connection)합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-120">More information: [Configure hello hybrid Connection](#configure-the-hybrid-connection).</span></span>
- <span data-ttu-id="48a30-121">지원되는 Service Manager 버전: 2012 R2 또는 2016</span><span class="sxs-lookup"><span data-stu-id="48a30-121">Supported versions of Service Manager:  2012 R2 or 2016.</span></span>
- <span data-ttu-id="48a30-122">사용자 역할: [고급 운영자](https://technet.microsoft.com/library/ff461054.aspx)</span><span class="sxs-lookup"><span data-stu-id="48a30-122">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="48a30-123">연결 절차</span><span class="sxs-lookup"><span data-stu-id="48a30-123">Connection procedure</span></span>

<span data-ttu-id="48a30-124">다음 프로시저 tooconnect hello System Center Service Manager 인스턴스 toohello IT 서비스 관리 커넥터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-124">Use hello following procedure tooconnect your System Center Service Manager instance toohello IT Service Management Connector:</span></span>

1. <span data-ttu-id="48a30-125">너무 이동**OMS** >**설정** > **연결 된 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-125">Go too**OMS** >**Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="48a30-126">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-126">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![<span data-ttu-id="48a30-127">Service Manager</span><span class="sxs-lookup"><span data-stu-id="48a30-127">Service manager</span></span> ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. <span data-ttu-id="48a30-128">다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결:</span><span class="sxs-lookup"><span data-stu-id="48a30-128">Provide hello information as described in hello following table, and click **Save** toocreate hello connection:</span></span>

> [!NOTE]
> <span data-ttu-id="48a30-129">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-129">All these parameters are mandatory.</span></span>

| <span data-ttu-id="48a30-130">**필드**</span><span class="sxs-lookup"><span data-stu-id="48a30-130">**Field**</span></span> | <span data-ttu-id="48a30-131">**설명**</span><span class="sxs-lookup"><span data-stu-id="48a30-131">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="48a30-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="48a30-132">**Name**</span></span>   | <span data-ttu-id="48a30-133">IT 서비스 관리 커넥터 hello로 tooconnect 원하는 hello System Center Service Manager 인스턴스의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-133">Type a name for hello System Center Service Manager instance that you want tooconnect with hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-134">이 이름은 나중에 이 인스턴스/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-134">You use this name later when you configure work items in this instance/ view detailed log analytics.</span></span> |
| <span data-ttu-id="48a30-135">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="48a30-135">**Select Connection type**</span></span>   | <span data-ttu-id="48a30-136">**System Center Service Manager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-136">Select **System Center Service Manager**.</span></span> |
| <span data-ttu-id="48a30-137">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="48a30-137">**Server URL**</span></span>   | <span data-ttu-id="48a30-138">Hello 서비스 관리자 웹 응용 프로그램의 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-138">Type hello URL of hello Service Manager Web app.</span></span> <span data-ttu-id="48a30-139">Service Manager 웹앱에 대한 자세한 내용은 [여기](#create-and-deploy-service-manager-web-app-service)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-139">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
| <span data-ttu-id="48a30-140">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="48a30-140">**Client ID**</span></span>   | <span data-ttu-id="48a30-141">Hello 웹 앱을 인증 하기 위한 (hello 자동 스크립트를 사용 하 여)을 생성 하는 hello 클라이언트 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-141">Type hello client ID that you generated (using hello automatic script) for authenticating hello Web app.</span></span> <span data-ttu-id="48a30-142">Hello 자동화 된 스크립트에 대 한 자세한 정보는 [여기 합니다.](log-analytics-itsmc-service-manager-script.md)</span><span class="sxs-lookup"><span data-stu-id="48a30-142">More information about hello automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span></span>|
| <span data-ttu-id="48a30-143">**클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="48a30-143">**Client Secret**</span></span>   | <span data-ttu-id="48a30-144">형식 hello 클라이언트 암호에 대 한이 ID 생성</span><span class="sxs-lookup"><span data-stu-id="48a30-144">Type hello client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="48a30-145">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="48a30-145">**Data Sync Scope**</span></span>   | <span data-ttu-id="48a30-146">Hello toosync hello IT 서비스 관리 커넥터를 통해 지정 하는 Service Manager 작업 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-146">Select hello Service Manager work items that you want toosync through hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-147">이러한 작업 항목을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-147">These work items are imported into Log Analytics.</span></span> <span data-ttu-id="48a30-148">**옵션:** 인시던트, 변경 요청</span><span class="sxs-lookup"><span data-stu-id="48a30-148">**Options:**  Incidents, Change Requests.</span></span>|
| <span data-ttu-id="48a30-149">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="48a30-149">**Sync Data**</span></span> | <span data-ttu-id="48a30-150">Hello hello 데이터를 원하는 과거 일 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-150">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="48a30-151">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="48a30-151">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="48a30-152">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="48a30-152">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="48a30-153">Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-153">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="48a30-154">옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-154">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="48a30-155">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-155">**Default**: disabled.</span></span> |

<span data-ttu-id="48a30-156">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="48a30-156">When successfully connected, and synced:</span></span>

- <span data-ttu-id="48a30-157">Service Manager의 선택한 작업 항목을 OMS **Log Analytics**로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-157">Selected work items from Service Manager are imported into OMS **Log Analytics.**</span></span> <span data-ttu-id="48a30-158">이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.</span><span class="sxs-lookup"><span data-stu-id="48a30-158">You can view hello summary of these work items on hello IT Service Management Connector tile.</span></span>

- <span data-ttu-id="48a30-159">OMS에서는 OMS 경고 또는 이 Service Manager 인스턴스의 로그 검색에서 인시던트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-159">From OMS, you can create incidents from OMS alerts or from log search, in this Service Manager instance.</span></span>

<span data-ttu-id="48a30-160">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="48a30-160">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-and-deploy-service-manager-web-app-service"></a><span data-ttu-id="48a30-161">Service Manager 웹앱 서비스 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="48a30-161">Create and deploy Service Manager web app service</span></span>

<span data-ttu-id="48a30-162">tooconnect OMS의 IT 서비스 관리 커넥터 hello로 온-프레미스 서비스 관리자 hello, Microsoft는 GitHub hello에 Service Manager 웹 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-162">tooconnect hello on-premises Service Manager with hello IT Service Management Connector on OMS, Microsoft has created a Service Manager Web app on hello GitHub.</span></span>

<span data-ttu-id="48a30-163">hello ITSM 웹 응용 프로그램에서 Service Manager에 대 한를 tooset 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-163">tooset up hello ITSM Web app for your Service Manager, do hello following:</span></span>

- <span data-ttu-id="48a30-164">**Hello 웹 응용 프로그램 배포** – hello 웹 앱을 배포, hello 속성을 설정 및 Azure AD로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-164">**Deploy hello Web app** – Deploy hello Web app, set hello properties, and authenticate with Azure AD.</span></span> <span data-ttu-id="48a30-165">Hello를 사용 하 여 hello 웹 앱을 배포할 수 있습니다 [스크립트 자동화 된](log-analytics-itsmc-service-manager-script.md) 는 Microsoft에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-165">You can deploy hello web app by using hello [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span></span>
- <span data-ttu-id="48a30-166">**Hello 하이브리드 연결을 구성** - [이 연결을 구성할](#configure-the-hybrid-connection)수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-166">**Configure hello hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span></span>

#### <a name="deploy-hello-web-app"></a><span data-ttu-id="48a30-167">Hello 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="48a30-167">Deploy hello web app</span></span>
<span data-ttu-id="48a30-168">자동으로 사용 하 여 hello [스크립트](log-analytics-itsmc-service-manager-script.md) toodeploy 웹 응용 프로그램 hello hello 속성을 설정 하 고 Azure AD로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-168">Use hello automated [script](log-analytics-itsmc-service-manager-script.md) toodeploy hello Web app, set hello properties, and authenticate with Azure AD.</span></span>

<span data-ttu-id="48a30-169">Hello 다음 필요한 세부 정보를 제공 하 여 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-169">Run hello script by providing hello following required details:</span></span>

- <span data-ttu-id="48a30-170">Azure 구독 정보</span><span class="sxs-lookup"><span data-stu-id="48a30-170">Azure subscription details</span></span>
- <span data-ttu-id="48a30-171">리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="48a30-171">Resource group name</span></span>
- <span data-ttu-id="48a30-172">위치</span><span class="sxs-lookup"><span data-stu-id="48a30-172">Location</span></span>
- <span data-ttu-id="48a30-173">Service Manager 서버 세부 정보(서버 이름, 도메인, 사용자 이름 및 암호)</span><span class="sxs-lookup"><span data-stu-id="48a30-173">Service Manager server details (server name, domain, user name, and password)</span></span>
- <span data-ttu-id="48a30-174">웹앱에 대한 사이트 이름 접두사</span><span class="sxs-lookup"><span data-stu-id="48a30-174">Site name prefix for your Web app</span></span>
- <span data-ttu-id="48a30-175">ServiceBus 네임스페이스.</span><span class="sxs-lookup"><span data-stu-id="48a30-175">ServiceBus Namespace.</span></span>

<span data-ttu-id="48a30-176">hello 스크립트 만듭니다 지정한 hello 이름을 사용 하 여 hello 웹 응용 프로그램 (몇 가지 추가 문자열 toomake와 함께 고유한 것).</span><span class="sxs-lookup"><span data-stu-id="48a30-176">hello script creates hello Web app using hello name that you specified (along with few additional strings toomake it unique).</span></span> <span data-ttu-id="48a30-177">Hello 생성 **웹 앱 URL**, **클라이언트 ID** 및 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-177">It generates hello **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="48a30-178">Hello 값 저장 사용할 있습니다 IT 서비스 관리 커넥터와 연결을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="48a30-178">Save hello values, you use them when you create a connection with IT Service Management Connector.</span></span>

<span data-ttu-id="48a30-179">**Hello 웹 앱을 설치를 확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="48a30-179">**Check hello Web app installation**</span></span>

1. <span data-ttu-id="48a30-180">너무 이동**Azure 포털** > **리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-180">Go too**Azure portal** > **Resources**.</span></span>
2. <span data-ttu-id="48a30-181">Hello 웹 앱 선택를 클릭 **설정** > **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-181">Select hello Web app, click **Settings** > **Application Settings**.</span></span>
3. <span data-ttu-id="48a30-182">Hello 스크립트를 통해 hello 앱 배포의 hello 시 제공 하는 hello 서비스 관리자 인스턴스에 대 한 hello 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-182">Confirm hello information about hello Service Manager instance that you provided at hello time of deploying hello app through hello script.</span></span>

### <a name="configure-hello-hybrid-connection"></a><span data-ttu-id="48a30-183">Hello 하이브리드 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-183">Configure hello hybrid connection</span></span>

<span data-ttu-id="48a30-184">OMS의 IT 서비스 관리 커넥터 hello로 hello 서비스 관리자 인스턴스를 연결 하는 프로시저 tooconfigure hello 하이브리드 연결을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-184">Use hello following procedure tooconfigure hello hybrid connection that connects hello Service Manager instance with hello IT Service Management Connector in OMS.</span></span>

1. <span data-ttu-id="48a30-185">Hello 서비스 관리자 웹 응용 프로그램 아래에서 찾을 **Azure 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-185">Find hello Service Manager Web app, under **Azure Resources**.</span></span>
2. <span data-ttu-id="48a30-186">**설정** > **네트워킹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-186">Click **Settings** > **Networking**.</span></span>
3. <span data-ttu-id="48a30-187">**하이브리드 연결**에서 **하이브리드 연결 끝점 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-187">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span></span>

    ![하이브리드 연결 네트워킹](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. <span data-ttu-id="48a30-189">Hello에 **하이브리드 연결** 블레이드에서 클릭 **하이브리드 연결을 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-189">In hello **Hybrid Connections** blade, click **Add hybrid connection**.</span></span>

    ![하이브리드 연결 추가](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. <span data-ttu-id="48a30-191">Hello에 **하이브리드 연결 추가** 블레이드에서 클릭 **만들기 새 하이브리드 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-191">In hello **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span></span>

    ![새 하이브리드 연결](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. <span data-ttu-id="48a30-193">Hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-193">Type hello following values:</span></span>

    - <span data-ttu-id="48a30-194">**끝점 이름**: hello 새 하이브리드 연결의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-194">**EndPoint Name**: Specify a name for hello new Hybrid connection.</span></span>
    -  <span data-ttu-id="48a30-195">**끝점 호스트**: hello Service Manager 관리 서버의 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-195">**EndPoint Host**: FQDN of hello Service Manager management server.</span></span>
    - <span data-ttu-id="48a30-196">**끝점 포트**: 5724를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-196">**EndPoint Port**: Type 5724</span></span>
    - <span data-ttu-id="48a30-197">**Servicebus 네임스페이스**: 기존 Servicebus 네임스페이스를 사용하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-197">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span></span>
    - <span data-ttu-id="48a30-198">**위치**: hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-198">**Location**: select hello location.</span></span>
    -  <span data-ttu-id="48a30-199">**이름**: 만드는 경우 이름 toohello servicebus를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-199">**Name**: Specify a name toohello servicebus if you are creating it.</span></span>

    ![하이브리드 연결 값](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. <span data-ttu-id="48a30-201">클릭 **확인** tooclose hello **하이브리드 연결** 블레이드와 hello 하이브리드 연결을 만들기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-201">Click **OK** tooclose hello **Create hybrid connection** blade and start creating hello hybrid connection.</span></span>

    <span data-ttu-id="48a30-202">Hello 하이브리드 연결을 만든 후 hello 블레이드 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-202">Once hello Hybrid connection is created, it is displayed under hello blade.</span></span>

7. <span data-ttu-id="48a30-203">Hello 하이브리드 연결을 만든 후 hello 연결을 선택 하 고 클릭 **하이브리드 연결을 선택 하는 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-203">After hello hybrid connection is created, select hello connection and click **Add selected hybrid connection**.</span></span>

    ![새 하이브리드 연결](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a><span data-ttu-id="48a30-205">Hello 수신기 설치 구성</span><span class="sxs-lookup"><span data-stu-id="48a30-205">Configure hello listener setup</span></span>

<span data-ttu-id="48a30-206">다음과 같은 hello 하이브리드 연결에 대 한 프로시저 tooconfigure hello 수신기 설정이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-206">Use hello following procedure tooconfigure hello listener setup for hello hybrid connection.</span></span>

1. <span data-ttu-id="48a30-207">Hello에 **하이브리드 연결** 블레이드에서 클릭 **연결 관리자 다운로드 hello** System Center Service Manager 인스턴스가 실행 되 고 hello 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-207">In hello **Hybrid Connections** blade, click **Download hello Connection Manager** and install it on hello machine where System Center Service Manager instance is running.</span></span>

    <span data-ttu-id="48a30-208">Hello 설치가 완료 되 면 **하이브리드 연결 관리자 UI** 옵션은 아래에서 사용할 수 **시작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="48a30-208">Once hello installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span></span>

2. <span data-ttu-id="48a30-209">**하이브리드 연결 관리자 UI**를 클릭하면 Azure 자격 증명을 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-209">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span></span>

3. <span data-ttu-id="48a30-210">Azure 자격 증명으로 로그인 하 고 하이브리드 연결 hello 만들어진 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-210">Login with your Azure credentials and select your subscription where hello Hybrid connection was created.</span></span>

4. <span data-ttu-id="48a30-211">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-211">Click **Save**.</span></span>

<span data-ttu-id="48a30-212">하이브리드 연결이 성공적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-212">Your hybrid connection is successfully connected.</span></span>

![하이브리드 연결 성공](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> <span data-ttu-id="48a30-214">Hello 하이브리드 연결을 만들고 확인 하 고 hello를 방문 하 여 hello 연결 테스트 서비스 관리자 웹 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-214">After hello hybrid connection is created, verify and test hello connection by visiting hello deployed Service Manager Web app.</span></span> <span data-ttu-id="48a30-215">Tooconnect toohello OMS의 IT 서비스 관리 커넥터를 시도 하기 전에 hello 연결을 성공적으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-215">Ensure hello connection is successful before you try tooconnect toohello IT Service Management Connector in OMS.</span></span>

<span data-ttu-id="48a30-216">hello 다음 이미지 표시 성공적으로 연결의 hello 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="48a30-216">hello following image shows hello details of a successful connection:</span></span>

![하이브리드 연결 테스트](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a><span data-ttu-id="48a30-218">ServiceNow tooIT OMS에서 서비스 관리 커넥터 연결</span><span class="sxs-lookup"><span data-stu-id="48a30-218">Connect ServiceNow tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="48a30-219">hello 다음 섹션에서는 제공 방법에 대 한 세부 정보 tooconnect ServiceNow 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-219">hello following sections provide details about how tooconnect your ServiceNow product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48a30-220">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48a30-220">Prerequisites</span></span>

<span data-ttu-id="48a30-221">다음 필수 구성 요소가 충족 하는 hello 있는지 확인.</span><span class="sxs-lookup"><span data-stu-id="48a30-221">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="48a30-222">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-222">IT Service Management Connector installed.</span></span> <span data-ttu-id="48a30-223">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="48a30-223">More information: [Configuration.](log-analytics-itsmc-overview.md#configuration)</span></span>
- <span data-ttu-id="48a30-224">ServiceNow 지원 버전 – Fuji, Geneva, Helsinki</span><span class="sxs-lookup"><span data-stu-id="48a30-224">ServiceNow supported versions – Fuji, Geneva, Helsinki.</span></span>

<span data-ttu-id="48a30-225">ServiceNow 관리자가 수행 해야 자신의 ServiceNow 인스턴스 다음에 오는 hello:</span><span class="sxs-lookup"><span data-stu-id="48a30-225">ServiceNow Admins must do hello following in their ServiceNow instance:</span></span>
- <span data-ttu-id="48a30-226">클라이언트 ID와 hello ServiceNow 제품에 대 한 클라이언트 암호를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-226">Generate client ID and client secret for hello ServiceNow product.</span></span> <span data-ttu-id="48a30-227">Toogenerate 클라이언트 ID 및 암호를 참조 하는 방법에 대 한 내용은 [OAuth 설치](http://wiki.servicenow.com/index.php?title=OAuth_Setup)합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-227">For information on how toogenerate client ID and secret, see [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span>
- <span data-ttu-id="48a30-228">Microsoft OMS (ServiceNow app) 통합에 대 한 hello 사용자 앱을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-228">Install hello User App for Microsoft OMS integration (ServiceNow app).</span></span> <span data-ttu-id="48a30-229">[자세히 알아봅니다](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span><span class="sxs-lookup"><span data-stu-id="48a30-229">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span></span>
- <span data-ttu-id="48a30-230">설치 된 hello 사용자 응용 프로그램에 대 한 통합 사용자 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-230">Create integration user role for hello user app installed.</span></span> <span data-ttu-id="48a30-231">Toocreate hello 통합 사용자 역할을 하는 방법을 알아보려면 [여기](#create-integration-user-role-in-servicenow-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-231">Information on how toocreate hello integration user role is [here](#create-integration-user-role-in-servicenow-app).</span></span>


### <a name="connection-procedure"></a><span data-ttu-id="48a30-232">**연결 절차**</span><span class="sxs-lookup"><span data-stu-id="48a30-232">**Connection procedure**</span></span>

<span data-ttu-id="48a30-233">다음 프로시저 toocreate ServiceNow 연결 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-233">Use hello following procedure toocreate a ServiceNow connection:</span></span>

1. <span data-ttu-id="48a30-234">너무 이동**OMS** > **설정** > **연결 된 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-234">Go too**OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="48a30-235">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-235">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![ServiceNow 연결](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. <span data-ttu-id="48a30-237">다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결:</span><span class="sxs-lookup"><span data-stu-id="48a30-237">Provide hello information as described in hello following table, and click **Save** toocreate hello connection:</span></span>

> [!NOTE]
> <span data-ttu-id="48a30-238">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-238">All these parameters are mandatory.</span></span>

| <span data-ttu-id="48a30-239">**필드**</span><span class="sxs-lookup"><span data-stu-id="48a30-239">**Field**</span></span> | <span data-ttu-id="48a30-240">**설명**</span><span class="sxs-lookup"><span data-stu-id="48a30-240">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="48a30-241">**Name**</span><span class="sxs-lookup"><span data-stu-id="48a30-241">**Name**</span></span>   | <span data-ttu-id="48a30-242">IT 서비스 관리 커넥터 hello로 tooconnect 원하는 hello ServiceNow 인스턴스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-242">Type a name for hello ServiceNow instance that you want tooconnect with hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-243">이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-243">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="48a30-244">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="48a30-244">**Select Connection type**</span></span>   | <span data-ttu-id="48a30-245">**ServiceNow**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-245">Select **ServiceNow**.</span></span> |
| <span data-ttu-id="48a30-246">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="48a30-246">**Username**</span></span>   | <span data-ttu-id="48a30-247">Hello ServiceNow 앱 toosupport hello 연결 toohello IT 서비스 관리 커넥터에서에서 만든 hello 통합 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-247">Type hello integration user name that you created in hello ServiceNow app toosupport hello connection toohello IT Service Management Connector.</span></span> <span data-ttu-id="48a30-248">추가 정보: [ServiceNow 앱 사용자 역할 만들기](#create-integration-user-role-in-servicenow-app)</span><span class="sxs-lookup"><span data-stu-id="48a30-248">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span></span>|
| <span data-ttu-id="48a30-249">**암호**</span><span class="sxs-lookup"><span data-stu-id="48a30-249">**Password**</span></span>   | <span data-ttu-id="48a30-250">이 사용자 이름과 관련 된 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-250">Type hello password associated with this user name.</span></span> <span data-ttu-id="48a30-251">**참고**: 사용자 이름 및 암호 인증 토큰 생성에 사용 되 고 hello OMS 서비스 내에서 아무 곳 이나 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-251">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within hello OMS service.</span></span>  |
| <span data-ttu-id="48a30-252">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="48a30-252">**Server URL**</span></span>   | <span data-ttu-id="48a30-253">서비스 관리 커넥터 tooconnect tooIT 원하는 hello ServiceNow 인스턴스 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-253">Type hello URL of hello ServiceNow instance that you want tooconnect tooIT Service Management Connector.</span></span> |
| <span data-ttu-id="48a30-254">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="48a30-254">**Client ID**</span></span>   | <span data-ttu-id="48a30-255">앞에서 생성 하는 OAuth2 인증 toouse 원하는 hello 클라이언트 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-255">Type hello client ID that you want toouse for OAuth2 Authentication, which you generated earlier.</span></span>  <span data-ttu-id="48a30-256">클라이언트 ID 및 암호 생성에 대한 추가 정보: [OAuth 설정](http://wiki.servicenow.com/index.php?title=OAuth_Setup)</span><span class="sxs-lookup"><span data-stu-id="48a30-256">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span> |
| <span data-ttu-id="48a30-257">**클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="48a30-257">**Client Secret**</span></span>   | <span data-ttu-id="48a30-258">형식 hello 클라이언트 암호에 대 한이 ID 생성</span><span class="sxs-lookup"><span data-stu-id="48a30-258">Type hello client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="48a30-259">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="48a30-259">**Data Sync Scope**</span></span>   | <span data-ttu-id="48a30-260">Toosync tooOMS hello IT 서비스 관리 커넥터를 통해 원하는 hello ServiceNow 작업 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-260">Select hello ServiceNow work items that you want toosync tooOMS, through hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-261">로그 분석에 hello 선택한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-261">hello selected values are imported into log analytics.</span></span>   <span data-ttu-id="48a30-262">**옵션:** 인시던트 및 변경 요청</span><span class="sxs-lookup"><span data-stu-id="48a30-262">**Options:**  Incidents and Change Requests.</span></span>|
| <span data-ttu-id="48a30-263">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="48a30-263">**Sync Data**</span></span> | <span data-ttu-id="48a30-264">Hello hello 데이터를 원하는 과거 일 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-264">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="48a30-265">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="48a30-265">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="48a30-266">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="48a30-266">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="48a30-267">Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-267">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="48a30-268">옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-268">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="48a30-269">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-269">**Default**: disabled.</span></span> |


<span data-ttu-id="48a30-270">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="48a30-270">When successfully connected, and synced:</span></span>

- <span data-ttu-id="48a30-271">ServiceNow 연결의 선택한 작업 항목을 OMS Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-271">Selected work items from ServiceNow connection are imported into OMS Log Analytics.</span></span>  <span data-ttu-id="48a30-272">이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.</span><span class="sxs-lookup"><span data-stu-id="48a30-272">You can view hello summary of these work items on hello IT Service Management Connector tile.</span></span>
- <span data-ttu-id="48a30-273">OMS 경고 또는 이 ServiceNow 인스턴스의 로그 검색에서 인시던트, 경고 및 이벤트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-273">You can create incidents, alerts, and events from OMS Alerts or log search in this ServiceNow instance.</span></span>  


<span data-ttu-id="48a30-274">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="48a30-274">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-integration-user-role-in-servicenow-app"></a><span data-ttu-id="48a30-275">ServiceNow 앱에서 통합 사용자 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="48a30-275">Create integration user role in ServiceNow app</span></span>

<span data-ttu-id="48a30-276">사용자 hello 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-276">User hello following procedure:</span></span>

1.  <span data-ttu-id="48a30-277">Hello 방문 [ServiceNow 저장소](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) hello를 설치 하 고 **ServiceNow와 Microsoft OMS 통합을 위한 사용자 응용 프로그램** ServiceNow 인스턴스로.</span><span class="sxs-lookup"><span data-stu-id="48a30-277">Visit hello [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) and install hello **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span></span>
2.  <span data-ttu-id="48a30-278">설치가 끝나면 hello ServiceNow 인스턴스, 검색 및 선택 Microsoft OMS integrator의 탐색 모음 왼쪽 hello를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-278">After installation, visit hello left navigation bar of hello ServiceNow instance, search, and select Microsoft OMS integrator.</span></span>  
3.  <span data-ttu-id="48a30-279">**설치 검사 목록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-279">Click **Installation Checklist**.</span></span>

    <span data-ttu-id="48a30-280">hello 상태가으로 표시 됩니다 **완료할** hello 사용자 역할은 아직 toobe 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-280">hello status is displayed as  **Not complete** if hello user role is yet toobe created.</span></span>

4.  <span data-ttu-id="48a30-281">Hello 텍스트에서 상자에 다음 너무**통합 사용자 만들기**, toohello OMS의 IT 서비스 관리 커넥터에 연결할 수 있는 hello 사용자에 대 한 hello 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-281">In hello text boxes, next too**Create integration user**, enter hello user name for hello user that can connect toohello IT Service Management Connector in OMS.</span></span>
5.  <span data-ttu-id="48a30-282">이 사용자에 대 한 hello 암호를 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-282">Enter hello password for this user, and click **OK**.</span></span>  

>[!NOTE]

> <span data-ttu-id="48a30-283">OMS에서 이러한 자격 증명 toomake hello ServiceNow 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-283">You use these credentials toomake hello ServiceNow connection in OMS.</span></span>

<span data-ttu-id="48a30-284">새로 만든 사용자 hello hello 기본 역할 할당 된 상태로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-284">hello newly created user is displayed with hello default roles assigned.</span></span>

<span data-ttu-id="48a30-285">기본 역할:</span><span class="sxs-lookup"><span data-stu-id="48a30-285">Default roles:</span></span>
- <span data-ttu-id="48a30-286">personalize_choices</span><span class="sxs-lookup"><span data-stu-id="48a30-286">personalize_choices</span></span>
- <span data-ttu-id="48a30-287">import_transformer</span><span class="sxs-lookup"><span data-stu-id="48a30-287">import_transformer</span></span>
-   <span data-ttu-id="48a30-288">x_mioms_microsoft.user</span><span class="sxs-lookup"><span data-stu-id="48a30-288">x_mioms_microsoft.user</span></span>
-   <span data-ttu-id="48a30-289">itil</span><span class="sxs-lookup"><span data-stu-id="48a30-289">itil</span></span>
-   <span data-ttu-id="48a30-290">template_editor</span><span class="sxs-lookup"><span data-stu-id="48a30-290">template_editor</span></span>
-   <span data-ttu-id="48a30-291">view_changer</span><span class="sxs-lookup"><span data-stu-id="48a30-291">view_changer</span></span>

<span data-ttu-id="48a30-292">Hello 사용자가 성공적으로 만들어지면 hello 상태의 **설치 검사 목록 확인** hello 앱에 대해 생성 하는 hello 사용자 역할의 hello 세부 정보를 나열 tooCompleted 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-292">Once hello user is successfully created, hello status of **Check Installation Checklist** moves tooCompleted, listing hello details of hello user role created for hello app.</span></span>

> [!NOTE]

> <span data-ttu-id="48a30-293">사용자 toocreate tooallow **경고** 및 **이벤트** OMS에서 ServiceNow에서:</span><span class="sxs-lookup"><span data-stu-id="48a30-293">tooallow a user toocreate **alerts** and **events** in ServiceNow from OMS:</span></span>

> - <span data-ttu-id="48a30-294">ServiceNow 인스턴스에 hello 이벤트 관리 모듈 설치를 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-294">Ensure you have hello Event Management module Installed on your ServiceNow instance.</span></span>

> - <span data-ttu-id="48a30-295">Hello 다음 toohello 통합 사용자 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-295">Add hello following roles toohello integration user:</span></span>
>      - <span data-ttu-id="48a30-296">evt_mgmt_integration</span><span class="sxs-lookup"><span data-stu-id="48a30-296">evt_mgmt_integration</span></span>
>      - <span data-ttu-id="48a30-297">evt_mgmt_operator</span><span class="sxs-lookup"><span data-stu-id="48a30-297">evt_mgmt_operator</span></span>  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a><span data-ttu-id="48a30-298">연결 Provance tooIT OMS에서 서비스 관리 커넥터</span><span class="sxs-lookup"><span data-stu-id="48a30-298">Connect Provance tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="48a30-299">hello 다음 섹션에서는 제공 방법에 대 한 세부 정보 tooconnect Provance 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-299">hello following sections provide details about how tooconnect your Provance product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48a30-300">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48a30-300">Prerequisites</span></span>

<span data-ttu-id="48a30-301">다음 필수 구성 요소가 충족 하는 hello 있는지 확인.</span><span class="sxs-lookup"><span data-stu-id="48a30-301">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="48a30-302">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-302">IT Service Management Connector installed.</span></span> <span data-ttu-id="48a30-303">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="48a30-303">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="48a30-304">Provance 앱을 Azure AD에 등록해야 합니다. 그래야 클라이언트 ID를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-304">Provance App should be registered with Azure AD - and client ID is made available.</span></span> <span data-ttu-id="48a30-305">자세한 내용은 참조 [어떻게 tooconfigure active directory 인증](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-305">For detailed information, see [how tooconfigure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
- <span data-ttu-id="48a30-306">사용자 역할: 관리자</span><span class="sxs-lookup"><span data-stu-id="48a30-306">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="48a30-307">연결 절차</span><span class="sxs-lookup"><span data-stu-id="48a30-307">Connection Procedure</span></span>

<span data-ttu-id="48a30-308">다음 프로시저 toocreate Provance 연결 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-308">Use hello following procedure toocreate a Provance connection:</span></span>

1. <span data-ttu-id="48a30-309">너무 이동**OMS** > **설정** > **연결 된 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-309">Go too**OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="48a30-310">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-310">Select **ITSM Connector,** click **Add New Connection**.</span></span>  

    ![Provance 연결](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. <span data-ttu-id="48a30-312">다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-312">Provide hello information as described in hello following table, and click **Save** toocreate hello connection.</span></span>

> [!NOTE]
> <span data-ttu-id="48a30-313">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-313">All these parameters are mandatory.</span></span>

| <span data-ttu-id="48a30-314">**필드**</span><span class="sxs-lookup"><span data-stu-id="48a30-314">**Field**</span></span> | <span data-ttu-id="48a30-315">**설명**</span><span class="sxs-lookup"><span data-stu-id="48a30-315">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="48a30-316">**Name**</span><span class="sxs-lookup"><span data-stu-id="48a30-316">**Name**</span></span>   | <span data-ttu-id="48a30-317">IT 서비스 관리 커넥터 hello로 tooconnect 원하는 hello Provance 인스턴스에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-317">Type a name for hello Provance instance that you want tooconnect with hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-318">이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-318">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="48a30-319">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="48a30-319">**Select Connection type**</span></span>   | <span data-ttu-id="48a30-320">**Provance**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-320">Select **Provance**.</span></span> |
| <span data-ttu-id="48a30-321">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="48a30-321">**Username**</span></span>   | <span data-ttu-id="48a30-322">Toohello IT 서비스 관리 커넥터에 연결할 수 있는 hello 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-322">Type hello user name that can connect toohello IT Service Management Connector.</span></span>    |
| <span data-ttu-id="48a30-323">**암호**</span><span class="sxs-lookup"><span data-stu-id="48a30-323">**Password**</span></span>   | <span data-ttu-id="48a30-324">이 사용자 이름과 관련 된 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-324">Type hello password associated with this user name.</span></span> <span data-ttu-id="48a30-325">**참고:** 사용자 이름 및 암호 인증 토큰 생성에 사용 되 고 hello OMS 서비스 내에서 아무 곳 이나 저장 되지 않습니다. _</span><span class="sxs-lookup"><span data-stu-id="48a30-325">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within hello OMS service._</span></span>|
| <span data-ttu-id="48a30-326">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="48a30-326">**Server URL**</span></span>   | <span data-ttu-id="48a30-327">서비스 관리 커넥터 tooconnect tooIT 원하는 Provance 인스턴스 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-327">Type hello URL of your Provance instance that you want tooconnect tooIT Service Management Connector.</span></span> |
| <span data-ttu-id="48a30-328">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="48a30-328">**Client ID**</span></span>   | <span data-ttu-id="48a30-329">Provance 인스턴스에 생성 된이 연결을 인증 하는 hello 클라이언트 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-329">Type hello client ID for authenticating this connection, which you generated in your Provance instance.</span></span>  <span data-ttu-id="48a30-330">클라이언트 ID에 대 한 자세한 내용은 참조 [어떻게 tooconfigure active directory 인증](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-330">More information on client ID, see [how tooconfigure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> |
| <span data-ttu-id="48a30-331">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="48a30-331">**Data Sync Scope**</span></span>   | <span data-ttu-id="48a30-332">Toosync tooOMS hello IT 서비스 관리 커넥터를 통해 원하는 hello Provance 작업 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-332">Select hello Provance work items that you want toosync tooOMS, through hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-333">이러한 작업 항목을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-333">These work items are imported into log analytics.</span></span>   <span data-ttu-id="48a30-334">**옵션:** 인시던트, 변경 요청</span><span class="sxs-lookup"><span data-stu-id="48a30-334">**Options:**   Incidents, Change Requests.</span></span>|
| <span data-ttu-id="48a30-335">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="48a30-335">**Sync Data**</span></span> | <span data-ttu-id="48a30-336">Hello hello 데이터를 원하는 과거 일 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-336">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="48a30-337">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="48a30-337">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="48a30-338">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="48a30-338">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="48a30-339">Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-339">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="48a30-340">옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-340">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="48a30-341">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-341">**Default**: disabled.</span></span>|

<span data-ttu-id="48a30-342">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="48a30-342">When successfully connected, and synced:</span></span>

- <span data-ttu-id="48a30-343">Provance 연결의 선택한 작업 항목을 OMS **Log Analytics**로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-343">Selected work items from Provance connection are imported into OMS **Log Analytics.**</span></span>  <span data-ttu-id="48a30-344">이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.</span><span class="sxs-lookup"><span data-stu-id="48a30-344">You can view hello summary of these work items on hello IT Service Management Connector tile.</span></span>
- <span data-ttu-id="48a30-345">OMS 경고 또는 이 Provance 인스턴스의 로그 검색에서 인시던트 및 이벤트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-345">You can create incidents and events from OMS Alerts or Log Search in this Provance instance.</span></span>

<span data-ttu-id="48a30-346">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="48a30-346">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a><span data-ttu-id="48a30-347">Cherwell tooIT OMS에서 서비스 관리 커넥터 연결</span><span class="sxs-lookup"><span data-stu-id="48a30-347">Connect Cherwell tooIT Service Management Connector in OMS</span></span>

<span data-ttu-id="48a30-348">hello 다음 섹션에서는 제공 방법에 대 한 세부 정보 tooconnect Cherwell 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-348">hello following sections provide details about how tooconnect your Cherwell product toohello IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48a30-349">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48a30-349">Prerequisites</span></span>

<span data-ttu-id="48a30-350">다음 필수 구성 요소가 충족 하는 hello 있는지 확인.</span><span class="sxs-lookup"><span data-stu-id="48a30-350">Ensure you have hello following prerequisites met:</span></span>

- <span data-ttu-id="48a30-351">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-351">IT Service Management Connector installed.</span></span> <span data-ttu-id="48a30-352">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="48a30-352">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="48a30-353">클라이언트 ID가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-353">Client ID generated.</span></span> <span data-ttu-id="48a30-354">추가 정보: [Cherwell용 클라이언트 ID 생성](#generate-client-id-for-cherwell)</span><span class="sxs-lookup"><span data-stu-id="48a30-354">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span></span>
- <span data-ttu-id="48a30-355">사용자 역할: 관리자</span><span class="sxs-lookup"><span data-stu-id="48a30-355">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="48a30-356">연결 절차</span><span class="sxs-lookup"><span data-stu-id="48a30-356">Connection Procedure</span></span>

<span data-ttu-id="48a30-357">다음 프로시저 toocreate Cherwell 연결 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-357">Use hello following procedure toocreate a Cherwell connection:</span></span>

1. <span data-ttu-id="48a30-358">너무 이동**OMS** >  **설정** > **연결 된 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-358">Go too**OMS** >  **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="48a30-359">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-359">Select **ITSM Connector** click **Add New Connection**.</span></span>  

    ![Cherwell 사용자 ID](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. <span data-ttu-id="48a30-361">다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-361">Provide hello information as described in hello following table, and click  **Save** toocreate hello connection.</span></span>

> [!NOTE]
> <span data-ttu-id="48a30-362">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-362">All these parameters are mandatory.</span></span>

| <span data-ttu-id="48a30-363">**필드**</span><span class="sxs-lookup"><span data-stu-id="48a30-363">**Field**</span></span> | <span data-ttu-id="48a30-364">**설명**</span><span class="sxs-lookup"><span data-stu-id="48a30-364">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="48a30-365">**Name**</span><span class="sxs-lookup"><span data-stu-id="48a30-365">**Name**</span></span>   | <span data-ttu-id="48a30-366">Hello Cherwell 인스턴스 원하는 tooconnect toohello IT 서비스 관리 커넥터에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-366">Type a name for hello Cherwell instance that you want tooconnect toohello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-367">이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-367">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="48a30-368">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="48a30-368">**Select Connection type**</span></span>   | <span data-ttu-id="48a30-369">**Cherwell**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-369">Select **Cherwell.**</span></span> |
| <span data-ttu-id="48a30-370">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="48a30-370">**Username**</span></span>   | <span data-ttu-id="48a30-371">Toohello IT 서비스 관리 커넥터에 연결할 수 있는 hello Cherwell 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-371">Type hello Cherwell user name that can connect toohello IT Service Management Connector.</span></span> |
| <span data-ttu-id="48a30-372">**암호**</span><span class="sxs-lookup"><span data-stu-id="48a30-372">**Password**</span></span>   | <span data-ttu-id="48a30-373">이 사용자 이름과 관련 된 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-373">Type hello password associated with this user name.</span></span> <span data-ttu-id="48a30-374">**참고:** 사용자 이름 및 암호 인증 토큰 생성에 사용 되 고 hello OMS 서비스 내에서 아무 곳 이나 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-374">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within hello OMS service.</span></span>|
| <span data-ttu-id="48a30-375">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="48a30-375">**Server URL**</span></span>   | <span data-ttu-id="48a30-376">서비스 관리 커넥터 tooconnect tooIT 원하는 Cherwell 인스턴스 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-376">Type hello URL of your Cherwell instance that you want tooconnect tooIT Service Management Connector.</span></span> |
| <span data-ttu-id="48a30-377">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="48a30-377">**Client ID**</span></span>   | <span data-ttu-id="48a30-378">Cherwell 인스턴스에 생성 된이 연결을 인증 하는 hello 클라이언트 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-378">Type hello client ID for authenticating this connection, which you generated in your Cherwell instance.</span></span>   |
| <span data-ttu-id="48a30-379">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="48a30-379">**Data Sync Scope**</span></span>   | <span data-ttu-id="48a30-380">Toosync hello IT 서비스 관리 커넥터를 통해 원하는 hello Cherwell 작업 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-380">Select hello Cherwell work items that you want toosync through hello IT Service Management Connector.</span></span>  <span data-ttu-id="48a30-381">이러한 작업 항목을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-381">These work items are imported into log analytics.</span></span>   <span data-ttu-id="48a30-382">**옵션:** 인시던트, 변경 요청</span><span class="sxs-lookup"><span data-stu-id="48a30-382">**Options:**  Incidents, Change Requests.</span></span> |
| <span data-ttu-id="48a30-383">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="48a30-383">**Sync Data**</span></span> | <span data-ttu-id="48a30-384">Hello hello 데이터를 원하는 과거 일 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-384">Type hello number of past days that you want hello data from.</span></span> <span data-ttu-id="48a30-385">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="48a30-385">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="48a30-386">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="48a30-386">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="48a30-387">Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-387">Select this option if you want toocreate hello configuration items in hello ITSM product.</span></span> <span data-ttu-id="48a30-388">옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-388">When selected, OMS creates hello affected CIs as configuration items (in case of non-existing CIs) in hello supported ITSM system.</span></span> <span data-ttu-id="48a30-389">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-389">**Default**: disabled.</span></span> |

<span data-ttu-id="48a30-390">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="48a30-390">When successfully connected, and synced:</span></span>

- <span data-ttu-id="48a30-391">이 Cherwell 연결에서 선택된 작업 항목을 OMS Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-391">Selected work items from this Cherwell connection are imported into OMS Log Analytics.</span></span> <span data-ttu-id="48a30-392">이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.</span><span class="sxs-lookup"><span data-stu-id="48a30-392">You can view hello summary of these work items  on hello IT Service Management Connector tile.</span></span>
- <span data-ttu-id="48a30-393">OMS에서 이 Cherwell 인스턴스의 인시던트 및 이벤트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-393">You can create incidents and events in this Cherwell instance from OMS.</span></span> <span data-ttu-id="48a30-394">추가 정보: OMS 경고에 대한 ITSM 작업 항목 만들기 및 OMS 로그에서 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="48a30-394">More information: Create ITSM work items for OMS alerts and Create ITSM work items from OMS logs.</span></span>

<span data-ttu-id="48a30-395">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="48a30-395">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="generate-client-id-for-cherwell"></a><span data-ttu-id="48a30-396">Cherwell용 클라이언트 ID 생성</span><span class="sxs-lookup"><span data-stu-id="48a30-396">Generate client ID for Cherwell</span></span>

<span data-ttu-id="48a30-397">toogenerate는 Cherwell에 대 한 클라이언트가 D/키 hello, 절차를 수행 하는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="48a30-397">toogenerate hello client ID/key for Cherwell, use hello following procedure:</span></span>

1. <span data-ttu-id="48a30-398">로그인 tooyour Cherwell 인스턴스 관리자로</span><span class="sxs-lookup"><span data-stu-id="48a30-398">Log in tooyour Cherwell instance as admin.</span></span>
2. <span data-ttu-id="48a30-399">**보안** > **REST API 클라이언트 설정 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-399">Click **Security** > **Edit REST API client settings**.</span></span>
3. <span data-ttu-id="48a30-400">**새 클라이언트 만들기** > **클라이언트 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48a30-400">Select **Create new client** > **client secret**.</span></span>

    ![Cherwell 사용자 ID](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a><span data-ttu-id="48a30-402">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48a30-402">Next steps</span></span>
 - [<span data-ttu-id="48a30-403">OMS 경고에 대한 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="48a30-403">Create ITSM work items for OMS alerts</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [<span data-ttu-id="48a30-404">OMS 로그에서 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="48a30-404">Create ITSM work items from OMS logs</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [<span data-ttu-id="48a30-405">연결에 대한 Log Analytics 보기</span><span class="sxs-lookup"><span data-stu-id="48a30-405">View log analytics for your connection</span></span>](log-analytics-itsmc-overview.md#using-the-solution)
