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
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a><span data-ttu-id="97a3c-103">미사용 Azure Cosmos DB 데이터베이스 암호화</span><span class="sxs-lookup"><span data-stu-id="97a3c-103">Azure Cosmos DB database encryption at rest</span></span>

<span data-ttu-id="97a3c-104">미사용 데이터 암호화 (Ssd)의 반도체 드라이브와 같은 비휘발성 저장소 장치에 있는 데이터의 암호화 toohello 일반적으로 참조 하는 구문 및 하드 디스크 드라이브 (Hdd) 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-104">Encryption at rest is a phrase that commonly refers toohello encryption of data on nonvolatile storage devices, such as solid state drives (SSDs) and hard disk drives (HDDs).</span></span> <span data-ttu-id="97a3c-105">Cosmos DB는 해당 주 데이터베이스를 SSD에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-105">Cosmos DB stores its primary databases on SSDs.</span></span> <span data-ttu-id="97a3c-106">해당 미디어 첨부 파일 및 백업은 일반적으로 HDD로 백업되는 Azure Blob Storage에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-106">Its media attachments and backups are stored in Azure Blob storage, which is generally backed up by HDDs.</span></span> <span data-ttu-id="97a3c-107">Cosmos DB에 대 한 미사용 데이터 암호화의 hello 릴리스로 모든 데이터베이스, 미디어 첨부 파일 및 백업 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-107">With hello release of encryption at rest for Cosmos DB, all your databases, media attachments, and backups are encrypted.</span></span> <span data-ttu-id="97a3c-108">데이터 (네트워크를 통해 hello) 전송에 암호화 되며 이제 미사용 (비휘발성 저장소) 제공 종단 간 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-108">Your data is now encrypted in transit (over hello network) and at rest (nonvolatile storage), giving you end-to-end encryption.</span></span>

<span data-ttu-id="97a3c-109">As DB Cosmos PaaS 서비스는 매우 쉽게 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-109">As a PaaS service, Cosmos DB is very easy toouse.</span></span> <span data-ttu-id="97a3c-110">Cosmos DB에 저장 된 모든 사용자 데이터 전송에서 휴지 암호화 되며, 필요는 없습니다 tootake 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-110">Because all user data stored in Cosmos DB is encrypted at rest and in transport, you don't have tootake any action.</span></span> <span data-ttu-id="97a3c-111">암호화에는 이것이 또 다른 방법은 tooput rest는 기본적으로 "on"입니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-111">Another way tooput this is that encryption at rest is "on" by default.</span></span> <span data-ttu-id="97a3c-112">없는 컨트롤 tooturn는 설정 또는 해제 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-112">There are no controls tooturn it off or on.</span></span> <span data-ttu-id="97a3c-113">Toomeet를 계속 실행 하는 동안이 기능을 제공 했습니다 우리의 [가용성 및 성능 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db)합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-113">We provide this feature while we continue toomeet our [availability and performance SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db).</span></span>

## <a name="implement-encryption-at-rest"></a><span data-ttu-id="97a3c-114">미사용 암호화 구현</span><span class="sxs-lookup"><span data-stu-id="97a3c-114">Implement encryption at rest</span></span>

<span data-ttu-id="97a3c-115">미사용 암호화는 보안 키 저장소 시스템, 암호화된 네트워크 및 암호화 API를 비롯한 수많은 보안 기술을 사용하여 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-115">Encryption at rest is implemented by using a number of security technologies, including secure key storage systems, encrypted networks, and cryptographic APIs.</span></span> <span data-ttu-id="97a3c-116">암호를 해독 하 고 데이터를 처리 하는 시스템에는 키를 관리 하는 시스템과 toocommunicate가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-116">Systems that decrypt and process data have toocommunicate with systems that manage keys.</span></span> <span data-ttu-id="97a3c-117">hello 다이어그램 저장소 키의 암호화 된 데이터 및 hello 관리 어떻게 분리 되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-117">hello diagram shows how storage of encrypted data and hello management of keys is separated.</span></span> 

![디자인 다이어그램](./media/database-encryption-at-rest/design-diagram.png)

<span data-ttu-id="97a3c-119">사용자 요청 hello 기본 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-119">hello basic flow of a user request is as follows:</span></span>
- <span data-ttu-id="97a3c-120">hello 사용자 데이터베이스 계정이 준비 되 면 만들어지고 저장소 키 요청 toohello 관리 서비스 리소스 공급자를 통해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-120">hello user database account is made ready, and storage keys are retrieved via a request toohello Management Service Resource Provider.</span></span>
- <span data-ttu-id="97a3c-121">사용자는 HTTPS/secure 전송을 통해 연결 tooCosmos DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-121">A user creates a connection tooCosmos DB via HTTPS/secure transport.</span></span> <span data-ttu-id="97a3c-122">(hello Sdk 추상 hello 정보)입니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-122">(hello SDKs abstract hello details.)</span></span>
- <span data-ttu-id="97a3c-123">hello 사용자가 이전에 만든 보안 연결 hello를 통해 저장 된 JSON 문서 toobe를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-123">hello user sends a JSON document toobe stored over hello previously created secure connection.</span></span>
- <span data-ttu-id="97a3c-124">hello JSON 문서는 hello 사용자가을 인덱싱을 해제 하지 않는 한 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-124">hello JSON document is indexed unless hello user has turned off indexing.</span></span>
- <span data-ttu-id="97a3c-125">JSON 문서 hello 및 인덱스 데이터를 모두 toosecure 저장소에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-125">Both hello JSON document and index data are written toosecure storage.</span></span>
- <span data-ttu-id="97a3c-126">정기적으로 데이터 hello 보안 저장소에서 읽기 및 toohello Azure 암호화 된 Blob 저장소를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-126">Periodically, data is read from hello secure storage and backed up toohello Azure Encrypted Blob Store.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="97a3c-127">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="97a3c-127">Frequently asked questions</span></span>

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a><span data-ttu-id="97a3c-128">Q: 저장소 서비스 암호화를 사용하는 경우 Azure Storage 비용은 얼마나 늘어나나요?</span><span class="sxs-lookup"><span data-stu-id="97a3c-128">Q: How much more does Azure Storage cost if Storage Service Encryption is enabled?</span></span>
<span data-ttu-id="97a3c-129">A: 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-129">A: There is no additional cost.</span></span>

### <a name="q-who-manages-hello-encryption-keys"></a><span data-ttu-id="97a3c-130">Q: 누구 hello 암호화 키를 관리?</span><span class="sxs-lookup"><span data-stu-id="97a3c-130">Q: Who manages hello encryption keys?</span></span>
<span data-ttu-id="97a3c-131">A: hello 키 Microsoft에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-131">A: hello keys are managed by Microsoft.</span></span>

### <a name="q-how-often-are-encryption-keys-rotated"></a><span data-ttu-id="97a3c-132">Q: 얼마나 자주 암호화 키가 순환되나요?</span><span class="sxs-lookup"><span data-stu-id="97a3c-132">Q: How often are encryption keys rotated?</span></span>
<span data-ttu-id="97a3c-133">A: Microsoft에는 Cosmos DB가 따르는 암호화 키 회전에 대한 일련의 내부 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-133">A: Microsoft has a set of internal guidelines for encryption key rotation, which Cosmos DB follows.</span></span> <span data-ttu-id="97a3c-134">hello 지침이 게시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-134">hello specific guidelines are not published.</span></span> <span data-ttu-id="97a3c-135">Microsoft는 hello 게시 [수명 주기 SDL (Security Development)](https://www.microsoft.com/sdl/default.aspx), 내부 지침의 하위 집합으로 간주 되 고 개발자를 위한 유용한 모범 사례에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-135">Microsoft does publish hello [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), which is seen as a subset of internal guidance and has useful best practices for developers.</span></span>

### <a name="q-can-i-use-my-own-encryption-keys"></a><span data-ttu-id="97a3c-136">Q: 나만의 암호화 키를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="97a3c-136">Q: Can I use my own encryption keys?</span></span>
<span data-ttu-id="97a3c-137">A: cosmos DB PaaS 서비스 이며 하드 tookeep hello 서비스 쉽게 toouse 했습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-137">A: Cosmos DB is a PaaS service, and we worked hard tookeep hello service easy toouse.</span></span> <span data-ttu-id="97a3c-138">이 질문이 PCI-DSS와 같은 규정 준수 요구 사항을 충족시키기 위한 프록시 질문으로 자주 제기되는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-138">We've noticed this question is often asked as a proxy question for meeting a compliance requirement like PCI-DSS.</span></span> <span data-ttu-id="97a3c-139">이 기능을 작성 과정의 일부로 Cosmos DB를 사용 하는 고객 hello 필요 toomanage 키 자체 없이 해당 요구 사항을 충족 하는지 준수 감사자 tooensure 들과 협력 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-139">As part of building this feature, we worked with compliance auditors tooensure that customers who use Cosmos DB meet their requirements without hello need toomanage keys themselves.</span></span>
<span data-ttu-id="97a3c-140">결과적으로, 현재 제공 하지 않습니다 사용자 hello 옵션 tooburden 자체 키 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-140">As a result, we currently do not offer users hello option tooburden themselves with key management.</span></span>

### <a name="q-what-regions-have-encryption-turned-on"></a><span data-ttu-id="97a3c-141">Q: 암호화가 설정된 지역은 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="97a3c-141">Q: What regions have encryption turned on?</span></span>
<span data-ttu-id="97a3c-142">A: 모든 Azure Cosmos DB 지역에서 모든 사용자 데이터에 대해 암호화가 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-142">A: All Azure Cosmos DB regions have encryption turned on for all user data.</span></span>

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a><span data-ttu-id="97a3c-143">Q: 암호화 영향은 hello 성능 대기 시간 및 처리량 Sla?</span><span class="sxs-lookup"><span data-stu-id="97a3c-143">Q: Does encryption affect hello performance latency and throughput SLAs?</span></span>
<span data-ttu-id="97a3c-144">A: 경우 영향이 나 변경을 toohello 성능 Sla 미사용 데이터 암호화는 모든 기존 및 새 계정에 대해 사용 하도록 설정 했으므로</span><span class="sxs-lookup"><span data-stu-id="97a3c-144">A: There is no impact or changes toohello performance SLAs now that encryption at rest is enabled for all existing and new accounts.</span></span> <span data-ttu-id="97a3c-145">자세한 내용은 hello에 [Cosmos DB에 대 한 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) 페이지 toosee hello 최신 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-145">You can read more on hello [SLA for Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) page toosee hello latest guarantees.</span></span>

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a><span data-ttu-id="97a3c-146">Q: hello 로컬 에뮬레이터 미사용 데이터 암호화를 지원 합니까?</span><span class="sxs-lookup"><span data-stu-id="97a3c-146">Q: Does hello local emulator support encryption at rest?</span></span>
<span data-ttu-id="97a3c-147">A: hello 에뮬레이터는 독립 실행형 개발/테스트 도구와 관리 되는 Cosmos DB 서비스 사용 하 여 hello hello 키 관리 서비스를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-147">A: hello emulator is a standalone dev/test tool and does not use hello key management services that hello managed Cosmos DB service uses.</span></span> <span data-ttu-id="97a3c-148">중요 한 에뮬레이터 테스트 데이터를 저장 하는 드라이브에 BitLocker tooenable 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-148">Our recommendation is tooenable BitLocker on drives where you are storing sensitive emulator test data.</span></span> <span data-ttu-id="97a3c-149">hello [에뮬레이터의 hello 기본 데이터 디렉터리를 변경 지원](local-emulator.md) 잘 알려진 위치를 사용 하 여 뿐만 아니라 합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-149">hello [emulator supports changing hello default data directory](local-emulator.md) as well as using a well-known location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97a3c-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97a3c-150">Next steps</span></span>

<span data-ttu-id="97a3c-151">Cosmos DB 보안과 hello 최신 향상 기능 개요를 참조 하십시오. [Azure Cosmos DB 데이터베이스 보안](database-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-151">For an overview of Cosmos DB security and hello latest improvements, see [Azure Cosmos DB database security](database-security.md).</span></span>
<span data-ttu-id="97a3c-152">Microsoft 인증에 대 한 자세한 내용은 참조 hello [Azure 보안 센터](https://azure.microsoft.com/en-us/support/trust-center/)합니다.</span><span class="sxs-lookup"><span data-stu-id="97a3c-152">For more information about Microsoft certifications, see hello [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).</span></span>
