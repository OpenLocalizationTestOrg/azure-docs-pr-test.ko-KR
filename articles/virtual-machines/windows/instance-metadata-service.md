---
title: "Windows 용 인스턴스 메타 데이터 서비스 aaaAzure | Microsoft Docs"
description: "Windows VM의 계산, 네트워크 및 향후 유지 관리 이벤트에 대 한 rESTful 인터페이스 tooget 정보입니다."
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a><span data-ttu-id="22a43-103">Windows VM용 Azure Instance Metadata Service</span><span class="sxs-lookup"><span data-stu-id="22a43-103">Azure Instance Metadata service for Windows VMs</span></span>


<span data-ttu-id="22a43-104">hello Azure 인스턴스 메타 데이터 서비스는 가상 컴퓨터를 구성 하 고 사용 하는 toomanage 수 있는 가상 컴퓨터 인스턴스를 실행 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="22a43-105">여기에는 SKU, 네트워크 구성, 예정된 유지 관리 이벤트 등의 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="22a43-106">사용 가능한 정보 유형에 대한 자세한 내용은 [메타데이터 범주](#instance-metadata-data-categories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22a43-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="22a43-107">Azure의 인스턴스 메타 데이터 서비스는 hello를 통해 액세스할 수 있는 tooall IaaS Vm 만든 REST 끝점 [Azure 리소스 관리자](https://docs.microsoft.com/rest/api/resources/)합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="22a43-108">hello 끝점은 잘 알려진 라우팅할 수 없는 IP 주소에서 사용할 수 (`169.254.169.254`) hello VM 내 에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>



> [!IMPORTANT]
> <span data-ttu-id="22a43-109">이 서비스는 글로벌 Azure 지역에서 **일반 공급**됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="22a43-110">정부, 중국 및 독일어 Azure 클라우드에 대한 공개 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="22a43-111">정기적으로 가상 컴퓨터 인스턴스에 대 한 업데이트 tooexpose 새 정보를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="22a43-112">이 페이지에는 최신 hello 반영 [데이터 범주](#instance-metadata-data-categories) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>



## <a name="service-availability"></a><span data-ttu-id="22a43-113">서비스 가용성</span><span class="sxs-lookup"><span data-stu-id="22a43-113">Service Availability</span></span>
<span data-ttu-id="22a43-114">hello 서비스를 사용할 수 있는 모든 전역 Azure 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="22a43-115">hello 서비스는 hello 정부, 중국, 또는 독일 지역에서 공개 미리 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="22a43-116">영역</span><span class="sxs-lookup"><span data-stu-id="22a43-116">Regions</span></span>                                        | <span data-ttu-id="22a43-117">가용성</span><span class="sxs-lookup"><span data-stu-id="22a43-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="22a43-118">일반 공급되는 모든 글로벌 Azure 지역</span><span class="sxs-lookup"><span data-stu-id="22a43-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="22a43-119">일반 공급</span><span class="sxs-lookup"><span data-stu-id="22a43-119">Generally Available</span></span> 
[<span data-ttu-id="22a43-120">Azure Government</span><span class="sxs-lookup"><span data-stu-id="22a43-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="22a43-121">미리 보기</span><span class="sxs-lookup"><span data-stu-id="22a43-121">In Preview</span></span> 
[<span data-ttu-id="22a43-122">Azure 중국</span><span class="sxs-lookup"><span data-stu-id="22a43-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="22a43-123">미리 보기</span><span class="sxs-lookup"><span data-stu-id="22a43-123">In Preview</span></span>
[<span data-ttu-id="22a43-124">Azure 독일</span><span class="sxs-lookup"><span data-stu-id="22a43-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="22a43-125">미리 보기</span><span class="sxs-lookup"><span data-stu-id="22a43-125">In Preview</span></span>

<span data-ttu-id="22a43-126">이 테이블의 다른 Azure 클라우드의 hello 서비스 사용할 수 있을 때 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="22a43-127">tootry 아웃 hello 인스턴스 메타 데이터 서비스에서 VM을 만들 [Azure 리소스 관리자](https://docs.microsoft.com/rest/api/resources/) 또는 hello [Azure 포털](http://portal.azure.com) 영역 및 아래에 따라 hello 예제 위에 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="22a43-128">사용</span><span class="sxs-lookup"><span data-stu-id="22a43-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="22a43-129">버전 관리</span><span class="sxs-lookup"><span data-stu-id="22a43-129">Versioning</span></span>
<span data-ttu-id="22a43-130">hello 인스턴스 메타 데이터 서비스 버전 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="22a43-131">버전은 필수 이며 hello 현재 버전은 `2017-04-02`합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="22a43-132">이전 버전으로 hello api 버전 {최신 버전을 (를) 지원 되는 예약 된 이벤트의 미리 보기.</span><span class="sxs-lookup"><span data-stu-id="22a43-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="22a43-133">이 형식은 더 이상 지원 하며 hello 나중에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="22a43-134">새로운 버전이 추가되더라도 스크립트가 특정 데이터 형식에 종속성이 있는 경우 이전 버전에 여전히 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="22a43-135">그러나 해당 hello 현재 미리 보기 version(2017-03-01) 하지 못할 hello 서비스를 일반적으로 사용할 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="22a43-136">헤더 사용</span><span class="sxs-lookup"><span data-stu-id="22a43-136">Using headers</span></span>
<span data-ttu-id="22a43-137">Hello 헤더를 제공 해야 hello 인스턴스 메타 데이터 서비스를 쿼리할 때 `Metadata: true` tooensure hello 요청이 실수로 리디렉션된 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="22a43-138">메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="22a43-138">Retrieving metadata</span></span>

<span data-ttu-id="22a43-139">인스턴스 메타데이터는 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)를 사용하여 생성/관리되는 VM을 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="22a43-140">요청을 수행 하는 hello를 사용 하 여 가상 컴퓨터 인스턴스에 대 한 모든 데이터 범주에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="22a43-141">모든 인스턴스 메타데이터 쿼리는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="22a43-142">데이터 출력</span><span class="sxs-lookup"><span data-stu-id="22a43-142">Data output</span></span>
<span data-ttu-id="22a43-143">기본적으로 인스턴스 메타 데이터 서비스 hello JSON 형식의 데이터를 반환 (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="22a43-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="22a43-144">그러나 다른 API는 요청된 경우 다른 형식으로 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="22a43-145">hello 다음 표는에 대 한 참조의 다른 데이터 형식의 Api 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="22a43-146">API</span><span class="sxs-lookup"><span data-stu-id="22a43-146">API</span></span> | <span data-ttu-id="22a43-147">기본 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="22a43-147">Default Data Format</span></span> | <span data-ttu-id="22a43-148">다른 형식</span><span class="sxs-lookup"><span data-stu-id="22a43-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="22a43-149">/instance</span><span class="sxs-lookup"><span data-stu-id="22a43-149">/instance</span></span> | <span data-ttu-id="22a43-150">json :</span><span class="sxs-lookup"><span data-stu-id="22a43-150">json</span></span> | <span data-ttu-id="22a43-151">텍스트</span><span class="sxs-lookup"><span data-stu-id="22a43-151">text</span></span>
<span data-ttu-id="22a43-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="22a43-152">/scheduledevents</span></span> | <span data-ttu-id="22a43-153">json :</span><span class="sxs-lookup"><span data-stu-id="22a43-153">json</span></span> | <span data-ttu-id="22a43-154">없음</span><span class="sxs-lookup"><span data-stu-id="22a43-154">none</span></span>

<span data-ttu-id="22a43-155">tooaccess 기본이 아닌 응답 형식으로 hello 요청 쿼리 문자열 매개 변수로 hello 요청 된 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="22a43-156">예:</span><span class="sxs-lookup"><span data-stu-id="22a43-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="22a43-157">보안</span><span class="sxs-lookup"><span data-stu-id="22a43-157">Security</span></span>
<span data-ttu-id="22a43-158">hello 인스턴스 메타 데이터 서비스 끝점을 라우팅할 수 없는 IP 주소를 가상 컴퓨터 인스턴스를 실행 하는 hello 내 에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="22a43-159">또한 모든 요청을 `X-Forwarded-For` 헤더 hello 서비스에 의해 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="22a43-160">또한 요청 toocontain 필요는 `Metadata: true` hello 실제 요청 헤더 tooensure 의도 대로 되었으며 직접 의도 하지 않은 리디렉션의 일부분이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="22a43-161">오류</span><span class="sxs-lookup"><span data-stu-id="22a43-161">Error</span></span>
<span data-ttu-id="22a43-162">데이터 요소를 찾을 수 없음 또는 잘못 된 요청 있는 경우 hello 인스턴스 메타 데이터 서비스는 표준 HTTP 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="22a43-163">예:</span><span class="sxs-lookup"><span data-stu-id="22a43-163">For example:</span></span>

<span data-ttu-id="22a43-164">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="22a43-164">HTTP Status Code</span></span> | <span data-ttu-id="22a43-165">이유</span><span class="sxs-lookup"><span data-stu-id="22a43-165">Reason</span></span>
----------------|-------
<span data-ttu-id="22a43-166">200 정상</span><span class="sxs-lookup"><span data-stu-id="22a43-166">200 OK</span></span> |
<span data-ttu-id="22a43-167">400 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="22a43-167">400 Bad Request</span></span> | <span data-ttu-id="22a43-168">누락된 `Metadata: true` 헤더</span><span class="sxs-lookup"><span data-stu-id="22a43-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="22a43-169">404 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="22a43-169">404 Not Found</span></span> | <span data-ttu-id="22a43-170">hello 요청 된 요소와 존재</span><span class="sxs-lookup"><span data-stu-id="22a43-170">hello requested element does't exist</span></span> 
<span data-ttu-id="22a43-171">405 메서드를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="22a43-171">405 Method Not Allowed</span></span> | <span data-ttu-id="22a43-172">`GET` 및 `POST` 요청만 지원됨</span><span class="sxs-lookup"><span data-stu-id="22a43-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="22a43-173">429 요청이 너무 많음</span><span class="sxs-lookup"><span data-stu-id="22a43-173">429 Too Many Requests</span></span> | <span data-ttu-id="22a43-174">hello API에는 현재 5 queries / sec의 최대 지원</span><span class="sxs-lookup"><span data-stu-id="22a43-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="22a43-175">500 서비스 오류</span><span class="sxs-lookup"><span data-stu-id="22a43-175">500 Service Error</span></span>     | <span data-ttu-id="22a43-176">잠시 후 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="22a43-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="22a43-177">예</span><span class="sxs-lookup"><span data-stu-id="22a43-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="22a43-178">모든 API 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-178">All API responses are JSON strings.</span></span> <span data-ttu-id="22a43-179">다음 예제 응답은 모두 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="22a43-180">네트워크 정보 검색</span><span class="sxs-lookup"><span data-stu-id="22a43-180">Retrieving network information</span></span>

<span data-ttu-id="22a43-181">**요청**</span><span class="sxs-lookup"><span data-stu-id="22a43-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="22a43-182">**응답**</span><span class="sxs-lookup"><span data-stu-id="22a43-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="22a43-183">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-183">hello response is a JSON string.</span></span> <span data-ttu-id="22a43-184">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-184">hello following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="22a43-185">공용 IP 주소 검색</span><span class="sxs-lookup"><span data-stu-id="22a43-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="22a43-186">인스턴스에 대한 모든 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="22a43-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="22a43-187">**요청**</span><span class="sxs-lookup"><span data-stu-id="22a43-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="22a43-188">**응답**</span><span class="sxs-lookup"><span data-stu-id="22a43-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="22a43-189">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-189">hello response is a JSON string.</span></span> <span data-ttu-id="22a43-190">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-190">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="22a43-191">Windows 가상 컴퓨터에서 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="22a43-191">Retrieving metadata in Windows virtual machine</span></span>

<span data-ttu-id="22a43-192">**요청**</span><span class="sxs-lookup"><span data-stu-id="22a43-192">**Request**</span></span>

<span data-ttu-id="22a43-193">Hello PowerShell 유틸리티를 통해 Windows에서 인스턴스 메타 데이터를 검색할 수 있는 `curl`:</span><span class="sxs-lookup"><span data-stu-id="22a43-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="22a43-194">또는 hello 통해 `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="22a43-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="22a43-195">**응답**</span><span class="sxs-lookup"><span data-stu-id="22a43-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="22a43-196">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-196">hello response is a JSON string.</span></span> <span data-ttu-id="22a43-197">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-197">hello following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="22a43-198">인스턴스 메타데이터 데이터 범주</span><span class="sxs-lookup"><span data-stu-id="22a43-198">Instance metadata data categories</span></span>
<span data-ttu-id="22a43-199">다음 데이터 범주 hello hello 인스턴스 메타 데이터 서비스를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="22a43-200">Data</span><span class="sxs-lookup"><span data-stu-id="22a43-200">Data</span></span> | <span data-ttu-id="22a43-201">설명</span><span class="sxs-lookup"><span data-stu-id="22a43-201">Description</span></span>
-----|------------
<span data-ttu-id="22a43-202">location</span><span class="sxs-lookup"><span data-stu-id="22a43-202">location</span></span> | <span data-ttu-id="22a43-203">Azure 지역 hello VM에서 실행 되</span><span class="sxs-lookup"><span data-stu-id="22a43-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="22a43-204">name</span><span class="sxs-lookup"><span data-stu-id="22a43-204">name</span></span> | <span data-ttu-id="22a43-205">Hello VM의 이름</span><span class="sxs-lookup"><span data-stu-id="22a43-205">Name of hello VM</span></span> 
<span data-ttu-id="22a43-206">offer</span><span class="sxs-lookup"><span data-stu-id="22a43-206">offer</span></span> | <span data-ttu-id="22a43-207">Hello VM 이미지에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-207">Offer information for hello VM image.</span></span> <span data-ttu-id="22a43-208">이 값은 Azure 이미지 갤러리에서 배포된 이미지에 대해서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="22a43-209">publisher</span><span class="sxs-lookup"><span data-stu-id="22a43-209">publisher</span></span> | <span data-ttu-id="22a43-210">Hello VM 이미지의 게시자</span><span class="sxs-lookup"><span data-stu-id="22a43-210">Publisher of hello VM image</span></span>
<span data-ttu-id="22a43-211">sku</span><span class="sxs-lookup"><span data-stu-id="22a43-211">sku</span></span> | <span data-ttu-id="22a43-212">Hello VM 이미지에 대 한 특정 SKU</span><span class="sxs-lookup"><span data-stu-id="22a43-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="22a43-213">버전</span><span class="sxs-lookup"><span data-stu-id="22a43-213">version</span></span> | <span data-ttu-id="22a43-214">Hello VM 이미지의 버전</span><span class="sxs-lookup"><span data-stu-id="22a43-214">Version of hello VM image</span></span> 
<span data-ttu-id="22a43-215">osType</span><span class="sxs-lookup"><span data-stu-id="22a43-215">osType</span></span> | <span data-ttu-id="22a43-216">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="22a43-216">Linux or Windows</span></span> 
<span data-ttu-id="22a43-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="22a43-217">platformUpdateDomain</span></span> |  <span data-ttu-id="22a43-218">[업데이트 도메인](manage-availability.md) hello VM에서 실행 되 고</span><span class="sxs-lookup"><span data-stu-id="22a43-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="22a43-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="22a43-219">platformFaultDomain</span></span> | <span data-ttu-id="22a43-220">[오류 도메인](manage-availability.md) hello VM에서 실행 되 고</span><span class="sxs-lookup"><span data-stu-id="22a43-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="22a43-221">vmId</span><span class="sxs-lookup"><span data-stu-id="22a43-221">vmId</span></span> | <span data-ttu-id="22a43-222">[고유 식별자](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) hello VM에 대 한</span><span class="sxs-lookup"><span data-stu-id="22a43-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="22a43-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="22a43-223">vmSize</span></span> | [<span data-ttu-id="22a43-224">VM 크기</span><span class="sxs-lookup"><span data-stu-id="22a43-224">VM size</span></span>](sizes.md)
<span data-ttu-id="22a43-225">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="22a43-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="22a43-226">Hello VM의 로컬 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="22a43-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="22a43-227">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="22a43-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="22a43-228">Hello VM의 공용 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="22a43-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="22a43-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="22a43-229">subnet/address</span></span> | <span data-ttu-id="22a43-230">Hello VM의 서브넷 주소</span><span class="sxs-lookup"><span data-stu-id="22a43-230">Subnet address of hello VM</span></span>
<span data-ttu-id="22a43-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="22a43-231">subnet/prefix</span></span> | <span data-ttu-id="22a43-232">서브넷 접두사, 예:24</span><span class="sxs-lookup"><span data-stu-id="22a43-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="22a43-233">ipv6/ipaddress</span><span class="sxs-lookup"><span data-stu-id="22a43-233">ipv6/ipAddress</span></span> | <span data-ttu-id="22a43-234">Hello VM의 로컬 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="22a43-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="22a43-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="22a43-235">macAddress</span></span> | <span data-ttu-id="22a43-236">VM MAC 주소</span><span class="sxs-lookup"><span data-stu-id="22a43-236">VM mac address</span></span> 
<span data-ttu-id="22a43-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="22a43-237">scheduledevents</span></span> | <span data-ttu-id="22a43-238">현재 공개 미리 보기 [scheduledevents](scheduled-events.md) 참조</span><span class="sxs-lookup"><span data-stu-id="22a43-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="22a43-239">사용법을 위한 예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="22a43-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="22a43-240">Azure에서 실행 중인 VM 추적</span><span class="sxs-lookup"><span data-stu-id="22a43-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="22a43-241">서비스 공급자로 서 소프트웨어를 실행 중인 Vm tootrack hello 수 필요할 수 있습니다 또는 hello VM이 tootrack 고유 해야 하는 에이전트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="22a43-242">VM 사용 하 여 hello에 대 한 toobe 수 tooget 고유 ID `vmId` 인스턴스 메타 데이터 서비스에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="22a43-243">**요청**</span><span class="sxs-lookup"><span data-stu-id="22a43-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="22a43-244">**응답**</span><span class="sxs-lookup"><span data-stu-id="22a43-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="22a43-245">장애/업데이트 도메인 기반 컨테이너, 데이터 파티션 배치</span><span class="sxs-lookup"><span data-stu-id="22a43-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="22a43-246">특정 시나리오의 경우 다양한 데이터 복제본 배치가 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="22a43-247">예를 들어 [HDFS 복제본 배치](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) 또는 통해 컨테이너 위치는 [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) tooknow hello 필요할 수 있습니다 `platformFaultDomain` 및 `platformUpdateDomain` hello VM에서 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="22a43-248">Hello 인스턴스 메타 데이터 서비스를 통해 직접이 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="22a43-249">**요청**</span><span class="sxs-lookup"><span data-stu-id="22a43-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="22a43-250">**응답**</span><span class="sxs-lookup"><span data-stu-id="22a43-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="22a43-251">지원 사례 중 VM hello에 대 한 추가 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="22a43-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="22a43-252">서비스 공급자로 서 발생할 수 있습니다 지원 통화 넣을 tooknow hello VM에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="22a43-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="22a43-253">Hello 계산 메타 데이터 요청 hello 고객 tooshare Azure에서 VM의 hello 종류에 대 한 지원 전문가 tooknow hello에 대 한 기본 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="22a43-254">**요청**</span><span class="sxs-lookup"><span data-stu-id="22a43-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="22a43-255">**응답**</span><span class="sxs-lookup"><span data-stu-id="22a43-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="22a43-256">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-256">hello response is a JSON string.</span></span> <span data-ttu-id="22a43-257">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-257">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="22a43-258">Hello VM 내 서로 다른 언어를 사용 하 여 메타 데이터 서비스 호출의 예</span><span class="sxs-lookup"><span data-stu-id="22a43-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="22a43-259">언어</span><span class="sxs-lookup"><span data-stu-id="22a43-259">Language</span></span> | <span data-ttu-id="22a43-260">예제</span><span class="sxs-lookup"><span data-stu-id="22a43-260">Example</span></span> 
---------|----------------
<span data-ttu-id="22a43-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="22a43-261">Ruby</span></span>     | <span data-ttu-id="22a43-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="22a43-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="22a43-263">Go Lan</span><span class="sxs-lookup"><span data-stu-id="22a43-263">Go Lan</span></span>   | <span data-ttu-id="22a43-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="22a43-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="22a43-265">python</span><span class="sxs-lookup"><span data-stu-id="22a43-265">python</span></span>   | <span data-ttu-id="22a43-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="22a43-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="22a43-267">C++</span><span class="sxs-lookup"><span data-stu-id="22a43-267">C++</span></span>      | <span data-ttu-id="22a43-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="22a43-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="22a43-269">C#</span><span class="sxs-lookup"><span data-stu-id="22a43-269">C#</span></span>       | <span data-ttu-id="22a43-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="22a43-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="22a43-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="22a43-271">Javascript</span></span> | <span data-ttu-id="22a43-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="22a43-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="22a43-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a43-273">Powershell</span></span> | <span data-ttu-id="22a43-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="22a43-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="22a43-275">Bash</span><span class="sxs-lookup"><span data-stu-id="22a43-275">Bash</span></span>       | <span data-ttu-id="22a43-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="22a43-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="22a43-277">FAQ</span><span class="sxs-lookup"><span data-stu-id="22a43-277">FAQ</span></span>
1. <span data-ttu-id="22a43-278">Hello 오류가 발생 `400 Bad Request, Required metadata header not specified`합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="22a43-279">무슨 의미인가요?</span><span class="sxs-lookup"><span data-stu-id="22a43-279">What does this mean?</span></span>
   * <span data-ttu-id="22a43-280">hello 헤더를 요구 하는 hello 인스턴스 메타 데이터 서비스 `Metadata: true` toobe hello 요청에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="22a43-281">Hello REST 호출에이 헤더를 전달 하면 액세스 toohello 인스턴스 메타 데이터 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="22a43-282">VM에 대한 계산 정보를 구할 수 없는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="22a43-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="22a43-283">현재 hello 인스턴스 메타 데이터 서비스는 Azure 리소스 관리자와 함께 만든 인스턴스에 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="22a43-284">Hello 이후,에서는 클라우드 서비스 Vm에 대 한 지원을 추가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="22a43-285">잠시 전에 Azure Resource Manager를 통해 내 가상 컴퓨터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="22a43-286">계산 메타데이터 정보가 왜 표시되지 않나요?</span><span class="sxs-lookup"><span data-stu-id="22a43-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="22a43-287">2016 년 9 월 이후 만들어진 모든 Vm을 추가 하는 [태그](../../azure-resource-manager/resource-group-using-tags.md) toostart 보는 계산 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="22a43-288">이전 Vm (2016 년 9 월 이전에 만든)을 위한 추가/제거 확장 또는 데이터 디스크 toohello VM toorefresh 메타 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="22a43-289">이유는 무엇입니까 hello 오류 `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="22a43-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="22a43-290">지수 백오프 시스템을 기반으로 요청을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="22a43-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="22a43-291">Hello 문제가 계속 되 면 Azure 지원을 담당자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="22a43-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="22a43-292">추가 질문/의견은 어디에 공유하나요?</span><span class="sxs-lookup"><span data-stu-id="22a43-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="22a43-293">의견은 http://feedback.azure.com에서 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="22a43-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="22a43-294">가상 컴퓨터 확장 집합 인스턴스에 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="22a43-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="22a43-295">예, 메타데이터 서비스는 확장 집합 인스턴스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="22a43-296">Hello 서비스에 대 한 지원 받기</span><span class="sxs-lookup"><span data-stu-id="22a43-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="22a43-297">hello 서비스에 대 한 tooget 지원 hello 없는 수 tooget 메타 데이터 응답 긴 다시 시도한 후 VM에 대 한 Azure 포털에서 지원 문제를 만들려면</span><span class="sxs-lookup"><span data-stu-id="22a43-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![인스턴스 메타데이터 지원](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="22a43-299">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22a43-299">Next steps</span></span>

- <span data-ttu-id="22a43-300">Hello에 대 한 자세한 [예약 된 이벤트](scheduled-events.md) API **공개 미리 보기에서** hello 인스턴스 메타 데이터 서비스에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a43-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
