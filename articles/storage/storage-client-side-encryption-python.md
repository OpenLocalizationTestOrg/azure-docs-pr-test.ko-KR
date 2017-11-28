---
title: "Microsoft Azure 저장소에 대 한 python aaaClient 쪽 암호화 | Microsoft Docs"
description: "hello Python 용 Azure 저장소 클라이언트 라이브러리는 Azure 저장소 응용 프로그램에 대 한 보안을 최대화 하기 위해 클라이언트 쪽 암호화를 지원합니다."
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
ms.openlocfilehash: d2e943977322b97b777369508b957a1b2cbaa4e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a><span data-ttu-id="d490d-103">Microsoft Azure Storage용 Python을 이용한 클라이언트쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="d490d-103">Client-Side Encryption with Python for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="d490d-104">개요</span><span class="sxs-lookup"><span data-stu-id="d490d-104">Overview</span></span>
<span data-ttu-id="d490d-105">hello [Python 용 Azure 저장소 클라이언트 라이브러리](https://pypi.python.org/pypi/azure-storage) tooAzure 저장소에 업로드 하 고 toohello 클라이언트를 다운로드 하는 동안 데이터를 해독 하기 전에 클라이언트 응용 프로그램 내에서 데이터를 암호화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-105">hello [Azure Storage Client Library for Python](https://pypi.python.org/pypi/azure-storage) supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span>

> [!NOTE]
> <span data-ttu-id="d490d-106">hello Azure 저장소 Python 라이브러리는 미리 보기 상태에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-106">hello Azure Storage Python library is in preview.</span></span>
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a><span data-ttu-id="d490d-107">암호화 및 암호 해독 hello 봉투 (envelope) 기술을 통해</span><span class="sxs-lookup"><span data-stu-id="d490d-107">Encryption and decryption via hello envelope technique</span></span>
<span data-ttu-id="d490d-108">암호화 및 암호 해독의 hello 프로세스 hello 봉투 (envelope) 기법을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-108">hello processes of encryption and decryption follow hello envelope technique.</span></span>

### <a name="encryption-via-hello-envelope-technique"></a><span data-ttu-id="d490d-109">Hello 봉투 (envelope) 기술을 통해 암호화</span><span class="sxs-lookup"><span data-stu-id="d490d-109">Encryption via hello envelope technique</span></span>
<span data-ttu-id="d490d-110">Hello 봉투 (envelope) 기술을 통해 암호화 hello 방식으로 다음에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-110">Encryption via hello envelope technique works in hello following way:</span></span>

1. <span data-ttu-id="d490d-111">hello Azure 저장소 클라이언트 라이브러리는 콘텐츠 암호화 키 (CEK)는 한 번 사용 대칭 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-111">hello Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="d490d-112">사용자 데이터는 이 CEK를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-112">User data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="d490d-113">hello CEK 다음 래핑된 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-113">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="d490d-114">hello KEK 키 식별자로 식별 되 고 비대칭 키 쌍 또는 대칭 키를 로컬로 관리 되는 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-114">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key, which is managed locally.</span></span>
   <span data-ttu-id="d490d-115">자체 hello 저장소 클라이언트 라이브러리에 대 한 액세스 tooKEK에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-115">hello storage client library itself never has access tooKEK.</span></span> <span data-ttu-id="d490d-116">hello 라이브러리 hello 키 래핑 KEK hello에서 제공 되는 알고리즘을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-116">hello library invokes hello key wrapping algorithm that is provided by hello KEK.</span></span> <span data-ttu-id="d490d-117">사용자에 대 한 키 래핑/원하는 경우 사용자 지정 공급자 toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-117">Users can choose toouse custom providers for key wrapping/unwrapping if desired.</span></span>
4. <span data-ttu-id="d490d-118">hello 암호화 된 데이터는 다음 toohello Azure 저장소 서비스에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-118">hello encrypted data is then uploaded toohello Azure Storage service.</span></span> <span data-ttu-id="d490d-119">몇 가지 추가 암호화 메타 데이터와 함께 hello 래핑된 키 (blob)에 메타 데이터로 저장 또는 보간 hello 암호화 된 데이터 (메시지 큐 및 테이블 엔터티)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-119">hello wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with hello encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-hello-envelope-technique"></a><span data-ttu-id="d490d-120">Hello 봉투 (envelope) 기술을 통해 암호 해독</span><span class="sxs-lookup"><span data-stu-id="d490d-120">Decryption via hello envelope technique</span></span>
<span data-ttu-id="d490d-121">Hello 봉투 (envelope) 기술을 통해 암호 해독 hello 방식으로 다음에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-121">Decryption via hello envelope technique works in hello following way:</span></span>

1. <span data-ttu-id="d490d-122">hello 클라이언트 라이브러리 해당 hello 사용자가 (KEK) hello 키 암호화 키를 로컬로 관리 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-122">hello client library assumes that hello user is managing hello key encryption key (KEK) locally.</span></span> <span data-ttu-id="d490d-123">hello 사용자 암호화에 사용 된 tooknow hello 특정 키가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-123">hello user does not need tooknow hello specific key that was used for encryption.</span></span> <span data-ttu-id="d490d-124">대신, 서로 다른 키 식별자 tookeys 확인 되 면 키 해결 프로그램 수를 설정 하 고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-124">Instead, a key resolver, which resolves different key identifiers tookeys, can be set up and used.</span></span>
2. <span data-ttu-id="d490d-125">hello 클라이언트 라이브러리는 hello 서비스에 저장 된 모든 암호화 자료 함께 hello 암호화 된 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-125">hello client library downloads hello encrypted data along with any encryption material that is stored on hello service.</span></span>
3. <span data-ttu-id="d490d-126">키 암호화 키 (KEK) hello 래핑되지 않은 (암호 해독 된)를 사용 하 여 hello 래핑된 콘텐츠 암호화 키 (CEK)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-126">hello wrapped content encryption key (CEK) is then unwrapped (decrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="d490d-127">여기서 다시 hello 클라이언트 라이브러리 않아도 액세스 tooKEK 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-127">Here again, hello client library does not have access tooKEK.</span></span> <span data-ttu-id="d490d-128">래핑 해제 알고리즘 hello 사용자 지정 공급자를 호출 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-128">It simply invokes hello custom provider's unwrapping algorithm.</span></span>
4. <span data-ttu-id="d490d-129">hello 암호화 키 (CEK)는 다음 콘텐츠 toodecrypt hello 암호화 된 사용자 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-129">hello content encryption key (CEK) is then used toodecrypt hello encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="d490d-130">암호화 메커니즘</span><span class="sxs-lookup"><span data-stu-id="d490d-130">Encryption Mechanism</span></span>
<span data-ttu-id="d490d-131">hello 저장소 클라이언트 라이브러리를 사용 하 여 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 주문 tooencrypt 사용자 데이터에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-131">hello storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order tooencrypt user data.</span></span> <span data-ttu-id="d490d-132">특히, AES를 이용한 [CBC(암호화 블록 체인)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="d490d-133">각 서비스는 하는 일이 각각 다르므로 여기서 이것들을 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="d490d-134">Blob</span><span class="sxs-lookup"><span data-stu-id="d490d-134">Blobs</span></span>
<span data-ttu-id="d490d-135">hello 클라이언트 라이브러리는 현재 전체 blob만 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-135">hello client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="d490d-136">사용자가 hello를 사용할 때 암호화가 지원 특히 **만들*** 메서드.</span><span class="sxs-lookup"><span data-stu-id="d490d-136">Specifically, encryption is supported when users use hello **create*** methods.</span></span> <span data-ttu-id="d490d-137">다운로드로는 전체 및 범위 다운로드가 지원되며, 업로드 및 다운로드의 병렬화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-137">For downloads, both complete and range downloads are supported, and parallelization of both upload and download is available.</span></span>

<span data-ttu-id="d490d-138">암호화 하는 동안 hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector) 32 바이트는 임의의 콘텐츠 암호화 키 (CEK)와 함께 16 바이트의 생성 되며이 정보를 사용 하 여 hello blob 데이터의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-138">During encryption, hello client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of hello blob data using this information.</span></span> <span data-ttu-id="d490d-139">hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 함께 hello hello 서비스에 암호화 된 blob 메타 데이터를 blob으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-139">hello wrapped CEK and some additional encryption metadata are then stored as blob metadata along with hello encrypted blob on hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="d490d-140">편집 하거나 hello blob에 대 한 사용자 고유의 메타 데이터를 업로드 하는 경우 tooensure이 메타이 데이터는 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-140">If you are editing or uploading your own metadata for hello blob, you need tooensure that this metadata is preserved.</span></span> <span data-ttu-id="d490d-141">이 메타 데이터 없이 새 메타 데이터를 업로드 하는 경우 래핑된 CEK hello, IV 및 기타 메타 데이터는 손실 됩니다 및 hello blob 콘텐츠를 절대로 다시 검색할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-141">If you upload new metadata without this metadata, hello wrapped CEK, IV and other metadata will be lost and hello blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="d490d-142">Hello를 사용 하 여 hello 전체 blob의 hello 콘텐츠를 검색에서는 암호화 된 blob 다운로드 **가져오기*** 편의 메서드.</span><span class="sxs-lookup"><span data-stu-id="d490d-142">Downloading an encrypted blob involves retrieving hello content of hello entire blob using hello **get*** convenience methods.</span></span> <span data-ttu-id="d490d-143">래핑된 CEK 래핑이 해제 하 고 hello IV와 함께 사용 하는 hello (으로 저장 blob 메타 데이터가 예제의) tooreturn hello 암호 해독 데이터 toohello 사용자.</span><span class="sxs-lookup"><span data-stu-id="d490d-143">hello wrapped CEK is unwrapped and used together with hello IV (stored as blob metadata in this case) tooreturn hello decrypted data toohello users.</span></span>

<span data-ttu-id="d490d-144">임의의 범위를 다운로드 (**가져오기*** 범위 매개 변수가 있는 메서드에 전달 된) hello에서 암호화 된 blob의 순서 tooget 약간의 추가 데이터는 사용할 수 있는 사용자가 제공 된 hello 범위를 조정 하려면 toosuccessfully decrypt hello 범위를 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-144">Downloading an arbitrary range (**get*** methods with range parameters passed in) in hello encrypted blob involves adjusting hello range provided by users in order tooget a small amount of additional data that can be used toosuccessfully decrypt hello requested range.</span></span>

<span data-ttu-id="d490d-145">이 스키마를 사용하여 블록 Blob 및 페이지 Blob만 암호화/암호 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-145">Block blobs and page blobs only can be encrypted/decrypted using this scheme.</span></span> <span data-ttu-id="d490d-146">추가 Blob에 대한 암호화 지원은 현재 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-146">There is currently no support for encrypting append blobs.</span></span>

### <a name="queues"></a><span data-ttu-id="d490d-147">큐</span><span class="sxs-lookup"><span data-stu-id="d490d-147">Queues</span></span>
<span data-ttu-id="d490d-148">큐 메시지의 모든 형식이 될 수, 있으므로 hello 클라이언트 라이브러리 hello 메시지 텍스트에 IV (Initialization Vector) hello 및 hello 암호화 된 콘텐츠 암호화 키 (CEK) 포함 된 사용자 지정 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-148">Since queue messages can be of any format, hello client library defines a custom format that includes hello Initialization Vector (IV) and hello encrypted content encryption key (CEK) in hello message text.</span></span>

<span data-ttu-id="d490d-149">암호화 하는 동안 hello 클라이언트 라이브러리는 32 바이트의 임의 CEK 함께 16 바이트의 임의 IV를 생성 하 고이 정보를 사용 하 여 hello 큐 메시지 텍스트의 봉투 (envelope) 암호화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-149">During encryption, hello client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of hello queue message text using this information.</span></span> <span data-ttu-id="d490d-150">hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 toohello 암호화 된 큐 메시지 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-150">hello wrapped CEK and some additional encryption metadata are then added toohello encrypted queue message.</span></span> <span data-ttu-id="d490d-151">(아래 참조)이 수정 된 메시지는 hello 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-151">This modified message (shown below) is stored on hello service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="d490d-152">암호 해독 하는 동안 hello 래핑된 키 hello 큐 메시지에서 추출 되며 래핑이 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-152">During decryption, hello wrapped key is extracted from hello queue message and unwrapped.</span></span> <span data-ttu-id="d490d-153">또한 hello IV hello 큐 메시지에서 추출 된 이며 래핑이 해제 hello 키 toodecrypt hello 큐 메시지 데이터와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-153">hello IV is also extracted from hello queue message and used along with hello unwrapped key toodecrypt hello queue message data.</span></span> <span data-ttu-id="d490d-154">Hello 암호화 메타 데이터를 작으면 (500 바이트의 경우) 아래 큐 메시지에 대 한 hello 64KB 제한에 대해 계산지 않습니다 것, hello 영향을 관리할 수 있어야 하므로 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-154">Note that hello encryption metadata is small (under 500 bytes), so while it does count toward hello 64KB limit for a queue message, hello impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="d490d-155">테이블</span><span class="sxs-lookup"><span data-stu-id="d490d-155">Tables</span></span>
<span data-ttu-id="d490d-156">삽입을 위한 엔터티 속성의 클라이언트 라이브러리 지원 암호화 hello 및 교체 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-156">hello client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="d490d-157">병합은 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-157">Merge is not currently supported.</span></span> <span data-ttu-id="d490d-158">속성 하위 집합 암호화 된 다른 키를 사용 하 여 이전에, 이후 hello 새 속성을 병합 하 고 hello 메타 데이터를 업데이트 하기만 하면 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-158">Since a subset of properties may have been encrypted previously using a different key, simply merging hello new properties and updating hello metadata will result in data loss.</span></span> <span data-ttu-id="d490d-159">Hello 서비스에서 tooread hello 기존 엔터티를 호출 추가 서비스를 만드는 또는 속성 당 새 키를 사용 하는 적합 하지 않은 성능상의 이유로 필요 하거나 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-159">Merging either requires making extra service calls tooread hello pre-existing entity from hello service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="d490d-160">테이블 데이터 암호화는 다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-160">Table data encryption works as follows:</span></span>

1. <span data-ttu-id="d490d-161">사용자가 hello 속성 toobe 암호화를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-161">Users specify hello properties toobe encrypted.</span></span>
2. <span data-ttu-id="d490d-162">hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector)의 모든 엔터티에 대 한 32 바이트 (CEK) 임의의 콘텐츠 암호화 키와 함께 16 바이트를 생성 하 고 hello 개별 속성 toobe 당 새 IV를 파생 하 여 암호화에서 봉투 (envelope) 암호화를 수행 합니다. 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-162">hello client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on hello individual properties toobe encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="d490d-163">암호화 된 hello 속성 이진 데이터로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-163">hello encrypted property is stored as binary data.</span></span>
3. <span data-ttu-id="d490d-164">hello CEK 되 고 그런 다음 몇 가지 추가 암호화 메타 데이터는 두 개의 추가 예약 된 속성으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-164">hello wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="d490d-165">먼저 예약 된 hello 속성 (\_ClientEncryptionMetadata1)은 4, 버전 및 래핑된 키에 대 한 hello 정보를 보유 하는 문자열 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-165">hello first reserved property (\_ClientEncryptionMetadata1) is a string property that holds hello information about IV, version, and wrapped key.</span></span> <span data-ttu-id="d490d-166">두 번째 예약된 속성 hello (\_ClientEncryptionMetadata2) 암호화 된 hello 속성에 대 한 hello 정보를 보유 하는 이진 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-166">hello second reserved property (\_ClientEncryptionMetadata2) is a binary property that holds hello information about hello properties that are encrypted.</span></span> <span data-ttu-id="d490d-167">이 두 번째 속성에 대 한 정보를 hello (\_ClientEncryptionMetadata2) 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-167">hello information in this second property (\_ClientEncryptionMetadata2) is itself encrypted.</span></span>
4. <span data-ttu-id="d490d-168">Toothese 추가 예약 된 속성 암호화에 필요, 인해 이제가 있습니다 252 대신 사용자 지정 속성을 250만.</span><span class="sxs-lookup"><span data-stu-id="d490d-168">Due toothese additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="d490d-169">hello hello 엔터티의 전체 크기는 1MB 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-169">hello total size of hello entity must be less than 1MB.</span></span>
   
   <span data-ttu-id="d490d-170">문자열 속성만 암호화 할 수 있다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="d490d-170">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="d490d-171">다른 유형의 속성 암호화 toobe 인 경우 변환 된 toostrings 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-171">If other types of properties are toobe encrypted, they must be converted toostrings.</span></span> <span data-ttu-id="d490d-172">이진 속성으로 암호화 하는 hello 문자열 hello 서비스에 저장 됩니다 및 암호 해독 한 후 뒤로 toostrings (EdmType.STRING 형식과 EntityProperties 하지 원시 문자열) 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-172">hello encrypted strings are stored on hello service as binary properties, and they are converted back toostrings (raw strings, not EntityProperties with type EdmType.STRING) after decryption.</span></span>
   
   <span data-ttu-id="d490d-173">테이블의 경우 또한 toohello 암호화 정책 사용자 지정 해야 hello 속성 toobe 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-173">For tables, in addition toohello encryption policy, users must specify hello properties toobe encrypted.</span></span> <span data-ttu-id="d490d-174">이 중 하나를 저장 하 여 이러한 속성 유형 집합 tooEdmType.STRING hello 사용 하 여 TableEntity 개체에서 수행할 수 있습니다 및 집합 tootrue 또는 설정 hello encryption_resolver_function hello tableservice 개체에 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-174">This can be done by either storing these properties in TableEntity objects with hello type set tooEdmType.STRING and encrypt set tootrue or setting hello encryption_resolver_function on hello tableservice object.</span></span> <span data-ttu-id="d490d-175">암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는 부울을 반환하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-175">An encryption resolver is a function that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="d490d-176">암호화 하는 동안 toohello 통신에 쓰는 동안 속성을 암호화 해야 하는지 여부를 hello 클라이언트 라이브러리 정보 toodecide이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-176">During encryption, hello client library will use this information toodecide whether a property should be encrypted while writing toohello wire.</span></span> <span data-ttu-id="d490d-177">또한 hello 대리자 hello 가능성은 속성이 암호화 주위 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-177">hello delegate also provides for hello possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="d490d-178">(예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 한다는 확인은 필요 하지 않은 tooprovide 읽기 또는 엔터티를 쿼리 하는 동안이 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-178">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary tooprovide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="d490d-179">배치 작업</span><span class="sxs-lookup"><span data-stu-id="d490d-179">Batch Operations</span></span>
<span data-ttu-id="d490d-180">하나의 암호화 정책이 hello 일괄 처리의 tooall 행을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-180">One encryption policy applies tooall rows in hello batch.</span></span> <span data-ttu-id="d490d-181">hello 클라이언트 라이브러리 새 임의 IV와 행당 임의 CEK hello 일괄 처리에서 내부적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-181">hello client library will internally generate a new random IV and random CEK per row in hello batch.</span></span> <span data-ttu-id="d490d-182">사용자가 선택할 수도 tooencrypt 모든 작업에 대해 서로 다른 속성 hello 일괄 처리의 hello 암호화 해결 프로그램에서이 동작을 정의 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-182">Users can also choose tooencrypt different properties for every operation in hello batch by defining this behavior in hello encryption resolver.</span></span>
<span data-ttu-id="d490d-183">컨텍스트 관리자는 hello tableservice batch() 메서드를 통해 일괄 처리를 만든 경우 hello tableservice 암호화 정책에 자동으로 적용 된 toohello 일괄 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-183">If a batch is created as a context manager through hello tableservice batch() method, hello tableservice's encryption policy will automatically be applied toohello batch.</span></span> <span data-ttu-id="d490d-184">일괄 처리를를 만드는 경우 명시적으로 hello 생성자를 호출 하 여 hello 암호화 정책 hello 일괄 처리의 hello 수명에 대 한 수정 되지 않은 왼쪽 매개 변수로 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-184">If a batch is created explicitly by calling hello constructor, hello encryption policy must be passed as a parameter and left unmodified for hello lifetime of hello batch.</span></span>
<span data-ttu-id="d490d-185">Note hello 일괄 처리의 암호화 정책 (엔터티는 hello tableservice 암호화 정책을 사용 하 여 hello 일괄 처리를 커밋할 hello 시 암호화 되지 않습니다)를 사용 하 여 hello 일괄 처리에 삽입 될 때 엔터티 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-185">Note that entities are encrypted as they are inserted into hello batch using hello batch's encryption policy (entities are NOT encrypted at hello time of committing hello batch using hello tableservice's encryption policy).</span></span>

### <a name="queries"></a><span data-ttu-id="d490d-186">쿼리</span><span class="sxs-lookup"><span data-stu-id="d490d-186">Queries</span></span>
<span data-ttu-id="d490d-187">tooperform 쿼리 작업 수 tooresolve 있는 키 해결 프로그램을 지정 해야 모든 hello hello 결과 집합의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-187">tooperform query operations, you must specify a key resolver that is able tooresolve all hello keys in hello result set.</span></span> <span data-ttu-id="d490d-188">Hello 쿼리 결과에 포함 된 엔터티 해결된 tooa 공급자 일 수 없습니다, hello 클라이언트 라이브러리는 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-188">If an entity contained in hello query result cannot be resolved tooa provider, hello client library will throw an error.</span></span> <span data-ttu-id="d490d-189">서버 쪽 프로젝션을 수행 하는 모든 쿼리에 대 한 hello 클라이언트 라이브러리 hello 특수 한 암호화 메타 데이터 속성을 추가 합니다 (\_ClientEncryptionMetadata1 및 \_ClientEncryptionMetadata2) toohello 기본적으로 열을 선택 .</span><span class="sxs-lookup"><span data-stu-id="d490d-189">For any query that performs server side projections, hello client library will add hello special encryption metadata properties (\_ClientEncryptionMetadata1 and \_ClientEncryptionMetadata2) by default toohello selected columns.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d490d-190">클라이언트 쪽 암호화를 사용할 때는 이러한 중요점을 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="d490d-190">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="d490d-191">읽기 또는 쓰기 tooan 암호화 경우 blob, 전체 blob 업로드 명령을 사용 하 여 및 범위/전체 blob 다운로드 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-191">When reading from or writing tooan encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="d490d-192">블록 배치, 블록 목록 배치, 페이지 쓰기 또는 지우기 페이지; 등의 프로토콜 작업을 사용 하 여 tooan 암호화 된 blob에 쓰기 방지 그렇지 않으면 hello 암호화 blob를 손상 하 고 읽을 수 없도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-192">Avoid writing tooan encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, or Clear Pages; otherwise you may corrupt hello encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="d490d-193">테이블의 경우에는 유사한 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-193">For tables, a similar constraint exists.</span></span> <span data-ttu-id="d490d-194">Hello 암호화 메타 데이터를 업데이트 하지 않고 toonot 신중 하 게 암호화 하는 업데이트 속성 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-194">Be careful toonot update encrypted properties without updating hello encryption metadata.</span></span>
> * <span data-ttu-id="d490d-195">Hello 암호화 된 blob에서 메타 데이터를 설정 하는 경우 hello 암호화 관련에 필요한 메타 데이터 암호 해독, 가산적가 메타 데이터를 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-195">If you set metadata on hello encrypted blob, you may overwrite hello encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="d490d-196">이것은 스냅숏에 대해서 마찬가지입니다. 암호화된 blob의 스냅숏을 생성하는 동안 메타데이터를 지정하지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="d490d-196">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="d490d-197">메타 데이터와 설정 해야 하는 경우 수 있는지 toocall hello **get_blob_metadata** 메서드 첫 번째 tooget hello 현재 암호화 메타 데이터 및 메타 데이터 설정 되어 있는 동안 동시 쓰기를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-197">If metadata must be set, be sure toocall hello **get_blob_metadata** method first tooget hello current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>
> * <span data-ttu-id="d490d-198">Hello를 사용 하도록 설정 **require_encryption** 암호화 된 데이터에만 작동 해야 하는 사용자에 대 한 hello 서비스 개체에 대 한 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-198">Enable hello **require_encryption** flag on hello service object for users that should work only with encrypted data.</span></span> <span data-ttu-id="d490d-199">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d490d-199">See below for more info.</span></span>
> 
> 

<span data-ttu-id="d490d-200">hello 저장소 클라이언트 라이브러리는 hello 제공 하 고 KEK 키 확인자 인터페이스 뒤 tooimplement hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-200">hello storage client library expects hello provided KEK and key resolver tooimplement hello following interface.</span></span> <span data-ttu-id="d490d-201">[Azure 주요 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 지원이 보류 중이며, 완료 시 이 라이브러리에 통합될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-201">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) support for Python KEK management is pending and will be integrated into this library when completed.</span></span>

## <a name="client-api--interface"></a><span data-ttu-id="d490d-202">클라이언트 API / 인터페이스</span><span class="sxs-lookup"><span data-stu-id="d490d-202">Client API / Interface</span></span>
<span data-ttu-id="d490d-203">저장소 서비스 개체 (예: blockblobservice)를 만든 후 hello 사용자 수 값을 할당할 암호화 정책을 구성 하는 toohello 필드: key_encryption_key, key_resolver_function, 및 require_encryption 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-203">After a storage service object (i.e. blockblobservice) has been created, hello user may assign values toohello fields that constitute an encryption policy: key_encryption_key, key_resolver_function, and require_encryption.</span></span> <span data-ttu-id="d490d-204">사용자는 KEK만, 확인자만 또는 둘 다를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-204">Users can provide only a KEK, only a resolver, or both.</span></span> <span data-ttu-id="d490d-205">key_encryption_key 형식이 hello 기본 키에 대 한 래핑/hello 논리를 제공 하 고 키 식별자를 사용 하 여 식별 되는.</span><span class="sxs-lookup"><span data-stu-id="d490d-205">key_encryption_key is hello basic key type that is identified using a key identifier and that provides hello logic for wrapping/unwrapping.</span></span> <span data-ttu-id="d490d-206">key_resolver_function은 hello 암호 해독 프로세스 동안 사용 되는 tooresolve 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-206">key_resolver_function is used tooresolve a key during hello decryption process.</span></span> <span data-ttu-id="d490d-207">지정된 키 식별자에 대해 유효한 KEK를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-207">It returns a valid KEK given a key identifier.</span></span> <span data-ttu-id="d490d-208">여러 위치에서 관리 되는 여러 키 간의 사용자 hello 기능 toochoose를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-208">This provides users hello ability toochoose between multiple keys that are managed in multiple locations.</span></span>

<span data-ttu-id="d490d-209">hello KEK hello 다음을 구현 해야 메서드 toosuccessfully 데이터를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-209">hello KEK must implement hello following methods toosuccessfully encrypt data:</span></span>

* <span data-ttu-id="d490d-210">wrap_key(cek): 래핑하고 hello hello 사용자가 선택한 알고리즘을 사용 하 여 CEK (바이트)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-210">wrap_key(cek): Wraps hello specified CEK (bytes) using an algorithm of hello user's choice.</span></span> <span data-ttu-id="d490d-211">반환 hello 래핑된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-211">Returns hello wrapped key.</span></span>
* <span data-ttu-id="d490d-212">get_key_wrap_algorithm(): 반환 hello 알고리즘 toowrap 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-212">get_key_wrap_algorithm(): Returns hello algorithm used toowrap keys.</span></span>
* <span data-ttu-id="d490d-213">get_kid(): hello 문자열 키 id를 반환이이 KEK에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-213">get_kid(): Returns hello string key id for this KEK.</span></span>
  <span data-ttu-id="d490d-214">hello KEK hello 같은 toosuccessfully decrypt 데이터가 메서드를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-214">hello KEK must implement hello following methods toosuccessfully decrypt data:</span></span>
* <span data-ttu-id="d490d-215">(cek, 알고리즘) unwrap_key: 반환 래핑이 해제 hello 형태의 hello hello 문자열이 지정 알고리즘을 사용 하 여 CEK를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-215">unwrap_key(cek, algorithm): Returns hello unwrapped form of hello specified CEK using hello string-specified algorithm.</span></span>
* <span data-ttu-id="d490d-216">get_kid(): 이 KEK에 대한 문자열 키 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-216">get_kid(): Returns a string key id for this KEK.</span></span>

<span data-ttu-id="d490d-217">hello 키 해결 프로그램에 반환 하는 메서드, 키 id를 지정 된 hello 해당 KEK 구현 hello 인터페이스 위의 구현 이상 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-217">hello key resolver must at least implement a method that, given a key id, returns hello corresponding KEK implementing hello interface above.</span></span> <span data-ttu-id="d490d-218">만이 방법은 toobe toohello key_resolver_function 속성이 hello 서비스 개체에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-218">Only this method is toobe assigned toohello key_resolver_function property on hello service object.</span></span>

* <span data-ttu-id="d490d-219">암호화, hello 키가 항상 사용 하 고 키 hello 없을 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-219">For encryption, hello key is used always and hello absence of a key will result in an error.</span></span>
* <span data-ttu-id="d490d-220">암호를 해독하려면</span><span class="sxs-lookup"><span data-stu-id="d490d-220">For decryption:</span></span>
  
  * <span data-ttu-id="d490d-221">hello 키 확인자 tooget hello 키를 지정 하는 경우 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-221">hello key resolver is invoked if specified tooget hello key.</span></span> <span data-ttu-id="d490d-222">가 지정 hello 확인자 hello 키 식별자에 대 한 매핑이 없는 경우 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-222">If hello resolver is specified but does not have a mapping for hello key identifier, an error is thrown.</span></span>
  * <span data-ttu-id="d490d-223">해결 프로그램 지정 하지 않으면 표시 되지만 키가 지정 하는 경우 해당 식별자에는 필요한 hello 키 식별자와 일치 하는 경우 hello 키는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-223">If resolver is not specified but a key is specified, hello key is used if its identifier matches hello required key identifier.</span></span> <span data-ttu-id="d490d-224">Hello 식별자와 일치 하지 않는 경우 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-224">If hello identifier does not match, an error is thrown.</span></span>
    
    <span data-ttu-id="d490d-225">azure.storage.samples의 암호화 샘플 hello <fix URL>blob, 큐 및 테이블에 대 한 보다 자세한 종단 간 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-225">hello encryption samples in azure.storage.samples <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables.</span></span>
      <span data-ttu-id="d490d-226">KEK hello 및 키 해결 프로그램의 예제 구현은 각각 KeyWrapper 및 KeyResolver hello 샘플 파일에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-226">Sample implementations of hello KEK and key resolver are provided in hello sample files as KeyWrapper and KeyResolver respectively.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="d490d-227">RequireEncryption 모드</span><span class="sxs-lookup"><span data-stu-id="d490d-227">RequireEncryption mode</span></span>
<span data-ttu-id="d490d-228">사용자는 모든 업로드 및 다운로드를 암호화해야 할 경우 작업 모드를 선택적으로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-228">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="d490d-229">이 모드에서는 hello 서비스에서 암호화 되지 않은 한 암호화 정책 또는 다운로드 데이터 없이 시도 tooupload 데이터는 클라이언트 hello에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-229">In this mode, attempts tooupload data without an encryption policy or download data that is not encrypted on hello service will fail on hello client.</span></span> <span data-ttu-id="d490d-230">hello **require_encryption** hello 서비스 개체를 컨트롤에이 동작을 플래그 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-230">hello **require_encryption** flag on hello service object controls this behavior.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="d490d-231">Blob 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="d490d-231">Blob service encryption</span></span>
<span data-ttu-id="d490d-232">Hello blockblobservice 개체에 hello 암호화 정책 필드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-232">Set hello encryption policy fields on hello blockblobservice object.</span></span> <span data-ttu-id="d490d-233">다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-233">Everything else will be handled by hello client library internally.</span></span>

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a><span data-ttu-id="d490d-234">큐 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="d490d-234">Queue service encryption</span></span>
<span data-ttu-id="d490d-235">Hello queueservice 개체에 hello 암호화 정책 필드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-235">Set hello encryption policy fields on hello queueservice object.</span></span> <span data-ttu-id="d490d-236">다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-236">Everything else will be handled by hello client library internally.</span></span>

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a><span data-ttu-id="d490d-237">테이블 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="d490d-237">Table service encryption</span></span>
<span data-ttu-id="d490d-238">또한 암호화 정책 toocreating 및 요청 옵션에 설정 지정는 **encryption_resolver_function** hello에 **tableservice**, 또는에서 특성을 암호화 하는 집합 hello hello EntityProperty 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-238">In addition toocreating an encryption policy and setting it on request options, you must either specify an **encryption_resolver_function** on hello **tableservice**, or set hello encrypt attribute on hello EntityProperty.</span></span>

### <a name="using-hello-resolver"></a><span data-ttu-id="d490d-239">Hello 확인자를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d490d-239">Using hello resolver</span></span>

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a><span data-ttu-id="d490d-240">특성을 사용하여</span><span class="sxs-lookup"><span data-stu-id="d490d-240">Using attributes</span></span>
<span data-ttu-id="d490d-241">EntityProperty 개체에 저장 하 여 암호화에 대 한 속성이 표시 될 위에서 설명 했 듯이 하 고 필드 암호화 hello 설정.</span><span class="sxs-lookup"><span data-stu-id="d490d-241">As mentioned above, a property may be marked for encryption by storing it in an EntityProperty object and setting hello encrypt field.</span></span>

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a><span data-ttu-id="d490d-242">암호화 및 성능</span><span class="sxs-lookup"><span data-stu-id="d490d-242">Encryption and performance</span></span>
<span data-ttu-id="d490d-243">저장소 데이터를 암호화하면 추가 성능 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-243">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="d490d-244">hello 콘텐츠 키와 IV를 생성 해야, hello 콘텐츠 자체 암호화, 및 추가 메타 데이터를 포맷 하 고 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-244">hello content key and IV must be generated, hello content itself must be encrypted, and additional metadata must be formatted and uploaded.</span></span> <span data-ttu-id="d490d-245">이 오버 헤드는 암호화 되는 데이터의 hello 양에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-245">This overhead will vary depending on hello quantity of data being encrypted.</span></span> <span data-ttu-id="d490d-246">고객은 항상 개발 중에 응용 프로그램 성능을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d490d-246">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d490d-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d490d-247">Next steps</span></span>
* <span data-ttu-id="d490d-248">Hello 다운로드 [Java PyPi 패키지에 대 한 Azure 저장소 클라이언트 라이브러리](https://pypi.python.org/pypi/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="d490d-248">Download hello [Azure Storage Client Library for Java PyPi package](https://pypi.python.org/pypi/azure-storage)</span></span>
* <span data-ttu-id="d490d-249">Hello 다운로드 [GitHub에서 Python 소스 코드에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-python)</span><span class="sxs-lookup"><span data-stu-id="d490d-249">Download hello [Azure Storage Client Library for Python Source Code from GitHub](https://github.com/Azure/azure-storage-python)</span></span>
