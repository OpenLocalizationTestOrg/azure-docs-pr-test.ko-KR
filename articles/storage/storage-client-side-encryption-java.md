---
title: "Microsoft Azure Storage용 Java를 사용하는 클라이언트 쪽 암호화 | Microsoft Docs"
description: "Java용 Azure 저장소 클라이언트 라이브러리는 Azure 저장소 응용 프로그램의 보안을 최대화하기 위해 클라이언트 쪽 암호화 및 Azure 키 자격 증명 모음과의 통합을 지원합니다."
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
ms.openlocfilehash: c4ed9a073d4323ed79c4ad9f9e8082d23b970ccf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="client-side-encryption-and-azure-key-vault-with-java-for-microsoft-azure-storage"></a><span data-ttu-id="258e3-103">Microsoft Azure Storage용 Java를 사용하는 클라이언트 쪽 암호화 및 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="258e3-103">Client-Side Encryption and Azure Key Vault with Java for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="258e3-104">개요</span><span class="sxs-lookup"><span data-stu-id="258e3-104">Overview</span></span>
<span data-ttu-id="258e3-105">[Java용 Azure 저장소 클라이언트 라이브러리](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) 는 Azure 저장소에 업로드하기 전에 클라이언트 응용 프로그램 내부에서 데이터를 암호화하고 클라이언트로 다운로드하는 동안 데이터 암호를 해독하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-105">The [Azure Storage Client Library for Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="258e3-106">라이브러리 또한 저장소 계정 키 관리를 위해 Azure [키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 과의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-106">The library also supports integration with [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) for storage account key management.</span></span>

## <a name="encryption-and-decryption-via-the-envelope-technique"></a><span data-ttu-id="258e3-107">봉투(Envelope) 기술을 통해 암호화 및 암호 해독</span><span class="sxs-lookup"><span data-stu-id="258e3-107">Encryption and decryption via the envelope technique</span></span>
<span data-ttu-id="258e3-108">암호화 및 암호 해독 프로세스는봉투(Envelope) 기법을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-108">The processes of encryption and decryption follow the envelope technique.</span></span>  

### <a name="encryption-via-the-envelope-technique"></a><span data-ttu-id="258e3-109">봉투(Envelope) 기술을 통해 암호화</span><span class="sxs-lookup"><span data-stu-id="258e3-109">Encryption via the envelope technique</span></span>
<span data-ttu-id="258e3-110">암호화는 봉투(Envelope) 기술을 통해 다음과 같은 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-110">Encryption via the envelope technique works in the following way:</span></span>  

1. <span data-ttu-id="258e3-111">Azure 저장소 클라이언트 라이브러리는 1회용 대칭 키인 콘텐츠 암호화 키(CEK)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-111">The Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>  
2. <span data-ttu-id="258e3-112">사용자 데이터는 이 CEK를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-112">User data is encrypted using this CEK.</span></span>   
3. <span data-ttu-id="258e3-113">그런 다음 키 암호화 KEK를 사용하여 CEK를 래핑(암호화)합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-113">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="258e3-114">KEK는 키 식별자로 식별되고 비대칭 키 쌍 또는 대칭 키일 수 있으며 로컬로 관리되거나 Azure 키 자격 증명 모음에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-114">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vaults.</span></span>  
   <span data-ttu-id="258e3-115">저장소 클라이언트 라이브러리 자체는 KEK에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-115">The storage client library itself never has access to KEK.</span></span> <span data-ttu-id="258e3-116">라이브러리는 자격 증명 모음에서 제공되는 키 래핑 알고리즘을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-116">The library invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="258e3-117">사용자는 원하는 경우 키 래핑/래핑 해제를 위해 사용자 지정 공급자를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-117">Users can choose to use custom providers for key wrapping/unwrapping if desired.</span></span>  
4. <span data-ttu-id="258e3-118">그런 다음 암호화된 데이터를 Azure 저장소 서비스에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-118">The encrypted data is then uploaded to the Azure Storage service.</span></span> <span data-ttu-id="258e3-119">일부 추가 암호화 메타데이터와 함께 래핑된 키에 메타 데이터로(Blob) 저장 되거나 암호화 된 데이터 (메시지 큐 및 테이블 엔터티)와 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-119">The wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with the encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-the-envelope-technique"></a><span data-ttu-id="258e3-120">봉투(Envelope) 기술을 통해 암호해독</span><span class="sxs-lookup"><span data-stu-id="258e3-120">Decryption via the envelope technique</span></span>
<span data-ttu-id="258e3-121">암호해독은 봉투(Envelope) 기술을 통해 다음과 같은 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-121">Decryption via the envelope technique works in the following way:</span></span>  

1. <span data-ttu-id="258e3-122">클라이언트 라이브러리는 사용자가 키 암호화 키를  로컬로 또는 Azure 키 자격증명모음으로 관리한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-122">The client library assumes that the user is managing the key encryption key (KEK) either locally or in Azure Key Vaults.</span></span> <span data-ttu-id="258e3-123">사용자는 암호화에 사용된 특정 키를 알 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-123">The user does not need to know the specific key that was used for encryption.</span></span> <span data-ttu-id="258e3-124">대신 키를 서로 다른 키 식별자를 확인 하는 키 확인자 수를 설정하고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-124">Instead, a key resolver which resolves different key identifiers to keys can be set up and used.</span></span>  
2. <span data-ttu-id="258e3-125">클라이언트 라이브러리는 서비스에 저장된 모든 암호화 자료와 함께 암호화된 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-125">The client library downloads the encrypted data along with any encryption material that is stored on the service.</span></span>  
3. <span data-ttu-id="258e3-126">래핑된 콘텐츠 암호화 키 (CEK)는 키 암호화 키를(KEK) 사용하여 래핑해제(암호 해독)합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-126">The wrapped content encryption key (CEK) is then unwrapped (decrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="258e3-127">여기서 다시, 클라이언트 라이브러리는 KEK에 대한 액세스권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-127">Here again, the client library does not have access to KEK.</span></span> <span data-ttu-id="258e3-128">단순히 사용자 지정 또는 래핑 해제 알고리즘 키 자격 증명 모음 공급자를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-128">It simply invokes the custom or Key Vault provider's unwrapping algorithm.</span></span>  
4. <span data-ttu-id="258e3-129">그리고 콘텐츠 암호화 키 (CEK)는  암호화 된 사용자 데이터의 암호를 해독 하는데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-129">The content encryption key (CEK) is then used to decrypt the encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="258e3-130">암호화 메커니즘</span><span class="sxs-lookup"><span data-stu-id="258e3-130">Encryption Mechanism</span></span>
<span data-ttu-id="258e3-131">저장소 클라이언트 라이브러리는 사용자 데이터를 암호화하기 위해 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-131">The storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order to encrypt user data.</span></span> <span data-ttu-id="258e3-132">특히, AES를 이용한 [CBC(암호화 블록 체인)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="258e3-133">각 서비스는 하는 일이 각각 다르므로 여기서 이것들을 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="258e3-134">Blob</span><span class="sxs-lookup"><span data-stu-id="258e3-134">Blobs</span></span>
<span data-ttu-id="258e3-135">클라이언트 라이브러리는 현재 전체 blob 암호화만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-135">The client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="258e3-136">특히 사용자가 **upload*** 메서드 또는 **openOutputStream** 메서드를 사용할 때 암호화가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-136">Specifically, encryption is supported when users use the **upload*** methods or the **openOutputStream** method.</span></span> <span data-ttu-id="258e3-137">다운로드는 전체 및 범위 다운로드가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-137">For downloads, both complete and range downloads are supported.</span></span>  

<span data-ttu-id="258e3-138">암호화 하는 동안 클라이언트 라이브러리는 임의 IV (Initialization Vector) 32 바이트의 임의의 콘텐츠 암호화 키 (CEK)와 함께 16 바이트를 생성 하고 이 정보를 사용 여 blob 데이터의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-138">During encryption, the client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of the blob data using this information.</span></span> <span data-ttu-id="258e3-139">래핑된 CEK 및 일부 추가 암호화 메타 데이터 서비스에서 암호화 된 blob과 함께 메타 데이터를 blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-139">The wrapped CEK and some additional encryption metadata are then stored as blob metadata along with the encrypted blob on the service.</span></span>

> [!WARNING]
> <span data-ttu-id="258e3-140">blob에 대해 고유 메타데이터를 편집하거나 업로드 할 경우, 메타데이타가 유지되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-140">If you are editing or uploading your own metadata for the blob, you need to ensure that this metadata is preserved.</span></span> <span data-ttu-id="258e3-141">이 메타 데이터 없이 새 메타 데이터를 업로드 하는 경우에는 래핑된 CEK, IV 및 기타 메타 데이터가 손실 되고 blob 콘텐츠를 절대로 다시 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-141">If you upload new metadata without this metadata, the wrapped CEK, IV and other metadata will be lost and the blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="258e3-142">암호화 BLOB 다운로드는 **download*/openInputStream** 편리한 메서드를 사용한 전체 BLOB의 콘텐츠 검색을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-142">Downloading an encrypted blob involves retrieving the content of the entire blob using the **download*/openInputStream** convenience methods.</span></span> <span data-ttu-id="258e3-143">래핑된 CEK는 IV (blob 메타 데이터로 저장된 경우)와 함께 암호해독되고 사용되어 지며 해독된 데이터가 사용자에게 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-143">The wrapped CEK is unwrapped and used together with the IV (stored as blob metadata in this case) to return the decrypted data to the users.</span></span>

<span data-ttu-id="258e3-144">암호화된 BLOB 내에서 임의의 범위를 다운로드할 경우(**DownloadRange*** 메서드) 요청된 범위를 성공적으로 암호를 해독하는 데 사용되는 소량의 추가 데이터를 얻기 위해 사용자가 제공하는 범위가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-144">Downloading an arbitrary range (**downloadRange*** methods) in the encrypted blob involves adjusting the range provided by users in order to get a small amount of additional data that can be used to successfully decrypt the requested range.</span></span>  

<span data-ttu-id="258e3-145">이 스키마를 사용하여 모든 blob 유형(블록 blob, 페이지 blob 및 추가 blob)을 암호화/암호 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-145">All blob types (block blobs, page blobs, and append blobs) can be encrypted/decrypted using this scheme.</span></span>

### <a name="queues"></a><span data-ttu-id="258e3-146">큐</span><span class="sxs-lookup"><span data-stu-id="258e3-146">Queues</span></span>
<span data-ttu-id="258e3-147">큐 메시지의 모든 형식이 될 수, 있으므로 클라이언트 라이브러리는 IV (Initialization Vector) 및 암호화 된 콘텐츠 암호화 키 (CEK) 메시지 텍스트에 포함 된 사용자 지정 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-147">Since queue messages can be of any format, the client library defines a custom format that includes the Initialization Vector (IV) and the encrypted content encryption key (CEK) in the message text.</span></span>  

<span data-ttu-id="258e3-148">암호화 하는 동안 클라이언트 라이브러리는 32 바이트의 임의 CEK 함께 16 바이트의 임의 IV를 생성하고 이 정보를 사용하여 큐 메시지 텍스트의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-148">During encryption, the client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of the queue message text using this information.</span></span> <span data-ttu-id="258e3-149">래핑된 CEK 및 일부 추가 암호화 메타 데이터를 암호화 된 큐 메시지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-149">The wrapped CEK and some additional encryption metadata are then added to the encrypted queue message.</span></span> <span data-ttu-id="258e3-150">(아래 참조)이 수정 된 메시지는 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-150">This modified message (shown below) is stored on the service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="258e3-151">암호를 해독 하는 동안, 래핑된 키는 큐 메시지에서 추출되고 래핑이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-151">During decryption, the wrapped key is extracted from the queue message and unwrapped.</span></span> <span data-ttu-id="258e3-152">IV 또한 큐메시지에서 추출되고 큐 메시지 데이터를 암호해독하기 위해 래핑해제된 키와 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-152">The IV is also extracted from the queue message and used along with the unwrapped key to decrypt the queue message data.</span></span> <span data-ttu-id="258e3-153">참고로 암호화 메타데이터는 작아야하므로(500바이트 이하),큐 메시지는 64KB의 제한이 있어야만 영향을 관리 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-153">Note that the encryption metadata is small (under 500 bytes), so while it does count toward the 64KB limit for a queue message, the impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="258e3-154">테이블</span><span class="sxs-lookup"><span data-stu-id="258e3-154">Tables</span></span>
<span data-ttu-id="258e3-155">클라이언트 라이브러리는 작업 삽입 및 삭제의 엔터티 속성 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-155">The client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="258e3-156">병합은 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-156">Merge is not currently supported.</span></span> <span data-ttu-id="258e3-157">속성의 하위 집합은 이전에 다른 키를 사용하여 암호화됐을 가능성이 있기 때문에 단순히 새로운 속성을 병합하는 것과 메타데이터를 업데이트 하는 것은 데이터 손실을 불러 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-157">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="258e3-158">서비스에서 기존 엔터티를 읽을 수 있는 추가 서비스 호출을 수행 하거나 속성 당 새 키를 사용하는 것 모두에 성능상의 이유로 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-158">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="258e3-159">테이블 데이터 암호화는 다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-159">Table data encryption works as follows:</span></span>  

1. <span data-ttu-id="258e3-160">사용자는 암호화할 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-160">Users specify the properties to be encrypted.</span></span>  
2. <span data-ttu-id="258e3-161">클라이언트 라이브러리는 모든 엔터티에 대해 16바이트의 임의 IV(Initialization Vector)와 함께 32바이트의 임의 CEK(콘텐츠 암호화 키)를 생성하고 속성당 새 IV를 파생하여 암호화해야 하는 개별적인 속성에 대해 봉투(envelope) 암호화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-161">The client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on the individual properties to be encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="258e3-162">암호화된 속성은 이진 데이터로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-162">The encrypted property is stored as binary data.</span></span>  
3. <span data-ttu-id="258e3-163">래핑된 CEK 및 일부 추가 암호화 메타 데이터는 다음  추가 예약 된 두 가지 속성으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-163">The wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="258e3-164">첫 번째 예약 된 속성 (_ClientEncryptionMetadata1)은 IV, 버전, 래핑된 키의 정보를 담고 있는 문자열 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-164">The first reserved property (_ClientEncryptionMetadata1) is a string property that holds the information about IV, version, and wrapped key.</span></span> <span data-ttu-id="258e3-165">또 다른 예약된 속성(_ClientEncryptionMetadata2)은 암호화된 속성에 대한 정보를 담고 있는 이진 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-165">The second reserved property (_ClientEncryptionMetadata2) is a binary property that holds the information about the properties that are encrypted.</span></span> <span data-ttu-id="258e3-166">이 두 번째 속성(_ClientEncryptionMetadata2)의 정보는 자체적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-166">The information in this second property (_ClientEncryptionMetadata2) is itself encrypted.</span></span>  
4. <span data-ttu-id="258e3-167">이 추가적인 예약 속성이 암호화에 필요하기 때문에 사용자들은 252가지 사용자 지정 속성 대신 250가지를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-167">Due to these additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="258e3-168">엔터티의 총 크기는 1MB 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-168">The total size of the entity must be less than 1MB.</span></span>  
   
   <span data-ttu-id="258e3-169">문자열 속성만 암호화 할 수 있다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-169">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="258e3-170">다른 유형의 속성이 암호화 된 경우, 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-170">If other types of properties are to be encrypted, they must be converted to strings.</span></span> <span data-ttu-id="258e3-171">암호화된 문자열은 서비스에 이진 속성으로 저장되고 암호 해독 후에는 다시 문자열로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-171">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>
   
   <span data-ttu-id="258e3-172">테이블의 경우, 암호화 정책 외에도 사용자가 암호화할 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-172">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="258e3-173">이것은 특성(TableEntity에서 파생 되는 POCO 엔터티)을 지정[Encrypt]하거나 암호화 해결 프로그램 요청 옵션에서 수행할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="258e3-173">This can be done by either specifying an [Encrypt] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="258e3-174">암호화 해결 프로그램은 파티션 키, 행 키 및 속성 이름을 취하고 해당 속성을 암호화해야 하는지 여부를 나타내는 부울 값을 반환하는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-174">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="258e3-175">암호화 하는 동안 클라이언트 라이브러리는 네트워크에 쓰는 동안 속성을 암호화 해야 하는지 여부를 결정하는데 이 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-175">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="258e3-176">대리자 속성은 암호화 하는 방법 논리의 가능성도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-176">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="258e3-177">(예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 읽기 또는 엔터티를 쿼리 하는 동안은 이정보가 필요없다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-177">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="258e3-178">배치 작업</span><span class="sxs-lookup"><span data-stu-id="258e3-178">Batch Operations</span></span>
<span data-ttu-id="258e3-179">일괄 처리 작업에서, 같은 kek가 배치 작업 안의 모든 행간에 사용되는데, 클라이언트 라이브러리는 배치 작업당 오직 하나의 옵션개체(하나의 정책/kek 때문에 )만 허용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-179">In batch operations, the same KEK will be used across all the rows in that batch operation because the client library only allows one options object (and hence one policy/KEK) per batch operation.</span></span> <span data-ttu-id="258e3-180">그러나 클라이언트 라이브러리는 배치 안에 새로운 임의 IV와 행 당 임의 CEK를 내부적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-180">However, the client library will internally generate a new random IV and random CEK per row in the batch.</span></span> <span data-ttu-id="258e3-181">사용자가 암호화 해결 프로그램에 이동작을 정의하여 배치의 모든 작업에 대해 암호화 할 다른 속성들을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-181">Users can also choose to encrypt different properties for every operation in the batch by defining this behavior in the encryption resolver.</span></span>

### <a name="queries"></a><span data-ttu-id="258e3-182">쿼리</span><span class="sxs-lookup"><span data-stu-id="258e3-182">Queries</span></span>
<span data-ttu-id="258e3-183">쿼리 작업을 수행 하려면 결과 집합에 있는 모든 키를 확인할 수 있는 키 확인자를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-183">To perform query operations, you must specify a key resolver that is able to resolve all the keys in the result set.</span></span> <span data-ttu-id="258e3-184">공급자에는 쿼리 결과에 포함 된 엔터티를 확인할 수 없으면, 클라이언트 라이브러리는 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-184">If an entity contained in the query result cannot be resolved to a provider, the client library will throw an error.</span></span> <span data-ttu-id="258e3-185">서버 쪽 프로젝션을 수행하는 모든 쿼리에 대해 클라이언트 라이브러리는 선택한 열에 기본적으로 특별한 암호 메타데이터 속성(_ClientEncryptionMetadata1 및 _ClientEncryptionMetadata2)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-185">For any query that performs server side projections, the client library will add the special encryption metadata properties (_ClientEncryptionMetadata1 and _ClientEncryptionMetadata2) by default to the selected columns.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="258e3-186">Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="258e3-186">Azure Key Vault</span></span>
<span data-ttu-id="258e3-187">Azure 키 자격 증명 모음은 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-187">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span> <span data-ttu-id="258e3-188">Azure 키 자격 증명 모음을 사용하여, 사용자는 키와 비밀(예: 인증 키, 저장소 계정 키, 데이터 암호화 키, PFX 파일 및 암호)을 암호화하여 하드웨어 보안 모듈(HSM)로 보호된 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-188">By using Azure Key Vault, users can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords) by using keys that are protected by hardware security modules (HSMs).</span></span> <span data-ttu-id="258e3-189">자세한 내용은 [Azure 주요 자격 증명 모음이란?](../key-vault/key-vault-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-189">For more information, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="258e3-190">저장소 클라이언트 라이브러리는 Azure 내에서 키를 관리 하기 위한 공통 프레임 워크를 제공 하기 위해 키 자격 증명 모음 핵심 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-190">The storage client library uses the Key Vault core library in order to provide a common framework across Azure for managing keys.</span></span> <span data-ttu-id="258e3-191">사용자는 또한 키 자격 증명 모음 확장 라이브러리를 사용하여 추가적인 이점을 제공을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-191">Users also get the additional benefit of using the Key Vault extensions library.</span></span> <span data-ttu-id="258e3-192">이 확장 라이브러리는 간단하고 원활한 대칭/RSA 로컬 및 집계와 캐싱같은 클라우드 키 공급자 관련 유용한 기능을 제공합니다. .</span><span class="sxs-lookup"><span data-stu-id="258e3-192">The extensions library provides useful functionality around simple and seamless Symmetric/RSA local and cloud key providers as well as with aggregation and caching.</span></span>

### <a name="interface-and-dependencies"></a><span data-ttu-id="258e3-193">인터페이스 및 종속성</span><span class="sxs-lookup"><span data-stu-id="258e3-193">Interface and dependencies</span></span>
<span data-ttu-id="258e3-194">세 가지 키 자격증명 모음 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-194">There are three Key Vault packages:</span></span>  

* <span data-ttu-id="258e3-195">azure-keyvault-core는 IKey 및 IKeyResolver 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-195">azure-keyvault-core contains the IKey and IKeyResolver.</span></span> <span data-ttu-id="258e3-196">어떤 부속품도 없는 작은 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-196">It is a small package with no dependencies.</span></span> <span data-ttu-id="258e3-197">Java용 저장소 클라이언트 라이브러리는 이를 종속성으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-197">The storage client library for Java defines it as a dependency.</span></span>
* <span data-ttu-id="258e3-198">azure-keyvault는 키 자격 증명 모음 REST 클라이언트를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-198">azure-keyvault contains the Key Vault REST client.</span></span>  
* <span data-ttu-id="258e3-199">azure-keyvault-extensions는 암호화 알고리즘 및 RSAKey와  SymmetricKey의 구현이 포함된 확장 코드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-199">azure-keyvault-extensions contains extension code that includes implementations of cryptographic algorithms and an RSAKey and a SymmetricKey.</span></span> <span data-ttu-id="258e3-200">코어 및 KeyVault 네임 스페이스에 의존하고 (여러 키 공급자를 사용하여 사용자가 원하는) 경우 집계 해결 프로그램 및 캐싱 키 해결 프로그램을 정의 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-200">It depends on the Core and KeyVault namespaces and provides functionality to define an aggregate resolver (when users want to use multiple key providers) and a caching key resolver.</span></span> <span data-ttu-id="258e3-201">비록 저장소 클라이언트 라이브러리가 이 패키지에 직접적으로 의존하지 않지만, 사용자가 그들의 키를 저장하거나 로컬과 클라우드 암호화 공급자를 소비하는 키 자격증명 모음 확장을 사용에 Azure 키 자격증명 모음을 사용하고 싶을 때는 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-201">Although the storage client library does not directly depend on this package, if users wish to use Azure Key Vault to store their keys or to use the Key Vault extensions to consume the local and cloud cryptographic providers, they will need this package.</span></span>  
  
  <span data-ttu-id="258e3-202">키 자격증명모음은 고급 가치 마스터키로 고안되었으며 키 자격증명 모음당 스로틀 한계는 이것을 염두에 두고 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-202">Key Vault is designed for high-value master keys, and throttling limits per Key Vault are designed with this in mind.</span></span> <span data-ttu-id="258e3-203">키 자격 증명 모음을 사용하여 클라이언트측 암호화를 수행할 때 모델을 선호 로컬로 대칭 마스터 키 암호 키 자격 증명 모음에로 저장  하 고 캐시를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-203">When performing client-side encryption with Key Vault, the preferred model is to use symmetric master keys stored as secrets in Key Vault and cached locally.</span></span> <span data-ttu-id="258e3-204">다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-204">Users must do the following:</span></span>  

1. <span data-ttu-id="258e3-205">암호를 오프라인으로 만들고 키 자격 증명 모음에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-205">Create a secret offline and upload it to Key Vault.</span></span>  
2. <span data-ttu-id="258e3-206">비밀의 기본 식별자를 현재 버전의 암호화에 대한 암호를 풀기 위해 매개변수로 사용하고 이 정보를 로컬로 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-206">Use the secret's base identifier as a parameter to resolve the current version of the secret for encryption and cache this information locally.</span></span> <span data-ttu-id="258e3-207">CachingKeyResolver를 사용합니다. 사용자는 자체 캐싱 논리가 구현되지 않는 것을 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-207">Use CachingKeyResolver for caching; users are not expected to implement their own caching logic.</span></span>  
3. <span data-ttu-id="258e3-208">암호화 정책을 생성하는 동안 캐싱 확인자를 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-208">Use the caching resolver as an input while creating the encryption policy.</span></span>
   <span data-ttu-id="258e3-209">주요 자격 증명 모음 사용법에 대한 자세한 내용은 암호화 코드 샘플에서 찾을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-209">More information regarding Key Vault usage can be found in the encryption code samples.</span></span> <fix URL>  

## <a name="best-practices"></a><span data-ttu-id="258e3-210">모범 사례</span><span class="sxs-lookup"><span data-stu-id="258e3-210">Best practices</span></span>
<span data-ttu-id="258e3-211">암호화 지원은 Java용 저장소 클라이언트 라이브러리에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-211">Encryption support is available only in the storage client library for Java.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="258e3-212">클라이언트 쪽 암호화를 사용할 때는 이러한 중요점을 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-212">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="258e3-213">암호화된 blob에서 읽거나 여기에 쓸 때는 전체 blob 업로드 명령 및 범위/전체 blob 다운로드 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-213">When reading from or writing to an encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="258e3-214">블록 배치, 블록 목록 배치, 페이지 쓰기, 페이지 지우기 또는 블록 추가와 같은 프로토콜 작업을 사용하여 암호화된 blob에 쓰지 않도록 합니다. 그렇지 않으면 암호화된 blob이 손상되어 읽지 못하게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-214">Avoid writing to an encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, Clear Pages, or Append Block; otherwise you may corrupt the encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="258e3-215">테이블의 경우에는 유사한 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-215">For tables, a similar constraint exists.</span></span> <span data-ttu-id="258e3-216">암호화 메타데이터를 업데이트하지 않고 암호화된 속성을 업데이트하지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-216">Be careful to not update encrypted properties without updating the encryption metadata.</span></span>  
> * <span data-ttu-id="258e3-217">암호화된 blob에서 메타데이터를 설정하는 경우 메타데이터의 설정은 가산적이 아니므로 암호 해독에 필요한 암호화 관련 메타데이터를 덮어쓸 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-217">If you set metadata on the encrypted blob, you may overwrite the encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="258e3-218">이것은 스냅숏에 대해서 마찬가지입니다. 암호화된 blob의 스냅숏을 생성하는 동안 메타데이터를 지정하지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-218">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="258e3-219">메타데이터가 설정되어야 하는 경우 먼저 **downloadAttributes** 메서드를 호출하여 현재 암호화 메타데이터를 가져오고, 메타데이터가 설정되는 동안에는 동시 쓰기를 피합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-219">If metadata must be set, be sure to call the **downloadAttributes** method first to get the current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>  
> * <span data-ttu-id="258e3-220">암호화된 데이터에만 작동해야 하는 사용자의 기본 요청 옵션에는 **requireEncryption** 플래그를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-220">Enable the **requireEncryption** flag in the default request options for users that should work only with encrypted data.</span></span> <span data-ttu-id="258e3-221">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="258e3-221">See below for more info.</span></span>  
> 
> 

## <a name="client-api--interface"></a><span data-ttu-id="258e3-222">클라이언트 API / 인터페이스</span><span class="sxs-lookup"><span data-stu-id="258e3-222">Client API / Interface</span></span>
<span data-ttu-id="258e3-223">EncryptionPolicy 개체를 만드는 동안 사용자만 키를 공급 (IKey 구현), 확인자만 키를 공급 (IKeyResolver 구현) 또는 둘 모두 키를 공급.</span><span class="sxs-lookup"><span data-stu-id="258e3-223">While creating an EncryptionPolicy object, users can provide only a Key (implementing IKey), only a resolver (implementing IKeyResolver), or both.</span></span> <span data-ttu-id="258e3-224">IKey 래핑/래핑 해제에 대한 논리를 제공하고 키 식별자를 사용하여 식별 되는 기본 키 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-224">IKey is the basic key type that is identified using a key identifier and that provides the logic for wrapping/unwrapping.</span></span> <span data-ttu-id="258e3-225">IKeyResolver 키는 암호 해독 프로세스에서 키를 해독하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-225">IKeyResolver is used to resolve a key during the decryption process.</span></span> <span data-ttu-id="258e3-226">키 식별자가 제공하는 IKey를 반환하는 ResolveKey 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-226">It defines a ResolveKey method that returns an IKey given a key identifier.</span></span> <span data-ttu-id="258e3-227">이것은 사용자에게 여러 위치에서 관리되는 여러 키 중 하나를 선택할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-227">This provides users the ability to choose between multiple keys that are managed in multiple locations.</span></span>

* <span data-ttu-id="258e3-228">암호화는 키가 항상 사용되고, 키가 없으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-228">For encryption, the key is used always and the absence of a key will result in an error.</span></span>  
* <span data-ttu-id="258e3-229">암호를 해독하려면</span><span class="sxs-lookup"><span data-stu-id="258e3-229">For decryption:</span></span>  
  
  * <span data-ttu-id="258e3-230">키 확인자는 키를 가져오기 위해 지정된 경우 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-230">The key resolver is invoked if specified to get the key.</span></span> <span data-ttu-id="258e3-231">확인자를 지정 하 고 키 식별자에 대한 매핑이 없는 경우, 오류가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-231">If the resolver is specified but does not have a mapping for the key identifier, an error is thrown.</span></span>  
  * <span data-ttu-id="258e3-232">확인자는 지정하지 않고 키는 지정한 경우 해당 식별자가 필요한 키 식별자와 일치하는 경우 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-232">If resolver is not specified but a key is specified, the key is used if its identifier matches the required key identifier.</span></span> <span data-ttu-id="258e3-233">식별자가 일치하지 않으면 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-233">If the identifier does not match, an error is thrown.</span></span>  
    
    <span data-ttu-id="258e3-234">[암호화 샘플](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples)<fix URL>은 Key Vault 통합과 함께 BLOB, 큐 및 테이블에 대한 보다 자세한 종단 간 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-234">The [encryption samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables, along with Key Vault integration.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="258e3-235">RequireEncryption 모드</span><span class="sxs-lookup"><span data-stu-id="258e3-235">RequireEncryption mode</span></span>
<span data-ttu-id="258e3-236">사용자는 모든 업로드 및 다운로드를 암호화해야 할 경우 작업 모드를 선택적으로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-236">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="258e3-237">이 모드에서는 클라이언트에서 암호화 정책 없이 데이터를 업로드하거나 서비스에서 암호화되지 않은 데이터를 다운로드하려고 하면 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-237">In this mode, attempts to upload data without an encryption policy or download data that is not encrypted on the service will fail on the client.</span></span> <span data-ttu-id="258e3-238">요청 옵션 개체의 **requireEncryption** 플래그가 이 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-238">The **requireEncryption** flag of the request options object controls this behavior.</span></span> <span data-ttu-id="258e3-239">응용 프로그램이 Azure 저장소에 저장된 모든 개체를 암호화하는 경우 서비스 클라이언트 개체에 대한 기본 요청 옵션에서 **requireEncryption** 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-239">If your application will encrypt all objects stored in Azure Storage, then you can set the **requireEncryption** property on the default request options for the service client object.</span></span>   

<span data-ttu-id="258e3-240">예를 들어 모든 BLOB 작업에 대한 암호화가 해당 클라이언트 개체를 통해 수행되도록 하려면 **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-240">For example, use **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** to require encryption for all blob operations performed through that client object.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="258e3-241">Blob 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="258e3-241">Blob service encryption</span></span>
<span data-ttu-id="258e3-242">**BlobEncryptionPolicy** 개체를 만들고 요청 옵션에서 설정합니다(**DefaultRequestOptions**를 사용하여 API 기준으로 또는 클라이언트 수준에서).</span><span class="sxs-lookup"><span data-stu-id="258e3-242">Create a **BlobEncryptionPolicy** object and set it in the request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="258e3-243">다른 모든 요소에서 처리 되는 클라이언트 라이브러리는 내부적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-243">Everything else will be handled by the client library internally.</span></span>

```java
// Create the IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create the encryption policy to be used for upload and download.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

// Set the encryption policy on the request options.
BlobRequestOptions options = new BlobRequestOptions();
options.setEncryptionPolicy(policy);

// Upload the encrypted contents to the blob.
blob.upload(stream, size, null, options, null);

// Download and decrypt the encrypted contents from the blob.
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
blob.download(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a><span data-ttu-id="258e3-244">큐 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="258e3-244">Queue service encryption</span></span>
<span data-ttu-id="258e3-245">**QueueEncryptionPolicy** 개체를 만들고 요청 옵션에서 설정합니다(**DefaultRequestOptions**를 사용하여 API 기준으로 또는 클라이언트 수준에서).</span><span class="sxs-lookup"><span data-stu-id="258e3-245">Create a **QueueEncryptionPolicy** object and set it in the request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="258e3-246">다른 모든 요소에서 처리 되는 클라이언트 라이브러리는 내부적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-246">Everything else will be handled by the client library internally.</span></span>

```java
// Create the IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create the encryption policy to be used for upload and download.
QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

// Add message
QueueRequestOptions options = new QueueRequestOptions();
options.setEncryptionPolicy(policy);

queue.addMessage(message, 0, 0, options, null);

// Retrieve message
CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);
```

### <a name="table-service-encryption"></a><span data-ttu-id="258e3-247">테이블 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="258e3-247">Table service encryption</span></span>
<span data-ttu-id="258e3-248">암호화 정책을 생성하고 요청 옵션에 설정하는 것 외에도 사용자는 **TableRequestOptions**에서 **EncryptionResolver**를 지정하거나 엔터티의 getter와 setter에 대해 [Encrypt] 특성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-248">In addition to creating an encryption policy and setting it on request options, you must either specify an **EncryptionResolver** in **TableRequestOptions**, or set the [Encrypt] attribute on the entity's getter and setter.</span></span>

### <a name="using-the-resolver"></a><span data-ttu-id="258e3-249">확인자를 사용하여</span><span class="sxs-lookup"><span data-stu-id="258e3-249">Using the resolver</span></span>

```java
// Create the IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create the encryption policy to be used for upload and download.
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
// No need to specify an encryption resolver for retrieve
TableRequestOptions retrieveOptions = new TableRequestOptions()
retrieveOptions.setEncryptionPolicy(policy);

TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
TableResult result = currentTable.execute(operation, retrieveOptions, null);
```

### <a name="using-attributes"></a><span data-ttu-id="258e3-250">특성을 사용하여</span><span class="sxs-lookup"><span data-stu-id="258e3-250">Using attributes</span></span>
<span data-ttu-id="258e3-251">앞서 설명한 것처럼 엔터티가 TableEntity를 구현하는 경우 **EncryptionResolver**를 지정하는 대신 [Encrypt] 특성으로 속성 getter와 setter를 데코레이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-251">As mentioned above, if the entity implements TableEntity, then the properties getter and setter can be decorated with the [Encrypt] attribute instead of specifying the **EncryptionResolver**.</span></span>

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

## <a name="encryption-and-performance"></a><span data-ttu-id="258e3-252">암호화 및 성능</span><span class="sxs-lookup"><span data-stu-id="258e3-252">Encryption and performance</span></span>
<span data-ttu-id="258e3-253">저장소 데이터를 암호화하면 추가 성능 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-253">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="258e3-254">콘텐츠 키 및 IV를 생성해야 하고, 콘텐츠 자체를 암호화해야 하고, 추가 메타데이터의 형식을 지정한 후 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-254">The content key and IV must be generated, the content itself must be encrypted, and additional meta-data must be formatted and uploaded.</span></span> <span data-ttu-id="258e3-255">이 오버헤드는 암호화되는 데이터의 양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-255">This overhead will vary depending on the quantity of data being encrypted.</span></span> <span data-ttu-id="258e3-256">고객은 항상 개발 중에 응용 프로그램 성능을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="258e3-256">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="258e3-257">다음 단계</span><span class="sxs-lookup"><span data-stu-id="258e3-257">Next steps</span></span>
* <span data-ttu-id="258e3-258">[Java Maven 패키지에 대한 Azure 저장소 클라이언트 라이브러리](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="258e3-258">Download the [Azure Storage Client Library for Java Maven package](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)</span></span>  
* <span data-ttu-id="258e3-259">[GitHub에서 Java 소스 코드용 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-java)</span><span class="sxs-lookup"><span data-stu-id="258e3-259">Download the [Azure Storage Client Library for Java Source Code from GitHub](https://github.com/Azure/azure-storage-java)</span></span>   
* <span data-ttu-id="258e3-260">Java Maven 패키지에 대한 Azure 주요 자격 증명 Maven 라이브러리 다운로드</span><span class="sxs-lookup"><span data-stu-id="258e3-260">Download the Azure Key Vault Maven Library for Java Maven packages:</span></span>
  * <span data-ttu-id="258e3-261">[코어](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) 패키지</span><span class="sxs-lookup"><span data-stu-id="258e3-261">[Core](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) package</span></span>
  * <span data-ttu-id="258e3-262">[클라이언트](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) 패키지</span><span class="sxs-lookup"><span data-stu-id="258e3-262">[Client](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) package</span></span>
* <span data-ttu-id="258e3-263">[Azure 주요 자격 증명 모음 설명서](../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="258e3-263">Visit the [Azure Key Vault Documentation](../key-vault/key-vault-whatis.md)</span></span>