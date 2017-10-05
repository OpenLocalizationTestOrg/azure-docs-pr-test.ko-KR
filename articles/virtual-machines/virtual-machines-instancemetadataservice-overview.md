---
title: "Azure 인스턴스 메타데이터 서비스 개요 | Microsoft Docs"
description: "VM의 계산, 네트워크 및 예정된 유지 관리 이벤트에 대한 정보를 가져오는 RESTful 인터페이스입니다."
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
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="31778-103">Azure Instance Metadata Service</span><span class="sxs-lookup"><span data-stu-id="31778-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="31778-104">Azure Instance Metadata Service는 가상 컴퓨터를 관리 및 구성하는 데 사용할 수 있는 가상 컴퓨터 인스턴스를 실행하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="31778-105">여기에는 SKU, 네트워크 구성, 예정된 유지 관리 이벤트 등의 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="31778-106">사용 가능한 정보 유형에 대한 자세한 내용은 [메타데이터 범주](#instance-metadata-data-categories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31778-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="31778-107">Azure의 Instance Metadata Service는 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)를 통해 생성된 모든 IaaS VM에 액세스할 수 있는 REST 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="31778-108">이 끝점은 VM 내부에서만 액세스할 수 있는 잘 알려진 라우팅이 불가능한 IP 주소(`169.254.169.254`) 에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="31778-109">중요 정보</span><span class="sxs-lookup"><span data-stu-id="31778-109">Important information</span></span>

<span data-ttu-id="31778-110">이 서비스는 글로벌 Azure 지역에서 **일반 공급**됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="31778-111">정부, 중국 및 독일어 Azure 클라우드에 대한 공개 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="31778-112">정기적으로 업데이트를 받아 가상 컴퓨터 인스턴스에 대한 새 정보를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-112">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="31778-113">이 페이지에는 사용 가능한 최신 [데이터 범주](#instance-metadata-data-categories)가 반영되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-113">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="31778-114">서비스 가용성</span><span class="sxs-lookup"><span data-stu-id="31778-114">Service Availability</span></span>
<span data-ttu-id="31778-115">이 서비스는 일반 공급되는 모든 글로벌 Azure 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-115">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="31778-116">정부, 중국 또는 독일 지역에 대한 공개 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-116">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="31778-117">영역</span><span class="sxs-lookup"><span data-stu-id="31778-117">Regions</span></span>                                        | <span data-ttu-id="31778-118">가용성</span><span class="sxs-lookup"><span data-stu-id="31778-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="31778-119">일반 공급되는 모든 글로벌 Azure 지역</span><span class="sxs-lookup"><span data-stu-id="31778-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="31778-120">일반 공급</span><span class="sxs-lookup"><span data-stu-id="31778-120">Generally Available</span></span> 
[<span data-ttu-id="31778-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="31778-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="31778-122">미리 보기</span><span class="sxs-lookup"><span data-stu-id="31778-122">In Preview</span></span> 
[<span data-ttu-id="31778-123">Azure 중국</span><span class="sxs-lookup"><span data-stu-id="31778-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="31778-124">미리 보기</span><span class="sxs-lookup"><span data-stu-id="31778-124">In Preview</span></span>
[<span data-ttu-id="31778-125">Azure 독일</span><span class="sxs-lookup"><span data-stu-id="31778-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="31778-126">미리 보기</span><span class="sxs-lookup"><span data-stu-id="31778-126">In Preview</span></span>

<span data-ttu-id="31778-127">이 표는 다른 Azure 클라우드에서 서비스를 사용할 수 있을 때 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-127">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="31778-128">Instance Metadata Service를 평가하려면 위 지역의 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) 또는 [Azure Portal](http://portal.azure.com)에서 VM을 만들고 아래 예제를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="31778-128">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="31778-129">사용</span><span class="sxs-lookup"><span data-stu-id="31778-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="31778-130">버전 관리</span><span class="sxs-lookup"><span data-stu-id="31778-130">Versioning</span></span>
<span data-ttu-id="31778-131">인스턴스 메타데이터 서비스에는 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-131">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="31778-132">버전은 필수이며 최신 버전은 `2017-04-02`입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-132">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="31778-133">예약된 이벤트의 이전 미리 보기 릴리스는 api-version으로 {최신 버전}을 지원했습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-133">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="31778-134">이 형식은 더 이상 지원되지 않으며 향후 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-134">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="31778-135">새로운 버전이 추가되더라도 스크립트가 특정 데이터 형식에 종속성이 있는 경우 이전 버전에 여전히 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="31778-136">그러나 현재 미리 보기 버전(2017-03-01)은 서비스가 일반 공급되면 사용하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-136">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="31778-137">헤더 사용</span><span class="sxs-lookup"><span data-stu-id="31778-137">Using Headers</span></span>
<span data-ttu-id="31778-138">Instance Metadata Service를 쿼리할 때 요청이 실수로 리디렉션되지 않도록 `Metadata: true` 헤더를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-138">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="31778-139">메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="31778-139">Retrieving metadata</span></span>

<span data-ttu-id="31778-140">인스턴스 메타데이터는 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)를 사용하여 생성/관리되는 VM을 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="31778-141">다음 요청을 사용하여 가상 컴퓨터 인스턴스의 모든 데이터 범주에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-141">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="31778-142">모든 인스턴스 메타데이터 쿼리는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="31778-143">데이터 출력</span><span class="sxs-lookup"><span data-stu-id="31778-143">Data output</span></span>
<span data-ttu-id="31778-144">기본적으로 Instance Metadata Service는 JSON 형식(`Content-Type: application/json`)의 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-144">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="31778-145">그러나 다른 API는 요청된 경우 다른 형식으로 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="31778-146">다음 표는 API에서 지원할 수 있는 다른 데이터 형식에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-146">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="31778-147">API</span><span class="sxs-lookup"><span data-stu-id="31778-147">API</span></span> | <span data-ttu-id="31778-148">기본 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="31778-148">Default Data Format</span></span> | <span data-ttu-id="31778-149">다른 형식</span><span class="sxs-lookup"><span data-stu-id="31778-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="31778-150">/instance</span><span class="sxs-lookup"><span data-stu-id="31778-150">/instance</span></span> | <span data-ttu-id="31778-151">json :</span><span class="sxs-lookup"><span data-stu-id="31778-151">json</span></span> | <span data-ttu-id="31778-152">텍스트</span><span class="sxs-lookup"><span data-stu-id="31778-152">text</span></span>
<span data-ttu-id="31778-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="31778-153">/scheduledevents</span></span> | <span data-ttu-id="31778-154">json :</span><span class="sxs-lookup"><span data-stu-id="31778-154">json</span></span> | <span data-ttu-id="31778-155">없음</span><span class="sxs-lookup"><span data-stu-id="31778-155">none</span></span>

<span data-ttu-id="31778-156">기본이 아닌 응답 형식에 액세스하려면 요청된 형식을 요청의 querystring 매개 변수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-156">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="31778-157">예:</span><span class="sxs-lookup"><span data-stu-id="31778-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="31778-158">보안</span><span class="sxs-lookup"><span data-stu-id="31778-158">Security</span></span>
<span data-ttu-id="31778-159">Instance Metadata Service 끝점은 라우팅이 불가능한 IP 주소에서 실행 중인 가상 컴퓨터 인스턴스 내부에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-159">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="31778-160">또한 `X-Forwarded-For` 헤더가 포함된 모든 요청은 서비스에 의해 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-160">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="31778-161">또한 실제 요청이 의도치 않은 리디렉션의 일환이 아니라 직접적으로 의도된 것이라는 것을 확인하기 위해 요청에 `Metadata: true` 헤더가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-161">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="31778-162">오류</span><span class="sxs-lookup"><span data-stu-id="31778-162">Error</span></span>
<span data-ttu-id="31778-163">찾을 수 없는 데이터 요소 또는 형식이 잘못된 요청이 있으면 Instance Metadata Service는 표준 HTTP 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-163">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="31778-164">예:</span><span class="sxs-lookup"><span data-stu-id="31778-164">For example:</span></span>

<span data-ttu-id="31778-165">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="31778-165">HTTP Status Code</span></span> | <span data-ttu-id="31778-166">이유</span><span class="sxs-lookup"><span data-stu-id="31778-166">Reason</span></span>
----------------|-------
<span data-ttu-id="31778-167">200 정상</span><span class="sxs-lookup"><span data-stu-id="31778-167">200 OK</span></span> |
<span data-ttu-id="31778-168">400 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="31778-168">400 Bad Request</span></span> | <span data-ttu-id="31778-169">누락된 `Metadata: true` 헤더</span><span class="sxs-lookup"><span data-stu-id="31778-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="31778-170">404 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="31778-170">404 Not Found</span></span> | <span data-ttu-id="31778-171">요청된 요소가 없음</span><span class="sxs-lookup"><span data-stu-id="31778-171">The requested element does't exist</span></span> 
<span data-ttu-id="31778-172">405 메서드를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="31778-172">405 Method Not Allowed</span></span> | <span data-ttu-id="31778-173">`GET` 및 `POST` 요청만 지원됨</span><span class="sxs-lookup"><span data-stu-id="31778-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="31778-174">429 요청이 너무 많음</span><span class="sxs-lookup"><span data-stu-id="31778-174">429 Too Many Requests</span></span> | <span data-ttu-id="31778-175">API는 현재 초당 최대 5개의 쿼리를 지원함</span><span class="sxs-lookup"><span data-stu-id="31778-175">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="31778-176">500 서비스 오류</span><span class="sxs-lookup"><span data-stu-id="31778-176">500 Service Error</span></span>     | <span data-ttu-id="31778-177">잠시 후 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="31778-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="31778-178">예</span><span class="sxs-lookup"><span data-stu-id="31778-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="31778-179">모든 API 응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-179">All API responses are JSON strings.</span></span> <span data-ttu-id="31778-180">다음 예제 응답은 모두 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="31778-181">네트워크 정보 검색</span><span class="sxs-lookup"><span data-stu-id="31778-181">Retrieving network information</span></span>

<span data-ttu-id="31778-182">**요청**</span><span class="sxs-lookup"><span data-stu-id="31778-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="31778-183">**응답**</span><span class="sxs-lookup"><span data-stu-id="31778-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="31778-184">응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-184">The response is a JSON string.</span></span> <span data-ttu-id="31778-185">다음 예제 응답은 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-185">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="31778-186">공용 IP 주소 검색</span><span class="sxs-lookup"><span data-stu-id="31778-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="31778-187">인스턴스에 대한 모든 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="31778-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="31778-188">**요청**</span><span class="sxs-lookup"><span data-stu-id="31778-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="31778-189">**응답**</span><span class="sxs-lookup"><span data-stu-id="31778-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="31778-190">응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-190">The response is a JSON string.</span></span> <span data-ttu-id="31778-191">다음 예제 응답은 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-191">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="31778-192">Windows 가상 컴퓨터에서 메타데이터 검색</span><span class="sxs-lookup"><span data-stu-id="31778-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="31778-193">**요청**</span><span class="sxs-lookup"><span data-stu-id="31778-193">**Request**</span></span>

<span data-ttu-id="31778-194">인스턴스 메타데이터는 Powershell 유틸리티 `curl`을 통해 Windows에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-194">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="31778-195">또는 `Invoke-RestMethod` cmdlet을 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-195">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="31778-196">**응답**</span><span class="sxs-lookup"><span data-stu-id="31778-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="31778-197">응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-197">The response is a JSON string.</span></span> <span data-ttu-id="31778-198">다음 예제 응답은 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-198">The following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="31778-199">인스턴스 메타데이터 데이터 범주</span><span class="sxs-lookup"><span data-stu-id="31778-199">Instance metadata data categories</span></span>
<span data-ttu-id="31778-200">다음 데이터 범주는 Instance Metadata Service를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-200">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="31778-201">Data</span><span class="sxs-lookup"><span data-stu-id="31778-201">Data</span></span> | <span data-ttu-id="31778-202">설명</span><span class="sxs-lookup"><span data-stu-id="31778-202">Description</span></span>
-----|------------
<span data-ttu-id="31778-203">location</span><span class="sxs-lookup"><span data-stu-id="31778-203">location</span></span> | <span data-ttu-id="31778-204">VM을 실행하는 Azure 지역</span><span class="sxs-lookup"><span data-stu-id="31778-204">Azure Region the VM is running in</span></span>
<span data-ttu-id="31778-205">name</span><span class="sxs-lookup"><span data-stu-id="31778-205">name</span></span> | <span data-ttu-id="31778-206">VM의 이름</span><span class="sxs-lookup"><span data-stu-id="31778-206">Name of the VM</span></span> 
<span data-ttu-id="31778-207">offer</span><span class="sxs-lookup"><span data-stu-id="31778-207">offer</span></span> | <span data-ttu-id="31778-208">VM 이미지에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-208">Offer information for the VM image.</span></span> <span data-ttu-id="31778-209">이 값은 Azure 이미지 갤러리에서 배포된 이미지에 대해서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="31778-210">publisher</span><span class="sxs-lookup"><span data-stu-id="31778-210">publisher</span></span> | <span data-ttu-id="31778-211">VM 이미지 게시자</span><span class="sxs-lookup"><span data-stu-id="31778-211">Publisher of the VM image</span></span>
<span data-ttu-id="31778-212">sku</span><span class="sxs-lookup"><span data-stu-id="31778-212">sku</span></span> | <span data-ttu-id="31778-213">VM 이미지에 해당하는 SKU</span><span class="sxs-lookup"><span data-stu-id="31778-213">Specific SKU for the VM image</span></span>  
<span data-ttu-id="31778-214">버전</span><span class="sxs-lookup"><span data-stu-id="31778-214">version</span></span> | <span data-ttu-id="31778-215">VM 이미지의 버전</span><span class="sxs-lookup"><span data-stu-id="31778-215">Version of the VM image</span></span> 
<span data-ttu-id="31778-216">osType</span><span class="sxs-lookup"><span data-stu-id="31778-216">osType</span></span> | <span data-ttu-id="31778-217">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="31778-217">Linux or Windows</span></span> 
<span data-ttu-id="31778-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="31778-218">platformUpdateDomain</span></span> |  <span data-ttu-id="31778-219">VM을 실행 중인 [업데이트 도메인](virtual-machines-windows-manage-availability.md)</span><span class="sxs-lookup"><span data-stu-id="31778-219">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="31778-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="31778-220">platformFaultDomain</span></span> | <span data-ttu-id="31778-221">VM을 실행 중인 [장애 도메인](virtual-machines-windows-manage-availability.md)</span><span class="sxs-lookup"><span data-stu-id="31778-221">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="31778-222">vmId</span><span class="sxs-lookup"><span data-stu-id="31778-222">vmId</span></span> | <span data-ttu-id="31778-223">VM의 [고유 식별자](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)</span><span class="sxs-lookup"><span data-stu-id="31778-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="31778-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="31778-224">vmSize</span></span> | [<span data-ttu-id="31778-225">VM 크기</span><span class="sxs-lookup"><span data-stu-id="31778-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="31778-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="31778-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="31778-227">VM의 로컬 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="31778-227">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="31778-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="31778-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="31778-229">VM의 공용 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="31778-229">Public IPv4 address of the VM</span></span>
<span data-ttu-id="31778-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="31778-230">subnet/address</span></span> | <span data-ttu-id="31778-231">VM의 서브넷 주소</span><span class="sxs-lookup"><span data-stu-id="31778-231">Subnet address of the VM</span></span>
<span data-ttu-id="31778-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="31778-232">subnet/prefix</span></span> | <span data-ttu-id="31778-233">서브넷 접두사, 예:24</span><span class="sxs-lookup"><span data-stu-id="31778-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="31778-234">ipv6/ipaddress</span><span class="sxs-lookup"><span data-stu-id="31778-234">ipv6/ipAddress</span></span> | <span data-ttu-id="31778-235">VM의 로컬 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="31778-235">Local IPv6 address of the VM</span></span>
<span data-ttu-id="31778-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="31778-236">macAddress</span></span> | <span data-ttu-id="31778-237">VM MAC 주소</span><span class="sxs-lookup"><span data-stu-id="31778-237">VM mac address</span></span> 
<span data-ttu-id="31778-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="31778-238">scheduledevents</span></span> | <span data-ttu-id="31778-239">현재 공개 미리 보기 [scheduledevents](virtual-machines-scheduled-events.md) 참조</span><span class="sxs-lookup"><span data-stu-id="31778-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="31778-240">사용법을 위한 예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="31778-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="31778-241">Azure에서 실행 중인 VM 추적</span><span class="sxs-lookup"><span data-stu-id="31778-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="31778-242">서비스 공급자는 소프트웨어를 실행 중인 VM의 수를 추적하거나 VM의 고유성을 추적해야 하는 에이전트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-242">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="31778-243">VM의 고유 ID를 가져오려면 Instance Metadata Service의 `vmId` 필드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-243">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="31778-244">**요청**</span><span class="sxs-lookup"><span data-stu-id="31778-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="31778-245">**응답**</span><span class="sxs-lookup"><span data-stu-id="31778-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="31778-246">장애/업데이트 도메인 기반 컨테이너, 데이터 파티션 배치</span><span class="sxs-lookup"><span data-stu-id="31778-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="31778-247">특정 시나리오의 경우 다양한 데이터 복제본 배치가 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="31778-248">예를 들어 [HDFS 복제본 배치](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) 또는 [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/)를 통한 컨테이너 배치를 위해서는 VM을 실행 중인 `platformFaultDomain` 및 `platformUpdateDomain`을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="31778-249">Instance Metadata Service를 통해 이 데이터를 직접 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-249">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="31778-250">**요청**</span><span class="sxs-lookup"><span data-stu-id="31778-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="31778-251">**응답**</span><span class="sxs-lookup"><span data-stu-id="31778-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="31778-252">지원 사례 중 VM에 대한 자세한 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="31778-252">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="31778-253">서비스 공급자는 지원 요청을 받을 수 있으며 이 때 VM에 대해 자세한 정보를 알아야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-253">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="31778-254">고객에게 계산 메타데이터를 공유하도록 요청하면 지원 전문가가 Azure에서 VM의 종류에 대해 알 수 있도록 기본 정보가 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-254">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="31778-255">**요청**</span><span class="sxs-lookup"><span data-stu-id="31778-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="31778-256">**응답**</span><span class="sxs-lookup"><span data-stu-id="31778-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="31778-257">응답은 JSON 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="31778-257">The response is a JSON string.</span></span> <span data-ttu-id="31778-258">다음 예제 응답은 가독성을 높이기 위해 적절히 인쇄되었습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-258">The following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="31778-259">VM 내의 서로 다른 언어를 사용하여 메타데이터 서비스를 호출하는 예</span><span class="sxs-lookup"><span data-stu-id="31778-259">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="31778-260">언어</span><span class="sxs-lookup"><span data-stu-id="31778-260">Language</span></span> | <span data-ttu-id="31778-261">예제</span><span class="sxs-lookup"><span data-stu-id="31778-261">Example</span></span> 
---------|----------------
<span data-ttu-id="31778-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="31778-262">Ruby</span></span>     | <span data-ttu-id="31778-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="31778-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="31778-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="31778-264">Go Lan</span></span>   | <span data-ttu-id="31778-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="31778-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="31778-266">python</span><span class="sxs-lookup"><span data-stu-id="31778-266">python</span></span>   | <span data-ttu-id="31778-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="31778-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="31778-268">C++</span><span class="sxs-lookup"><span data-stu-id="31778-268">C++</span></span>      | <span data-ttu-id="31778-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="31778-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="31778-270">C#</span><span class="sxs-lookup"><span data-stu-id="31778-270">C#</span></span>       | <span data-ttu-id="31778-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="31778-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="31778-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="31778-272">Javascript</span></span> | <span data-ttu-id="31778-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="31778-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="31778-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31778-274">Powershell</span></span> | <span data-ttu-id="31778-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="31778-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="31778-276">Bash</span><span class="sxs-lookup"><span data-stu-id="31778-276">Bash</span></span>       | <span data-ttu-id="31778-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="31778-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="31778-278">FAQ</span><span class="sxs-lookup"><span data-stu-id="31778-278">FAQ</span></span>
1. <span data-ttu-id="31778-279">`400 Bad Request, Required metadata header not specified` 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-279">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="31778-280">무슨 의미인가요?</span><span class="sxs-lookup"><span data-stu-id="31778-280">What does this mean?</span></span>
   * <span data-ttu-id="31778-281">Instance Metadata Service에서는 `Metadata: true` 헤더를 요청에 포함시켜 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-281">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="31778-282">REST 호출에서 이 헤더를 전달하면 Instance Metadata Service에 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="31778-282">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="31778-283">VM에 대한 계산 정보를 구할 수 없는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="31778-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="31778-284">현재 Instance Metadata Service는 Azure Resource Manager를 사용하여 만든 인스턴스만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31778-284">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="31778-285">나중에 Cloud Service VM에 대한 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-285">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="31778-286">잠시 전에 Azure Resource Manager를 통해 내 가상 컴퓨터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="31778-287">계산 메타데이터 정보가 왜 표시되지 않나요?</span><span class="sxs-lookup"><span data-stu-id="31778-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="31778-288">2016년 9월 이후에 생성된 VM의 경우 계산 메타데이터를 표시하려면 [태그](../azure-resource-manager/resource-group-using-tags.md)를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="31778-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="31778-289">이전 VM(2016년 9월 전에 생성된)의 경우 메타데이터를 새로 고치도록 VM에 확장 또는 데이터 디스크를 추가/제거하세요.</span><span class="sxs-lookup"><span data-stu-id="31778-289">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="31778-290">`500 Internal Server Error` 오류가 발생하는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="31778-290">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="31778-291">지수 백오프 시스템을 기반으로 요청을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="31778-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="31778-292">문제가 지속되면 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="31778-292">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="31778-293">추가 질문/의견은 어디에 공유하나요?</span><span class="sxs-lookup"><span data-stu-id="31778-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="31778-294">의견은 http://feedback.azure.com에서 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="31778-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="31778-295">가상 컴퓨터 확장 집합 인스턴스에 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="31778-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="31778-296">예, 메타데이터 서비스는 확장 집합 인스턴스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31778-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="31778-297">서비스에 대한 지원을 받으려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="31778-297">How do I get support for the service?</span></span>
   * <span data-ttu-id="31778-298">서비스에 대한 지원을 받으려면 Azure Portal에서 긴 다시 시도 후 메타데이터 받을 수 없는 VM에 대한 지원 문제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31778-298">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![인스턴스 메타데이터 지원](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="31778-300">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31778-300">Next Steps</span></span>

- <span data-ttu-id="31778-301">Instance Metadata Service에서 **공개 미리 보기**로 제공되는 [scheduledevents](virtual-machines-scheduled-events.md) API에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31778-301">Learn more about the [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by the Instance Metadata Service.</span></span>
