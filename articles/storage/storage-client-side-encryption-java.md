---
title: "Microsoft Azure 저장소에 대 한 Java와 함께 aaaClient 쪽 암호화 | Microsoft Docs"
description: "hello Java 용 Azure 저장소 클라이언트 라이브러리는 Azure 저장소 응용 프로그램에 대 한 보안을 최대화 하기 위해 클라이언트 쪽 암호화 및 Azure 키 자격 증명 모음 통합을 지원합니다."
services: storage
documentationcenter: java
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 3df49907-554c-404a-9b0c-b3e3269ad04f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 60a928e8737e64a8bec97dbc9f423537bd9afe88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-with-java-for-microsoft-azure-storage"></a><span data-ttu-id="32851-103">Microsoft Azure Storage용 Java를 사용하는 클라이언트 쪽 암호화 및 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="32851-103">Client-Side Encryption and Azure Key Vault with Java for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="32851-104">개요</span><span class="sxs-lookup"><span data-stu-id="32851-104">Overview</span></span>
<span data-ttu-id="32851-105">hello [Java 용 Azure 저장소 클라이언트 라이브러리](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) tooAzure 저장소에 업로드 하 고 toohello 클라이언트를 다운로드 하는 동안 데이터를 해독 하기 전에 클라이언트 응용 프로그램 내에서 데이터를 암호화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-105">hello [Azure Storage Client Library for Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="32851-106">hello 라이브러리와의 통합에서는 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 저장소 계정 키 관리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-106">hello library also supports integration with [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) for storage account key management.</span></span>

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a><span data-ttu-id="32851-107">암호화 및 암호 해독 hello 봉투 (envelope) 기술을 통해</span><span class="sxs-lookup"><span data-stu-id="32851-107">Encryption and decryption via hello envelope technique</span></span>
<span data-ttu-id="32851-108">암호화 및 암호 해독의 hello 프로세스 hello 봉투 (envelope) 기법을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="32851-108">hello processes of encryption and decryption follow hello envelope technique.</span></span>  

### <a name="encryption-via-hello-envelope-technique"></a><span data-ttu-id="32851-109">Hello 봉투 (envelope) 기술을 통해 암호화</span><span class="sxs-lookup"><span data-stu-id="32851-109">Encryption via hello envelope technique</span></span>
<span data-ttu-id="32851-110">Hello 봉투 (envelope) 기술을 통해 암호화 hello 방식으로 다음에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-110">Encryption via hello envelope technique works in hello following way:</span></span>  

1. <span data-ttu-id="32851-111">hello Azure 저장소 클라이언트 라이브러리는 콘텐츠 암호화 키 (CEK)는 한 번 사용 대칭 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-111">hello Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>  
2. <span data-ttu-id="32851-112">사용자 데이터는 이 CEK를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-112">User data is encrypted using this CEK.</span></span>   
3. <span data-ttu-id="32851-113">hello CEK 다음 래핑된 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화) 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-113">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="32851-114">hello KEK 키 식별자로 식별 되 및 수 비대칭 키 쌍 또는 대칭 키 및 수 수 로컬로 관리 하거나 Azure 키 자격 증명 모음에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-114">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vaults.</span></span>  
   <span data-ttu-id="32851-115">자체 hello 저장소 클라이언트 라이브러리에 대 한 액세스 tooKEK에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-115">hello storage client library itself never has access tooKEK.</span></span> <span data-ttu-id="32851-116">hello 라이브러리 주요 자격 증명 모음에서 제공 하는 hello 키 래핑 알고리즘을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-116">hello library invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="32851-117">사용자에 대 한 키 래핑/원하는 경우 사용자 지정 공급자 toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-117">Users can choose toouse custom providers for key wrapping/unwrapping if desired.</span></span>  
4. <span data-ttu-id="32851-118">hello 암호화 된 데이터는 다음 toohello Azure 저장소 서비스에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-118">hello encrypted data is then uploaded toohello Azure Storage service.</span></span> <span data-ttu-id="32851-119">몇 가지 추가 암호화 메타 데이터와 함께 hello 래핑된 키 (blob)에 메타 데이터로 저장 또는 보간 hello 암호화 된 데이터 (메시지 큐 및 테이블 엔터티)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-119">hello wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with hello encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-hello-envelope-technique"></a><span data-ttu-id="32851-120">Hello 봉투 (envelope) 기술을 통해 암호 해독</span><span class="sxs-lookup"><span data-stu-id="32851-120">Decryption via hello envelope technique</span></span>
<span data-ttu-id="32851-121">Hello 봉투 (envelope) 기술을 통해 암호 해독 hello 방식으로 다음에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-121">Decryption via hello envelope technique works in hello following way:</span></span>  

1. <span data-ttu-id="32851-122">hello 클라이언트 라이브러리는 hello 사용자 관리 하는 hello 키 암호화 키 (KEK) 로컬로 또는 Azure 키 자격 증명 모음에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-122">hello client library assumes that hello user is managing hello key encryption key (KEK) either locally or in Azure Key Vaults.</span></span> <span data-ttu-id="32851-123">hello 사용자 암호화에 사용 된 tooknow hello 특정 키가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-123">hello user does not need tooknow hello specific key that was used for encryption.</span></span> <span data-ttu-id="32851-124">대신, 서로 다른 키 식별자 tookeys 확인 되는 키 확인자 수를 설정 하 고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-124">Instead, a key resolver which resolves different key identifiers tookeys can be set up and used.</span></span>  
2. <span data-ttu-id="32851-125">hello 클라이언트 라이브러리는 hello 서비스에 저장 된 모든 암호화 자료 함께 hello 암호화 된 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-125">hello client library downloads hello encrypted data along with any encryption material that is stored on hello service.</span></span>  
3. <span data-ttu-id="32851-126">키 암호화 키 (KEK) hello 래핑되지 않은 (암호 해독 된)를 사용 하 여 hello 래핑된 콘텐츠 암호화 키 (CEK)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-126">hello wrapped content encryption key (CEK) is then unwrapped (decrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="32851-127">여기서 다시 hello 클라이언트 라이브러리 않아도 액세스 tooKEK 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-127">Here again, hello client library does not have access tooKEK.</span></span> <span data-ttu-id="32851-128">사용자 지정 hello 또는 키 자격 증명 모음 공급자의 래핑 해제 알고리즘을 호출 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-128">It simply invokes hello custom or Key Vault provider's unwrapping algorithm.</span></span>  
4. <span data-ttu-id="32851-129">hello 암호화 키 (CEK)는 다음 콘텐츠 toodecrypt hello 암호화 된 사용자 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-129">hello content encryption key (CEK) is then used toodecrypt hello encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="32851-130">암호화 메커니즘</span><span class="sxs-lookup"><span data-stu-id="32851-130">Encryption Mechanism</span></span>
<span data-ttu-id="32851-131">hello 저장소 클라이언트 라이브러리를 사용 하 여 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 주문 tooencrypt 사용자 데이터에서입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-131">hello storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order tooencrypt user data.</span></span> <span data-ttu-id="32851-132">특히, AES를 이용한 [CBC(암호화 블록 체인)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="32851-133">각 서비스는 하는 일이 각각 다르므로 여기서 이것들을 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="32851-134">Blob</span><span class="sxs-lookup"><span data-stu-id="32851-134">Blobs</span></span>
<span data-ttu-id="32851-135">hello 클라이언트 라이브러리는 현재 전체 blob만 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-135">hello client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="32851-136">사용자가 hello를 사용할 때 암호화가 지원 특히 **업로드*** 메서드나 hello **openOutputStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="32851-136">Specifically, encryption is supported when users use hello **upload*** methods or hello **openOutputStream** method.</span></span> <span data-ttu-id="32851-137">다운로드는 전체 및 범위 다운로드가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-137">For downloads, both complete and range downloads are supported.</span></span>  

<span data-ttu-id="32851-138">암호화 하는 동안 hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector) 32 바이트는 임의의 콘텐츠 암호화 키 (CEK)와 함께 16 바이트의 생성 되며이 정보를 사용 하 여 hello blob 데이터의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-138">During encryption, hello client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of hello blob data using this information.</span></span> <span data-ttu-id="32851-139">hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 함께 hello hello 서비스에 암호화 된 blob 메타 데이터를 blob으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-139">hello wrapped CEK and some additional encryption metadata are then stored as blob metadata along with hello encrypted blob on hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="32851-140">편집 하거나 hello blob에 대 한 사용자 고유의 메타 데이터를 업로드 하는 경우 tooensure이 메타이 데이터는 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-140">If you are editing or uploading your own metadata for hello blob, you need tooensure that this metadata is preserved.</span></span> <span data-ttu-id="32851-141">이 메타 데이터 없이 새 메타 데이터를 업로드 하는 경우 래핑된 CEK hello, IV 및 기타 메타 데이터는 손실 됩니다 및 hello blob 콘텐츠를 절대로 다시 검색할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-141">If you upload new metadata without this metadata, hello wrapped CEK, IV and other metadata will be lost and hello blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="32851-142">Hello를 사용 하 여 hello 전체 blob의 hello 콘텐츠를 검색에서는 암호화 된 blob 다운로드  **다운로드*/openInputStream** 편의 메서드.</span><span class="sxs-lookup"><span data-stu-id="32851-142">Downloading an encrypted blob involves retrieving hello content of hello entire blob using hello **download*/openInputStream** convenience methods.</span></span> <span data-ttu-id="32851-143">래핑된 CEK 래핑이 해제 하 고 hello IV와 함께 사용 하는 hello (으로 저장 blob 메타 데이터가 예제의) tooreturn hello 암호 해독 데이터 toohello 사용자.</span><span class="sxs-lookup"><span data-stu-id="32851-143">hello wrapped CEK is unwrapped and used together with hello IV (stored as blob metadata in this case) tooreturn hello decrypted data toohello users.</span></span>

<span data-ttu-id="32851-144">임의의 범위를 다운로드 (**downloadRange*** 메서드) hello에서 암호화 된 blob의 순서 tooget 사용자가 적은 양의 toosuccessfully 사용된 될 수 있는 추가 데이터의 암호를 해독 hello 제공 hello 범위를 조정 하려면 요청 된 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-144">Downloading an arbitrary range (**downloadRange*** methods) in hello encrypted blob involves adjusting hello range provided by users in order tooget a small amount of additional data that can be used toosuccessfully decrypt hello requested range.</span></span>  

<span data-ttu-id="32851-145">이 스키마를 사용하여 모든 blob 유형(블록 blob, 페이지 blob 및 추가 blob)을 암호화/암호 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-145">All blob types (block blobs, page blobs, and append blobs) can be encrypted/decrypted using this scheme.</span></span>

### <a name="queues"></a><span data-ttu-id="32851-146">큐</span><span class="sxs-lookup"><span data-stu-id="32851-146">Queues</span></span>
<span data-ttu-id="32851-147">큐 메시지의 모든 형식이 될 수, 있으므로 hello 클라이언트 라이브러리 hello 메시지 텍스트에 IV (Initialization Vector) hello 및 hello 암호화 된 콘텐츠 암호화 키 (CEK) 포함 된 사용자 지정 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-147">Since queue messages can be of any format, hello client library defines a custom format that includes hello Initialization Vector (IV) and hello encrypted content encryption key (CEK) in hello message text.</span></span>  

<span data-ttu-id="32851-148">암호화 하는 동안 hello 클라이언트 라이브러리는 32 바이트의 임의 CEK 함께 16 바이트의 임의 IV를 생성 하 고이 정보를 사용 하 여 hello 큐 메시지 텍스트의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-148">During encryption, hello client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of hello queue message text using this information.</span></span> <span data-ttu-id="32851-149">hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 toohello 암호화 된 큐 메시지 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-149">hello wrapped CEK and some additional encryption metadata are then added toohello encrypted queue message.</span></span> <span data-ttu-id="32851-150">(아래 참조)이 수정 된 메시지는 hello 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-150">This modified message (shown below) is stored on hello service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="32851-151">암호 해독 하는 동안 hello 래핑된 키 hello 큐 메시지에서 추출 되며 래핑이 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-151">During decryption, hello wrapped key is extracted from hello queue message and unwrapped.</span></span> <span data-ttu-id="32851-152">또한 hello IV hello 큐 메시지에서 추출 된 이며 래핑이 해제 hello 키 toodecrypt hello 큐 메시지 데이터와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-152">hello IV is also extracted from hello queue message and used along with hello unwrapped key toodecrypt hello queue message data.</span></span> <span data-ttu-id="32851-153">Hello 암호화 메타 데이터를 작으면 (500 바이트의 경우) 아래 큐 메시지에 대 한 hello 64KB 제한에 대해 계산지 않습니다 것, hello 영향을 관리할 수 있어야 하므로 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-153">Note that hello encryption metadata is small (under 500 bytes), so while it does count toward hello 64KB limit for a queue message, hello impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="32851-154">테이블</span><span class="sxs-lookup"><span data-stu-id="32851-154">Tables</span></span>
<span data-ttu-id="32851-155">삽입을 위한 엔터티 속성의 클라이언트 라이브러리 지원 암호화 hello 및 교체 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-155">hello client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="32851-156">병합은 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-156">Merge is not currently supported.</span></span> <span data-ttu-id="32851-157">속성 하위 집합 암호화 된 다른 키를 사용 하 여 이전에, 이후 hello 새 속성을 병합 하 고 hello 메타 데이터를 업데이트 하기만 하면 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-157">Since a subset of properties may have been encrypted previously using a different key, simply merging hello new properties and updating hello metadata will result in data loss.</span></span> <span data-ttu-id="32851-158">Hello 서비스에서 tooread hello 기존 엔터티를 호출 추가 서비스를 만드는 또는 속성 당 새 키를 사용 하는 적합 하지 않은 성능상의 이유로 필요 하거나 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-158">Merging either requires making extra service calls tooread hello pre-existing entity from hello service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="32851-159">테이블 데이터 암호화는 다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-159">Table data encryption works as follows:</span></span>  

1. <span data-ttu-id="32851-160">사용자가 hello 속성 toobe 암호화를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-160">Users specify hello properties toobe encrypted.</span></span>  
2. <span data-ttu-id="32851-161">hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector)의 모든 엔터티에 대 한 32 바이트 (CEK) 임의의 콘텐츠 암호화 키와 함께 16 바이트를 생성 하 고 hello 개별 속성 toobe 당 새 IV를 파생 하 여 암호화에서 봉투 (envelope) 암호화를 수행 합니다. 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-161">hello client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on hello individual properties toobe encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="32851-162">암호화 된 hello 속성 이진 데이터로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-162">hello encrypted property is stored as binary data.</span></span>  
3. <span data-ttu-id="32851-163">hello CEK 되 고 그런 다음 몇 가지 추가 암호화 메타 데이터는 두 개의 추가 예약 된 속성으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-163">hello wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="32851-164">hello 첫 번째 예약 된 속성 (_ClientEncryptionMetadata1)은 4, 버전 및 래핑된 키에 대 한 hello 정보를 포함 하는 문자열 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-164">hello first reserved property (_ClientEncryptionMetadata1) is a string property that holds hello information about IV, version, and wrapped key.</span></span> <span data-ttu-id="32851-165">hello 두 번째 예약 된 속성 (_ClientEncryptionMetadata2)은 암호화 된 hello 속성에 대 한 hello 정보를 보유 하는 이진 속성.</span><span class="sxs-lookup"><span data-stu-id="32851-165">hello second reserved property (_ClientEncryptionMetadata2) is a binary property that holds hello information about hello properties that are encrypted.</span></span> <span data-ttu-id="32851-166">이 두 번째 속성 (_ClientEncryptionMetadata2)의 hello 정보 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-166">hello information in this second property (_ClientEncryptionMetadata2) is itself encrypted.</span></span>  
4. <span data-ttu-id="32851-167">Toothese 추가 예약 된 속성 암호화에 필요, 인해 이제가 있습니다 252 대신 사용자 지정 속성을 250만.</span><span class="sxs-lookup"><span data-stu-id="32851-167">Due toothese additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="32851-168">hello hello 엔터티의 전체 크기는 1MB 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-168">hello total size of hello entity must be less than 1MB.</span></span>  
   
   <span data-ttu-id="32851-169">문자열 속성만 암호화 할 수 있다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="32851-169">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="32851-170">다른 유형의 속성 암호화 toobe 인 경우 변환 된 toostrings 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-170">If other types of properties are toobe encrypted, they must be converted toostrings.</span></span> <span data-ttu-id="32851-171">이진 속성으로 암호화 하는 hello 문자열 hello 서비스에 저장 됩니다 및 암호 해독 한 후 뒤로 toostrings 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-171">hello encrypted strings are stored on hello service as binary properties, and they are converted back toostrings after decryption.</span></span>
   
   <span data-ttu-id="32851-172">테이블의 경우 또한 toohello 암호화 정책 사용자 지정 해야 hello 속성 toobe 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-172">For tables, in addition toohello encryption policy, users must specify hello properties toobe encrypted.</span></span> <span data-ttu-id="32851-173">이것은 특성(TableEntity에서 파생 되는 POCO 엔터티)을 지정[Encrypt]하거나 암호화 해결 프로그램 요청 옵션에서 수행할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="32851-173">This can be done by either specifying an [Encrypt] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="32851-174">암호화 해결 프로그램은 파티션 키, 행 키 및 속성 이름을 취하고 해당 속성을 암호화해야 하는지 여부를 나타내는 부울 값을 반환하는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-174">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="32851-175">암호화 하는 동안 toohello 통신에 쓰는 동안 속성을 암호화 해야 하는지 여부를 hello 클라이언트 라이브러리 정보 toodecide이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-175">During encryption, hello client library will use this information toodecide whether a property should be encrypted while writing toohello wire.</span></span> <span data-ttu-id="32851-176">또한 hello 대리자 hello 가능성은 속성이 암호화 주위 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-176">hello delegate also provides for hello possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="32851-177">(예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 한다는 확인은 필요 하지 않은 tooprovide 읽기 또는 엔터티를 쿼리 하는 동안이 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-177">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary tooprovide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="32851-178">배치 작업</span><span class="sxs-lookup"><span data-stu-id="32851-178">Batch Operations</span></span>
<span data-ttu-id="32851-179">일괄 처리 작업에서 hello 동일한 KEK 여러 사용 될 해당 일괄 처리 작업의 모든 hello 행 hello 클라이언트 라이브러리는 하나의 옵션 개체 (및 따라서 하나의 정책/KEK)에 허용 하기 때문에 일괄 처리 작업 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-179">In batch operations, hello same KEK will be used across all hello rows in that batch operation because hello client library only allows one options object (and hence one policy/KEK) per batch operation.</span></span> <span data-ttu-id="32851-180">그러나 hello 클라이언트 라이브러리는 hello 일괄 처리에서 새로운 임의 IV 및 행당 임의 CEK를 생성 내부적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-180">However, hello client library will internally generate a new random IV and random CEK per row in hello batch.</span></span> <span data-ttu-id="32851-181">사용자가 선택할 수도 tooencrypt 모든 작업에 대해 서로 다른 속성 hello 일괄 처리의 hello 암호화 해결 프로그램에서이 동작을 정의 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-181">Users can also choose tooencrypt different properties for every operation in hello batch by defining this behavior in hello encryption resolver.</span></span>

### <a name="queries"></a><span data-ttu-id="32851-182">쿼리</span><span class="sxs-lookup"><span data-stu-id="32851-182">Queries</span></span>
<span data-ttu-id="32851-183">tooperform 쿼리 작업 수 tooresolve 있는 키 해결 프로그램을 지정 해야 모든 hello hello 결과 집합의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-183">tooperform query operations, you must specify a key resolver that is able tooresolve all hello keys in hello result set.</span></span> <span data-ttu-id="32851-184">Hello 쿼리 결과에 포함 된 엔터티 해결된 tooa 공급자 일 수 없습니다, hello 클라이언트 라이브러리는 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-184">If an entity contained in hello query result cannot be resolved tooa provider, hello client library will throw an error.</span></span> <span data-ttu-id="32851-185">서버 쪽 프로젝션을 수행 하는 모든 쿼리에 대 한 hello 클라이언트 라이브러리는 기본 선택 toohello 열으로 hello 특수 한 암호화 메타 데이터 속성 (_ClientEncryptionMetadata1 및 _ClientEncryptionMetadata2)을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-185">For any query that performs server side projections, hello client library will add hello special encryption metadata properties (_ClientEncryptionMetadata1 and _ClientEncryptionMetadata2) by default toohello selected columns.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="32851-186">Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="32851-186">Azure Key Vault</span></span>
<span data-ttu-id="32851-187">Azure 키 자격 증명 모음은 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-187">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span> <span data-ttu-id="32851-188">Azure 키 자격 증명 모음을 사용하여, 사용자는 키와 비밀(예: 인증 키, 저장소 계정 키, 데이터 암호화 키, PFX 파일 및 암호)을 암호화하여 하드웨어 보안 모듈(HSM)로 보호된 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-188">By using Azure Key Vault, users can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords) by using keys that are protected by hardware security modules (HSMs).</span></span> <span data-ttu-id="32851-189">자세한 내용은 [Azure 주요 자격 증명 모음이란?](../key-vault/key-vault-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32851-189">For more information, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="32851-190">hello 저장소 클라이언트 라이브러리는 키를 관리 하기 위한 Azure 전체에서 순서 tooprovide 공통 프레임 워크에에서 hello 주요 자격 증명 모음 핵심 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-190">hello storage client library uses hello Key Vault core library in order tooprovide a common framework across Azure for managing keys.</span></span> <span data-ttu-id="32851-191">사용자가 가져올 hello 주요 자격 증명 모음 확장 라이브러리를 사용 하 여 hello 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-191">Users also get hello additional benefit of using hello Key Vault extensions library.</span></span> <span data-ttu-id="32851-192">hello 확장 프로그램 라이브러리 캐싱 및 집계와 뿐만 아니라 간단 하 고 원활한 대칭/RSA 로컬 및 클라우드 키 공급자의 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-192">hello extensions library provides useful functionality around simple and seamless Symmetric/RSA local and cloud key providers as well as with aggregation and caching.</span></span>

### <a name="interface-and-dependencies"></a><span data-ttu-id="32851-193">인터페이스 및 종속성</span><span class="sxs-lookup"><span data-stu-id="32851-193">Interface and dependencies</span></span>
<span data-ttu-id="32851-194">세 가지 키 자격증명 모음 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-194">There are three Key Vault packages:</span></span>  

* <span data-ttu-id="32851-195">azure keyvault 코어 IKey hello 및 IKeyResolver 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-195">azure-keyvault-core contains hello IKey and IKeyResolver.</span></span> <span data-ttu-id="32851-196">어떤 부속품도 없는 작은 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-196">It is a small package with no dependencies.</span></span> <span data-ttu-id="32851-197">Java 용 hello 저장소 클라이언트 라이브러리는 종속성으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-197">hello storage client library for Java defines it as a dependency.</span></span>
* <span data-ttu-id="32851-198">keyvault azure 키 자격 증명 모음 REST 클라이언트 hello를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-198">azure-keyvault contains hello Key Vault REST client.</span></span>  
* <span data-ttu-id="32851-199">azure-keyvault-extensions는 암호화 알고리즘 및 RSAKey와  SymmetricKey의 구현이 포함된 확장 코드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-199">azure-keyvault-extensions contains extension code that includes implementations of cryptographic algorithms and an RSAKey and a SymmetricKey.</span></span> <span data-ttu-id="32851-200">Hello 코어 및 KeyVault 네임 스페이스에 따라 달라 집니다 하 고 집계 해결 프로그램 (사용자가 여러 키 공급자 toouse를 원하는) 하는 경우 및 캐싱 키 확인자 toodefine 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-200">It depends on hello Core and KeyVault namespaces and provides functionality toodefine an aggregate resolver (when users want toouse multiple key providers) and a caching key resolver.</span></span> <span data-ttu-id="32851-201">Hello 저장소 클라이언트 라이브러리에 종속 되지 않지만 직접이 패키지에 사용자가 원하는 toouse Azure 키 자격 증명 모음 toostore가 키 또는 toouse hello 주요 자격 증명 모음 확장 tooconsume hello 로컬 및 클라우드 암호화 공급자 경우,이 패키지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-201">Although hello storage client library does not directly depend on this package, if users wish toouse Azure Key Vault toostore their keys or toouse hello Key Vault extensions tooconsume hello local and cloud cryptographic providers, they will need this package.</span></span>  
  
  <span data-ttu-id="32851-202">키 자격증명모음은 고급 가치 마스터키로 고안되었으며 키 자격증명 모음당 스로틀 한계는 이것을 염두에 두고 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-202">Key Vault is designed for high-value master keys, and throttling limits per Key Vault are designed with this in mind.</span></span> <span data-ttu-id="32851-203">주요 자격 증명 모음을 사용 하 여 클라이언트 쪽 암호화를 수행할 때는 hello 기본 모델 toouse 대칭 마스터 키는 암호로 키 자격 증명 모음에 저장 하 고 로컬로 캐시은입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-203">When performing client-side encryption with Key Vault, hello preferred model is toouse symmetric master keys stored as secrets in Key Vault and cached locally.</span></span> <span data-ttu-id="32851-204">사용자가 수행 해야 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="32851-204">Users must do hello following:</span></span>  

1. <span data-ttu-id="32851-205">암호를 오프 라인으로 만들고 tooKey 자격 증명 모음을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-205">Create a secret offline and upload it tooKey Vault.</span></span>  
2. <span data-ttu-id="32851-206">Hello 암호의 기본 식별자를 사용 하 여 매개 변수 tooresolve hello 현재 버전의 hello 암호를 암호화 하 고이 정보를 로컬로 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-206">Use hello secret's base identifier as a parameter tooresolve hello current version of hello secret for encryption and cache this information locally.</span></span> <span data-ttu-id="32851-207">CachingKeyResolver; 캐싱에 사용 사용자는 예상된 되지 tooimplement 자체 캐싱 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-207">Use CachingKeyResolver for caching; users are not expected tooimplement their own caching logic.</span></span>  
3. <span data-ttu-id="32851-208">입력으로 hello 암호화 정책을 만드는 동안 hello 캐싱 확인자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-208">Use hello caching resolver as an input while creating hello encryption policy.</span></span>
   <span data-ttu-id="32851-209">Hello 암호화 코드 샘플에서 주요 자격 증명 모음 사용에 대 한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-209">More information regarding Key Vault usage can be found in hello encryption code samples.</span></span> <fix URL>  

## <a name="best-practices"></a><span data-ttu-id="32851-210">모범 사례</span><span class="sxs-lookup"><span data-stu-id="32851-210">Best practices</span></span>
<span data-ttu-id="32851-211">Java 용 hello 저장소 클라이언트 라이브러리에만 암호화 지원이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-211">Encryption support is available only in hello storage client library for Java.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32851-212">클라이언트 쪽 암호화를 사용할 때는 이러한 중요점을 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="32851-212">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="32851-213">읽기 또는 쓰기 tooan 암호화 경우 blob, 전체 blob 업로드 명령을 사용 하 여 및 범위/전체 blob 다운로드 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-213">When reading from or writing tooan encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="32851-214">블록 배치, 블록 목록 배치, 페이지 쓰기, 일반 페이지 또는 블록 추가; 등의 프로토콜 작업을 사용 하 여 tooan 암호화 된 blob에 쓰기 방지 그렇지 않으면 hello 암호화 blob를 손상 하 고 읽을 수 없도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-214">Avoid writing tooan encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, Clear Pages, or Append Block; otherwise you may corrupt hello encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="32851-215">테이블의 경우에는 유사한 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-215">For tables, a similar constraint exists.</span></span> <span data-ttu-id="32851-216">Hello 암호화 메타 데이터를 업데이트 하지 않고 toonot 신중 하 게 암호화 하는 업데이트 속성 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-216">Be careful toonot update encrypted properties without updating hello encryption metadata.</span></span>  
> * <span data-ttu-id="32851-217">Hello 암호화 된 blob에서 메타 데이터를 설정 하는 경우 hello 암호화 관련에 필요한 메타 데이터 암호 해독, 가산적가 메타 데이터를 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-217">If you set metadata on hello encrypted blob, you may overwrite hello encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="32851-218">이것은 스냅숏에 대해서 마찬가지입니다. 암호화된 blob의 스냅숏을 생성하는 동안 메타데이터를 지정하지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="32851-218">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="32851-219">메타 데이터와 설정 해야 하는 경우 수 있는지 toocall hello **downloadAttributes** 메서드 첫 번째 tooget hello 현재 암호화 메타 데이터 및 메타 데이터 설정 되어 있는 동안 동시 쓰기를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-219">If metadata must be set, be sure toocall hello **downloadAttributes** method first tooget hello current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>  
> * <span data-ttu-id="32851-220">Hello를 사용 하도록 설정 **requireEncryption** 암호화 된 데이터에만 작동 해야 하는 사용자에 대 한 hello 기본 요청 옵션에는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-220">Enable hello **requireEncryption** flag in hello default request options for users that should work only with encrypted data.</span></span> <span data-ttu-id="32851-221">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32851-221">See below for more info.</span></span>  
> 
> 

## <a name="client-api--interface"></a><span data-ttu-id="32851-222">클라이언트 API / 인터페이스</span><span class="sxs-lookup"><span data-stu-id="32851-222">Client API / Interface</span></span>
<span data-ttu-id="32851-223">EncryptionPolicy 개체를 만드는 동안 사용자만 키를 공급 (IKey 구현), 확인자만 키를 공급 (IKeyResolver 구현) 또는 둘 모두 키를 공급.</span><span class="sxs-lookup"><span data-stu-id="32851-223">While creating an EncryptionPolicy object, users can provide only a Key (implementing IKey), only a resolver (implementing IKeyResolver), or both.</span></span> <span data-ttu-id="32851-224">IKey 형식이 hello 기본 키에 대 한 래핑/hello 논리를 제공 하 고 키 식별자를 사용 하 여 식별 되는.</span><span class="sxs-lookup"><span data-stu-id="32851-224">IKey is hello basic key type that is identified using a key identifier and that provides hello logic for wrapping/unwrapping.</span></span> <span data-ttu-id="32851-225">IKeyResolver는 hello 암호 해독 프로세스 동안 사용 되는 tooresolve 키입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-225">IKeyResolver is used tooresolve a key during hello decryption process.</span></span> <span data-ttu-id="32851-226">키 식별자가 제공하는 IKey를 반환하는 ResolveKey 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-226">It defines a ResolveKey method that returns an IKey given a key identifier.</span></span> <span data-ttu-id="32851-227">여러 위치에서 관리 되는 여러 키 간의 사용자 hello 기능 toochoose를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-227">This provides users hello ability toochoose between multiple keys that are managed in multiple locations.</span></span>

* <span data-ttu-id="32851-228">암호화, hello 키가 항상 사용 하 고 키 hello 없을 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-228">For encryption, hello key is used always and hello absence of a key will result in an error.</span></span>  
* <span data-ttu-id="32851-229">암호를 해독하려면</span><span class="sxs-lookup"><span data-stu-id="32851-229">For decryption:</span></span>  
  
  * <span data-ttu-id="32851-230">hello 키 확인자 tooget hello 키를 지정 하는 경우 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-230">hello key resolver is invoked if specified tooget hello key.</span></span> <span data-ttu-id="32851-231">가 지정 hello 확인자 hello 키 식별자에 대 한 매핑이 없는 경우 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-231">If hello resolver is specified but does not have a mapping for hello key identifier, an error is thrown.</span></span>  
  * <span data-ttu-id="32851-232">해결 프로그램 지정 하지 않으면 표시 되지만 키가 지정 하는 경우 해당 식별자에는 필요한 hello 키 식별자와 일치 하는 경우 hello 키는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-232">If resolver is not specified but a key is specified, hello key is used if its identifier matches hello required key identifier.</span></span> <span data-ttu-id="32851-233">Hello 식별자와 일치 하지 않는 경우 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32851-233">If hello identifier does not match, an error is thrown.</span></span>  
    
    <span data-ttu-id="32851-234">hello [암호화 샘플](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>주요 자격 증명 모음 통합 blob, 큐 및 테이블에 대 한 보다 자세한 종단 간 시나리오를 함께 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32851-234">hello [encryption samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables, along with Key Vault integration.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="32851-235">RequireEncryption 모드</span><span class="sxs-lookup"><span data-stu-id="32851-235">RequireEncryption mode</span></span>
<span data-ttu-id="32851-236">사용자는 모든 업로드 및 다운로드를 암호화해야 할 경우 작업 모드를 선택적으로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-236">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="32851-237">이 모드에서는 hello 서비스에서 암호화 되지 않은 한 암호화 정책 또는 다운로드 데이터 없이 시도 tooupload 데이터는 클라이언트 hello에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-237">In this mode, attempts tooupload data without an encryption policy or download data that is not encrypted on hello service will fail on hello client.</span></span> <span data-ttu-id="32851-238">hello **requireEncryption** hello 요청 옵션 개체가의 플래그는이 동작을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-238">hello **requireEncryption** flag of hello request options object controls this behavior.</span></span> <span data-ttu-id="32851-239">응용 프로그램은 Azure 저장소에 저장 된 모든 개체를 암호화 하는 경우 hello를 설정할 수 있습니다 **requireEncryption** hello 서비스 클라이언트 개체에 대 한 hello 기본 요청 옵션에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-239">If your application will encrypt all objects stored in Azure Storage, then you can set hello **requireEncryption** property on hello default request options for hello service client object.</span></span>   

<span data-ttu-id="32851-240">사용 예를 들어 **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** toorequire 암호화 모든 blob 작업에 대해 해당 클라이언트 개체를 통해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-240">For example, use **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** toorequire encryption for all blob operations performed through that client object.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="32851-241">Blob 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="32851-241">Blob service encryption</span></span>
<span data-ttu-id="32851-242">만들기는 **BlobEncryptionPolicy** hello 요청 옵션에 설정 및 개체 (또는 API를 사용 하 여 클라이언트 수준에서 **DefaultRequestOptions**).</span><span class="sxs-lookup"><span data-stu-id="32851-242">Create a **BlobEncryptionPolicy** object and set it in hello request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="32851-243">다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-243">Everything else will be handled by hello client library internally.</span></span>

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

// Set hello encryption policy on hello request options.
BlobRequestOptions options = new BlobRequestOptions();
options.setEncryptionPolicy(policy);

// Upload hello encrypted contents toohello blob.
blob.upload(stream, size, null, options, null);

// Download and decrypt hello encrypted contents from hello blob.
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
blob.download(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a><span data-ttu-id="32851-244">큐 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="32851-244">Queue service encryption</span></span>
<span data-ttu-id="32851-245">만들기는 **QueueEncryptionPolicy** hello 요청 옵션에 설정 및 개체 (또는 API를 사용 하 여 클라이언트 수준에서 **DefaultRequestOptions**).</span><span class="sxs-lookup"><span data-stu-id="32851-245">Create a **QueueEncryptionPolicy** object and set it in hello request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="32851-246">다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-246">Everything else will be handled by hello client library internally.</span></span>

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

// Add message
QueueRequestOptions options = new QueueRequestOptions();
options.setEncryptionPolicy(policy);

queue.addMessage(message, 0, 0, options, null);

// Retrieve message
CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);
```

### <a name="table-service-encryption"></a><span data-ttu-id="32851-247">테이블 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="32851-247">Table service encryption</span></span>
<span data-ttu-id="32851-248">또한 암호화 정책 toocreating 및 요청 옵션에 설정 지정는 **EncryptionResolver** 에 **TableRequestOptions**, 또는 hello에 hello [Encrypt] 특성 집합 엔터티의 getter 및 setter입니다.</span><span class="sxs-lookup"><span data-stu-id="32851-248">In addition toocreating an encryption policy and setting it on request options, you must either specify an **EncryptionResolver** in **TableRequestOptions**, or set hello [Encrypt] attribute on hello entity's getter and setter.</span></span>

### <a name="using-hello-resolver"></a><span data-ttu-id="32851-249">Hello 확인자를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="32851-249">Using hello resolver</span></span>

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

TableRequestOptions options = new TableRequestOptions()
options.setEncryptionPolicy(policy);
options.setEncryptionResolver(new EncryptionResolver() {
    public boolean encryptionResolver(String pk, String rk, String key) {
        if (key == "foo")
        {
            return true;
        }
        return false;
    }
});

// Insert Entity
currentTable.execute(TableOperation.insert(ent), options, null);

// Retrieve Entity
// No need toospecify an encryption resolver for retrieve
TableRequestOptions retrieveOptions = new TableRequestOptions()
retrieveOptions.setEncryptionPolicy(policy);

TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
TableResult result = currentTable.execute(operation, retrieveOptions, null);
```

### <a name="using-attributes"></a><span data-ttu-id="32851-250">특성을 사용하여</span><span class="sxs-lookup"><span data-stu-id="32851-250">Using attributes</span></span>
<span data-ttu-id="32851-251">Hello 엔터티 TableEntity 구현 하는 경우, 위에서 설명한 대로 다음 속성 getter hello 및 setter hello를 지정 하는 대신 hello [Encrypt] 특성으로 데코레이팅 될 수 **EncryptionResolver**합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-251">As mentioned above, if hello entity implements TableEntity, then hello properties getter and setter can be decorated with hello [Encrypt] attribute instead of specifying hello **EncryptionResolver**.</span></span>

```java
private string encryptedProperty1;

@Encrypt
public String getEncryptedProperty1 () {
    return this.encryptedProperty1;
}

@Encrypt
public void setEncryptedProperty1(final String encryptedProperty1) {
    this.encryptedProperty1 = encryptedProperty1;
}
```

## <a name="encryption-and-performance"></a><span data-ttu-id="32851-252">암호화 및 성능</span><span class="sxs-lookup"><span data-stu-id="32851-252">Encryption and performance</span></span>
<span data-ttu-id="32851-253">저장소 데이터를 암호화하면 추가 성능 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-253">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="32851-254">hello 콘텐츠 키와 IV를 생성 해야, hello 콘텐츠 자체 암호화, 및 추가 메타 데이터를 포맷 하 고 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-254">hello content key and IV must be generated, hello content itself must be encrypted, and additional meta-data must be formatted and uploaded.</span></span> <span data-ttu-id="32851-255">이 오버 헤드는 암호화 되는 데이터의 hello 양에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="32851-255">This overhead will vary depending on hello quantity of data being encrypted.</span></span> <span data-ttu-id="32851-256">고객은 항상 개발 중에 응용 프로그램 성능을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="32851-256">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32851-257">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32851-257">Next steps</span></span>
* <span data-ttu-id="32851-258">Hello 다운로드 [Java Maven 패키지에 대 한 Azure 저장소 클라이언트 라이브러리](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="32851-258">Download hello [Azure Storage Client Library for Java Maven package](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)</span></span>  
* <span data-ttu-id="32851-259">Hello 다운로드 [GitHub에서 Java 소스 코드에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-java)</span><span class="sxs-lookup"><span data-stu-id="32851-259">Download hello [Azure Storage Client Library for Java Source Code from GitHub](https://github.com/Azure/azure-storage-java)</span></span>   
* <span data-ttu-id="32851-260">Java Maven 패키지에 대 한 hello Azure 키 자격 증명 모음 Maven 라이브러리를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="32851-260">Download hello Azure Key Vault Maven Library for Java Maven packages:</span></span>
  * <span data-ttu-id="32851-261">[코어](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) 패키지</span><span class="sxs-lookup"><span data-stu-id="32851-261">[Core](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) package</span></span>
  * <span data-ttu-id="32851-262">[클라이언트](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) 패키지</span><span class="sxs-lookup"><span data-stu-id="32851-262">[Client](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) package</span></span>
* <span data-ttu-id="32851-263">Hello 방문 [Azure 키 자격 증명 모음 설명서](../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="32851-263">Visit hello [Azure Key Vault Documentation](../key-vault/key-vault-whatis.md)</span></span>
