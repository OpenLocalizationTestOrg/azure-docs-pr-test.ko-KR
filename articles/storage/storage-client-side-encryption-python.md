---
title: "Microsoft Azure Storage용 Python을 사용하는 클라이언트 쪽 암호화 | Microsoft Docs"
description: "Python용 Azure 저장소 클라이언트 라이브러리는 Azure 저장소 응용 프로그램의 보안을 최대화하기 위해 클라이언트 쪽 암호화를 지원합니다."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 95330d2662722784beabdf51c9331fdeb502fc53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a><span data-ttu-id="86dda-103">Microsoft Azure Storage용 Python을 이용한 클라이언트쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="86dda-103">Client-Side Encryption with Python for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="86dda-104">개요</span><span class="sxs-lookup"><span data-stu-id="86dda-104">Overview</span></span>
<span data-ttu-id="86dda-105">[Python용 Azure 저장소 클라이언트 라이브러리](https://pypi.python.org/pypi/azure-storage) 는 Azure Storage에 업로드하기 전에 클라이언트 응용 프로그램 내부에서 데이터를 암호화하고 클라이언트로 다운로드하는 동안 데이터 암호를 해독하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-105">The [Azure Storage Client Library for Python](https://pypi.python.org/pypi/azure-storage) supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="86dda-106">Azure 저장소 Python 라이브러리는 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-106">The Azure Storage Python library is in preview.</span></span>
> 
> 

## <a name="encryption-and-decryption-via-the-envelope-technique"></a><span data-ttu-id="86dda-107">봉투(Envelope) 기술을 통해 암호화 및 암호 해독</span><span class="sxs-lookup"><span data-stu-id="86dda-107">Encryption and decryption via the envelope technique</span></span>
<span data-ttu-id="86dda-108">암호화 및 암호 해독 프로세스는봉투(Envelope) 기법을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-108">The processes of encryption and decryption follow the envelope technique.</span></span>

### <a name="encryption-via-the-envelope-technique"></a><span data-ttu-id="86dda-109">봉투(Envelope) 기술을 통해 암호화</span><span class="sxs-lookup"><span data-stu-id="86dda-109">Encryption via the envelope technique</span></span>
<span data-ttu-id="86dda-110">암호화는 봉투(Envelope) 기술을 통해 다음과 같은 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-110">Encryption via the envelope technique works in the following way:</span></span>

1. <span data-ttu-id="86dda-111">Azure 저장소 클라이언트 라이브러리는 1회용 대칭 키인 콘텐츠 암호화 키(CEK)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-111">The Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="86dda-112">사용자 데이터는 이 CEK를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-112">User data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="86dda-113">그런 다음 키 암호화 KEK를 사용하여 CEK를 래핑(암호화)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-113">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="86dda-114">KEK는 키 식별자로 식별되고 비대칭 키 쌍 또는 대칭 키일 수 있으며 로컬로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-114">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key, which is managed locally.</span></span>
   <span data-ttu-id="86dda-115">저장소 클라이언트 라이브러리 자체는 KEK에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-115">The storage client library itself never has access to KEK.</span></span> <span data-ttu-id="86dda-116">라이브러리는 KEK에서 제공하는 키 래핑 알고리즘을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-116">The library invokes the key wrapping algorithm that is provided by the KEK.</span></span> <span data-ttu-id="86dda-117">사용자는 원하는 경우 키 래핑/래핑 해제를 위해 사용자 지정 공급자를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-117">Users can choose to use custom providers for key wrapping/unwrapping if desired.</span></span>
4. <span data-ttu-id="86dda-118">그런 다음 암호화된 데이터를 Azure 저장소 서비스에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-118">The encrypted data is then uploaded to the Azure Storage service.</span></span> <span data-ttu-id="86dda-119">일부 추가 암호화 메타데이터와 함께 래핑된 키에 메타 데이터로(Blob) 저장 되거나 암호화 된 데이터 (메시지 큐 및 테이블 엔터티)와 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-119">The wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with the encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-the-envelope-technique"></a><span data-ttu-id="86dda-120">봉투(Envelope) 기술을 통해 암호해독</span><span class="sxs-lookup"><span data-stu-id="86dda-120">Decryption via the envelope technique</span></span>
<span data-ttu-id="86dda-121">암호해독은 봉투(Envelope) 기술을 통해 다음과 같은 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-121">Decryption via the envelope technique works in the following way:</span></span>

1. <span data-ttu-id="86dda-122">클라이언트 라이브러리는 사용자가 KEK(키 암호화 키)를 로컬로 관리한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-122">The client library assumes that the user is managing the key encryption key (KEK) locally.</span></span> <span data-ttu-id="86dda-123">사용자는 암호화에 사용된 특정 키를 알 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-123">The user does not need to know the specific key that was used for encryption.</span></span> <span data-ttu-id="86dda-124">대신 다른 키 식별자를 키로 확인하는 키 확인자를 설정하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-124">Instead, a key resolver, which resolves different key identifiers to keys, can be set up and used.</span></span>
2. <span data-ttu-id="86dda-125">클라이언트 라이브러리는 서비스에 저장된 모든 암호화 자료와 함께 암호화된 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-125">The client library downloads the encrypted data along with any encryption material that is stored on the service.</span></span>
3. <span data-ttu-id="86dda-126">래핑된 콘텐츠 암호화 키 (CEK)는 키 암호화 키를(KEK) 사용하여 래핑해제(암호 해독)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-126">The wrapped content encryption key (CEK) is then unwrapped (decrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="86dda-127">여기서 다시, 클라이언트 라이브러리는 KEK에 대한 액세스권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-127">Here again, the client library does not have access to KEK.</span></span> <span data-ttu-id="86dda-128">단순히 사용자 지정 공급자의 래핑 해제 알고리즘을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-128">It simply invokes the custom provider's unwrapping algorithm.</span></span>
4. <span data-ttu-id="86dda-129">그리고 콘텐츠 암호화 키 (CEK)는  암호화 된 사용자 데이터의 암호를 해독 하는데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-129">The content encryption key (CEK) is then used to decrypt the encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="86dda-130">암호화 메커니즘</span><span class="sxs-lookup"><span data-stu-id="86dda-130">Encryption Mechanism</span></span>
<span data-ttu-id="86dda-131">저장소 클라이언트 라이브러리는 사용자 데이터를 암호화하기 위해 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-131">The storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order to encrypt user data.</span></span> <span data-ttu-id="86dda-132">특히, AES를 이용한 [CBC(암호화 블록 체인)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="86dda-133">각 서비스는 하는 일이 각각 다르므로 여기서 이것들을 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="86dda-134">Blob</span><span class="sxs-lookup"><span data-stu-id="86dda-134">Blobs</span></span>
<span data-ttu-id="86dda-135">클라이언트 라이브러리는 현재 전체 blob 암호화만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-135">The client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="86dda-136">특히 사용자가 **create*** 메서드를 사용할 때 암호화가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-136">Specifically, encryption is supported when users use the **create*** methods.</span></span> <span data-ttu-id="86dda-137">다운로드로는 전체 및 범위 다운로드가 지원되며, 업로드 및 다운로드의 병렬화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-137">For downloads, both complete and range downloads are supported, and parallelization of both upload and download is available.</span></span>

<span data-ttu-id="86dda-138">암호화 하는 동안 클라이언트 라이브러리는 임의 IV (Initialization Vector) 32 바이트의 임의의 콘텐츠 암호화 키 (CEK)와 함께 16 바이트를 생성 하고 이 정보를 사용 여 blob 데이터의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-138">During encryption, the client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of the blob data using this information.</span></span> <span data-ttu-id="86dda-139">래핑된 CEK 및 일부 추가 암호화 메타 데이터 서비스에서 암호화 된 blob과 함께 메타 데이터를 blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-139">The wrapped CEK and some additional encryption metadata are then stored as blob metadata along with the encrypted blob on the service.</span></span>

> [!WARNING]
> <span data-ttu-id="86dda-140">blob에 대해 고유 메타데이터를 편집하거나 업로드 할 경우, 메타데이타가 유지되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-140">If you are editing or uploading your own metadata for the blob, you need to ensure that this metadata is preserved.</span></span> <span data-ttu-id="86dda-141">이 메타 데이터 없이 새 메타 데이터를 업로드 하는 경우에는 래핑된 CEK, IV 및 기타 메타 데이터가 손실 되고 blob 콘텐츠를 절대로 다시 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-141">If you upload new metadata without this metadata, the wrapped CEK, IV and other metadata will be lost and the blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="86dda-142">암호화 Blob 다운로드는 **get*** 편리한 메서드를 사용한 전체 Blob의 콘텐츠 검색을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-142">Downloading an encrypted blob involves retrieving the content of the entire blob using the **get*** convenience methods.</span></span> <span data-ttu-id="86dda-143">래핑된 CEK는 IV (blob 메타 데이터로 저장된 경우)와 함께 암호해독되고 사용되어 지며 해독된 데이터가 사용자에게 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-143">The wrapped CEK is unwrapped and used together with the IV (stored as blob metadata in this case) to return the decrypted data to the users.</span></span>

<span data-ttu-id="86dda-144">암호화된 Blob 내에서 임의의 범위를 다운로드할 경우(범위 매개 변수가 제공된**get*** 메서드) 요청된 범위를 성공적으로 암호를 해독하는 데 사용되는 소량의 추가 데이터를 얻기 위해 사용자가 제공하는 범위가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-144">Downloading an arbitrary range (**get*** methods with range parameters passed in) in the encrypted blob involves adjusting the range provided by users in order to get a small amount of additional data that can be used to successfully decrypt the requested range.</span></span>

<span data-ttu-id="86dda-145">이 스키마를 사용하여 블록 Blob 및 페이지 Blob만 암호화/암호 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-145">Block blobs and page blobs only can be encrypted/decrypted using this scheme.</span></span> <span data-ttu-id="86dda-146">추가 Blob에 대한 암호화 지원은 현재 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-146">There is currently no support for encrypting append blobs.</span></span>

### <a name="queues"></a><span data-ttu-id="86dda-147">큐</span><span class="sxs-lookup"><span data-stu-id="86dda-147">Queues</span></span>
<span data-ttu-id="86dda-148">큐 메시지의 모든 형식이 될 수, 있으므로 클라이언트 라이브러리는 IV (Initialization Vector) 및 암호화 된 콘텐츠 암호화 키 (CEK) 메시지 텍스트에 포함 된 사용자 지정 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-148">Since queue messages can be of any format, the client library defines a custom format that includes the Initialization Vector (IV) and the encrypted content encryption key (CEK) in the message text.</span></span>

<span data-ttu-id="86dda-149">암호화 하는 동안 클라이언트 라이브러리는 32 바이트의 임의 CEK 함께 16 바이트의 임의 IV를 생성하고 이 정보를 사용하여 큐 메시지 텍스트의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-149">During encryption, the client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of the queue message text using this information.</span></span> <span data-ttu-id="86dda-150">래핑된 CEK 및 일부 추가 암호화 메타 데이터를 암호화 된 큐 메시지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-150">The wrapped CEK and some additional encryption metadata are then added to the encrypted queue message.</span></span> <span data-ttu-id="86dda-151">(아래 참조)이 수정 된 메시지는 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-151">This modified message (shown below) is stored on the service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="86dda-152">암호를 해독 하는 동안, 래핑된 키는 큐 메시지에서 추출되고 래핑이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-152">During decryption, the wrapped key is extracted from the queue message and unwrapped.</span></span> <span data-ttu-id="86dda-153">IV 또한 큐메시지에서 추출되고 큐 메시지 데이터를 암호해독하기 위해 래핑해제된 키와 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-153">The IV is also extracted from the queue message and used along with the unwrapped key to decrypt the queue message data.</span></span> <span data-ttu-id="86dda-154">참고로 암호화 메타데이터는 작아야하므로(500바이트 이하),큐 메시지는 64KB의 제한이 있어야만 영향을 관리 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-154">Note that the encryption metadata is small (under 500 bytes), so while it does count toward the 64KB limit for a queue message, the impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="86dda-155">테이블</span><span class="sxs-lookup"><span data-stu-id="86dda-155">Tables</span></span>
<span data-ttu-id="86dda-156">클라이언트 라이브러리는 작업 삽입 및 삭제의 엔터티 속성 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-156">The client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="86dda-157">병합은 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-157">Merge is not currently supported.</span></span> <span data-ttu-id="86dda-158">속성의 하위 집합은 이전에 다른 키를 사용하여 암호화됐을 가능성이 있기 때문에 단순히 새로운 속성을 병합하는 것과 메타데이터를 업데이트 하는 것은 데이터 손실을 불러 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-158">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="86dda-159">서비스에서 기존 엔터티를 읽을 수 있는 추가 서비스 호출을 수행 하거나 속성 당 새 키를 사용하는 것 모두에 성능상의 이유로 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-159">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="86dda-160">테이블 데이터 암호화는 다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-160">Table data encryption works as follows:</span></span>

1. <span data-ttu-id="86dda-161">사용자는 암호화할 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-161">Users specify the properties to be encrypted.</span></span>
2. <span data-ttu-id="86dda-162">클라이언트 라이브러리는 모든 엔터티에 대해 16바이트의 임의 IV(Initialization Vector)와 함께 32바이트의 임의 CEK(콘텐츠 암호화 키)를 생성하고 속성당 새 IV를 파생하여 암호화해야 하는 개별적인 속성에 대해 봉투(envelope) 암호화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-162">The client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on the individual properties to be encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="86dda-163">암호화된 속성은 이진 데이터로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-163">The encrypted property is stored as binary data.</span></span>
3. <span data-ttu-id="86dda-164">래핑된 CEK 및 일부 추가 암호화 메타 데이터는 다음  추가 예약 된 두 가지 속성으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-164">The wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="86dda-165">첫 번째 예약 된 속성 (\_ClientEncryptionMetadata1)은 IV, 버전, 래핑된 키의 정보를 담고 있는 문자열 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-165">The first reserved property (\_ClientEncryptionMetadata1) is a string property that holds the information about IV, version, and wrapped key.</span></span> <span data-ttu-id="86dda-166">또 다른 예약된 속성(\_ClientEncryptionMetadata2)은 암호화된 속성에 대한 정보를 담고 있는 이진 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-166">The second reserved property (\_ClientEncryptionMetadata2) is a binary property that holds the information about the properties that are encrypted.</span></span> <span data-ttu-id="86dda-167">이 두 번째 속성(\_ClientEncryptionMetadata2)의 정보는 자체적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-167">The information in this second property (\_ClientEncryptionMetadata2) is itself encrypted.</span></span>
4. <span data-ttu-id="86dda-168">이 추가적인 예약 속성이 암호화에 필요하기 때문에 사용자들은 252가지 사용자 지정 속성 대신 250가지를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-168">Due to these additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="86dda-169">엔터티의 총 크기는 1MB 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-169">The total size of the entity must be less than 1MB.</span></span>
   
   <span data-ttu-id="86dda-170">문자열 속성만 암호화 할 수 있다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-170">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="86dda-171">다른 유형의 속성이 암호화 된 경우, 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-171">If other types of properties are to be encrypted, they must be converted to strings.</span></span> <span data-ttu-id="86dda-172">암호화된 문자열은 서비스에 이진 속성으로 저장되고 암호 해독 후에는 다시 문자열(원시 문자열, EdmType.STRING 형식을 갖는 EntityProperties 아님)로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-172">The encrypted strings are stored on the service as binary properties, and they are converted back to strings (raw strings, not EntityProperties with type EdmType.STRING) after decryption.</span></span>
   
   <span data-ttu-id="86dda-173">테이블의 경우, 암호화 정책 외에도 사용자가 암호화할 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-173">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="86dda-174">형식을 EdmType.STRING으로 설정하고 암호화를 true로 설정하여 TableEntity 개체에 이러한 속성을 저장하거나 tableservice 개체에 대해 encryption_resolver_function을 설정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-174">This can be done by either storing these properties in TableEntity objects with the type set to EdmType.STRING and encrypt set to true or setting the encryption_resolver_function on the tableservice object.</span></span> <span data-ttu-id="86dda-175">암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는 부울을 반환하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-175">An encryption resolver is a function that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="86dda-176">암호화 하는 동안 클라이언트 라이브러리는 네트워크에 쓰는 동안 속성을 암호화 해야 하는지 여부를 결정하는데 이 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-176">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="86dda-177">대리자 속성은 암호화 하는 방법 논리의 가능성도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-177">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="86dda-178">(예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 읽기 또는 엔터티를 쿼리 하는 동안은 이정보가 필요없다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-178">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="86dda-179">배치 작업</span><span class="sxs-lookup"><span data-stu-id="86dda-179">Batch Operations</span></span>
<span data-ttu-id="86dda-180">배치의 모든 행에는 단일 암호화 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-180">One encryption policy applies to all rows in the batch.</span></span> <span data-ttu-id="86dda-181">클라이언트 라이브러리는 내부적으로 배치의 새로운 임의 IV와 행 기준 임의 CEK를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-181">The client library will internally generate a new random IV and random CEK per row in the batch.</span></span> <span data-ttu-id="86dda-182">사용자가 암호화 해결 프로그램에 이동작을 정의하여 배치의 모든 작업에 대해 암호화 할 다른 속성들을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-182">Users can also choose to encrypt different properties for every operation in the batch by defining this behavior in the encryption resolver.</span></span>
<span data-ttu-id="86dda-183">tableservice batch() 메서드를 통해 배치가 컨텍스트 관리자로 생성되면 tableservice의 암호화 정책이 해당 배치에 자동으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-183">If a batch is created as a context manager through the tableservice batch() method, the tableservice's encryption policy will automatically be applied to the batch.</span></span> <span data-ttu-id="86dda-184">생성자를 호출하여 배치를 명시적으로 만들 경우 암호화 정책이 매개 변수로 전달되고 배치의 수명 동안 수정되지 않은 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-184">If a batch is created explicitly by calling the constructor, the encryption policy must be passed as a parameter and left unmodified for the lifetime of the batch.</span></span>
<span data-ttu-id="86dda-185">엔터티는 배치의 암호화 정책을 사용하여 배치에 삽입될 때 암호화됩니다(tableservice의 암호화 정책을 사용하여 배치를 커밋할 때 암호화되지 않음).</span><span class="sxs-lookup"><span data-stu-id="86dda-185">Note that entities are encrypted as they are inserted into the batch using the batch's encryption policy (entities are NOT encrypted at the time of committing the batch using the tableservice's encryption policy).</span></span>

### <a name="queries"></a><span data-ttu-id="86dda-186">쿼리</span><span class="sxs-lookup"><span data-stu-id="86dda-186">Queries</span></span>
<span data-ttu-id="86dda-187">쿼리 작업을 수행 하려면 결과 집합에 있는 모든 키를 확인할 수 있는 키 확인자를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-187">To perform query operations, you must specify a key resolver that is able to resolve all the keys in the result set.</span></span> <span data-ttu-id="86dda-188">공급자에는 쿼리 결과에 포함 된 엔터티를 확인할 수 없으면, 클라이언트 라이브러리는 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-188">If an entity contained in the query result cannot be resolved to a provider, the client library will throw an error.</span></span> <span data-ttu-id="86dda-189">서버 쪽 프로젝션을 수행하는 모든 쿼리에 대해 클라이언트 라이브러리는 선택한 열에 기본적으로 특별한 암호 메타데이터 속성(\_ClientEncryptionMetadata1 및 \_ClientEncryptionMetadata2)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-189">For any query that performs server side projections, the client library will add the special encryption metadata properties (\_ClientEncryptionMetadata1 and \_ClientEncryptionMetadata2) by default to the selected columns.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86dda-190">클라이언트 쪽 암호화를 사용할 때는 이러한 중요점을 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-190">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="86dda-191">암호화된 blob에서 읽거나 여기에 쓸 때는 전체 blob 업로드 명령 및 범위/전체 blob 다운로드 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-191">When reading from or writing to an encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="86dda-192">블록 배치, 블록 목록 배치, 페이지 쓰기나 페이지 지우기와 같은 프로토콜 작업을 사용하여 암호화된 blob에 쓰기를 피하십시오. 그렇지 않으면 암호화된 blob이 손상되어 읽지 못하게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-192">Avoid writing to an encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, or Clear Pages; otherwise you may corrupt the encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="86dda-193">테이블의 경우에는 유사한 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-193">For tables, a similar constraint exists.</span></span> <span data-ttu-id="86dda-194">암호화 메타데이터를 업데이트하지 않고 암호화된 속성을 업데이트하지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-194">Be careful to not update encrypted properties without updating the encryption metadata.</span></span>
> * <span data-ttu-id="86dda-195">암호화된 blob에서 메타데이터를 설정하는 경우 메타데이터의 설정은 가산적이 아니므로 암호 해독에 필요한 암호화 관련 메타데이터를 덮어쓸 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-195">If you set metadata on the encrypted blob, you may overwrite the encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="86dda-196">이것은 스냅숏에 대해서 마찬가지입니다. 암호화된 blob의 스냅숏을 생성하는 동안 메타데이터를 지정하지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-196">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="86dda-197">메타데이터가 설정되어야 하는 경우 먼저 **get_blob_metadata** 메서드를 호출하여 현재 암호화 메타데이터를 가져오고, 메타데이터가 설정되는 동안에는 동시 쓰기를 피합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-197">If metadata must be set, be sure to call the **get_blob_metadata** method first to get the current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>
> * <span data-ttu-id="86dda-198">암호화된 데이터에만 작동해야 하는 사용자의 서비스 개체에 **require_encryption** 플래그를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-198">Enable the **require_encryption** flag on the service object for users that should work only with encrypted data.</span></span> <span data-ttu-id="86dda-199">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dda-199">See below for more info.</span></span>
> 
> 

<span data-ttu-id="86dda-200">저장소 클라이언트 라이브러리는 제공된 KEK 및 키 확인자가 다음 인터페이스를 구현할 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-200">The storage client library expects the provided KEK and key resolver to implement the following interface.</span></span> <span data-ttu-id="86dda-201">[Azure 주요 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 지원이 보류 중이며, 완료 시 이 라이브러리에 통합될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-201">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) support for Python KEK management is pending and will be integrated into this library when completed.</span></span>

## <a name="client-api--interface"></a><span data-ttu-id="86dda-202">클라이언트 API / 인터페이스</span><span class="sxs-lookup"><span data-stu-id="86dda-202">Client API / Interface</span></span>
<span data-ttu-id="86dda-203">저장소 서비스 개체(예: blockblobservice)가 생성된 후에 사용자는 암호화 정책 key_encryption_key, key_resolver_function 및 require_encryption을 구성하는 필드에 값을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-203">After a storage service object (i.e. blockblobservice) has been created, the user may assign values to the fields that constitute an encryption policy: key_encryption_key, key_resolver_function, and require_encryption.</span></span> <span data-ttu-id="86dda-204">사용자는 KEK만, 확인자만 또는 둘 다를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-204">Users can provide only a KEK, only a resolver, or both.</span></span> <span data-ttu-id="86dda-205">key_encryption_key는 key 래핑/래핑 해제에 대한 논리를 제공하고 키 식별자를 사용하여 식별 되는 기본 키 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-205">key_encryption_key is the basic key type that is identified using a key identifier and that provides the logic for wrapping/unwrapping.</span></span> <span data-ttu-id="86dda-206">key_resolver_function은 암호 해독 프로세스에서 키를 해독하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-206">key_resolver_function is used to resolve a key during the decryption process.</span></span> <span data-ttu-id="86dda-207">지정된 키 식별자에 대해 유효한 KEK를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-207">It returns a valid KEK given a key identifier.</span></span> <span data-ttu-id="86dda-208">이것은 사용자에게 여러 위치에서 관리되는 여러 키 중 하나를 선택할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-208">This provides users the ability to choose between multiple keys that are managed in multiple locations.</span></span>

<span data-ttu-id="86dda-209">KEK는 데이터를 성공적으로 암호화하기 위해 다음 메서드를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-209">The KEK must implement the following methods to successfully encrypt data:</span></span>

* <span data-ttu-id="86dda-210">wrap_key(cek): 사용자가 선택한 알고리즘을 사용하여 지정된 CEK(바이트)를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-210">wrap_key(cek): Wraps the specified CEK (bytes) using an algorithm of the user's choice.</span></span> <span data-ttu-id="86dda-211">래핑된 키를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-211">Returns the wrapped key.</span></span>
* <span data-ttu-id="86dda-212">get_key_wrap_algorithm(): 키를 래핑하는 데 사용되는 알고리즘을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-212">get_key_wrap_algorithm(): Returns the algorithm used to wrap keys.</span></span>
* <span data-ttu-id="86dda-213">get_kid(): 이 KEK에 대한 문자열 키 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-213">get_kid(): Returns the string key id for this KEK.</span></span>
  <span data-ttu-id="86dda-214">KEK는 데이터를 성공적으로 암호 해독하기 위해 다음 메서드를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-214">The KEK must implement the following methods to successfully decrypt data:</span></span>
* <span data-ttu-id="86dda-215">unwrap_key(cek, algorithm): 문자열 지정 알고리즘을 사용하여 지정된 CEK의 래핑 해제된 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-215">unwrap_key(cek, algorithm): Returns the unwrapped form of the specified CEK using the string-specified algorithm.</span></span>
* <span data-ttu-id="86dda-216">get_kid(): 이 KEK에 대한 문자열 키 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-216">get_kid(): Returns a string key id for this KEK.</span></span>

<span data-ttu-id="86dda-217">키 확인자는 적어도 지정된 키 ID에 대해 위의 인터페이스를 구현하는 해당 KEK를 반환하는 메서드를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-217">The key resolver must at least implement a method that, given a key id, returns the corresponding KEK implementing the interface above.</span></span> <span data-ttu-id="86dda-218">이 메서드만 서비스 개체의 key_resolver_function 속성에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-218">Only this method is to be assigned to the key_resolver_function property on the service object.</span></span>

* <span data-ttu-id="86dda-219">암호화는 키가 항상 사용되고, 키가 없으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-219">For encryption, the key is used always and the absence of a key will result in an error.</span></span>
* <span data-ttu-id="86dda-220">암호를 해독하려면</span><span class="sxs-lookup"><span data-stu-id="86dda-220">For decryption:</span></span>
  
  * <span data-ttu-id="86dda-221">키 확인자는 키를 가져오기 위해 지정된 경우 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-221">The key resolver is invoked if specified to get the key.</span></span> <span data-ttu-id="86dda-222">확인자를 지정 하 고 키 식별자에 대한 매핑이 없는 경우, 오류가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-222">If the resolver is specified but does not have a mapping for the key identifier, an error is thrown.</span></span>
  * <span data-ttu-id="86dda-223">확인자는 지정하지 않고 키는 지정한 경우 해당 식별자가 필요한 키 식별자와 일치하는 경우 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-223">If resolver is not specified but a key is specified, the key is used if its identifier matches the required key identifier.</span></span> <span data-ttu-id="86dda-224">식별자가 일치하지 않으면 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-224">If the identifier does not match, an error is thrown.</span></span>
    
    <span data-ttu-id="86dda-225">azure.storage.samples의 암호화 샘플은 <fix URL>Blob, 큐 및 테이블에 대한 보다 자세한 종단 간 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-225">The encryption samples in azure.storage.samples <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables.</span></span>
      <span data-ttu-id="86dda-226">KEK 및 키 확인자의 샘플 구현은 예제 파일에 각각 KeyWrapper 및 KeyResolver로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-226">Sample implementations of the KEK and key resolver are provided in the sample files as KeyWrapper and KeyResolver respectively.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="86dda-227">RequireEncryption 모드</span><span class="sxs-lookup"><span data-stu-id="86dda-227">RequireEncryption mode</span></span>
<span data-ttu-id="86dda-228">사용자는 모든 업로드 및 다운로드를 암호화해야 할 경우 작업 모드를 선택적으로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-228">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="86dda-229">이 모드에서는 클라이언트에서 암호화 정책 없이 데이터를 업로드하거나 서비스에서 암호화되지 않은 데이터를 다운로드하려고 하면 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-229">In this mode, attempts to upload data without an encryption policy or download data that is not encrypted on the service will fail on the client.</span></span> <span data-ttu-id="86dda-230">서비스 개체에 대한 **require_encryption** 플래그는 이 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-230">The **require_encryption** flag on the service object controls this behavior.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="86dda-231">Blob 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="86dda-231">Blob service encryption</span></span>
<span data-ttu-id="86dda-232">blockblobservice 개체에 대해 암호화 정책 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-232">Set the encryption policy fields on the blockblobservice object.</span></span> <span data-ttu-id="86dda-233">다른 모든 요소에서 처리 되는 클라이언트 라이브러리는 내부적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-233">Everything else will be handled by the client library internally.</span></span>

```python
# Create the KEK used for encryption.
# KeyWrapper is the provided sample implementation, but the user may use their own object as long as it implements the interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create the key resolver used for decryption.
# KeyResolver is the provided sample implementation, but the user may use whatever implementation they choose so long as the function set on the service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set the KEK and key resolver on the service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload the encrypted contents to the blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt the encrypted contents from the blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a><span data-ttu-id="86dda-234">큐 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="86dda-234">Queue service encryption</span></span>
<span data-ttu-id="86dda-235">queueservice 개체에 대해 암호화 정책 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-235">Set the encryption policy fields on the queueservice object.</span></span> <span data-ttu-id="86dda-236">다른 모든 요소에서 처리 되는 클라이언트 라이브러리는 내부적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-236">Everything else will be handled by the client library internally.</span></span>

```python
# Create the KEK used for encryption.
# KeyWrapper is the provided sample implementation, but the user may use their own object as long as it implements the interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create the key resolver used for decryption.
# KeyResolver is the provided sample implementation, but the user may use whatever implementation they choose so long as the function set on the service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set the KEK and key resolver on the service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a><span data-ttu-id="86dda-237">테이블 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="86dda-237">Table service encryption</span></span>
<span data-ttu-id="86dda-238">암호화 정책을 생성하고 요청 옵션에 설정하는 것 외에도 **tableservice**에서 **encryption_resolver_function**을 지정하거나 EntityProperty에 대해 encrypt 특성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-238">In addition to creating an encryption policy and setting it on request options, you must either specify an **encryption_resolver_function** on the **tableservice**, or set the encrypt attribute on the EntityProperty.</span></span>

### <a name="using-the-resolver"></a><span data-ttu-id="86dda-239">확인자를 사용하여</span><span class="sxs-lookup"><span data-stu-id="86dda-239">Using the resolver</span></span>

```python
# Create the KEK used for encryption.
# KeyWrapper is the provided sample implementation, but the user may use their own object as long as it implements the interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create the key resolver used for decryption.
# KeyResolver is the provided sample implementation, but the user may use whatever implementation they choose so long as the function set on the service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define the encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set the KEK and key resolver on the service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need to specify an encryption resolver for retrieve, but it is harmless to leave the property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a><span data-ttu-id="86dda-240">특성을 사용하여</span><span class="sxs-lookup"><span data-stu-id="86dda-240">Using attributes</span></span>
<span data-ttu-id="86dda-241">위에서 설명한 것처럼 EntityProperty 개체에 저장하고 암호화 필드를 설정하여 속성을 암호화용으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-241">As mentioned above, a property may be marked for encryption by storing it in an EntityProperty object and setting the encrypt field.</span></span>

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a><span data-ttu-id="86dda-242">암호화 및 성능</span><span class="sxs-lookup"><span data-stu-id="86dda-242">Encryption and performance</span></span>
<span data-ttu-id="86dda-243">저장소 데이터를 암호화하면 추가 성능 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-243">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="86dda-244">콘텐츠 키 및 IV를 생성해야 하고, 콘텐츠 자체를 암호화해야 하고, 추가 메타데이터의 형식을 지정한 후 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-244">The content key and IV must be generated, the content itself must be encrypted, and additional metadata must be formatted and uploaded.</span></span> <span data-ttu-id="86dda-245">이 오버헤드는 암호화되는 데이터의 양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-245">This overhead will vary depending on the quantity of data being encrypted.</span></span> <span data-ttu-id="86dda-246">고객은 항상 개발 중에 응용 프로그램 성능을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="86dda-246">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86dda-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86dda-247">Next steps</span></span>
* <span data-ttu-id="86dda-248">[Java PyPi 패키지에 대한 Azure 저장소 클라이언트 라이브러리](https://pypi.python.org/pypi/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="86dda-248">Download the [Azure Storage Client Library for Java PyPi package](https://pypi.python.org/pypi/azure-storage)</span></span>
* <span data-ttu-id="86dda-249">[Python 소스 코드용 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-python)</span><span class="sxs-lookup"><span data-stu-id="86dda-249">Download the [Azure Storage Client Library for Python Source Code from GitHub](https://github.com/Azure/azure-storage-python)</span></span>