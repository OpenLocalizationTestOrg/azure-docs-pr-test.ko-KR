---
title: "aaaAzure 인스턴스 메타 데이터 서비스 개요 | Microsoft Docs"
description: "VM의 계산, 네트워크 및 향후 유지 관리 이벤트에 대 한 rESTful 인터페이스 tooget 정보입니다."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="024a1-103">Azure Instance Metadata Service</span><span class="sxs-lookup"><span data-stu-id="024a1-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="024a1-104">hello Azure 인스턴스 메타 데이터 서비스는 가상 컴퓨터를 구성 하 고 사용 하는 toomanage 수 있는 가상 컴퓨터 인스턴스를 실행 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="024a1-105">여기에는 SKU, 네트워크 구성, 예정된 유지 관리 이벤트 등의 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="024a1-106">사용 가능한 정보 유형에 대한 자세한 내용은 [메타데이터 범주](#instance-metadata-data-categories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="024a1-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="024a1-107">Azure의 인스턴스 메타 데이터 서비스는 hello를 통해 액세스할 수 있는 tooall IaaS Vm 만든 REST 끝점 [Azure 리소스 관리자](https://docs.microsoft.com/rest/api/resources/)합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="024a1-108">hello 끝점은 잘 알려진 라우팅할 수 없는 IP 주소에서 사용할 수 (`169.254.169.254`) hello VM 내 에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="024a1-109">중요 정보</span><span class="sxs-lookup"><span data-stu-id="024a1-109">Important information</span></span>

<span data-ttu-id="024a1-110">이 서비스는 글로벌 Azure 지역에서 **일반 공급**됩니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="024a1-111">정부, 중국 및 독일어 Azure 클라우드에 대한 공개 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="024a1-112">정기적으로 가상 컴퓨터 인스턴스에 대 한 업데이트 tooexpose 새 정보를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="024a1-113">이 페이지에는 최신 hello 반영 [데이터 범주](#instance-metadata-data-categories) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="024a1-114">서비스 가용성</span><span class="sxs-lookup"><span data-stu-id="024a1-114">Service Availability</span></span>
<span data-ttu-id="024a1-115">hello 서비스를 사용할 수 있는 모든 전역 Azure 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="024a1-116">hello 서비스는 hello 정부, 중국, 또는 독일 지역에서 공개 미리 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="024a1-117">영역</span><span class="sxs-lookup"><span data-stu-id="024a1-117">Regions</span></span>                                        | <span data-ttu-id="024a1-118">가용성</span><span class="sxs-lookup"><span data-stu-id="024a1-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="024a1-119">일반 공급되는 모든 글로벌 Azure 지역</span><span class="sxs-lookup"><span data-stu-id="024a1-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="024a1-120">일반 공급</span><span class="sxs-lookup"><span data-stu-id="024a1-120">Generally Available</span></span> 
[<span data-ttu-id="024a1-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="024a1-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="024a1-122">미리 보기</span><span class="sxs-lookup"><span data-stu-id="024a1-122">In Preview</span></span> 
[<span data-ttu-id="024a1-123">Azure 중국</span><span class="sxs-lookup"><span data-stu-id="024a1-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="024a1-124">미리 보기</span><span class="sxs-lookup"><span data-stu-id="024a1-124">In Preview</span></span>
[<span data-ttu-id="024a1-125">Azure 독일</span><span class="sxs-lookup"><span data-stu-id="024a1-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="024a1-126">미리 보기</span><span class="sxs-lookup"><span data-stu-id="024a1-126">In Preview</span></span>

<span data-ttu-id="024a1-127">이 테이블의 다른 Azure 클라우드의 hello 서비스 사용할 수 있을 때 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="024a1-128">tootry 아웃 hello 인스턴스 메타 데이터 서비스에서 VM을 만들 [Azure 리소스 관리자](https://docs.microsoft.com/rest/api/resources/) 또는 hello [Azure 포털](http://portal.azure.com) 영역 및 아래에 따라 hello 예제 위에 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="024a1-129">사용</span><span class="sxs-lookup"><span data-stu-id="024a1-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="024a1-130">버전 관리</span><span class="sxs-lookup"><span data-stu-id="024a1-130">Versioning</span></span>
<span data-ttu-id="024a1-131">hello 인스턴스 메타 데이터 서비스 버전 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="024a1-132">버전은 필수 이며 hello 현재 버전은 `2017-04-02`합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="024a1-133">이전 버전으로 hello api 버전 {최신 버전을 (를) 지원 되는 예약 된 이벤트의 미리 보기.</span><span class="sxs-lookup"><span data-stu-id="024a1-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="024a1-134">이 형식은 더 이상 지원 하며 hello 나중에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="024a1-135">새로운 버전이 추가되더라도 스크립트가 특정 데이터 형식에 종속성이 있는 경우 이전 버전에 여전히 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="024a1-136">그러나 해당 hello 현재 미리 보기 version(2017-03-01) 하지 못할 hello 서비스를 일반적으로 사용할 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="024a1-137">헤더 사용</span><span class="sxs-lookup"><span data-stu-id="024a1-137">Using Headers</span></span>
<span data-ttu-id="024a1-138">Hello 헤더를 제공 해야 hello 인스턴스 메타 데이터 서비스를 쿼리할 때 `Metadata: true` tooensure hello 요청이 실수로 리디렉션된 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="024a1-139">메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="024a1-139">Retrieving metadata</span></span>

<span data-ttu-id="024a1-140">인스턴스 메타데이터는 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)를 사용하여 생성/관리되는 VM을 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="024a1-141">요청을 수행 하는 hello를 사용 하 여 가상 컴퓨터 인스턴스에 대 한 모든 데이터 범주에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="024a1-142">모든 인스턴스 메타데이터 쿼리는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="024a1-143">데이터 출력</span><span class="sxs-lookup"><span data-stu-id="024a1-143">Data output</span></span>
<span data-ttu-id="024a1-144">기본적으로 인스턴스 메타 데이터 서비스 hello JSON 형식의 데이터를 반환 (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="024a1-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="024a1-145">그러나 다른 API는 요청된 경우 다른 형식으로 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="024a1-146">hello 다음 표는에 대 한 참조의 다른 데이터 형식의 Api 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="024a1-147">API</span><span class="sxs-lookup"><span data-stu-id="024a1-147">API</span></span> | <span data-ttu-id="024a1-148">기본 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="024a1-148">Default Data Format</span></span> | <span data-ttu-id="024a1-149">다른 형식</span><span class="sxs-lookup"><span data-stu-id="024a1-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="024a1-150">/instance</span><span class="sxs-lookup"><span data-stu-id="024a1-150">/instance</span></span> | <span data-ttu-id="024a1-151">json :</span><span class="sxs-lookup"><span data-stu-id="024a1-151">json</span></span> | <span data-ttu-id="024a1-152">텍스트</span><span class="sxs-lookup"><span data-stu-id="024a1-152">text</span></span>
<span data-ttu-id="024a1-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="024a1-153">/scheduledevents</span></span> | <span data-ttu-id="024a1-154">json :</span><span class="sxs-lookup"><span data-stu-id="024a1-154">json</span></span> | <span data-ttu-id="024a1-155">없음</span><span class="sxs-lookup"><span data-stu-id="024a1-155">none</span></span>

<span data-ttu-id="024a1-156">tooaccess 기본이 아닌 응답 형식으로 hello 요청 쿼리 문자열 매개 변수로 hello 요청 된 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="024a1-157">예:</span><span class="sxs-lookup"><span data-stu-id="024a1-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="024a1-158">보안</span><span class="sxs-lookup"><span data-stu-id="024a1-158">Security</span></span>
<span data-ttu-id="024a1-159">hello 인스턴스 메타 데이터 서비스 끝점을 라우팅할 수 없는 IP 주소를 가상 컴퓨터 인스턴스를 실행 하는 hello 내 에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="024a1-160">또한 모든 요청을 `X-Forwarded-For` 헤더 hello 서비스에 의해 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="024a1-161">또한 요청 toocontain 필요는 `Metadata: true` hello 실제 요청 헤더 tooensure 의도 대로 되었으며 직접 의도 하지 않은 리디렉션의 일부분이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="024a1-162">오류</span><span class="sxs-lookup"><span data-stu-id="024a1-162">Error</span></span>
<span data-ttu-id="024a1-163">데이터 요소를 찾을 수 없음 또는 잘못 된 요청 있는 경우 hello 인스턴스 메타 데이터 서비스는 표준 HTTP 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="024a1-164">예:</span><span class="sxs-lookup"><span data-stu-id="024a1-164">For example:</span></span>

<span data-ttu-id="024a1-165">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="024a1-165">HTTP Status Code</span></span> | <span data-ttu-id="024a1-166">이유</span><span class="sxs-lookup"><span data-stu-id="024a1-166">Reason</span></span>
----------------|-------
<span data-ttu-id="024a1-167">200 정상</span><span class="sxs-lookup"><span data-stu-id="024a1-167">200 OK</span></span> |
<span data-ttu-id="024a1-168">400 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="024a1-168">400 Bad Request</span></span> | <span data-ttu-id="024a1-169">누락된 `Metadata: true` 헤더</span><span class="sxs-lookup"><span data-stu-id="024a1-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="024a1-170">404 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="024a1-170">404 Not Found</span></span> | <span data-ttu-id="024a1-171">hello 요청 된 요소와 존재</span><span class="sxs-lookup"><span data-stu-id="024a1-171">hello requested element does't exist</span></span> 
<span data-ttu-id="024a1-172">405 메서드를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="024a1-172">405 Method Not Allowed</span></span> | <span data-ttu-id="024a1-173">`GET` 및 `POST` 요청만 지원됨</span><span class="sxs-lookup"><span data-stu-id="024a1-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="024a1-174">429 요청이 너무 많음</span><span class="sxs-lookup"><span data-stu-id="024a1-174">429 Too Many Requests</span></span> | <span data-ttu-id="024a1-175">hello API에는 현재 5 queries / sec의 최대 지원</span><span class="sxs-lookup"><span data-stu-id="024a1-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="024a1-176">500 서비스 오류</span><span class="sxs-lookup"><span data-stu-id="024a1-176">500 Service Error</span></span>     | <span data-ttu-id="024a1-177">잠시 후 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="024a1-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="024a1-178">예</span><span class="sxs-lookup"><span data-stu-id="024a1-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="024a1-179">모든 API 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-179">All API responses are JSON strings.</span></span> <span data-ttu-id="024a1-180">다음 예제 응답은 모두 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="024a1-181">네트워크 정보 검색</span><span class="sxs-lookup"><span data-stu-id="024a1-181">Retrieving network information</span></span>

<span data-ttu-id="024a1-182">**요청**</span><span class="sxs-lookup"><span data-stu-id="024a1-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="024a1-183">**응답**</span><span class="sxs-lookup"><span data-stu-id="024a1-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="024a1-184">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-184">hello response is a JSON string.</span></span> <span data-ttu-id="024a1-185">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-185">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="024a1-186">공용 IP 주소 검색</span><span class="sxs-lookup"><span data-stu-id="024a1-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="024a1-187">인스턴스에 대한 모든 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="024a1-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="024a1-188">**요청**</span><span class="sxs-lookup"><span data-stu-id="024a1-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="024a1-189">**응답**</span><span class="sxs-lookup"><span data-stu-id="024a1-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="024a1-190">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-190">hello response is a JSON string.</span></span> <span data-ttu-id="024a1-191">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-191">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="024a1-192">Windows 가상 컴퓨터에서 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="024a1-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="024a1-193">**요청**</span><span class="sxs-lookup"><span data-stu-id="024a1-193">**Request**</span></span>

<span data-ttu-id="024a1-194">Hello PowerShell 유틸리티를 통해 Windows에서 인스턴스 메타 데이터를 검색할 수 있는 `curl`:</span><span class="sxs-lookup"><span data-stu-id="024a1-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="024a1-195">또는 hello 통해 `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="024a1-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="024a1-196">**응답**</span><span class="sxs-lookup"><span data-stu-id="024a1-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="024a1-197">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-197">hello response is a JSON string.</span></span> <span data-ttu-id="024a1-198">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-198">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="024a1-199">인스턴스 메타데이터 데이터 범주</span><span class="sxs-lookup"><span data-stu-id="024a1-199">Instance metadata data categories</span></span>
<span data-ttu-id="024a1-200">다음 데이터 범주 hello hello 인스턴스 메타 데이터 서비스를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="024a1-201">Data</span><span class="sxs-lookup"><span data-stu-id="024a1-201">Data</span></span> | <span data-ttu-id="024a1-202">설명</span><span class="sxs-lookup"><span data-stu-id="024a1-202">Description</span></span>
-----|------------
<span data-ttu-id="024a1-203">location</span><span class="sxs-lookup"><span data-stu-id="024a1-203">location</span></span> | <span data-ttu-id="024a1-204">Azure 지역 hello VM에서 실행 되</span><span class="sxs-lookup"><span data-stu-id="024a1-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="024a1-205">name</span><span class="sxs-lookup"><span data-stu-id="024a1-205">name</span></span> | <span data-ttu-id="024a1-206">Hello VM의 이름</span><span class="sxs-lookup"><span data-stu-id="024a1-206">Name of hello VM</span></span> 
<span data-ttu-id="024a1-207">offer</span><span class="sxs-lookup"><span data-stu-id="024a1-207">offer</span></span> | <span data-ttu-id="024a1-208">Hello VM 이미지에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-208">Offer information for hello VM image.</span></span> <span data-ttu-id="024a1-209">이 값은 Azure 이미지 갤러리에서 배포된 이미지에 대해서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="024a1-210">publisher</span><span class="sxs-lookup"><span data-stu-id="024a1-210">publisher</span></span> | <span data-ttu-id="024a1-211">Hello VM 이미지의 게시자</span><span class="sxs-lookup"><span data-stu-id="024a1-211">Publisher of hello VM image</span></span>
<span data-ttu-id="024a1-212">sku</span><span class="sxs-lookup"><span data-stu-id="024a1-212">sku</span></span> | <span data-ttu-id="024a1-213">Hello VM 이미지에 대 한 특정 SKU</span><span class="sxs-lookup"><span data-stu-id="024a1-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="024a1-214">버전</span><span class="sxs-lookup"><span data-stu-id="024a1-214">version</span></span> | <span data-ttu-id="024a1-215">Hello VM 이미지의 버전</span><span class="sxs-lookup"><span data-stu-id="024a1-215">Version of hello VM image</span></span> 
<span data-ttu-id="024a1-216">osType</span><span class="sxs-lookup"><span data-stu-id="024a1-216">osType</span></span> | <span data-ttu-id="024a1-217">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="024a1-217">Linux or Windows</span></span> 
<span data-ttu-id="024a1-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="024a1-218">platformUpdateDomain</span></span> |  <span data-ttu-id="024a1-219">[업데이트 도메인](virtual-machines-windows-manage-availability.md) hello VM에서 실행 되 고</span><span class="sxs-lookup"><span data-stu-id="024a1-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="024a1-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="024a1-220">platformFaultDomain</span></span> | <span data-ttu-id="024a1-221">[오류 도메인](virtual-machines-windows-manage-availability.md) hello VM에서 실행 되 고</span><span class="sxs-lookup"><span data-stu-id="024a1-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="024a1-222">vmId</span><span class="sxs-lookup"><span data-stu-id="024a1-222">vmId</span></span> | <span data-ttu-id="024a1-223">[고유 식별자](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) hello VM에 대 한</span><span class="sxs-lookup"><span data-stu-id="024a1-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="024a1-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="024a1-224">vmSize</span></span> | [<span data-ttu-id="024a1-225">VM 크기</span><span class="sxs-lookup"><span data-stu-id="024a1-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="024a1-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="024a1-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="024a1-227">Hello VM의 로컬 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="024a1-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="024a1-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="024a1-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="024a1-229">Hello VM의 공용 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="024a1-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="024a1-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="024a1-230">subnet/address</span></span> | <span data-ttu-id="024a1-231">Hello VM의 서브넷 주소</span><span class="sxs-lookup"><span data-stu-id="024a1-231">Subnet address of hello VM</span></span>
<span data-ttu-id="024a1-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="024a1-232">subnet/prefix</span></span> | <span data-ttu-id="024a1-233">서브넷 접두사, 예:24</span><span class="sxs-lookup"><span data-stu-id="024a1-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="024a1-234">ipv6/ipaddress</span><span class="sxs-lookup"><span data-stu-id="024a1-234">ipv6/ipAddress</span></span> | <span data-ttu-id="024a1-235">Hello VM의 로컬 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="024a1-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="024a1-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="024a1-236">macAddress</span></span> | <span data-ttu-id="024a1-237">VM MAC 주소</span><span class="sxs-lookup"><span data-stu-id="024a1-237">VM mac address</span></span> 
<span data-ttu-id="024a1-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="024a1-238">scheduledevents</span></span> | <span data-ttu-id="024a1-239">현재 공개 미리 보기 [scheduledevents](virtual-machines-scheduled-events.md) 참조</span><span class="sxs-lookup"><span data-stu-id="024a1-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="024a1-240">사용법을 위한 예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="024a1-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="024a1-241">Azure에서 실행 중인 VM 추적</span><span class="sxs-lookup"><span data-stu-id="024a1-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="024a1-242">서비스 공급자로 서 소프트웨어를 실행 중인 Vm tootrack hello 수 필요할 수 있습니다 또는 hello VM이 tootrack 고유 해야 하는 에이전트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="024a1-243">VM 사용 하 여 hello에 대 한 toobe 수 tooget 고유 ID `vmId` 인스턴스 메타 데이터 서비스에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="024a1-244">**요청**</span><span class="sxs-lookup"><span data-stu-id="024a1-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="024a1-245">**응답**</span><span class="sxs-lookup"><span data-stu-id="024a1-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="024a1-246">장애/업데이트 도메인 기반 컨테이너, 데이터 파티션 배치</span><span class="sxs-lookup"><span data-stu-id="024a1-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="024a1-247">특정 시나리오의 경우 다양한 데이터 복제본 배치가 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="024a1-248">예를 들어 [HDFS 복제본 배치](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) 또는 통해 컨테이너 위치는 [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) tooknow hello 필요할 수 있습니다 `platformFaultDomain` 및 `platformUpdateDomain` hello VM에서 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="024a1-249">Hello 인스턴스 메타 데이터 서비스를 통해 직접이 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="024a1-250">**요청**</span><span class="sxs-lookup"><span data-stu-id="024a1-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="024a1-251">**응답**</span><span class="sxs-lookup"><span data-stu-id="024a1-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="024a1-252">지원 사례 중 VM hello에 대 한 추가 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="024a1-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="024a1-253">서비스 공급자로 서 발생할 수 있습니다 지원 통화 넣을 tooknow hello VM에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="024a1-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="024a1-254">Hello 계산 메타 데이터 요청 hello 고객 tooshare Azure에서 VM의 hello 종류에 대 한 지원 전문가 tooknow hello에 대 한 기본 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="024a1-255">**요청**</span><span class="sxs-lookup"><span data-stu-id="024a1-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="024a1-256">**응답**</span><span class="sxs-lookup"><span data-stu-id="024a1-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="024a1-257">hello 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-257">hello response is a JSON string.</span></span> <span data-ttu-id="024a1-258">다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-258">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="024a1-259">Hello VM 내 서로 다른 언어를 사용 하 여 메타 데이터 서비스 호출의 예</span><span class="sxs-lookup"><span data-stu-id="024a1-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="024a1-260">언어</span><span class="sxs-lookup"><span data-stu-id="024a1-260">Language</span></span> | <span data-ttu-id="024a1-261">예제</span><span class="sxs-lookup"><span data-stu-id="024a1-261">Example</span></span> 
---------|----------------
<span data-ttu-id="024a1-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="024a1-262">Ruby</span></span>     | <span data-ttu-id="024a1-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="024a1-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="024a1-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="024a1-264">Go Lan</span></span>   | <span data-ttu-id="024a1-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="024a1-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="024a1-266">python</span><span class="sxs-lookup"><span data-stu-id="024a1-266">python</span></span>   | <span data-ttu-id="024a1-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="024a1-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="024a1-268">C++</span><span class="sxs-lookup"><span data-stu-id="024a1-268">C++</span></span>      | <span data-ttu-id="024a1-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="024a1-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="024a1-270">C#</span><span class="sxs-lookup"><span data-stu-id="024a1-270">C#</span></span>       | <span data-ttu-id="024a1-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="024a1-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="024a1-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="024a1-272">Javascript</span></span> | <span data-ttu-id="024a1-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="024a1-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="024a1-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="024a1-274">Powershell</span></span> | <span data-ttu-id="024a1-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="024a1-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="024a1-276">Bash</span><span class="sxs-lookup"><span data-stu-id="024a1-276">Bash</span></span>       | <span data-ttu-id="024a1-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="024a1-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="024a1-278">FAQ</span><span class="sxs-lookup"><span data-stu-id="024a1-278">FAQ</span></span>
1. <span data-ttu-id="024a1-279">Hello 오류가 발생 `400 Bad Request, Required metadata header not specified`합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="024a1-280">무슨 의미인가요?</span><span class="sxs-lookup"><span data-stu-id="024a1-280">What does this mean?</span></span>
   * <span data-ttu-id="024a1-281">hello 헤더를 요구 하는 hello 인스턴스 메타 데이터 서비스 `Metadata: true` toobe hello 요청에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="024a1-282">Hello REST 호출에이 헤더를 전달 하면 액세스 toohello 인스턴스 메타 데이터 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="024a1-283">VM에 대한 계산 정보를 구할 수 없는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="024a1-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="024a1-284">현재 hello 인스턴스 메타 데이터 서비스는 Azure 리소스 관리자와 함께 만든 인스턴스에 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="024a1-285">Hello 이후,에서는 클라우드 서비스 Vm에 대 한 지원을 추가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="024a1-286">잠시 전에 Azure Resource Manager를 통해 내 가상 컴퓨터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="024a1-287">계산 메타데이터 정보가 왜 표시되지 않나요?</span><span class="sxs-lookup"><span data-stu-id="024a1-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="024a1-288">2016 년 9 월 이후 만들어진 모든 Vm을 추가 하는 [태그](../azure-resource-manager/resource-group-using-tags.md) toostart 보는 계산 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="024a1-289">이전 Vm (2016 년 9 월 이전에 만든)을 위한 추가/제거 확장 또는 데이터 디스크 toohello VM toorefresh 메타 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="024a1-290">이유는 무엇입니까 hello 오류 `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="024a1-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="024a1-291">지수 백오프 시스템을 기반으로 요청을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="024a1-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="024a1-292">Hello 문제가 계속 되 면 Azure 지원을 담당자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="024a1-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="024a1-293">추가 질문/의견은 어디에 공유하나요?</span><span class="sxs-lookup"><span data-stu-id="024a1-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="024a1-294">의견은 http://feedback.azure.com에서 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="024a1-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="024a1-295">가상 컴퓨터 확장 집합 인스턴스에 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="024a1-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="024a1-296">예, 메타데이터 서비스는 확장 집합 인스턴스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="024a1-297">Hello 서비스에 대 한 지원 받기</span><span class="sxs-lookup"><span data-stu-id="024a1-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="024a1-298">hello 서비스에 대 한 tooget 지원 hello 없는 수 tooget 메타 데이터 응답 긴 다시 시도한 후 VM에 대 한 Azure 포털에서 지원 문제를 만들려면</span><span class="sxs-lookup"><span data-stu-id="024a1-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![인스턴스 메타데이터 지원](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="024a1-300">다음 단계</span><span class="sxs-lookup"><span data-stu-id="024a1-300">Next Steps</span></span>

- <span data-ttu-id="024a1-301">Hello에 대 한 자세한 [scheduledevents](virtual-machines-scheduled-events.md) API **에서 공개 미리 보기** hello 인스턴스 메타 데이터 서비스에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="024a1-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
