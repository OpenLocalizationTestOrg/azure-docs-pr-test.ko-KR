---
title: "미사용 데이터베이스 암호화 - Azure Cosmos DB | Microsoft Docs"
description: "Azure Cosmos DB가 모든 데이터의 기본 암호화를 제공하는 방법을 알아봅니다."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d8967d4504a8ccabb444c7f3d5635e2d00f287c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a><span data-ttu-id="b2b78-103">미사용 Azure Cosmos DB 데이터베이스 암호화</span><span class="sxs-lookup"><span data-stu-id="b2b78-103">Azure Cosmos DB database encryption at rest</span></span>

<span data-ttu-id="b2b78-104">미사용 암호화는 일반적으로 반도체 드라이브(SSD) 및 하드 디스크(HDD)와 같은 비휘발성 저장소 장치에서 데이터를 암호화하는 것을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-104">Encryption at rest is a phrase that commonly refers to the encryption of data on nonvolatile storage devices, such as solid state drives (SSDs) and hard disk drives (HDDs).</span></span> <span data-ttu-id="b2b78-105">Cosmos DB는 해당 주 데이터베이스를 SSD에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-105">Cosmos DB stores its primary databases on SSDs.</span></span> <span data-ttu-id="b2b78-106">해당 미디어 첨부 파일 및 백업은 일반적으로 HDD로 백업되는 Azure Blob Storage에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-106">Its media attachments and backups are stored in Azure Blob storage, which is generally backed up by HDDs.</span></span> <span data-ttu-id="b2b78-107">Cosmos DB에 대한 미사용 암호화가 릴리스됨에 따라 모든 데이터베이스, 미디어 첨부 파일 및 백업이 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-107">With the release of encryption at rest for Cosmos DB, all your databases, media attachments, and backups are encrypted.</span></span> <span data-ttu-id="b2b78-108">이제 데이터는 전송 중(네트워크를 통해)과 미사용 시(비휘발성 저장소) 암호화되므로 종단 간 암호화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-108">Your data is now encrypted in transit (over the network) and at rest (nonvolatile storage), giving you end-to-end encryption.</span></span>

<span data-ttu-id="b2b78-109">PaaS 서비스인 Cosmos DB는 사용하기가 매우 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-109">As a PaaS service, Cosmos DB is very easy to use.</span></span> <span data-ttu-id="b2b78-110">Cosmos DB에 저장된 모든 사용자 데이터는 미사용 및 전송 시 암호화되기 때문에 어떤 조치도 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-110">Because all user data stored in Cosmos DB is encrypted at rest and in transport, you don't have to take any action.</span></span> <span data-ttu-id="b2b78-111">또한 미사용 암호화가 기본적으로 "설정" 상태라는 것도 이러한 노력 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-111">Another way to put this is that encryption at rest is "on" by default.</span></span> <span data-ttu-id="b2b78-112">설정하거나 해제하는 데 사용되는 컨트롤이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-112">There are no controls to turn it off or on.</span></span> <span data-ttu-id="b2b78-113">Microsoft는 [가용성 및 성능 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db)를 지속적으로 충족하면서 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-113">We provide this feature while we continue to meet our [availability and performance SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db).</span></span>

## <a name="implement-encryption-at-rest"></a><span data-ttu-id="b2b78-114">미사용 암호화 구현</span><span class="sxs-lookup"><span data-stu-id="b2b78-114">Implement encryption at rest</span></span>

<span data-ttu-id="b2b78-115">미사용 암호화는 보안 키 저장소 시스템, 암호화된 네트워크 및 암호화 API를 비롯한 수많은 보안 기술을 사용하여 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-115">Encryption at rest is implemented by using a number of security technologies, including secure key storage systems, encrypted networks, and cryptographic APIs.</span></span> <span data-ttu-id="b2b78-116">데이터를 암호 해독하고 처리하는 시스템은 키를 관리하는 시스템과 통신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-116">Systems that decrypt and process data have to communicate with systems that manage keys.</span></span> <span data-ttu-id="b2b78-117">다이어그램에서는 암호화된 데이터의 저장소와 키 관리가 어떻게 구분되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-117">The diagram shows how storage of encrypted data and the management of keys is separated.</span></span> 

![디자인 다이어그램](./media/database-encryption-at-rest/design-diagram.png)

<span data-ttu-id="b2b78-119">사용자 요청의 기본 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-119">The basic flow of a user request is as follows:</span></span>
- <span data-ttu-id="b2b78-120">사용자 데이터베이스 계정은 이미 준비되어 있고 저장소 키는 관리 서비스 리소스 공급자에 대한 요청을 통해 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-120">The user database account is made ready, and storage keys are retrieved via a request to the Management Service Resource Provider.</span></span>
- <span data-ttu-id="b2b78-121">사용자는 HTTPS/보안 전송을 통해 Cosmos DB에 대한 연결을</span><span class="sxs-lookup"><span data-stu-id="b2b78-121">A user creates a connection to Cosmos DB via HTTPS/secure transport.</span></span> <span data-ttu-id="b2b78-122">만듭니다(SDK가 세부 정보를 추상화함).</span><span class="sxs-lookup"><span data-stu-id="b2b78-122">(The SDKs abstract the details.)</span></span>
- <span data-ttu-id="b2b78-123">사용자는 이전에 만든 보안 연결을 통해 저장할 JSON 문서를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-123">The user sends a JSON document to be stored over the previously created secure connection.</span></span>
- <span data-ttu-id="b2b78-124">JSON 문서는 사용자가 인덱싱을 해제하지 않는다면, 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-124">The JSON document is indexed unless the user has turned off indexing.</span></span>
- <span data-ttu-id="b2b78-125">JSON 문서와 인덱스 데이터 모두 보안 저장소에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-125">Both the JSON document and index data are written to secure storage.</span></span>
- <span data-ttu-id="b2b78-126">데이터는 보안 저장소에서 주기적으로 읽어오고 Azure Encrypted Blob Store에 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-126">Periodically, data is read from the secure storage and backed up to the Azure Encrypted Blob Store.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b2b78-127">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="b2b78-127">Frequently asked questions</span></span>

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a><span data-ttu-id="b2b78-128">Q: 저장소 서비스 암호화를 사용하는 경우 Azure Storage 비용은 얼마나 늘어나나요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-128">Q: How much more does Azure Storage cost if Storage Service Encryption is enabled?</span></span>
<span data-ttu-id="b2b78-129">A: 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-129">A: There is no additional cost.</span></span>

### <a name="q-who-manages-the-encryption-keys"></a><span data-ttu-id="b2b78-130">Q: 암호화 키는 누가 관리하나요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-130">Q: Who manages the encryption keys?</span></span>
<span data-ttu-id="b2b78-131">A: 키는 Microsoft에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-131">A: The keys are managed by Microsoft.</span></span>

### <a name="q-how-often-are-encryption-keys-rotated"></a><span data-ttu-id="b2b78-132">Q: 얼마나 자주 암호화 키가 순환되나요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-132">Q: How often are encryption keys rotated?</span></span>
<span data-ttu-id="b2b78-133">A: Microsoft에는 Cosmos DB가 따르는 암호화 키 회전에 대한 일련의 내부 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-133">A: Microsoft has a set of internal guidelines for encryption key rotation, which Cosmos DB follows.</span></span> <span data-ttu-id="b2b78-134">특정 지침은 게시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-134">The specific guidelines are not published.</span></span> <span data-ttu-id="b2b78-135">Microsoft는 내부 지침의 하위 집합으로 간주되고 개발자를 위한 유용한 모범 사례가 있는 [SDL(Security Development Lifecycle)](https://www.microsoft.com/sdl/default.aspx)을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-135">Microsoft does publish the [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), which is seen as a subset of internal guidance and has useful best practices for developers.</span></span>

### <a name="q-can-i-use-my-own-encryption-keys"></a><span data-ttu-id="b2b78-136">Q: 나만의 암호화 키를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-136">Q: Can I use my own encryption keys?</span></span>
<span data-ttu-id="b2b78-137">A: Cosmos DB는 PaaS 서비스로, Microsoft는 서비스의 사용 용이성을 높이기 위해 열심히 노력해 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-137">A: Cosmos DB is a PaaS service, and we worked hard to keep the service easy to use.</span></span> <span data-ttu-id="b2b78-138">이 질문이 PCI-DSS와 같은 규정 준수 요구 사항을 충족시키기 위한 프록시 질문으로 자주 제기되는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-138">We've noticed this question is often asked as a proxy question for meeting a compliance requirement like PCI-DSS.</span></span> <span data-ttu-id="b2b78-139">이 기능을 구축하는 과정에서 준수 감사자와 협력하여 Cosmos DB를 사용하는 고객이 키를 직접 관리할 필요 없이 요구 사항을 충족할 수 있도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-139">As part of building this feature, we worked with compliance auditors to ensure that customers who use Cosmos DB meet their requirements without the need to manage keys themselves.</span></span>
<span data-ttu-id="b2b78-140">따라서 현재 사용자에게 직접 키를 관리하는 부담을 주는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-140">As a result, we currently do not offer users the option to burden themselves with key management.</span></span>

### <a name="q-what-regions-have-encryption-turned-on"></a><span data-ttu-id="b2b78-141">Q: 암호화가 설정된 지역은 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-141">Q: What regions have encryption turned on?</span></span>
<span data-ttu-id="b2b78-142">A: 모든 Azure Cosmos DB 지역에서 모든 사용자 데이터에 대해 암호화가 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-142">A: All Azure Cosmos DB regions have encryption turned on for all user data.</span></span>

### <a name="q-does-encryption-affect-the-performance-latency-and-throughput-slas"></a><span data-ttu-id="b2b78-143">Q: 암호화는 성능 대기 시간 및 처리량 SLA에 영향을 주나요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-143">Q: Does encryption affect the performance latency and throughput SLAs?</span></span>
<span data-ttu-id="b2b78-144">A: 이제 기존의 모든 계정과 새 계정에 대해 미사용 암호화가 사용되므로 성능 SLA에 대한 영향이나 변경 내용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-144">A: There is no impact or changes to the performance SLAs now that encryption at rest is enabled for all existing and new accounts.</span></span> <span data-ttu-id="b2b78-145">최신 보장 내용을 보려면 [Cosmos DB에 대한 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2b78-145">You can read more on the [SLA for Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) page to see the latest guarantees.</span></span>

### <a name="q-does-the-local-emulator-support-encryption-at-rest"></a><span data-ttu-id="b2b78-146">Q: 로컬 에뮬레이터가 미사용 암호화를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="b2b78-146">Q: Does the local emulator support encryption at rest?</span></span>
<span data-ttu-id="b2b78-147">A: 에뮬레이터는 독립 실행형 개발/테스트 도구이며 관리되는 Cosmos DB 서비스에서 사용되는 키 관리 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-147">A: The emulator is a standalone dev/test tool and does not use the key management services that the managed Cosmos DB service uses.</span></span> <span data-ttu-id="b2b78-148">중요한 에뮬레이터 테스트 데이터를 저장할 드라이브에서 BitLocker를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-148">Our recommendation is to enable BitLocker on drives where you are storing sensitive emulator test data.</span></span> <span data-ttu-id="b2b78-149">[에뮬레이터는 기본 데이터 디렉터리 변경을 지원](local-emulator.md)할 뿐만 아니라 잘 알려진 위치 사용을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b78-149">The [emulator supports changing the default data directory](local-emulator.md) as well as using a well-known location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2b78-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2b78-150">Next steps</span></span>

<span data-ttu-id="b2b78-151">Cosmos DB 보안 및 최신 개선 사항에 대한 개요는 [Azure Cosmos DB 데이터베이스 보안](database-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2b78-151">For an overview of Cosmos DB security and the latest improvements, see [Azure Cosmos DB database security](database-security.md).</span></span>
<span data-ttu-id="b2b78-152">Microsoft 인증에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/en-us/support/trust-center/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2b78-152">For more information about Microsoft certifications, see the [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).</span></span>
