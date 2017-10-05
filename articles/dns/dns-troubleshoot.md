---
title: "Azure DNS 문제 해결 가이드 | Microsoft Docs"
description: "Azure DNS와 관련된 일반적인 문제를 해결하는 방법"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="80f21-103">Azure DNS 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="80f21-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="80f21-104">이 페이지에서는 일반적인 Azure DNS 질문에 대한 문제 해결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="80f21-105">이 단계에서 문제를 해결하지 못하는 경우 [MSDN의 커뮤니티 지원 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork)에서 검색하거나 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="80f21-106">또는 Azure 지원 요청을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="80f21-107">DNS 영역을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-107">I can't create a DNS zone</span></span>

<span data-ttu-id="80f21-108">일반적인 문제를 해결하려면 다음 단계 중 하나 이상을 수행해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="80f21-109">Azure DNS 감사 로그를 검토하여 실패 이유를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="80f21-110">각 DNS 영역 이름은 해당 리소스 그룹 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="80f21-111">즉, 이름이 같은 두 개의 DNS 영역이 리소스 그룹을 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="80f21-112">다른 영역 이름을 사용하거나 다른 리소스 그룹을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="80f21-113">"{subscription id} 구독에서 영역의 최대 수에 도달했거나 최대 수를 초과했습니다."라는 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="80f21-114">다른 Azure 구독을 사용하거나 일부 영역을 삭제하세요. 아니면 Azure 지원부에 문의하여 구독 제한을 높이세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="80f21-115">"영역 '{zone name}'을(를) 사용할 수 없습니다."라는 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="80f21-116">이 오류는 Azure DNS가 이 DNS 영역에 대해 이름 서버를 할당할 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="80f21-117">다른 영역 이름을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-117">Try using a different zone name.</span></span> <span data-ttu-id="80f21-118">또는 도메인 이름 소유자인 경우에는 Azure 지원에 문의하세요. Azure 지원에서 이름 서버를 대신 할당해 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="80f21-119">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="80f21-119">**Recommended documents**</span></span>

<span data-ttu-id="80f21-120">[DNS 영역 및 레코드](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="80f21-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="80f21-121">
[DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="80f21-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="80f21-122">DNS 레코드를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-122">I can't create a DNS record</span></span>

<span data-ttu-id="80f21-123">일반적인 문제를 해결하려면 다음 단계 중 하나 이상을 수행해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="80f21-124">Azure DNS 감사 로그를 검토하여 실패 이유를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="80f21-125">레코드 집합이 이미 있습니까?</span><span class="sxs-lookup"><span data-stu-id="80f21-125">Does the record set exist already?</span></span>  <span data-ttu-id="80f21-126">Azure DNS는 레코드 *집합*, 다시 말해서 이름과 유형이 같은 레코드 컬렉션을 사용하여 레코드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="80f21-127">이름과 유형이 같은 레코드가 이미 있는 상태에서 같은 레코드를 추가하려면 기존 레코드 집합을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="80f21-128">DNS 영역 루트(영역의 '루트')에서 레코드를 만들려고 하시나요?</span><span class="sxs-lookup"><span data-stu-id="80f21-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="80f21-129">그렇다면 레코드 이름으로 ‘@’ 문자를 사용하는 것이 DNS 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="80f21-130">또한 DNS 표준은 영역 루트에 CNAME 레코드를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="80f21-131">CNAME 충돌이 있나요?</span><span class="sxs-lookup"><span data-stu-id="80f21-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="80f21-132">DNS 표준은 다른 유형의 레코드와 이름이 같은 CNAME 레코드를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="80f21-133">기존 CNAME이 있으면 다른 유형의 레코드와 이름이 같은 레코드를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="80f21-134">마찬가지로 유형이 다른 기존 레코드와 이름이 일치하면 CNAME을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="80f21-135">다른 레코드를 제거하거나 다른 레코드 이름을 선택하여 충돌을 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="80f21-136">DNS 영역에서 허용되는 레코드 집합 수 제한에 도달했나요?</span><span class="sxs-lookup"><span data-stu-id="80f21-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="80f21-137">현재 레코드 집합 수와 최대 레코드 집합 수는 Azure Portal에서 해당 영역의 '속성'에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="80f21-138">이 제한에 도달했으면 일부 레코드 집합을 삭제하거나 Azure 지원에 문의하여 이 영역의 레코드 집합 제한을 높인 후 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="80f21-139">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="80f21-139">**Recommended documents**</span></span>

<span data-ttu-id="80f21-140">[DNS 영역 및 레코드](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="80f21-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="80f21-141">
[DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="80f21-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="80f21-142">DNS 레코드를 확인할 수 없음</span><span class="sxs-lookup"><span data-stu-id="80f21-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="80f21-143">DNS 이름 확인은 여러 가지 이유로 실패할 수 있는 다단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="80f21-144">다음 단계를 따르면 Azure DNS에 호스트된 영역의 DNS 레코드에 대한 DNS 확인이 실패하는 이유를 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="80f21-145">Azure DNS에서 DNS 레코드가 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="80f21-146">Azure Portal에서 DNS 레코드를 검토하여 영역 이름, 레코드 이름 및 레코드 유형이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="80f21-147">Azure DNS 이름 서버에서 DNS 레코드가 올바르게 확인되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="80f21-148">로컬 PC에서 DNS 쿼리를 작성할 수 있다면 이름 서버의 현재 상태를 반영하지 않는 캐시된 결과가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="80f21-149">또한 회사 네트워크는 종종 DNS 프록시 서버를 사용하는데, 이 서버는 DNS 쿼리를 특정 이름 서버로 보내지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="80f21-150">이러한 문제를 방지하려면 [digwebinterface](http://digwebinterface.com) 같은 웹 기반 이름 확인 서비스를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="80f21-151">Azure Portal에 표시된 대로 DNS 영역의 올바른 이름 서버를 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="80f21-152">DNS 이름이 올바른지(영역 이름을 포함하여 정규화된 이름을 지정해야 함), 또 레코드 유형이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="80f21-153">DNS 도메인 이름이 [Azure DNS 이름 서버에 올바르게 위임되었는지](dns-domain-delegation.md) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="80f21-154">[DNS 위임 유효성 검사를 제공하는 여러 타사 웹 사이트](https://www.bing.com/search?q=dns+check+tool)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="80f21-155">이 테스트는 *영역* 위임 테스트이므로 정규화된 레코드 이름이 아닌 DNS 영역 이름만 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="80f21-156">위의 단계를 완료하면 DNS 레코드가 올바르게 확인될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="80f21-157">[digwebinterface](http://digwebinterface.com)를 사용하여 문제가 해결되었는지 확인할 수 있습니다. 이번에는 기본 이름 서버 설정을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="80f21-158">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="80f21-158">**Recommended documents**</span></span>

[<span data-ttu-id="80f21-159">Azure DNS에 도메인 위임</span><span class="sxs-lookup"><span data-stu-id="80f21-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="80f21-160">SRV 레코드에 대한 ‘서비스’ 및 ‘프로토콜’을 지정하려면 어떻게 해냐 하나요?</span><span class="sxs-lookup"><span data-stu-id="80f21-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="80f21-161">Azure DNS는 DNS 레코드를 레코드 집합, 다시 말해서 이름과 유형이 같은 레코드 컬렉션으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="80f21-162">SRV 레코드 집합의 경우 레코드 집합 이름에 포함하여 '서비스'와 '프로토콜'을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="80f21-163">기타 SRV 매개 변수('우선 순위', '가중치', '포트', '대상')는 레코드 집합의 각 레코드에 대해 별도로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="80f21-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="80f21-164">SRV 레코드 이름(서비스 이름 'sip', 프로토콜 'tcp') 예제:</span><span class="sxs-lookup"><span data-stu-id="80f21-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="80f21-165">\_sip.\_tcp (영역 루트에 레코드 생성)</span><span class="sxs-lookup"><span data-stu-id="80f21-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="80f21-166">\_sip.\_tcp.sipservice ('sipservice'라는 이름의 레코드 생성)</span><span class="sxs-lookup"><span data-stu-id="80f21-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="80f21-167">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="80f21-167">**Recommended documents**</span></span>

<span data-ttu-id="80f21-168">[DNS 영역 및 레코드](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="80f21-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="80f21-169">
[Azure Portal을 사용하여 DNS 레코드 집합 및 레코드 만들기](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="80f21-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="80f21-170">
[SRV 레코드 유형(Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="80f21-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="80f21-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80f21-171">Next steps</span></span>

* <span data-ttu-id="80f21-172">[Azure DNS 영역 및 레코드](dns-zones-records.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="80f21-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="80f21-173">Azure DNS 사용을 시작하려면 [DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md) 및 [DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="80f21-174">기존 DNS 영역을 마이그레이션하려면 [DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="80f21-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

