---
title: "OMS IT Service Management Connector의 ITSM 연결 | Microsoft Docs"
description: "ITSM 제품/서비스를 OMS의 IT Service Management Connector로 연결하여 ITSM 작업 항목을 중앙에서 모니터링하고 관리합니다."
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
ms.openlocfilehash: e4f2e0a23aa52a0e02e7047916b77fb15107defa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a><span data-ttu-id="fc8b0-103">ITSM 제품/서비스를 IT Service Management Connector(미리 보기)에 연결</span><span class="sxs-lookup"><span data-stu-id="fc8b0-103">Connect ITSM products/services with IT Service Management Connector (Preview)</span></span>
<span data-ttu-id="fc8b0-104">이 문서에서는 ITSM 제품/서비스를 OMS의 IT Service Management Connector에 연결하고 작업 항목을 중앙에서 관리하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-104">This article provides information about how to connect your ITSM product/service to IT Service Management Connector in OMS and centrally manage your work items.</span></span> <span data-ttu-id="fc8b0-105">IT Service Management Connector에 대한 자세한 내용은 [개요](log-analytics-itsmc-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-105">More information about IT Service Management Connector, see [Overview](log-analytics-itsmc-overview.md).</span></span>

<span data-ttu-id="fc8b0-106">다음 제품/서비스는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-106">The following products/services are supported:</span></span>

- [<span data-ttu-id="fc8b0-107">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="fc8b0-107">System Center Service Manager</span></span>](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="fc8b0-108">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="fc8b0-108">ServiceNow</span></span>](#connect-servicenow-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="fc8b0-109">Provance</span><span class="sxs-lookup"><span data-stu-id="fc8b0-109">Provance</span></span>](#connect-provance-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="fc8b0-110">Cherwell</span><span class="sxs-lookup"><span data-stu-id="fc8b0-110">Cherwell</span></span>](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-to-it-service-management-connector-in-oms"></a><span data-ttu-id="fc8b0-111">System Center Service Manager를 OMS의 IT Service Management Connector에 연결</span><span class="sxs-lookup"><span data-stu-id="fc8b0-111">Connect System Center Service Manager to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="fc8b0-112">다음 섹션에서는 System Center Service Manager 제품을 OMS의 IT Service Management Connector에 연결하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-112">The following sections provide details about how to connect your System Center Service Manager product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fc8b0-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fc8b0-113">Prerequisites</span></span>

<span data-ttu-id="fc8b0-114">다음 필수 조건을 갖추고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-114">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="fc8b0-115">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-115">IT Service Management Connector installed.</span></span>
<span data-ttu-id="fc8b0-116">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-116">More information:  [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="fc8b0-117">Service Manager 웹 응용 프로그램(웹앱)이 배포 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-117">The Service Manager Web application (Web app) is deployed and configured.</span></span> <span data-ttu-id="fc8b0-118">웹앱에 대한 정보는 [여기](#create-and-deploy-service-manager-web-app-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-118">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
- <span data-ttu-id="fc8b0-119">하이브리드 연결이 생성 및 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-119">Hybrid connection created and configured.</span></span> <span data-ttu-id="fc8b0-120">추가 정보: [하이브리드 연결 구성](#configure-the-hybrid-connection)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-120">More information: [Configure the hybrid Connection](#configure-the-hybrid-connection).</span></span>
- <span data-ttu-id="fc8b0-121">지원되는 Service Manager 버전: 2012 R2 또는 2016</span><span class="sxs-lookup"><span data-stu-id="fc8b0-121">Supported versions of Service Manager:  2012 R2 or 2016.</span></span>
- <span data-ttu-id="fc8b0-122">사용자 역할: [고급 운영자](https://technet.microsoft.com/library/ff461054.aspx)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-122">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="fc8b0-123">연결 절차</span><span class="sxs-lookup"><span data-stu-id="fc8b0-123">Connection procedure</span></span>

<span data-ttu-id="fc8b0-124">System Center Service Manager 인스턴스를 IT Service Management Connector에 연결하려면 다음 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-124">Use the following procedure to connect your System Center Service Manager instance to the IT Service Management Connector:</span></span>

1. <span data-ttu-id="fc8b0-125">**OMS** >**설정** > **연결된 원본**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-125">Go to **OMS** >**Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="fc8b0-126">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-126">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![<span data-ttu-id="fc8b0-127">Service Manager</span><span class="sxs-lookup"><span data-stu-id="fc8b0-127">Service manager</span></span> ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. <span data-ttu-id="fc8b0-128">다음 표에 설명된 대로 정보를 제공하고 **저장**을 클릭하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-128">Provide the information as described in the following table, and click **Save** to create the connection:</span></span>

> [!NOTE]
> <span data-ttu-id="fc8b0-129">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-129">All these parameters are mandatory.</span></span>

| <span data-ttu-id="fc8b0-130">**필드**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-130">**Field**</span></span> | <span data-ttu-id="fc8b0-131">**설명**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-131">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fc8b0-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-132">**Name**</span></span>   | <span data-ttu-id="fc8b0-133">IT Service Management Connector에 연결하려는 System Center Service Manager 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-133">Type a name for the System Center Service Manager instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-134">이 이름은 나중에 이 인스턴스/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-134">You use this name later when you configure work items in this instance/ view detailed log analytics.</span></span> |
| <span data-ttu-id="fc8b0-135">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-135">**Select Connection type**</span></span>   | <span data-ttu-id="fc8b0-136">**System Center Service Manager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-136">Select **System Center Service Manager**.</span></span> |
| <span data-ttu-id="fc8b0-137">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-137">**Server URL**</span></span>   | <span data-ttu-id="fc8b0-138">Service Manager 웹앱의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-138">Type the URL of the Service Manager Web app.</span></span> <span data-ttu-id="fc8b0-139">Service Manager 웹앱에 대한 자세한 내용은 [여기](#create-and-deploy-service-manager-web-app-service)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-139">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
| <span data-ttu-id="fc8b0-140">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-140">**Client ID**</span></span>   | <span data-ttu-id="fc8b0-141">웹앱을 인증하기 위해 생성한 클라이언트 ID를 입력합니다(자동 스크립트 사용).</span><span class="sxs-lookup"><span data-stu-id="fc8b0-141">Type the client ID that you generated (using the automatic script) for authenticating the Web app.</span></span> <span data-ttu-id="fc8b0-142">자동화된 스크립트에 대한 자세한 내용은 [여기](log-analytics-itsmc-service-manager-script.md)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-142">More information about the automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span></span>|
| <span data-ttu-id="fc8b0-143">**클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-143">**Client Secret**</span></span>   | <span data-ttu-id="fc8b0-144">이 ID에 대해 생성된 클라이언트 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-144">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="fc8b0-145">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-145">**Data Sync Scope**</span></span>   | <span data-ttu-id="fc8b0-146">IT Service Management Connector를 통해 동기화할 Service Manager 작업 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-146">Select the Service Manager work items that you want to sync through the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-147">이러한 작업 항목을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-147">These work items are imported into Log Analytics.</span></span> <span data-ttu-id="fc8b0-148">**옵션:** 인시던트, 변경 요청</span><span class="sxs-lookup"><span data-stu-id="fc8b0-148">**Options:**  Incidents, Change Requests.</span></span>|
| <span data-ttu-id="fc8b0-149">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-149">**Sync Data**</span></span> | <span data-ttu-id="fc8b0-150">데이터를 원하는 이전 일 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-150">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="fc8b0-151">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="fc8b0-151">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="fc8b0-152">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-152">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="fc8b0-153">ITSM 제품에서 구성 항목을 만들려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-153">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="fc8b0-154">이 옵션을 선택하면 OMS는 지원되는 ITSM 시스템에서 영향을 받는 CI(존재하지 않는 CI)를 구성 항목으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-154">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="fc8b0-155">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-155">**Default**: disabled.</span></span> |

<span data-ttu-id="fc8b0-156">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="fc8b0-156">When successfully connected, and synced:</span></span>

- <span data-ttu-id="fc8b0-157">Service Manager의 선택한 작업 항목을 OMS **Log Analytics**로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-157">Selected work items from Service Manager are imported into OMS **Log Analytics.**</span></span> <span data-ttu-id="fc8b0-158">IT Service Management Connector 타일에서 이러한 작업 항목에 대한 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-158">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="fc8b0-159">OMS에서는 OMS 경고 또는 이 Service Manager 인스턴스의 로그 검색에서 인시던트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-159">From OMS, you can create incidents from OMS alerts or from log search, in this Service Manager instance.</span></span>

<span data-ttu-id="fc8b0-160">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-160">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-and-deploy-service-manager-web-app-service"></a><span data-ttu-id="fc8b0-161">Service Manager 웹앱 서비스 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="fc8b0-161">Create and deploy Service Manager web app service</span></span>

<span data-ttu-id="fc8b0-162">OMS에서 IT Service Management Connector에 온-프레미스 Service Manager를 연결하기 위해 Microsoft는 GitHub에 Service Manager 웹앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-162">To connect the on-premises Service Manager with the IT Service Management Connector on OMS, Microsoft has created a Service Manager Web app on the GitHub.</span></span>

<span data-ttu-id="fc8b0-163">Service Manager에 대해 ITSM 웹앱을 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-163">To set up the ITSM Web app for your Service Manager, do the following:</span></span>

- <span data-ttu-id="fc8b0-164">**웹앱 배포** – 웹앱을 배포하고, 속성을 설정하고, Azure AD를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-164">**Deploy the Web app** – Deploy the Web app, set the properties, and authenticate with Azure AD.</span></span> <span data-ttu-id="fc8b0-165">Microsoft에서 제공한 [자동화 스크립트](log-analytics-itsmc-service-manager-script.md)를 사용하여 웹앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-165">You can deploy the web app by using the [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span></span>
- <span data-ttu-id="fc8b0-166">**하이브리드 연결 구성** - 수동으로 [이 연결을 구성](#configure-the-hybrid-connection)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-166">**Configure the hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span></span>

#### <a name="deploy-the-web-app"></a><span data-ttu-id="fc8b0-167">웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="fc8b0-167">Deploy the web app</span></span>
<span data-ttu-id="fc8b0-168">자동화 [스크립트](log-analytics-itsmc-service-manager-script.md)를 사용하여 웹앱을 배포하고, 속성을 설정하고, Azure AD를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-168">Use the automated [script](log-analytics-itsmc-service-manager-script.md) to deploy the Web app, set the properties, and authenticate with Azure AD.</span></span>

<span data-ttu-id="fc8b0-169">다음 필수 정보를 제공하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-169">Run the script by providing the following required details:</span></span>

- <span data-ttu-id="fc8b0-170">Azure 구독 정보</span><span class="sxs-lookup"><span data-stu-id="fc8b0-170">Azure subscription details</span></span>
- <span data-ttu-id="fc8b0-171">리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="fc8b0-171">Resource group name</span></span>
- <span data-ttu-id="fc8b0-172">위치</span><span class="sxs-lookup"><span data-stu-id="fc8b0-172">Location</span></span>
- <span data-ttu-id="fc8b0-173">Service Manager 서버 세부 정보(서버 이름, 도메인, 사용자 이름 및 암호)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-173">Service Manager server details (server name, domain, user name, and password)</span></span>
- <span data-ttu-id="fc8b0-174">웹앱에 대한 사이트 이름 접두사</span><span class="sxs-lookup"><span data-stu-id="fc8b0-174">Site name prefix for your Web app</span></span>
- <span data-ttu-id="fc8b0-175">ServiceBus 네임스페이스.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-175">ServiceBus Namespace.</span></span>

<span data-ttu-id="fc8b0-176">이 스크립트는 사용자가 지정한 이름(및 웹앱을 고유하게 만드는 몇 가지 추가 설정)을 사용하여 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-176">The script creates the Web app using the name that you specified (along with few additional strings to make it unique).</span></span> <span data-ttu-id="fc8b0-177">**웹앱 URL**, **클라이언트 ID** 및 **클라이언트 암호**를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-177">It generates the **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="fc8b0-178">값을 저장한 다음, IT Service Management Connector와의 연결을 만들 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-178">Save the values, you use them when you create a connection with IT Service Management Connector.</span></span>

<span data-ttu-id="fc8b0-179">**웹앱 설치 확인**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-179">**Check the Web app installation**</span></span>

1. <span data-ttu-id="fc8b0-180">**Azure Portal** > **리소스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-180">Go to **Azure portal** > **Resources**.</span></span>
2. <span data-ttu-id="fc8b0-181">웹앱을 선택하고 **설정** > **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-181">Select the Web app, click **Settings** > **Application Settings**.</span></span>
3. <span data-ttu-id="fc8b0-182">스크립트를 통해 앱을 배포할 때 제공한 Service Manager 인스턴스에 대한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-182">Confirm the information about the Service Manager instance that you provided at the time of deploying the app through the script.</span></span>

### <a name="configure-the-hybrid-connection"></a><span data-ttu-id="fc8b0-183">하이브리드 연결 구성</span><span class="sxs-lookup"><span data-stu-id="fc8b0-183">Configure the hybrid connection</span></span>

<span data-ttu-id="fc8b0-184">다음 절차에 따라 Service Manager 인스턴스를 OMS의 IT Service Management Connector에 연결하는 하이브리드 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-184">Use the following procedure to configure the hybrid connection that connects the Service Manager instance with the IT Service Management Connector in OMS.</span></span>

1. <span data-ttu-id="fc8b0-185">**Azure 리소스** 아래에서 Service Manager 웹앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-185">Find the Service Manager Web app, under **Azure Resources**.</span></span>
2. <span data-ttu-id="fc8b0-186">**설정** > **네트워킹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-186">Click **Settings** > **Networking**.</span></span>
3. <span data-ttu-id="fc8b0-187">**하이브리드 연결**에서 **하이브리드 연결 끝점 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-187">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span></span>

    ![하이브리드 연결 네트워킹](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. <span data-ttu-id="fc8b0-189">**하이브리드 연결** 블레이드에서 **하이브리드 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-189">In the **Hybrid Connections** blade, click **Add hybrid connection**.</span></span>

    ![하이브리드 연결 추가](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. <span data-ttu-id="fc8b0-191">**하이브리드 연결 추가** 블레이드에서 **새 하이브리드 연결 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-191">In the **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span></span>

    ![새 하이브리드 연결](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. <span data-ttu-id="fc8b0-193">다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-193">Type the following values:</span></span>

    - <span data-ttu-id="fc8b0-194">**끝점 이름**: 새 하이브리드 연결의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-194">**EndPoint Name**: Specify a name for the new Hybrid connection.</span></span>
    -  <span data-ttu-id="fc8b0-195">**끝점 호스트**: Service Manager 관리 서버의 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-195">**EndPoint Host**: FQDN of the Service Manager management server.</span></span>
    - <span data-ttu-id="fc8b0-196">**끝점 포트**: 5724를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-196">**EndPoint Port**: Type 5724</span></span>
    - <span data-ttu-id="fc8b0-197">**Servicebus 네임스페이스**: 기존 Servicebus 네임스페이스를 사용하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-197">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span></span>
    - <span data-ttu-id="fc8b0-198">**위치**: 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-198">**Location**: select the location.</span></span>
    -  <span data-ttu-id="fc8b0-199">**이름**: servicebus를 만드는 경우 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-199">**Name**: Specify a name to the servicebus if you are creating it.</span></span>

    ![하이브리드 연결 값](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. <span data-ttu-id="fc8b0-201">**확인**을 클릭하여 **하이브리드 연결 만들기** 블레이드를 닫고 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-201">Click **OK** to close the **Create hybrid connection** blade and start creating the hybrid connection.</span></span>

    <span data-ttu-id="fc8b0-202">하이브리드 연결이 만들어지면 블레이드 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-202">Once the Hybrid connection is created, it is displayed under the blade.</span></span>

7. <span data-ttu-id="fc8b0-203">하이브리드 연결을 만든 후 연결을 선택하고 **선택한 하이브리드 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-203">After the hybrid connection is created, select the connection and click **Add selected hybrid connection**.</span></span>

    ![새 하이브리드 연결](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-the-listener-setup"></a><span data-ttu-id="fc8b0-205">수신기 설정 구성</span><span class="sxs-lookup"><span data-stu-id="fc8b0-205">Configure the listener setup</span></span>

<span data-ttu-id="fc8b0-206">다음 절차에 따라 하이브리드 연결에 대한 수신기 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-206">Use the following procedure to configure the listener setup for the hybrid connection.</span></span>

1. <span data-ttu-id="fc8b0-207">**하이브리드 연결** 블레이드에서 **연결 관리자 다운로드**를 클릭한 후 System Center Service Manager 인스턴스가 실행되고 있는 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-207">In the **Hybrid Connections** blade, click **Download the Connection Manager** and install it on the machine where System Center Service Manager instance is running.</span></span>

    <span data-ttu-id="fc8b0-208">설치가 완료되면 **시작** 메뉴 아래에서 **하이브리드 연결 관리자 UI** 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-208">Once the installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span></span>

2. <span data-ttu-id="fc8b0-209">**하이브리드 연결 관리자 UI**를 클릭하면 Azure 자격 증명을 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-209">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span></span>

3. <span data-ttu-id="fc8b0-210">Azure 자격 증명으로 로그인하고 하이브리드 연결이 만들어진 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-210">Login with your Azure credentials and select your subscription where the Hybrid connection was created.</span></span>

4. <span data-ttu-id="fc8b0-211">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-211">Click **Save**.</span></span>

<span data-ttu-id="fc8b0-212">하이브리드 연결이 성공적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-212">Your hybrid connection is successfully connected.</span></span>

![하이브리드 연결 성공](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> <span data-ttu-id="fc8b0-214">하이브리드 연결이 만들어진 후 배포된 Service Manager 웹앱을 방문하여 연결을 확인한 후 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-214">After the hybrid connection is created, verify and test the connection by visiting the deployed Service Manager Web app.</span></span> <span data-ttu-id="fc8b0-215">OMS에서 IT Service Management Connector에 연결을 시도하기 전에 연결이 성공적으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-215">Ensure the connection is successful before you try to connect to the IT Service Management Connector in OMS.</span></span>

<span data-ttu-id="fc8b0-216">다음 이미지는 성공적으로 설정된 연결의 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-216">The following image shows the details of a successful connection:</span></span>

![하이브리드 연결 테스트](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-to-it-service-management-connector-in-oms"></a><span data-ttu-id="fc8b0-218">ServiceNow를 OMS의 IT Service Management Connector에 연결</span><span class="sxs-lookup"><span data-stu-id="fc8b0-218">Connect ServiceNow to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="fc8b0-219">다음 섹션에서는 ServiceNow 제품을 OMS의 IT Service Management Connector에 연결하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-219">The following sections provide details about how to connect your ServiceNow product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fc8b0-220">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fc8b0-220">Prerequisites</span></span>

<span data-ttu-id="fc8b0-221">다음 필수 조건을 갖추고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-221">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="fc8b0-222">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-222">IT Service Management Connector installed.</span></span> <span data-ttu-id="fc8b0-223">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-223">More information: [Configuration.](log-analytics-itsmc-overview.md#configuration)</span></span>
- <span data-ttu-id="fc8b0-224">ServiceNow 지원 버전 – Fuji, Geneva, Helsinki</span><span class="sxs-lookup"><span data-stu-id="fc8b0-224">ServiceNow supported versions – Fuji, Geneva, Helsinki.</span></span>

<span data-ttu-id="fc8b0-225">ServiceNow 관리자는 ServiceNow 인스턴스에서 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-225">ServiceNow Admins must do the following in their ServiceNow instance:</span></span>
- <span data-ttu-id="fc8b0-226">ServiceNow 제품에 대한 클라이언트 ID 및 클라이언트 암호를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-226">Generate client ID and client secret for the ServiceNow product.</span></span> <span data-ttu-id="fc8b0-227">클라이언트 ID 및 암호를 생성하는 방법에 대한 자세한 내용은 [OAuth 설정](http://wiki.servicenow.com/index.php?title=OAuth_Setup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-227">For information on how to generate client ID and secret, see [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span>
- <span data-ttu-id="fc8b0-228">Microsoft OMS 통합용 사용자 앱(ServiceNow 앱)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-228">Install the User App for Microsoft OMS integration (ServiceNow app).</span></span> <span data-ttu-id="fc8b0-229">[자세히 알아보세요](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 )을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-229">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span></span>
- <span data-ttu-id="fc8b0-230">설치된 사용자 앱에 대한 통합 사용자 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-230">Create integration user role for the user app installed.</span></span> <span data-ttu-id="fc8b0-231">통합 사용자 역할을 만드는 방법에 대한 자세한 내용은 [여기](#create-integration-user-role-in-servicenow-app)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-231">Information on how to create the integration user role is [here](#create-integration-user-role-in-servicenow-app).</span></span>


### <a name="connection-procedure"></a><span data-ttu-id="fc8b0-232">**연결 절차**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-232">**Connection procedure**</span></span>

<span data-ttu-id="fc8b0-233">다음 절차에 따라 ServiceNow 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-233">Use the following procedure to create a ServiceNow connection:</span></span>

1. <span data-ttu-id="fc8b0-234">**OMS** > **설정** > **연결된 원본**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-234">Go to **OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="fc8b0-235">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-235">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![ServiceNow 연결](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. <span data-ttu-id="fc8b0-237">다음 표에 설명된 대로 정보를 제공하고 **저장**을 클릭하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-237">Provide the information as described in the following table, and click **Save** to create the connection:</span></span>

> [!NOTE]
> <span data-ttu-id="fc8b0-238">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-238">All these parameters are mandatory.</span></span>

| <span data-ttu-id="fc8b0-239">**필드**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-239">**Field**</span></span> | <span data-ttu-id="fc8b0-240">**설명**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-240">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fc8b0-241">**Name**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-241">**Name**</span></span>   | <span data-ttu-id="fc8b0-242">IT Service Management Connector에 연결하려는 ServiceNow 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-242">Type a name for the ServiceNow instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-243">이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-243">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="fc8b0-244">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-244">**Select Connection type**</span></span>   | <span data-ttu-id="fc8b0-245">**ServiceNow**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-245">Select **ServiceNow**.</span></span> |
| <span data-ttu-id="fc8b0-246">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-246">**Username**</span></span>   | <span data-ttu-id="fc8b0-247">IT Service Management Connector에 대한 연결을 지원하기 위해 ServiceNow 앱에서 만든 통합 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-247">Type the integration user name that you created in the ServiceNow app to support the connection to the IT Service Management Connector.</span></span> <span data-ttu-id="fc8b0-248">추가 정보: [ServiceNow 앱 사용자 역할 만들기](#create-integration-user-role-in-servicenow-app)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-248">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span></span>|
| <span data-ttu-id="fc8b0-249">**암호**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-249">**Password**</span></span>   | <span data-ttu-id="fc8b0-250">이 사용자 이름과 관련된 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-250">Type the password associated with this user name.</span></span> <span data-ttu-id="fc8b0-251">**참고**: 사용자 이름 및 암호는 인증 토큰 생성에만 사용되며 OMS 서비스에는 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-251">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service.</span></span>  |
| <span data-ttu-id="fc8b0-252">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-252">**Server URL**</span></span>   | <span data-ttu-id="fc8b0-253">IT Service Management Connector에 연결하려는 ServiceNow 인스턴스의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-253">Type the URL of the ServiceNow instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="fc8b0-254">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-254">**Client ID**</span></span>   | <span data-ttu-id="fc8b0-255">이전에 생성한 OAuth2 인증에 사용하려는 클라이언트 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-255">Type the client ID that you want to use for OAuth2 Authentication, which you generated earlier.</span></span>  <span data-ttu-id="fc8b0-256">클라이언트 ID 및 암호 생성에 대한 추가 정보: [OAuth 설정](http://wiki.servicenow.com/index.php?title=OAuth_Setup)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-256">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span> |
| <span data-ttu-id="fc8b0-257">**클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-257">**Client Secret**</span></span>   | <span data-ttu-id="fc8b0-258">이 ID에 대해 생성된 클라이언트 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-258">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="fc8b0-259">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-259">**Data Sync Scope**</span></span>   | <span data-ttu-id="fc8b0-260">IT Service Management Connector를 통해 OMS와 동기화할 ServiceNow 작업 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-260">Select the ServiceNow work items that you want to sync to OMS, through the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-261">선택한 값을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-261">The selected values are imported into log analytics.</span></span>   <span data-ttu-id="fc8b0-262">**옵션:** 인시던트 및 변경 요청</span><span class="sxs-lookup"><span data-stu-id="fc8b0-262">**Options:**  Incidents and Change Requests.</span></span>|
| <span data-ttu-id="fc8b0-263">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-263">**Sync Data**</span></span> | <span data-ttu-id="fc8b0-264">데이터를 원하는 이전 일 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-264">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="fc8b0-265">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="fc8b0-265">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="fc8b0-266">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-266">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="fc8b0-267">ITSM 제품에서 구성 항목을 만들려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-267">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="fc8b0-268">이 옵션을 선택하면 OMS는 지원되는 ITSM 시스템에서 영향을 받는 CI(존재하지 않는 CI)를 구성 항목으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-268">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="fc8b0-269">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-269">**Default**: disabled.</span></span> |


<span data-ttu-id="fc8b0-270">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="fc8b0-270">When successfully connected, and synced:</span></span>

- <span data-ttu-id="fc8b0-271">ServiceNow 연결의 선택한 작업 항목을 OMS Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-271">Selected work items from ServiceNow connection are imported into OMS Log Analytics.</span></span>  <span data-ttu-id="fc8b0-272">IT Service Management Connector 타일에서 이러한 작업 항목에 대한 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-272">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="fc8b0-273">OMS 경고 또는 이 ServiceNow 인스턴스의 로그 검색에서 인시던트, 경고 및 이벤트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-273">You can create incidents, alerts, and events from OMS Alerts or log search in this ServiceNow instance.</span></span>  


<span data-ttu-id="fc8b0-274">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-274">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-integration-user-role-in-servicenow-app"></a><span data-ttu-id="fc8b0-275">ServiceNow 앱에서 통합 사용자 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="fc8b0-275">Create integration user role in ServiceNow app</span></span>

<span data-ttu-id="fc8b0-276">다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-276">User the following procedure:</span></span>

1.  <span data-ttu-id="fc8b0-277">[ServiceNow 스토어](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0)를 방문하고 **ServiceNow 및 Microsoft OMS 통합용 사용자 앱**을 ServiceNow 인스턴스에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-277">Visit the [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) and install the **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span></span>
2.  <span data-ttu-id="fc8b0-278">설치 후 ServiceNow 인스턴스의 왼쪽 탐색 모음으로 가서 Microsoft OMS 통합기를 검색한 후 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-278">After installation, visit the left navigation bar of the ServiceNow instance, search, and select Microsoft OMS integrator.</span></span>  
3.  <span data-ttu-id="fc8b0-279">**설치 검사 목록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-279">Click **Installation Checklist**.</span></span>

    <span data-ttu-id="fc8b0-280">사용자 역할을 아직 생성해야 할 경우 상태가 **완료되지 않음**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-280">The status is displayed as  **Not complete** if the user role is yet to be created.</span></span>

4.  <span data-ttu-id="fc8b0-281">**통합 사용자 만들기** 옆의 텍스트 상자에 OMS에서 IT Service Management Connector에 연결될 수 있는 사용자의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-281">In the text boxes, next to **Create integration user**, enter the user name for the user that can connect to the IT Service Management Connector in OMS.</span></span>
5.  <span data-ttu-id="fc8b0-282">이 사용자에 대한 암호를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-282">Enter the password for this user, and click **OK**.</span></span>  

>[!NOTE]

> <span data-ttu-id="fc8b0-283">이러한 자격 증명을 사용하여 OMS에서 ServiceNow 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-283">You use these credentials to make the ServiceNow connection in OMS.</span></span>

<span data-ttu-id="fc8b0-284">새로 만든 사용자는 기본 역할이 할당된 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-284">The newly created user is displayed with the default roles assigned.</span></span>

<span data-ttu-id="fc8b0-285">기본 역할:</span><span class="sxs-lookup"><span data-stu-id="fc8b0-285">Default roles:</span></span>
- <span data-ttu-id="fc8b0-286">personalize_choices</span><span class="sxs-lookup"><span data-stu-id="fc8b0-286">personalize_choices</span></span>
- <span data-ttu-id="fc8b0-287">import_transformer</span><span class="sxs-lookup"><span data-stu-id="fc8b0-287">import_transformer</span></span>
-   <span data-ttu-id="fc8b0-288">x_mioms_microsoft.user</span><span class="sxs-lookup"><span data-stu-id="fc8b0-288">x_mioms_microsoft.user</span></span>
-   <span data-ttu-id="fc8b0-289">itil</span><span class="sxs-lookup"><span data-stu-id="fc8b0-289">itil</span></span>
-   <span data-ttu-id="fc8b0-290">template_editor</span><span class="sxs-lookup"><span data-stu-id="fc8b0-290">template_editor</span></span>
-   <span data-ttu-id="fc8b0-291">view_changer</span><span class="sxs-lookup"><span data-stu-id="fc8b0-291">view_changer</span></span>

<span data-ttu-id="fc8b0-292">사용자가 성공적으로 만들어지면 **설치 검사 목록 확인**의 상태가 완료됨으로 바뀌고 해당 앱에 대해 만들어진 사용자의 역할 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-292">Once the user is successfully created, the status of **Check Installation Checklist** moves to Completed, listing the details of the user role created for the app.</span></span>

> [!NOTE]

> <span data-ttu-id="fc8b0-293">사용자가 OMS에서 ServiceNow에 **경고** 및 **이벤트**를 만들 수 있게 하려면</span><span class="sxs-lookup"><span data-stu-id="fc8b0-293">To allow a user to create **alerts** and **events** in ServiceNow from OMS:</span></span>

> - <span data-ttu-id="fc8b0-294">ServiceNow 인스턴스에 이벤트 관리 모듈이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-294">Ensure you have the Event Management module Installed on your ServiceNow instance.</span></span>

> - <span data-ttu-id="fc8b0-295">통합 사용자에게 다음과 같은 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-295">Add the following roles to the integration user:</span></span>
>      - <span data-ttu-id="fc8b0-296">evt_mgmt_integration</span><span class="sxs-lookup"><span data-stu-id="fc8b0-296">evt_mgmt_integration</span></span>
>      - <span data-ttu-id="fc8b0-297">evt_mgmt_operator</span><span class="sxs-lookup"><span data-stu-id="fc8b0-297">evt_mgmt_operator</span></span>  


## <a name="connect-provance-to-it-service-management-connector-in-oms"></a><span data-ttu-id="fc8b0-298">Province를 OMS의 IT Service Management Connector에 연결</span><span class="sxs-lookup"><span data-stu-id="fc8b0-298">Connect Provance to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="fc8b0-299">다음 섹션에서는 Provance 제품을 OMS의 IT Service Management Connector에 연결하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-299">The following sections provide details about how to connect your Provance product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fc8b0-300">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fc8b0-300">Prerequisites</span></span>

<span data-ttu-id="fc8b0-301">다음 필수 조건을 갖추고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-301">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="fc8b0-302">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-302">IT Service Management Connector installed.</span></span> <span data-ttu-id="fc8b0-303">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-303">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="fc8b0-304">Provance 앱을 Azure AD에 등록해야 합니다. 그래야 클라이언트 ID를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-304">Provance App should be registered with Azure AD - and client ID is made available.</span></span> <span data-ttu-id="fc8b0-305">자세한 내용은 [Active Directory 인증을 구성하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-305">For detailed information, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
- <span data-ttu-id="fc8b0-306">사용자 역할: 관리자</span><span class="sxs-lookup"><span data-stu-id="fc8b0-306">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="fc8b0-307">연결 절차</span><span class="sxs-lookup"><span data-stu-id="fc8b0-307">Connection Procedure</span></span>

<span data-ttu-id="fc8b0-308">다음 절차에 따라 Provance 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-308">Use the following procedure to create a Provance connection:</span></span>

1. <span data-ttu-id="fc8b0-309">**OMS** > **설정** > **연결된 원본**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-309">Go to **OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="fc8b0-310">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-310">Select **ITSM Connector,** click **Add New Connection**.</span></span>  

    ![Provance 연결](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. <span data-ttu-id="fc8b0-312">다음 표에 설명된 대로 정보를 제공하고 **저장**을 클릭하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-312">Provide the information as described in the following table, and click **Save** to create the connection.</span></span>

> [!NOTE]
> <span data-ttu-id="fc8b0-313">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-313">All these parameters are mandatory.</span></span>

| <span data-ttu-id="fc8b0-314">**필드**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-314">**Field**</span></span> | <span data-ttu-id="fc8b0-315">**설명**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-315">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fc8b0-316">**Name**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-316">**Name**</span></span>   | <span data-ttu-id="fc8b0-317">IT Service Management Connector에 연결하려는 Provance 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-317">Type a name for the Provance instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-318">이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-318">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="fc8b0-319">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-319">**Select Connection type**</span></span>   | <span data-ttu-id="fc8b0-320">**Provance**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-320">Select **Provance**.</span></span> |
| <span data-ttu-id="fc8b0-321">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-321">**Username**</span></span>   | <span data-ttu-id="fc8b0-322">IT Service Management Connector에 연결할 수 있는 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-322">Type the user name that can connect to the IT Service Management Connector.</span></span>    |
| <span data-ttu-id="fc8b0-323">**암호**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-323">**Password**</span></span>   | <span data-ttu-id="fc8b0-324">이 사용자 이름과 관련된 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-324">Type the password associated with this user name.</span></span> <span data-ttu-id="fc8b0-325">**참고**: 사용자 이름 및 암호는 인증 토큰 생성에만 사용되며 OMS 서비스에는 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-325">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service._</span></span>|
| <span data-ttu-id="fc8b0-326">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-326">**Server URL**</span></span>   | <span data-ttu-id="fc8b0-327">IT Service Management Connector에 연결하려는 Provance 인스턴스의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-327">Type the URL of your Provance instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="fc8b0-328">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-328">**Client ID**</span></span>   | <span data-ttu-id="fc8b0-329">Provance 인스턴스에서 생성한 이 연결을 인증하기 위한 클라이언트 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-329">Type the client ID for authenticating this connection, which you generated in your Provance instance.</span></span>  <span data-ttu-id="fc8b0-330">클라이언트 ID에 대한 자세한 내용은 [Active Directory 인증을 구성하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-330">More information on client ID, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> |
| <span data-ttu-id="fc8b0-331">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-331">**Data Sync Scope**</span></span>   | <span data-ttu-id="fc8b0-332">IT Service Management Connector를 통해 OMS와 동기화할 Provance 작업 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-332">Select the Provance work items that you want to sync to OMS, through the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-333">이러한 작업 항목을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-333">These work items are imported into log analytics.</span></span>   <span data-ttu-id="fc8b0-334">**옵션:** 인시던트, 변경 요청</span><span class="sxs-lookup"><span data-stu-id="fc8b0-334">**Options:**   Incidents, Change Requests.</span></span>|
| <span data-ttu-id="fc8b0-335">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-335">**Sync Data**</span></span> | <span data-ttu-id="fc8b0-336">데이터를 원하는 이전 일 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-336">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="fc8b0-337">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="fc8b0-337">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="fc8b0-338">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-338">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="fc8b0-339">ITSM 제품에서 구성 항목을 만들려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-339">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="fc8b0-340">이 옵션을 선택하면 OMS는 지원되는 ITSM 시스템에서 영향을 받는 CI(존재하지 않는 CI)를 구성 항목으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-340">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="fc8b0-341">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-341">**Default**: disabled.</span></span>|

<span data-ttu-id="fc8b0-342">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="fc8b0-342">When successfully connected, and synced:</span></span>

- <span data-ttu-id="fc8b0-343">Provance 연결의 선택한 작업 항목을 OMS **Log Analytics**로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-343">Selected work items from Provance connection are imported into OMS **Log Analytics.**</span></span>  <span data-ttu-id="fc8b0-344">IT Service Management Connector 타일에서 이러한 작업 항목에 대한 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-344">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="fc8b0-345">OMS 경고 또는 이 Provance 인스턴스의 로그 검색에서 인시던트 및 이벤트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-345">You can create incidents and events from OMS Alerts or Log Search in this Provance instance.</span></span>

<span data-ttu-id="fc8b0-346">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-346">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

## <a name="connect-cherwell-to-it-service-management-connector-in-oms"></a><span data-ttu-id="fc8b0-347">Cherwell를 OMS의 IT Service Management Connector에 연결</span><span class="sxs-lookup"><span data-stu-id="fc8b0-347">Connect Cherwell to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="fc8b0-348">다음 섹션에서는 Cherwell 제품을 OMS의 IT Service Management Connector에 연결하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-348">The following sections provide details about how to connect your Cherwell product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fc8b0-349">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fc8b0-349">Prerequisites</span></span>

<span data-ttu-id="fc8b0-350">다음 필수 조건을 갖추고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-350">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="fc8b0-351">IT Service Management Connector가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-351">IT Service Management Connector installed.</span></span> <span data-ttu-id="fc8b0-352">추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-352">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="fc8b0-353">클라이언트 ID가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-353">Client ID generated.</span></span> <span data-ttu-id="fc8b0-354">추가 정보: [Cherwell용 클라이언트 ID 생성](#generate-client-id-for-cherwell)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-354">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span></span>
- <span data-ttu-id="fc8b0-355">사용자 역할: 관리자</span><span class="sxs-lookup"><span data-stu-id="fc8b0-355">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="fc8b0-356">연결 절차</span><span class="sxs-lookup"><span data-stu-id="fc8b0-356">Connection Procedure</span></span>

<span data-ttu-id="fc8b0-357">다음 절차에 따라 Cherwell 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-357">Use the following procedure to create a Cherwell connection:</span></span>

1. <span data-ttu-id="fc8b0-358">**OMS** >  **설정** > **연결된 원본**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-358">Go to **OMS** >  **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="fc8b0-359">**ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-359">Select **ITSM Connector** click **Add New Connection**.</span></span>  

    ![Cherwell 사용자 ID](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. <span data-ttu-id="fc8b0-361">다음 표에 설명된 대로 정보를 제공하고 **저장**을 클릭하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-361">Provide the information as described in the following table, and click  **Save** to create the connection.</span></span>

> [!NOTE]
> <span data-ttu-id="fc8b0-362">이러한 모든 매개 변수는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-362">All these parameters are mandatory.</span></span>

| <span data-ttu-id="fc8b0-363">**필드**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-363">**Field**</span></span> | <span data-ttu-id="fc8b0-364">**설명**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-364">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fc8b0-365">**Name**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-365">**Name**</span></span>   | <span data-ttu-id="fc8b0-366">IT Service Management Connector에 연결하려는 Cherwell 인스턴스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-366">Type a name for the Cherwell instance that you want to connect to the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-367">이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-367">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="fc8b0-368">**연결 형식 선택**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-368">**Select Connection type**</span></span>   | <span data-ttu-id="fc8b0-369">**Cherwell**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-369">Select **Cherwell.**</span></span> |
| <span data-ttu-id="fc8b0-370">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-370">**Username**</span></span>   | <span data-ttu-id="fc8b0-371">IT Service Management Connector에 연결할 수 있는 Cherwell 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-371">Type the Cherwell user name that can connect to the IT Service Management Connector.</span></span> |
| <span data-ttu-id="fc8b0-372">**암호**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-372">**Password**</span></span>   | <span data-ttu-id="fc8b0-373">이 사용자 이름과 관련된 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-373">Type the password associated with this user name.</span></span> <span data-ttu-id="fc8b0-374">**참고**: 사용자 이름 및 암호는 인증 토큰 생성에만 사용되며 OMS 서비스에는 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-374">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service.</span></span>|
| <span data-ttu-id="fc8b0-375">**서버 URL**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-375">**Server URL**</span></span>   | <span data-ttu-id="fc8b0-376">IT Service Management Connector에 연결하려는 Cherwell 인스턴스의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-376">Type the URL of your Cherwell instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="fc8b0-377">**클라이언트 ID**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-377">**Client ID**</span></span>   | <span data-ttu-id="fc8b0-378">Cherwell 인스턴스에서 생성한 이 연결을 인증하기 위한 클라이언트 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-378">Type the client ID for authenticating this connection, which you generated in your Cherwell instance.</span></span>   |
| <span data-ttu-id="fc8b0-379">**데이터 동기화 범위**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-379">**Data Sync Scope**</span></span>   | <span data-ttu-id="fc8b0-380">IT Service Management Connector를 통해 동기화할 Cherwell 작업 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-380">Select the Cherwell work items that you want to sync through the IT Service Management Connector.</span></span>  <span data-ttu-id="fc8b0-381">이러한 작업 항목을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-381">These work items are imported into log analytics.</span></span>   <span data-ttu-id="fc8b0-382">**옵션:** 인시던트, 변경 요청</span><span class="sxs-lookup"><span data-stu-id="fc8b0-382">**Options:**  Incidents, Change Requests.</span></span> |
| <span data-ttu-id="fc8b0-383">**데이터 동기화**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-383">**Sync Data**</span></span> | <span data-ttu-id="fc8b0-384">데이터를 원하는 이전 일 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-384">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="fc8b0-385">**최대 제한**: 120일</span><span class="sxs-lookup"><span data-stu-id="fc8b0-385">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="fc8b0-386">**ITSM 솔루션에서 새 구성 항목 만들기**</span><span class="sxs-lookup"><span data-stu-id="fc8b0-386">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="fc8b0-387">ITSM 제품에서 구성 항목을 만들려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-387">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="fc8b0-388">이 옵션을 선택하면 OMS는 지원되는 ITSM 시스템에서 영향을 받는 CI(존재하지 않는 CI)를 구성 항목으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-388">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="fc8b0-389">**기본**: 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-389">**Default**: disabled.</span></span> |

<span data-ttu-id="fc8b0-390">성공적으로 연결 및 동기화된 경우:</span><span class="sxs-lookup"><span data-stu-id="fc8b0-390">When successfully connected, and synced:</span></span>

- <span data-ttu-id="fc8b0-391">이 Cherwell 연결에서 선택된 작업 항목을 OMS Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-391">Selected work items from this Cherwell connection are imported into OMS Log Analytics.</span></span> <span data-ttu-id="fc8b0-392">IT Service Management Connector 타일에서 이러한 작업 항목에 대한 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-392">You can view the summary of these work items  on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="fc8b0-393">OMS에서 이 Cherwell 인스턴스의 인시던트 및 이벤트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-393">You can create incidents and events in this Cherwell instance from OMS.</span></span> <span data-ttu-id="fc8b0-394">추가 정보: OMS 경고에 대한 ITSM 작업 항목 만들기 및 OMS 로그에서 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="fc8b0-394">More information: Create ITSM work items for OMS alerts and Create ITSM work items from OMS logs.</span></span>

<span data-ttu-id="fc8b0-395">추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)</span><span class="sxs-lookup"><span data-stu-id="fc8b0-395">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="generate-client-id-for-cherwell"></a><span data-ttu-id="fc8b0-396">Cherwell용 클라이언트 ID 생성</span><span class="sxs-lookup"><span data-stu-id="fc8b0-396">Generate client ID for Cherwell</span></span>

<span data-ttu-id="fc8b0-397">Cherwell용 클라이언트 ID/키를 생성하려면 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-397">To generate the client ID/key for Cherwell, use the following procedure:</span></span>

1. <span data-ttu-id="fc8b0-398">Cherwell 인스턴스에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-398">Log in to your Cherwell instance as admin.</span></span>
2. <span data-ttu-id="fc8b0-399">**보안** > **REST API 클라이언트 설정 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-399">Click **Security** > **Edit REST API client settings**.</span></span>
3. <span data-ttu-id="fc8b0-400">**새 클라이언트 만들기** > **클라이언트 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc8b0-400">Select **Create new client** > **client secret**.</span></span>

    ![Cherwell 사용자 ID](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a><span data-ttu-id="fc8b0-402">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc8b0-402">Next steps</span></span>
 - [<span data-ttu-id="fc8b0-403">OMS 경고에 대한 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="fc8b0-403">Create ITSM work items for OMS alerts</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [<span data-ttu-id="fc8b0-404">OMS 로그에서 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="fc8b0-404">Create ITSM work items from OMS logs</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [<span data-ttu-id="fc8b0-405">연결에 대한 Log Analytics 보기</span><span class="sxs-lookup"><span data-stu-id="fc8b0-405">View log analytics for your connection</span></span>](log-analytics-itsmc-overview.md#using-the-solution)
