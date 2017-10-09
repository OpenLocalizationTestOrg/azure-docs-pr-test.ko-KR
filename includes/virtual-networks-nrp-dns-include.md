## <a name="azure-dns"></a><span data-ttu-id="13ffd-101">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="13ffd-101">Azure DNS</span></span>
<span data-ttu-id="13ffd-102">Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="13ffd-103">속성</span><span class="sxs-lookup"><span data-stu-id="13ffd-103">Property</span></span> | <span data-ttu-id="13ffd-104">설명</span><span class="sxs-lookup"><span data-stu-id="13ffd-104">Description</span></span> | <span data-ttu-id="13ffd-105">샘플 값</span><span class="sxs-lookup"><span data-stu-id="13ffd-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13ffd-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="13ffd-106">**DNSzones**</span></span> |<span data-ttu-id="13ffd-107">특정 도메인의 도메인 영역 정보 toohost DNS 레코드</span><span class="sxs-lookup"><span data-stu-id="13ffd-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="13ffd-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="13ffd-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="13ffd-109">DNS 레코드 집합</span><span class="sxs-lookup"><span data-stu-id="13ffd-109">DNS record sets</span></span>
<span data-ttu-id="13ffd-110">DNS 영역에는 레코드 집합이라고 하는 자식 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="13ffd-111">레코드 집합은 DNS 영역에 대한 유형별 호스트 레코드 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="13ffd-112">레코드 유형은 A, AAAA, CNAME, MX, NS, SOA, SRV 및 TXT입니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="13ffd-113">속성</span><span class="sxs-lookup"><span data-stu-id="13ffd-113">Property</span></span> | <span data-ttu-id="13ffd-114">설명</span><span class="sxs-lookup"><span data-stu-id="13ffd-114">Description</span></span> | <span data-ttu-id="13ffd-115">샘플 값</span><span class="sxs-lookup"><span data-stu-id="13ffd-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13ffd-116">문자열(UTF-8 형식) 또는</span><span class="sxs-lookup"><span data-stu-id="13ffd-116">A</span></span> |<span data-ttu-id="13ffd-117">IPv4 레코드 유형</span><span class="sxs-lookup"><span data-stu-id="13ffd-117">IPv4 record type</span></span> |<span data-ttu-id="13ffd-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="13ffd-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="13ffd-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="13ffd-119">AAAA</span></span> |<span data-ttu-id="13ffd-120">IPv6 레코드 유형</span><span class="sxs-lookup"><span data-stu-id="13ffd-120">IPv6 record type</span></span> |<span data-ttu-id="13ffd-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="13ffd-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="13ffd-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="13ffd-122">CNAME</span></span> |<span data-ttu-id="13ffd-123">Canonical 이름 레코드 유형 <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="13ffd-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="13ffd-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="13ffd-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="13ffd-125">MX</span><span class="sxs-lookup"><span data-stu-id="13ffd-125">MX</span></span> |<span data-ttu-id="13ffd-126">메일 레코드 유형</span><span class="sxs-lookup"><span data-stu-id="13ffd-126">mail record type</span></span> |<span data-ttu-id="13ffd-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="13ffd-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="13ffd-128">NS</span><span class="sxs-lookup"><span data-stu-id="13ffd-128">NS</span></span> |<span data-ttu-id="13ffd-129">이름 서버 레코드 유형</span><span class="sxs-lookup"><span data-stu-id="13ffd-129">name server record type</span></span> |<span data-ttu-id="13ffd-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="13ffd-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="13ffd-131">SOA</span><span class="sxs-lookup"><span data-stu-id="13ffd-131">SOA</span></span> |<span data-ttu-id="13ffd-132">권한 시작 레코드 종류 <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="13ffd-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="13ffd-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="13ffd-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="13ffd-134">SRV</span><span class="sxs-lookup"><span data-stu-id="13ffd-134">SRV</span></span> |<span data-ttu-id="13ffd-135">서비스 레코드 유형 </span><span class="sxs-lookup"><span data-stu-id="13ffd-135">service record type</span></span> |<span data-ttu-id="13ffd-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="13ffd-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="13ffd-137"><sup>1</sup> 레코드 집합당 하나의 값만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="13ffd-138"><sup>2</sup> DNS 영역당 하나의 레코드 종류 SOA만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="13ffd-139">Json 형식의 DNS 영역 샘플:</span><span class="sxs-lookup"><span data-stu-id="13ffd-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="13ffd-140">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="13ffd-140">Additional resources</span></span>
<span data-ttu-id="13ffd-141">읽기 hello [DNS 영역에 대 한 REST API 설명서 ](https://msdn.microsoft.com/library/azure/mt130626.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="13ffd-142">읽기 hello [DNS 레코드 집합에 대 한 REST API 설명서](https://msdn.microsoft.com/library/azure/mt130627.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ffd-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

