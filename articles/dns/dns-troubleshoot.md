---
title: "aaaAzure DNS 문제 해결 가이드 | Microsoft Docs"
description: "Azure dns tootroubleshoot 공통 발급 하는 방법"
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
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="bcdf0-103">Azure DNS 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="bcdf0-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="bcdf0-104">이 페이지에서는 일반적인 Azure DNS 질문에 대한 문제 해결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="bcdf0-105">이 단계에서 문제를 해결하지 못하는 경우 [MSDN의 커뮤니티 지원 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork)에서 검색하거나 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="bcdf0-106">또는 Azure 지원 요청을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="bcdf0-107">DNS 영역을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-107">I can't create a DNS zone</span></span>

<span data-ttu-id="bcdf0-108">tooresolve 일반적인 문제는 hello 다음 단계 중 하나 이상을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="bcdf0-109">Azure DNS 감사 검토 hello toodetermine hello 실패 이유를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="bcdf0-110">각 DNS 영역 이름은 해당 리소스 그룹 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="bcdf0-111">즉, 두 개의 DNS 영역의 hello로 동일한 이름은 리소스 그룹을 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="bcdf0-112">다른 영역 이름을 사용하거나 다른 리소스 그룹을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="bcdf0-113">"에 도달 했거나 hello {구독 id}를 구독에서 영역의 최대 수를 초과 했습니다." 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="bcdf0-114">다른 Azure 구독을 사용, 일부 영역을 삭제 또는 구독 제한 tooraise Azure 지원에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="bcdf0-115">오류가 표시 될 수 있습니다 "hello 영역 '{영역 name}'를 사용할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="bcdf0-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="bcdf0-116">이 오류는 Azure DNS이 DNS 영역에 대 한 이름 서버 수 없습니다 tooallocate 했음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="bcdf0-117">다른 영역 이름을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-117">Try using a different zone name.</span></span> <span data-ttu-id="bcdf0-118">또는 hello 도메인 이름 소유자 인 사용자에 대 한 이름 서버를 할당할 수 있는 Azure 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="bcdf0-119">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="bcdf0-119">**Recommended documents**</span></span>

<span data-ttu-id="bcdf0-120">[DNS 영역 및 레코드](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="bcdf0-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="bcdf0-121">
[DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bcdf0-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="bcdf0-122">DNS 레코드를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-122">I can't create a DNS record</span></span>

<span data-ttu-id="bcdf0-123">tooresolve 일반적인 문제는 hello 다음 단계 중 하나 이상을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="bcdf0-124">Azure DNS 감사 검토 hello toodetermine hello 실패 이유를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="bcdf0-125">레코드 집합 hello가 이미 존재 합니까?</span><span class="sxs-lookup"><span data-stu-id="bcdf0-125">Does hello record set exist already?</span></span>  <span data-ttu-id="bcdf0-126">Azure DNS 레코드를 사용 하 여 레코드를 관리 합니다. *설정*, 레코드의 이름을 지정 하 고 동일한 hello 동일 hello hello 컬렉션은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="bcdf0-127">경우에 동일한 이름을 지정 하 고 이미 입력 hello로 레코드가 없는 tooadd hello 기존 레코드를 편집 해야 하는 이러한 다른 레코드로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="bcdf0-128">발생 하는 것 toocreate hello DNS 영역 루트 (hello '루트' hello 영역)에 있는 레코드?</span><span class="sxs-lookup"><span data-stu-id="bcdf0-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="bcdf0-129">따라서 DNS 규칙 hello는 toouse hello 경우 ' @' 문자 hello 레코드 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="bcdf0-130">또한 hello DNS 표준 hello 영역 루트에서 CNAME 레코드를 허용 하지 않는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="bcdf0-131">CNAME 충돌이 있나요?</span><span class="sxs-lookup"><span data-stu-id="bcdf0-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="bcdf0-132">hello DNS 표준 이름과 같은 다른 종류의 레코드로 이름을 hello로 CNAME 레코드를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="bcdf0-133">다른 종류의 이름과 동일한 이름을 실패 hello로 레코드를 만들어 기존는 CNAME을 사용할 경우 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="bcdf0-134">마찬가지로, CNAME를 만들면 실패 hello 이름이 다른 종류의 기존 레코드와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="bcdf0-135">다른 레코드 또는 다른 레코드 이름 선택 hello를 제거 하 여 hello 충돌을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="bcdf0-136">DNS 영역에 사용할 수 있는 레코드 집합의 hello 수 hello 제한에 도달 했습니다. hello 현재 레코드 집합 수 고 hello 레코드 집합의 최대 수에에서 표시 됩니다 hello hello '속성' hello 영역에 대 한 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="bcdf0-137">이 제한에 도달 했으므로, 다음 일부 레코드 집합을 삭제 하거나이 영역에 대 한 레코드 집합 제한 tooraise Azure 지원에 문의 하는 경우 다음 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="bcdf0-138">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="bcdf0-138">**Recommended documents**</span></span>

<span data-ttu-id="bcdf0-139">[DNS 영역 및 레코드](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="bcdf0-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="bcdf0-140">
[DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bcdf0-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="bcdf0-141">DNS 레코드를 확인할 수 없음</span><span class="sxs-lookup"><span data-stu-id="bcdf0-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="bcdf0-142">DNS 이름 확인은 여러 가지 이유로 실패할 수 있는 다단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="bcdf0-143">hello 다음 단계 쉽게 Azure DNS에 호스트 되는 영역에서 DNS 레코드에 대 한 DNS 확인이 실패 하는 이유를 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="bcdf0-144">Hello DNS 레코드가 Azure DNS에서 올바르게 구성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="bcdf0-145">Hello hello 영역 이름, 레코드 이름 및 레코드 종류 정확한 지 확인 하는 Azure 포털의에서 hello DNS 레코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="bcdf0-146">Hello Azure DNS 이름 서버 hello DNS 레코드가 올바르게 해결 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="bcdf0-147">로컬 PC에서 DNS 쿼리를 만들면 hello hello 이름 서버의 현재 상태를 반영 하지 않는 캐시 된 결과 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="bcdf0-148">회사 네트워크 DNS 프록시 서버를 자주 사용 되는 또한 toospecific 이름 서버 연결에서 DNS 쿼리를 방지 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="bcdf0-149">tooavoid 이러한 문제를 사용 하 여 웹 기반 이름 확인 서비스와 같은 [digwebinterface](http://digwebinterface.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="bcdf0-150">Hello Azure 포털에에서 표시 된 대로 있는지 toospecify 프로그램 DNS 영역에 대 한 올바른 이름 서버 hello를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="bcdf0-151">Hello DNS가 (toospecify hello 정규화 된 이름, hello 영역 이름을 포함 하 여 있어야) 정확한 hello 레코드 종류 올바른지 확인</span><span class="sxs-lookup"><span data-stu-id="bcdf0-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="bcdf0-152">Hello DNS 도메인 이름을 올바르게 되었으면 확인 [toohello Azure DNS 이름 서버 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="bcdf0-153">[DNS 위임 유효성 검사를 제공하는 여러 타사 웹 사이트](https://www.bing.com/search?q=dns+check+tool)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="bcdf0-154">이 테스트 되는 *영역* 위임 테스트 hello DNS 영역 이름 및 hello 정규화 레코드 이름이 아니라만 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="bcdf0-155">위의 hello 마치면 DNS 레코드 이제 해결 해야 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="bcdf0-156">tooverify, 다시 사용할 수 있습니다 [digwebinterface](http://digwebinterface.com),이 이번에 hello 기본 이름 서버 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="bcdf0-157">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="bcdf0-157">**Recommended documents**</span></span>

[<span data-ttu-id="bcdf0-158">도메인 tooAzure DNS 위임</span><span class="sxs-lookup"><span data-stu-id="bcdf0-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="bcdf0-159">Hello 'service' 및 ' p' SRV 레코드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bcdf0-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="bcdf0-160">Azure DNS 레코드 집합으로 DNS 레코드를 관리 합니다.-동일한 이름을 지정 하 고 동일한 hello hello로 레코드의 컬렉션을 hello 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="bcdf0-161">SRV 레코드 집합에 대 한 hello 'service' 및 'p' toobe hello 레코드 집합 이름의 일부로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="bcdf0-162">hello 다른 SRV 매개 변수 (예: 'priority', 'weight', 'port' 및 'target')은 별도로 지정 되며 hello 레코드 집합의 각 레코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="bcdf0-163">SRV 레코드 이름(서비스 이름 'sip', 프로토콜 'tcp') 예제:</span><span class="sxs-lookup"><span data-stu-id="bcdf0-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="bcdf0-164">\_sip 합니다. \_tcp (hello 영역 루트에서 설정 하는 레코드를 만듭니다)</span><span class="sxs-lookup"><span data-stu-id="bcdf0-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="bcdf0-165">\_sip.\_tcp.sipservice ('sipservice'라는 이름의 레코드 생성)</span><span class="sxs-lookup"><span data-stu-id="bcdf0-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="bcdf0-166">**권장되는 문서**</span><span class="sxs-lookup"><span data-stu-id="bcdf0-166">**Recommended documents**</span></span>

<span data-ttu-id="bcdf0-167">[DNS 영역 및 레코드](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="bcdf0-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="bcdf0-168">
[Hello Azure 포털을 사용 하 여 DNS 레코드 집합 및 레코드를 만들으십시오](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="bcdf0-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="bcdf0-169">
[SRV 레코드 유형(Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="bcdf0-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="bcdf0-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcdf0-170">Next steps</span></span>

* <span data-ttu-id="bcdf0-171">[Azure DNS 영역 및 레코드](dns-zones-records.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="bcdf0-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="bcdf0-172">Azure DNS를 사용 하 여 toostart 너무 방법을 알아봅니다[DNS 영역을 만드는](dns-getstarted-create-dnszone-portal.md) 및 [DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="bcdf0-173">toomigrate 기존 DNS 영역을 알아보려면 어떻게 너무[DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcdf0-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

