---
title: "aaaUsing 공유 액세스 서명 (SAS) Azure 저장소에 | Microsoft Docs"
description: "Toouse 공유 액세스 서명 (SAS) toodelegate tooAzure 저장소 리소스에 액세스, blob, 큐, 테이블, 파일 등을 알아봅니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a><span data-ttu-id="51252-103">SAS(공유 액세스 서명) 사용</span><span class="sxs-lookup"><span data-stu-id="51252-103">Using shared access signatures (SAS)</span></span>

<span data-ttu-id="51252-104">공유 액세스 서명 (SAS) 사용 하면 저장소 계정의 방법 toogrant 제한 된 액세스 tooobjects tooother 클라이언트 계정 키를 노출 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-104">A shared access signature (SAS) provides you with a way toogrant limited access tooobjects in your storage account tooother clients, without exposing your account key.</span></span> <span data-ttu-id="51252-105">이 문서에서는 hello SAS 모델의 개요를 제공, SAS 모범 사례를 검토 하 고 몇 가지 예를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="51252-105">In this article, we provide an overview of hello SAS model, review SAS best practices, and look at some examples.</span></span>

<span data-ttu-id="51252-106">SAS를 사용 하 여 여기에 제시 된 것 이상의 추가 코드 예제를 보려면 [.NET에서 Azure Blob 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) 및 hello에서 사용할 수 있는 다른 샘플 [Azure 코드 예제](https://azure.microsoft.com/documentation/samples/?service=storage) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-106">For additional code examples using SAS beyond those presented here, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) and other samples available in hello [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage) library.</span></span> <span data-ttu-id="51252-107">Hello 예제 응용 프로그램을 다운로드 하 고 실행 하거나 GitHub에서 hello 코드를 찾아보려면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-107">You can download hello sample applications and run them, or browse hello code on GitHub.</span></span>

## <a name="what-is-a-shared-access-signature"></a><span data-ttu-id="51252-108">공유 액세스 서명이란?</span><span class="sxs-lookup"><span data-stu-id="51252-108">What is a shared access signature?</span></span>
<span data-ttu-id="51252-109">공유 액세스 서명은 저장소 계정에 위임 된 액세스 tooresources를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-109">A shared access signature provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="51252-110">SAS를 클라이언트에 계정 키를 공유 하지 않고 저장소 계정의 tooresources 액세스할을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-110">With a SAS, you can grant clients access tooresources in your storage account, without sharing your account keys.</span></span> <span data-ttu-id="51252-111">이 hello 중요 한 점은 응용 프로그램-SAS에서에서 공유 액세스 서명을 사용 하 여 안전 하 게 tooshare 계정 키를 손상 시 키 지 않고 저장소 리소스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-111">This is hello key point of using shared access signatures in your applications--a SAS is a secure way tooshare your storage resources without compromising your account keys.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

<span data-ttu-id="51252-112">SAS를 세밀 하 게 hello 유형의 tooclients SAS를 포함 하 여 hello 있는 권한을 부여 하는 액세스 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-112">A SAS gives you granular control over hello type of access you grant tooclients who have hello SAS, including:</span></span>

* <span data-ttu-id="51252-113">SAS는 hello를 통해 유효한 hello 시작 시간 및 hello 만료 시간을 포함 하는 hello 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-113">hello interval over which hello SAS is valid, including hello start time and hello expiry time.</span></span>
* <span data-ttu-id="51252-114">hello hello SAS 부여 된 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-114">hello permissions granted by hello SAS.</span></span> <span data-ttu-id="51252-115">예를 들어 blob에 대 한 SAS 수 읽기 권한을 부여 및 권한 toothat blob 쓰지만 삭제 권한은 부여 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-115">For example, a SAS for a blob might grant read and write permissions toothat blob, but not delete permissions.</span></span>
* <span data-ttu-id="51252-116">선택적 IP 주소 또는 IP 주소 범위에서 Azure 저장소를 수락할 SAS hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-116">An optional IP address or range of IP addresses from which Azure Storage will accept hello SAS.</span></span> <span data-ttu-id="51252-117">예를 들어 tooyour 조직에 속한 IP 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-117">For example, you might specify a range of IP addresses belonging tooyour organization.</span></span>
* <span data-ttu-id="51252-118">Azure 저장소는 hello SAS을 수락 하는 데는 hello 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-118">hello protocol over which Azure Storage will accept hello SAS.</span></span> <span data-ttu-id="51252-119">HTTPS를 사용 하 여이 선택적 매개 변수 toorestrict 액세스 tooclients를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-119">You can use this optional parameter toorestrict access tooclients using HTTPS.</span></span>

## <a name="when-should-you-use-a-shared-access-signature"></a><span data-ttu-id="51252-120">공유 액세스 서명은 언제 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="51252-120">When should you use a shared access signature?</span></span>
<span data-ttu-id="51252-121">저장소 계정의 액세스 키를 소유 하지 저장소 계정 tooany 클라이언트에서 tooprovide 액세스 tooresources 하려는 경우 SAS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-121">You can use a SAS when you want tooprovide access tooresources in your storage account tooany client not possessing your storage account's access keys.</span></span> <span data-ttu-id="51252-122">저장소 계정에는 tooyour 계정 관리 액세스를 부여 하는 기본 및 보조 액세스 키와 그 안에 있는 모든 리소스를 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-122">Your storage account includes both a primary and secondary access key, both of which grant administrative access tooyour account, and all resources within it.</span></span> <span data-ttu-id="51252-123">이러한 키를 노출 악성 또는 부주의로 사용 하 여 사용자 계정 toohello 가능성이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="51252-123">Exposing either of these keys opens your account toohello possibility of malicious or negligent use.</span></span> <span data-ttu-id="51252-124">공유 액세스 서명을 toohello 권한을 명시적으로 부여 하지에 따라 저장소 계정에 및 계정 키에 대 한 필요 없이 tooread, 쓰기 및 삭제 데이터 클라이언트를 허용 하는 안전한 좋은 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-124">Shared access signatures provide a safe alternative that allows clients tooread, write, and delete data in your storage account according toohello permissions you've explicitly granted, and without need for an account key.</span></span>

<span data-ttu-id="51252-125">SAS를 유용 하는 일반적인 시나리오는 서비스 사용자가 읽고 쓰는 자신의 데이터 tooyour 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-125">A common scenario where a SAS is useful is a service where users read and write their own data tooyour storage account.</span></span> <span data-ttu-id="51252-126">저장소 계정에 사용자 데이터를 저장하는 시나리오에는 다음과 같은 두 가지 일반적인 디자인 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-126">In a scenario where a storage account stores user data, there are two typical design patterns:</span></span>

1. <span data-ttu-id="51252-127">클라이언트는 인증을 수행하는 프런트 엔드 프록시 서비스를 통해 데이터를 업로드하고 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-127">Clients upload and download data via a front-end proxy service, which performs authentication.</span></span> <span data-ttu-id="51252-128">이 프런트 엔드 프록시 서비스에 비즈니스 규칙 유효성 검사 수 hello 이점이 있지만 데이터 또는 대규모 트랜잭션을, 많은 양의 대 한 toomatch 수요를 확장할 수 있는 서비스를 만드는 수도 비용이 많이 드는 하거나 어려운 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-128">This front-end proxy service has hello advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale toomatch demand may be expensive or difficult.</span></span>

  ![시나리오 다이어그램: 프런트 엔드 프록시 서비스](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. <span data-ttu-id="51252-130">필요에 따라 hello 클라이언트를 인증 하 고 SAS를 생성 하는 간단한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-130">A lightweight service authenticates hello client as needed and then generates a SAS.</span></span> <span data-ttu-id="51252-131">Hello 클라이언트 hello SAS를 받을 저장소 계정 리소스에 의해 정의 hello SAS hello SAS에서 허용 하는 hello 간격에 대 한 hello 권한으로 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-131">Once hello client receives hello SAS, they can access storage account resources directly with hello permissions defined by hello SAS and for hello interval allowed by hello SAS.</span></span> <span data-ttu-id="51252-132">hello SAS 완화 hello 프런트 엔드 모드 해제 프록시 서비스를 통해 모든 데이터를 라우팅에 대 한 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-132">hello SAS mitigates hello need for routing all data through hello front-end proxy service.</span></span>

  ![시나리오 다이어그램: SAS 공급자 서비스](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

<span data-ttu-id="51252-134">대부분의 실제 서비스에서는 이러한 두 가지 방법을 혼합하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-134">Many real-world services may use a hybrid of these two approaches.</span></span> <span data-ttu-id="51252-135">예를 들어 일부 데이터 처리 및 hello 프런트 엔드 프록시를 통해 다른 데이터 저장 하거나 SAS를 사용 하 여 직접 읽는 동안 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-135">For example, some data might be processed and validated via hello front-end proxy, while other data is saved and/or read directly using SAS.</span></span>

<span data-ttu-id="51252-136">또한 toouse SAS tooauthenticate hello 원본 개체를 특정 시나리오에서 복사 작업에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-136">Additionally, you will need toouse a SAS tooauthenticate hello source object in a copy operation in certain scenarios:</span></span>

* <span data-ttu-id="51252-137">다른 저장소 계정에 있는 blob tooanother blob을 복사할 때 SAS tooauthenticate hello 원본 blob를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-137">When you copy a blob tooanother blob that resides in a different storage account, you must use a SAS tooauthenticate hello source blob.</span></span> <span data-ttu-id="51252-138">필요에 따라 SAS tooauthenticate hello 대상 blob도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-138">You can optionally use a SAS tooauthenticate hello destination blob as well.</span></span>
* <span data-ttu-id="51252-139">다른 저장소 계정에 있는 파일 tooanother 파일을 복사할 때 SAS tooauthenticate hello 소스 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-139">When you copy a file tooanother file that resides in a different storage account, you must use a SAS tooauthenticate hello source file.</span></span> <span data-ttu-id="51252-140">필요에 따라 SAS tooauthenticate hello 대상 파일 에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-140">You can optionally use a SAS tooauthenticate hello destination file as well.</span></span>
* <span data-ttu-id="51252-141">Hello 원본 및 대상 개체 내에 있는 hello 동일한 경우에 SAS tooauthenticate hello 원본 개체를 사용 해야 blob tooa 파일 또는 파일 tooa blob을 복사할 때 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-141">When you copy a blob tooa file, or a file tooa blob, you must use a SAS tooauthenticate hello source object, even if hello source and destination objects reside within hello same storage account.</span></span>

## <a name="types-of-shared-access-signatures"></a><span data-ttu-id="51252-142">공유 액세스 서명의 유형</span><span class="sxs-lookup"><span data-stu-id="51252-142">Types of shared access signatures</span></span>
<span data-ttu-id="51252-143">두 가지 유형의 공유 액세스 서명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-143">You can create two types of shared access signatures:</span></span>

* <span data-ttu-id="51252-144">**서비스 SAS**</span><span class="sxs-lookup"><span data-stu-id="51252-144">**Service SAS.**</span></span> <span data-ttu-id="51252-145">hello 서비스 SAS 대리자 tooa 리소스 hello 저장소 서비스 중 하나에 액세스: Blob, 큐, 테이블 또는 파일 서비스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-145">hello service SAS delegates access tooa resource in just one of hello storage services: hello Blob, Queue, Table, or File service.</span></span> <span data-ttu-id="51252-146">참조 [서비스 SAS를 생성할](https://msdn.microsoft.com/library/dn140255.aspx) 및 [서비스의 SAS 예](https://msdn.microsoft.com/library/dn140256.aspx) hello 서비스 SAS 토큰을 생성 하는 방법에 대 한 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-146">See [Constructing a Service SAS](https://msdn.microsoft.com/library/dn140255.aspx) and [Service SAS Examples](https://msdn.microsoft.com/library/dn140256.aspx) for in-depth information about constructing hello service SAS token.</span></span>
* <span data-ttu-id="51252-147">**계정 SAS**</span><span class="sxs-lookup"><span data-stu-id="51252-147">**Account SAS.**</span></span> <span data-ttu-id="51252-148">hello 계정 SAS 대리인 tooresources 하나 이상의 hello 저장소 서비스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-148">hello account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="51252-149">모든 서비스 SAS 통해 사용할 수 있는 hello 작업 계정 SAS 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-149">All of hello operations available via a service SAS are also available via an account SAS.</span></span> <span data-ttu-id="51252-150">또한 hello 계정 SAS에 위임할 수 있습니다 tooa와 같은 특정 서비스, 적용 되는 액세스 toooperations **Get/Set 서비스 속성** 및 **서비스 통계 가져오기**합니다. 또한 액세스 tooread, 쓰기 및 삭제 작업을 blob 컨테이너, 테이블, 큐 및 서비스 SAS와 함께 사용할 수 없는 파일 공유를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-150">Additionally, with hello account SAS, you can delegate access toooperations that apply tooa given service, such as **Get/Set Service Properties** and **Get Service Stats**. You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="51252-151">참조 [계정 SAS를 생성할](https://msdn.microsoft.com/library/mt584140.aspx) hello 계정 SAS 토큰을 생성 하는 방법에 대 한 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-151">See [Constructing an Account SAS](https://msdn.microsoft.com/library/mt584140.aspx) for in-depth information about constructing hello account SAS token.</span></span>

## <a name="how-a-shared-access-signature-works"></a><span data-ttu-id="51252-152">공유 액세스 서명 사용 방법</span><span class="sxs-lookup"><span data-stu-id="51252-152">How a shared access signature works</span></span>
<span data-ttu-id="51252-153">공유 액세스 서명을 tooone 또는 더 많은 저장소 리소스를 가리키는 쿼리 매개 변수는 특별 한 집합을 포함 하는 토큰을 포함 하는 부호 있는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-153">A shared access signature is a signed URI that points tooone or more storage resources and includes a token that contains a special set of query parameters.</span></span> <span data-ttu-id="51252-154">hello 토큰 hello 리소스 hello 클라이언트에서 액세스할 수 있습니다 어떻게 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="51252-154">hello token indicates how hello resources may be accessed by hello client.</span></span> <span data-ttu-id="51252-155">Hello 쿼리 매개 변수 중 하나 서명 hello hello SAS 매개 변수에서 생성 되며 hello 계정 키로 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-155">One of hello query parameters, hello signature, is constructed from hello SAS parameters and signed with hello account key.</span></span> <span data-ttu-id="51252-156">Azure 저장소 tooauthenticate hello SAS이이 서명을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-156">This signature is used by Azure Storage tooauthenticate hello SAS.</span></span>

<span data-ttu-id="51252-157">SAS URI, 표시 된 hello 리소스 URI 및 hello SAS 토큰의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-157">Here's an example of a SAS URI, showing hello resource URI and hello SAS token:</span></span>

![SAS URI의 구성 요소](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

<span data-ttu-id="51252-159">hello SAS 토큰은 hello를 생성 하는 문자열 *클라이언트* 측면 (hello 참조 [SAS 예제](#sas-examples) 코드 예제에 대 한 섹션).</span><span class="sxs-lookup"><span data-stu-id="51252-159">hello SAS token is a string you generate on hello *client* side (see hello [SAS examples](#sas-examples) section for code examples).</span></span> <span data-ttu-id="51252-160">Hello 저장소 클라이언트 라이브러리를 생성 하는 SAS 토큰 예를 들어에서 추적 되지 않은 Azure 저장소에서 어떤 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-160">A SAS token you generate with hello storage client library, for example, is not tracked by Azure Storage in any way.</span></span> <span data-ttu-id="51252-161">SAS 토큰 개수에 제한 없이 hello 클라이언트 쪽에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-161">You can create an unlimited number of SAS tokens on hello client side.</span></span>

<span data-ttu-id="51252-162">요청의 일부로 SAS URI tooAzure 저장소를 제공 하는 클라이언트 hello 서비스가 hello SAS 매개 변수 및 서명 tooverify hello 요청 인증에 대 한 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-162">When a client provides a SAS URI tooAzure Storage as part of a request, hello service checks hello SAS parameters and signature tooverify that it is valid for authenticating hello request.</span></span> <span data-ttu-id="51252-163">Hello 서비스는 hello 서명이 유효한 확인, hello 요청이 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-163">If hello service verifies that hello signature is valid, then hello request is authenticated.</span></span> <span data-ttu-id="51252-164">그렇지 않은 경우 오류 코드 403 (금지 됨)와 함께 hello 요청이 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-164">Otherwise, hello request is declined with error code 403 (Forbidden).</span></span>

## <a name="shared-access-signature-parameters"></a><span data-ttu-id="51252-165">공유 액세스 서명 매개 변수</span><span class="sxs-lookup"><span data-stu-id="51252-165">Shared access signature parameters</span></span>
<span data-ttu-id="51252-166">hello 계정 SAS 및 서비스 SAS 토큰 일부 공통 매개 변수를 포함 하 고 있는 다른 몇 가지 매개 변수를 사용할 수도 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-166">hello account SAS and service SAS tokens include some common parameters, and also take a few parameters that that are different.</span></span>

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a><span data-ttu-id="51252-167">매개 변수 일반적인 tooaccount SAS 및 서비스 SAS 토큰</span><span class="sxs-lookup"><span data-stu-id="51252-167">Parameters common tooaccount SAS and service SAS tokens</span></span>
* <span data-ttu-id="51252-168">**Api 버전** hello 저장소 서비스 버전 toouse tooexecute hello 요청을 지정 하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-168">**Api version** An optional parameter that specifies hello storage service version toouse tooexecute hello request.</span></span>
* <span data-ttu-id="51252-169">**서비스 버전** hello 저장소 서비스 버전 toouse tooauthenticate hello 요청을 지정 하는 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-169">**Service version** A required parameter that specifies hello storage service version toouse tooauthenticate hello request.</span></span>
* <span data-ttu-id="51252-170">**시작 시간.**</span><span class="sxs-lookup"><span data-stu-id="51252-170">**Start time.**</span></span> <span data-ttu-id="51252-171">hello SAS 유효 해지는 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-171">This is hello time at which hello SAS becomes valid.</span></span> <span data-ttu-id="51252-172">공유 액세스 서명에 대 한 hello 시작 시간 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-172">hello start time for a shared access signature is optional.</span></span> <span data-ttu-id="51252-173">시작 시간을 생략 하면 hello SAS 즉시 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-173">If a start time is omitted, hello SAS is effective immediately.</span></span> <span data-ttu-id="51252-174">hello 시작 시간 단위는 UTC (협정 세계시)를 특수 UTC 지정자 ("Z")와 함께 예를 들어 `1994-11-05T13:15:30Z`합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-174">hello start time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z`.</span></span>
* <span data-ttu-id="51252-175">**만료 시간.**</span><span class="sxs-lookup"><span data-stu-id="51252-175">**Expiry time.**</span></span> <span data-ttu-id="51252-176">이후에 hello SAS가 더 이상 유효 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-176">This is hello time after which hello SAS is no longer valid.</span></span> <span data-ttu-id="51252-177">모범 사례에 따라 SAS의 만료 시간을 지정하거나 만료 시간을 저장된 액세스 정책과 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-177">Best practices recommend that you either specify an expiry time for a SAS, or associate it with a stored access policy.</span></span> <span data-ttu-id="51252-178">hello 만료 시간 단위는 UTC (협정 세계시)를 특수 UTC 지정자 ("Z")와 함께 예를 들어 `1994-11-05T13:15:30Z` (아래 참조).</span><span class="sxs-lookup"><span data-stu-id="51252-178">hello expiry time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z` (see more below).</span></span>
* <span data-ttu-id="51252-179">**사용 권한**</span><span class="sxs-lookup"><span data-stu-id="51252-179">**Permissions.**</span></span> <span data-ttu-id="51252-180">hello SAS에 지정 된 hello 권한을 hello 클라이언트 hello SAS를 사용 하 여 hello 저장소 리소스에 대해 수행할 수 있는 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="51252-180">hello permissions specified on hello SAS indicate what operations hello client can perform against hello storage resource using hello SAS.</span></span> <span data-ttu-id="51252-181">사용 가능한 권한은 계정 SAS와 서비스 SAS가 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="51252-181">Available permissions differ for an account SAS and a service SAS.</span></span>
* <span data-ttu-id="51252-182">**IP**</span><span class="sxs-lookup"><span data-stu-id="51252-182">**IP.**</span></span> <span data-ttu-id="51252-183">IP 주소 또는 Azure 외부 범위의 IP 주소를 지정 하는 선택적 매개 변수 (hello 섹션을 참조 [라우팅 세션 구성 상태](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) Express 경로 대 한) tooaccept 요청에서.</span><span class="sxs-lookup"><span data-stu-id="51252-183">An optional parameter that specifies an IP address or a range of IP addresses outside of Azure (see hello section [Routing session configuration state](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) for Express Route) from which tooaccept requests.</span></span>
* <span data-ttu-id="51252-184">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="51252-184">**Protocol.**</span></span> <span data-ttu-id="51252-185">Hello 프로토콜을 지정 하는 선택적 매개 변수는 요청에 대해 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-185">An optional parameter that specifies hello protocol permitted for a request.</span></span> <span data-ttu-id="51252-186">가능한 값은 HTTPS와 HTTP (`https,http`)을 하는 경우 hello 기본값 또는 HTTPS만 (`https`).</span><span class="sxs-lookup"><span data-stu-id="51252-186">Possible values are both HTTPS and HTTP (`https,http`), which is hello default value, or HTTPS only (`https`).</span></span> <span data-ttu-id="51252-187">HTTP만은 허용되는 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="51252-187">Note that HTTP only is not a permitted value.</span></span>
* <span data-ttu-id="51252-188">**서명**</span><span class="sxs-lookup"><span data-stu-id="51252-188">**Signature.**</span></span> <span data-ttu-id="51252-189">hello 서명을 hello에서 구성 된 다른 매개 변수 부분 토큰으로 지정 하 고 다음 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-189">hello signature is constructed from hello other parameters specified as part token and then encrypted.</span></span> <span data-ttu-id="51252-190">Tooauthenticate hello SAS를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-190">It's used tooauthenticate hello SAS.</span></span>

### <a name="parameters-for-a-service-sas-token"></a><span data-ttu-id="51252-191">서비스 SAS 토큰의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="51252-191">Parameters for a service SAS token</span></span>
* <span data-ttu-id="51252-192">**저장소 리소스**</span><span class="sxs-lookup"><span data-stu-id="51252-192">**Storage resource.**</span></span> <span data-ttu-id="51252-193">서비스 SAS를 사용하여 액세스 권한을 위임할 수 있는 저장소 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-193">Storage resources for which you can delegate access with a service SAS include:</span></span>
  * <span data-ttu-id="51252-194">컨테이너 및 Blob</span><span class="sxs-lookup"><span data-stu-id="51252-194">Containers and blobs</span></span>
  * <span data-ttu-id="51252-195">파일 공유 및 파일</span><span class="sxs-lookup"><span data-stu-id="51252-195">File shares and files</span></span>
  * <span data-ttu-id="51252-196">큐</span><span class="sxs-lookup"><span data-stu-id="51252-196">Queues</span></span>
  * <span data-ttu-id="51252-197">테이블 및 테이블 엔터티 범위</span><span class="sxs-lookup"><span data-stu-id="51252-197">Tables and ranges of table entities.</span></span>

### <a name="parameters-for-an-account-sas-token"></a><span data-ttu-id="51252-198">계정 SAS 토큰의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="51252-198">Parameters for an account SAS token</span></span>
* <span data-ttu-id="51252-199">**서비스**</span><span class="sxs-lookup"><span data-stu-id="51252-199">**Service or services.**</span></span> <span data-ttu-id="51252-200">SA 계정 액세스 tooone 또는 그 이상의 hello 저장소 서비스에 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-200">An account SAS can delegate access tooone or more of hello storage services.</span></span> <span data-ttu-id="51252-201">예를 들어 대리자 toohello Blob 및 파일 서비스에 액세스 하는 계정을 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-201">For example, you can create an account SAS that delegates access toohello Blob and File service.</span></span> <span data-ttu-id="51252-202">또는 대리자 tooall 4 개의 서비스 (Blob, 큐, 테이블 및 파일)에 액세스 하는 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-202">Or you can create a SAS that delegates access tooall four services (Blob, Queue, Table, and File).</span></span>
* <span data-ttu-id="51252-203">**저장소 리소스 유형**</span><span class="sxs-lookup"><span data-stu-id="51252-203">**Storage resource types.**</span></span> <span data-ttu-id="51252-204">계정 SAS tooone 또는 특정 리소스 대신 저장소 리소스의 더 많은 클래스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-204">An account SAS applies tooone or more classes of storage resources, rather than a specific resource.</span></span> <span data-ttu-id="51252-205">에 대 한 계정 SAS toodelegate 액세스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-205">You can create an account SAS toodelegate access to:</span></span>
  * <span data-ttu-id="51252-206">서비스 수준 Api를 hello 저장소 계정 리소스에 대해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-206">Service-level APIs, which are called against hello storage account resource.</span></span> <span data-ttu-id="51252-207">예를 들면 **서비스 속성 가져오기/설정**, **서비스 통계 가져오기**, **컨테이너/큐/테이블/공유 나열**이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-207">Examples include **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.</span></span>
  * <span data-ttu-id="51252-208">각 서비스에 대 한 hello 컨테이너 개체에 대해 호출 되는 컨테이너 수준 Api: 컨테이너, 큐, 테이블, blob 및 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-208">Container-level APIs, which are called against hello container objects for each service: blob containers, queues, tables, and file shares.</span></span> <span data-ttu-id="51252-209">예를 들어 **컨테이너 만들기/삭제**, **큐 만들기/삭제**, **테이블 만들기/삭제**, **공유 만들기/삭제**, **Blob/파일 및 디렉터리 나열**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-209">Examples include **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share**, and **List Blobs/Files and Directories**.</span></span>
  * <span data-ttu-id="51252-210">Blob, 큐 메시지, 테이블 엔터티, 파일에 대해 호출되는 개체 수준 API.</span><span class="sxs-lookup"><span data-stu-id="51252-210">Object-level APIs, which are called against blobs, queue messages, table entities, and files.</span></span> <span data-ttu-id="51252-211">예를 들어 **Blob 배치**, **쿼리 엔터티**, **메시지 가져오기**, **파일 만들기**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-211">For example, **Put Blob**, **Query Entity**, **Get Messages**, and **Create File**.</span></span>

## <a name="examples-of-sas-uris"></a><span data-ttu-id="51252-212">SAS URI의 예</span><span class="sxs-lookup"><span data-stu-id="51252-212">Examples of SAS URIs</span></span>

### <a name="service-sas-uri-example"></a><span data-ttu-id="51252-213">서비스 SAS URI 예</span><span class="sxs-lookup"><span data-stu-id="51252-213">Service SAS URI example</span></span>

<span data-ttu-id="51252-214">SAS URI를 제공 하는 한 읽기 및 쓰기 권한을 tooa blob 서비스의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-214">Here is an example of a service SAS URI that provides read and write permissions tooa blob.</span></span> <span data-ttu-id="51252-215">hello 테이블 toohello SAS를 기여 어떻게 hello URI toounderstand의 각 부분 다운이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-215">hello table breaks down each part of hello URI toounderstand how it contributes toohello SAS:</span></span>

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| <span data-ttu-id="51252-216">이름</span><span class="sxs-lookup"><span data-stu-id="51252-216">Name</span></span> | <span data-ttu-id="51252-217">SAS 부분</span><span class="sxs-lookup"><span data-stu-id="51252-217">SAS portion</span></span> | <span data-ttu-id="51252-218">설명</span><span class="sxs-lookup"><span data-stu-id="51252-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51252-219">Blob URI</span><span class="sxs-lookup"><span data-stu-id="51252-219">Blob URI</span></span> |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |<span data-ttu-id="51252-220">hello blob의 hello 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-220">hello address of hello blob.</span></span> <span data-ttu-id="51252-221">HTTPS를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-221">Note that using HTTPS is highly recommended.</span></span> |
| <span data-ttu-id="51252-222">저장소 서비스 버전</span><span class="sxs-lookup"><span data-stu-id="51252-222">Storage services version</span></span> |`sv=2015-04-05` |<span data-ttu-id="51252-223">저장소 서비스 버전 2012-02-12 및 이상 버전에서는이 매개 변수 hello 버전 toouse를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="51252-223">For storage services version 2012-02-12 and later, this parameter indicates hello version toouse.</span></span> |
| <span data-ttu-id="51252-224">시작 시간</span><span class="sxs-lookup"><span data-stu-id="51252-224">Start time</span></span> |`st=2015-04-29T22%3A18%3A26Z` |<span data-ttu-id="51252-225">UTC 시간으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-225">Specified in UTC time.</span></span> <span data-ttu-id="51252-226">원할 경우 hello SAS toobe 유효한 즉시 hello 시작 시간을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-226">If you want hello SAS toobe valid immediately, omit hello start time.</span></span> |
| <span data-ttu-id="51252-227">만료 시간</span><span class="sxs-lookup"><span data-stu-id="51252-227">Expiry time</span></span> |`se=2015-04-30T02%3A23%3A26Z` |<span data-ttu-id="51252-228">UTC 시간으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-228">Specified in UTC time.</span></span> |
| <span data-ttu-id="51252-229">리소스</span><span class="sxs-lookup"><span data-stu-id="51252-229">Resource</span></span> |`sr=b` |<span data-ttu-id="51252-230">hello 리소스는 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-230">hello resource is a blob.</span></span> |
| <span data-ttu-id="51252-231">권한</span><span class="sxs-lookup"><span data-stu-id="51252-231">Permissions</span></span> |`sp=rw` |<span data-ttu-id="51252-232">hello SAS가 부여 하는 hello 권한 Read (r) 포함 및 쓰기 (w).</span><span class="sxs-lookup"><span data-stu-id="51252-232">hello permissions granted by hello SAS include Read (r) and Write (w).</span></span> |
| <span data-ttu-id="51252-233">IP 범위</span><span class="sxs-lookup"><span data-stu-id="51252-233">IP range</span></span> |`sip=168.1.5.60-168.1.5.70` |<span data-ttu-id="51252-234">hello IP 주소 범위를 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-234">hello range of IP addresses from which a request will be accepted.</span></span> |
| <span data-ttu-id="51252-235">프로토콜</span><span class="sxs-lookup"><span data-stu-id="51252-235">Protocol</span></span> |`spr=https` |<span data-ttu-id="51252-236">HTTPS를 사용하는 요청만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-236">Only requests using HTTPS are permitted.</span></span> |
| <span data-ttu-id="51252-237">서명</span><span class="sxs-lookup"><span data-stu-id="51252-237">Signature</span></span> |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |<span data-ttu-id="51252-238">Tooauthenticate 액세스 toohello blob을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-238">Used tooauthenticate access toohello blob.</span></span> <span data-ttu-id="51252-239">hello 서명 문자열 대 기호 및 hello SHA256 알고리즘을 사용 하 여 키를 통해 계산 하 고 다음 Base64 인코딩을 사용 하 여 인코딩된 HMAC입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-239">hello signature is an HMAC computed over a string-to-sign and key using hello SHA256 algorithm, and then encoded using Base64 encoding.</span></span> |

### <a name="account-sas-uri-example"></a><span data-ttu-id="51252-240">계정 SAS URI 예</span><span class="sxs-lookup"><span data-stu-id="51252-240">Account SAS URI example</span></span>

<span data-ttu-id="51252-241">Hello hello 토큰에 동일한 일반 매개 변수를 사용 하는 계정의 SAS 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-241">Here is an example of an account SAS that uses hello same common parameters on hello token.</span></span> <span data-ttu-id="51252-242">이러한 매개 변수는 위에서 설명했으므로 여기에서는 설명을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-242">Since these parameters are described above, they are not described here.</span></span> <span data-ttu-id="51252-243">Hello 매개 변수만 되 특정 tooaccount SAS hello 테이블 아래에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-243">Only hello parameters that are specific tooaccount SAS are described in hello table below.</span></span>

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| <span data-ttu-id="51252-244">이름</span><span class="sxs-lookup"><span data-stu-id="51252-244">Name</span></span> | <span data-ttu-id="51252-245">SAS 부분</span><span class="sxs-lookup"><span data-stu-id="51252-245">SAS portion</span></span> | <span data-ttu-id="51252-246">설명</span><span class="sxs-lookup"><span data-stu-id="51252-246">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51252-247">리소스 URI</span><span class="sxs-lookup"><span data-stu-id="51252-247">Resource URI</span></span> |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |<span data-ttu-id="51252-248">hello Blob 서비스 끝점 (GET를 사용 하 여 호출) 하는 경우 서비스 속성을 가져오거나 (사용 하 여 호출) 하는 경우 서비스 속성 설정에 대 한 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-248">hello Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).</span></span> |
| <span data-ttu-id="51252-249">Services</span><span class="sxs-lookup"><span data-stu-id="51252-249">Services</span></span> |`ss=bf` |<span data-ttu-id="51252-250">hello SAS 적용 toohello Blob 및 파일 서비스</span><span class="sxs-lookup"><span data-stu-id="51252-250">hello SAS applies toohello Blob and File services</span></span> |
| <span data-ttu-id="51252-251">리소스 유형</span><span class="sxs-lookup"><span data-stu-id="51252-251">Resource types</span></span> |`srt=s` |<span data-ttu-id="51252-252">hello SAS tooservice 수준 작업을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-252">hello SAS applies tooservice-level operations.</span></span> |
| <span data-ttu-id="51252-253">권한</span><span class="sxs-lookup"><span data-stu-id="51252-253">Permissions</span></span> |`sp=rw` |<span data-ttu-id="51252-254">hello 권한을 tooread 액세스를 부여 하 고 쓰기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-254">hello permissions grant access tooread and write operations.</span></span> |

<span data-ttu-id="51252-255">이 SAS로 액세스할 수 있는 작업, toohello 서비스 수준에는 권한이 제한 된 있다고 가정 **Blob 서비스 속성 가져오기** (읽기) 및 **Blob 서비스 속성 설정** (쓰기).</span><span class="sxs-lookup"><span data-stu-id="51252-255">Given that permissions are restricted toohello service level, accessible operations with this SAS are **Get Blob Service Properties** (read) and **Set Blob Service Properties** (write).</span></span> <span data-ttu-id="51252-256">그러나 다른 리소스 URI와 hello 같은 SAS 토큰 수 toodelegate 액세스도 사용할**Blob 서비스 통계 가져오기** (읽기)입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-256">However, with a different resource URI, hello same SAS token could also be used toodelegate access too**Get Blob Service Stats** (read).</span></span>

## <a name="controlling-a-sas-with-a-stored-access-policy"></a><span data-ttu-id="51252-257">저장된 액세스 정책을 사용하여 SAS 관리</span><span class="sxs-lookup"><span data-stu-id="51252-257">Controlling a SAS with a stored access policy</span></span>
<span data-ttu-id="51252-258">공유 액세스 서명은 다음 두 가지 형식 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-258">A shared access signature can take one of two forms:</span></span>

* <span data-ttu-id="51252-259">**임시 SAS:** 는 임시 SAS, hello 시작 시간, 만료 시간을 만들고 SAS hello에 대 한 권한을 모두에 지정 된 SAS URI hello (명시적 이나 묵시적 시작 시간을 생략 하면 hello 경우에서).</span><span class="sxs-lookup"><span data-stu-id="51252-259">**Ad hoc SAS:** When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified in hello SAS URI (or implied, in hello case where start time is omitted).</span></span> <span data-ttu-id="51252-260">이 SAS 유형은 계정 SAS 또는 서비스 SAS로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-260">This type of SAS can be created as an account SAS or a service SAS.</span></span>
* <span data-ttu-id="51252-261">**저장 된 액세스 정책 사용 하 여 SAS:** 저장 된 액세스 정책은 리소스 컨테이너-blob 컨테이너에 정의 되어, 테이블, 큐 또는 파일 공유-및 하나 이상의 공유 액세스 서명에 대 한 제약 조건을 사용 하는 toomanage 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-261">**SAS with stored access policy:** A stored access policy is defined on a resource container--a blob container, table, queue, or file share--and can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="51252-262">저장 된 액세스 정책을 사용 하 여 SAS를 연결 하면 hello SAS hello 시작 시간, 만료 시간 및 권한을-hello 저장 된 액세스 정책에 대해 정의 된 hello 제약을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-262">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints--hello start time, expiry time, and permissions--defined for hello stored access policy.</span></span>

> [!NOTE]
> <span data-ttu-id="51252-263">현재, 계정 SAS는 애드혹 SAS여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-263">Currently, an account SAS must be an ad hoc SAS.</span></span> <span data-ttu-id="51252-264">저장된 액세스 정책은 아직 계정 SAS에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-264">Stored access policies are not yet supported for account SAS.</span></span>

<span data-ttu-id="51252-265">hello hello 두 형식의 차이 한 가지 주요 시나리오에 대 한 중요: 해지 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-265">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="51252-266">SAS URI URL 이기 때문에 hello가 가져오는 모든 사용자에 게 SAS을 사용 하려면 원래 만든 사람에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-266">Because a SAS URI is a URL, anyone that obtains hello SAS can use it, regardless of who originally created it.</span></span> <span data-ttu-id="51252-267">SAS를 공개적으로 게시 하는 경우에 hello world의 다른 사용자가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-267">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="51252-268">SAS 권한 부여 액세스 tooresources tooanyone 4 가지 중 하나가 발생 될 때까지 소유:</span><span class="sxs-lookup"><span data-stu-id="51252-268">A SAS grants access tooresources tooanyone possessing it until one of four things happens:</span></span>

1. <span data-ttu-id="51252-269">SAS에 도달 하는 hello에 지정 된 만료 시간을 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-269">hello expiry time specified on hello SAS is reached.</span></span>
2. <span data-ttu-id="51252-270">SAS (저장된 된 액세스 정책을 참조 하는 경우 및 만료 시간을 지정 하는 경우)에 도달 하는 hello에서 참조 하는 hello 저장 된 액세스 정책에 지정 된 만료 시간을 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-270">hello expiry time specified on hello stored access policy referenced by hello SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span></span> <span data-ttu-id="51252-271">이 hello 간격이 경과 하거나 한 가지 방법은 toorevoke hello SAS 않는 전의 hello에 만료 시간이 hello 저장 된 액세스 정책을 수정한 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-271">This can occur either because hello interval elapses, or because you've modified hello stored access policy with an expiry time in hello past, which is one way toorevoke hello SAS.</span></span>
3. <span data-ttu-id="51252-272">hello 저장 하는 또 다른 방법은 toorevoke hello SAS SAS 삭제 되 면 hello에서 참조 하는 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="51252-272">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="51252-273">가 토큰을 정확히 hello 저장 된 액세스 정책을 다시 만드는 경우 hello 이름이 같은 모든 기존 SAS는 다시 수에 따라 유효한 toohello 권한 해당 저장 된 액세스 정책과 연관 (SAS을 지나치지 않은 hello에 해당 hello 만료 시간을 가정).</span><span class="sxs-lookup"><span data-stu-id="51252-273">Note that if you recreate hello stored access policy with exactly hello same name, all existing SAS tokens will again be valid according toohello permissions associated with that stored access policy (assuming that hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="51252-274">Toorevoke hello SAS를 하려는 경우 수 있는지 toouse 다른 이름을 hello 액세스 정책 만료 시간이 hello 나중에 다시 만드는 경우.</span><span class="sxs-lookup"><span data-stu-id="51252-274">If you are intending toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>
4. <span data-ttu-id="51252-275">사용 하는 toocreate hello SAS hello 계정 키 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-275">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="51252-276">계정 키를 다시 생성 하면 해당 키 toofail tooauthenticate를 사용 하 여 모든 응용 프로그램 구성 요소 업데이트 될 때까지 toouse 다른 유효한 계정 키 또는 hello 새로 다시 생성된 된 계정 키를 하거나 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-276">Regenerating an account key will cause all application components using that key toofail tooauthenticate until they're updated toouse either hello other valid account key or hello newly regenerated account key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51252-277">공유 액세스 서명 URI hello 계정 키 사용 되는 toocreate hello 서명과 사용 하 여 연결 되며 hello (있는 경우) 저장 된 액세스 정책에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-277">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="51252-278">저장 된 액세스 정책이 없는 지정, hello만 방법은 toorevoke 공유 액세스 서명을 toochange hello 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-278">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

## <a name="authenticating-from-a-client-application-with-a-sas"></a><span data-ttu-id="51252-279">SAS를 사용하여 클라이언트 응용 프로그램 인증</span><span class="sxs-lookup"><span data-stu-id="51252-279">Authenticating from a client application with a SAS</span></span>
<span data-ttu-id="51252-280">클라이언트는 SAS 소유 하는 hello SAS tooauthenticate을가지고 있지 않기 hello 계정 키 저장소 계정에 대 한 요청을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-280">A client who is in possession of a SAS can use hello SAS tooauthenticate a request against a storage account for which they do not possess hello account keys.</span></span> <span data-ttu-id="51252-281">SAS 연결 문자열에 포함 또는 hello 적절 한 생성자 또는 메서드에에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-281">A SAS can be included in a connection string, or used directly from hello appropriate constructor or method.</span></span>

### <a name="using-a-sas-in-a-connection-string"></a><span data-ttu-id="51252-282">연결 문자열에서 SAS 사용</span><span class="sxs-lookup"><span data-stu-id="51252-282">Using a SAS in a connection string</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a><span data-ttu-id="51252-283">생성자 또는 메서드에서 SAS 사용</span><span class="sxs-lookup"><span data-stu-id="51252-283">Using a SAS in a constructor or method</span></span>
<span data-ttu-id="51252-284">여러 Azure 저장소 클라이언트 라이브러리 생성자 및 메서드 오버 로드 된 한 SAS 요청 toohello 서비스를 인증할 수 있도록 SAS 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-284">Several Azure Storage client library constructors and method overloads offer a SAS parameter, so that you can authenticate a request toohello service with a SAS.</span></span>

<span data-ttu-id="51252-285">예를 들어 다음 SAS URI은 사용 되는 toocreate 참조 tooa 블록 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-285">For example, here a SAS URI is used toocreate a reference tooa block blob.</span></span> <span data-ttu-id="51252-286">hello SAS hello 요청에 대 한 필요한 hello 유일한 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-286">hello SAS provides hello only credentials needed for hello request.</span></span> <span data-ttu-id="51252-287">hello 블록 blob 참조 쓰기 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-287">hello block blob reference is then used for a write operation:</span></span>

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a><span data-ttu-id="51252-288">SAS를 사용하는 경우 모범 사례</span><span class="sxs-lookup"><span data-stu-id="51252-288">Best practices when using SAS</span></span>
<span data-ttu-id="51252-289">응용 프로그램에서 공유 액세스 서명을 사용 하는 경우 필요 toobe 두 가지 잠재적인 위험을 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-289">When you use shared access signatures in your applications, you need toobe aware of two potential risks:</span></span>

* <span data-ttu-id="51252-290">SAS가 누설될 경우 SAS를 획득한 모든 사용자가 SAS를 사용하여 저장소 계정을 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-290">If a SAS is leaked, it can be used by anyone who obtains it, which can potentially compromise your storage account.</span></span>
* <span data-ttu-id="51252-291">SAS tooa 클라이언트 응용 프로그램이 만료 되 고 hello 응용 프로그램은 없습니다 tooretrieve 서비스에서 새 SAS를 제공 하면 hello 응용 프로그램의 기능 방해 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-291">If a SAS provided tooa client application expires and hello application is unable tooretrieve a new SAS from your service, then hello application's functionality may be hindered.</span></span>

<span data-ttu-id="51252-292">hello에 대 한 공유 액세스 서명을 사용 하 여 다음 권장 사항을 완화 시킬 수 있습니다 이러한 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-292">hello following recommendations for using shared access signatures can help mitigate these risks:</span></span>

1. <span data-ttu-id="51252-293">**항상 HTTPS를 사용 하 여** toocreate 하거나 SAS를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-293">**Always use HTTPS** toocreate or distribute a SAS.</span></span> <span data-ttu-id="51252-294">SAS를 HTTP를 통해 전달 되며 가로챌, 공격자가 중간자 개입 공격을 수행 수 tooread hello SAS 되며 다음 hello 잠재적으로 중요 한 데이터를 손상 또는 hello 하 여 데이터 손상 수 있도록 사용자가 수 고를 의도 한 것 처럼 사용 악의적인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-294">If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack is able tooread hello SAS and then use it just as hello intended user could have, potentially compromising sensitive data or allowing for data corruption by hello malicious user.</span></span>
2. <span data-ttu-id="51252-295">**저장된 액세스 정책을 최대한 참조합니다.**</span><span class="sxs-lookup"><span data-stu-id="51252-295">**Reference stored access policies where possible.**</span></span> <span data-ttu-id="51252-296">Tooregenerate hello 저장소 계정 키 필요 없이 옵션 toorevoke 권한을 hello 액세스 정책을 제공을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-296">Stored access policies give you hello option toorevoke permissions without having tooregenerate hello storage account keys.</span></span> <span data-ttu-id="51252-297">이후 (또는 무한) hello에 매우 많이 이러한 이벤트에 대해 hello 만료를 설정 하 고 있는지 확인 toomove 정기적으로 업데이트는 hello 향후에 더 멀리 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-297">Set hello expiration on these very far in hello future (or infinite) and make sure it's regularly updated toomove it farther into hello future.</span></span>
3. <span data-ttu-id="51252-298">**임시 SAS의 경우 짧은 만료 시간을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="51252-298">**Use near-term expiration times on an ad hoc SAS.**</span></span> <span data-ttu-id="51252-299">그러면 SAS가 손상되더라도 단기적으로만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-299">In this way, even if a SAS is compromised, it's valid only for a short time.</span></span> <span data-ttu-id="51252-300">이 방법은 저장된 액세스 정책을 참조할 수 없는 경우에 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-300">This practice is especially important if you cannot reference a stored access policy.</span></span> <span data-ttu-id="51252-301">단기적 만료 시간에는 또한 hello hello 시간 사용 가능한 tooupload tooit 제한 하 여 tooa blob을 쓸 수 있는 데이터 양을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-301">Near-term expiration times also limit hello amount of data that can be written tooa blob by limiting hello time available tooupload tooit.</span></span>
4. <span data-ttu-id="51252-302">**에 클라이언트 hello SAS 필요한 경우 자동으로 갱신 합니다.**</span><span class="sxs-lookup"><span data-stu-id="51252-302">**Have clients automatically renew hello SAS if necessary.**</span></span> <span data-ttu-id="51252-303">클라이언트는 hello SAS를 제공 하는 hello 서비스를 사용할 수 없는 경우 재시도 대 한 순서 tooallow 시간 hello 만료 전에 hello SAS를 갱신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-303">Clients should renew hello SAS well before hello expiration, in order tooallow time for retries if hello service providing hello SAS is unavailable.</span></span> <span data-ttu-id="51252-304">프로그램 SAS toobe 적은 수의 직접 실행에 사용 되는 것입니다를 수명이 짧은 작업을 예상 toobe hello 만료 시간 내에 완료할 경우 hello SAS가 갱신 toobe 예상 대로 불필요 할 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-304">If your SAS is meant toobe used for a small number of immediate, short-lived operations that are expected toobe completed within hello expiration period, then this may be unnecessary as hello SAS is not expected toobe renewed.</span></span> <span data-ttu-id="51252-305">그러나 정기적으로 SAS 통해 요청을 수행 하는 클라이언트를 설정한 경우 다음의 만료 hello 가능성 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-305">However, if you have client that is routinely making requests via SAS, then hello possibility of expiration comes into play.</span></span> <span data-ttu-id="51252-306">hello 주요 고려 사항인 toobalance hello 필요는 hello SAS toobe 수명이 짧은 (이전에 명시 된) 클라이언트 hello hello 필요 tooensure와 초기 갱신을 요청에 대 한 충분 한 (tooavoid 중단 toohello SAS 만료 이전 toosuccessful 갱신 인해).</span><span class="sxs-lookup"><span data-stu-id="51252-306">hello key consideration is toobalance hello need for hello SAS toobe short-lived (as previously stated) with hello need tooensure that hello client is requesting renewal early enough (tooavoid disruption due toohello SAS expiring prior toosuccessful renewal).</span></span>
5. <span data-ttu-id="51252-307">**SAS 시작 시간에 유의하세요.**</span><span class="sxs-lookup"><span data-stu-id="51252-307">**Be careful with SAS start time.**</span></span> <span data-ttu-id="51252-308">경우 hello 시작 시간에 대해 설정한 SAS 너무**이제**, tooclock 기울이기 (현재 시간 toodifferent 컴퓨터에 따라 차이점) 기한 오류 관찰 될 수 있습니다 간헐적으로 hello에 대 한 처음 몇 분 후입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-308">If you set hello start time for a SAS too**now**, then due tooclock skew (differences in current time according toodifferent machines), failures may be observed intermittently for hello first few minutes.</span></span> <span data-ttu-id="51252-309">일반적으로 설정 hello 시작 시간 toobe 최소 15 분 이상 지난 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-309">In general, set hello start time toobe at least 15 minutes in hello past.</span></span> <span data-ttu-id="51252-310">설정하지 않습니다. 그러면 시작 시간이 즉시 유효해집니다.</span><span class="sxs-lookup"><span data-stu-id="51252-310">Or, don't set it at all, which will make it valid immediately in all cases.</span></span> <span data-ttu-id="51252-311">해질 수 있습니다 too15 분의 클럭을 모든 요청에서 어느 방향으로든에서 시간차 기억 하는 hello tooexpiry 시간 역시-일반적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51252-311">hello same generally applies tooexpiry time as well--remember that you may observe up too15 minutes of clock skew in either direction on any request.</span></span> <span data-ttu-id="51252-312">클라이언트는 REST 버전 이전 too2012-02-12를 사용 하 여 hello 최대 저장된 된 액세스 정책을 참조 하지 않는 SAS에 대 한 기간은 1 시간 및 정책을 지정 장기적인 보다는 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-312">For clients using a REST version prior too2012-02-12, hello maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.</span></span>
6. <span data-ttu-id="51252-313">**구체적으로 액세스 하는 hello 리소스 toobe 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="51252-313">**Be specific with hello resource toobe accessed.**</span></span> <span data-ttu-id="51252-314">보안 모범 사례는 tooprovide hello 필요한 최소한의 권한 있는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-314">A security best practice is tooprovide a user with hello minimum required privileges.</span></span> <span data-ttu-id="51252-315">사용자만 읽기 권한을 tooa 단일 엔터티를 필요로 한다면 하지: 읽기/쓰기/삭제 액세스 tooall 엔터티와 toothat 단일 엔터티 읽기 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-315">If a user only needs read access tooa single entity, then grant them read access toothat single entity, and not read/write/delete access tooall entities.</span></span> <span data-ttu-id="51252-316">또한 SAS hello SAS는 공격자의 hello 손에 전력에 있기 때문에 손상 된 경우 hello 손상 취약성을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-316">This also helps lessen hello damage if a SAS is compromised because hello SAS has less power in hello hands of an attacker.</span></span>
7. <span data-ttu-id="51252-317">**SAS 사용 작업을 포함한 모든 사용량에 대한 요금이 계정에 청구됩니다.**</span><span class="sxs-lookup"><span data-stu-id="51252-317">**Understand that your account will be billed for any usage, including that done with SAS.**</span></span> <span data-ttu-id="51252-318">쓰기 액세스 tooa blob를 제공 하면 200GB blob 사용자 tooupload 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-318">If you provide write access tooa blob, a user may choose tooupload a 200GB blob.</span></span> <span data-ttu-id="51252-319">에 읽기 액세스 권한도 부여 하였습니다, toodownload를 선택할 수 있습니다 10 회 발생 시 키 지 2TB 송신 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-319">If you've given them read access as well, they may choose toodownload it 10 times, incurring 2 TB in egress costs for you.</span></span> <span data-ttu-id="51252-320">제한 된 사용 권한 다시 제공 toohelp hello 잠재적인 작업 악의적인 사용자가 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-320">Again, provide limited permissions toohelp mitigate hello potential actions of malicious users.</span></span> <span data-ttu-id="51252-321">이 위협을 수명이 짧은 SAS tooreduce를 사용 합니다 (그러나 클럭 오차가 hello 종료 시간에 주의 기울여야).</span><span class="sxs-lookup"><span data-stu-id="51252-321">Use short-lived SAS tooreduce this threat (but be mindful of clock skew on hello end time).</span></span>
8. <span data-ttu-id="51252-322">**SAS를 사용하여 작성된 데이터의 유효성을 검사하세요.**</span><span class="sxs-lookup"><span data-stu-id="51252-322">**Validate data written using SAS.**</span></span> <span data-ttu-id="51252-323">클라이언트 응용 프로그램 데이터 tooyour 저장소 계정에 쓰기 때 염두에 해당 데이터에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-323">When a client application writes data tooyour storage account, keep in mind that there can be problems with that data.</span></span> <span data-ttu-id="51252-324">응용 프로그램에 필요한 데이터 유효성을 검사 하거나 준비 toouse 되기 전에 인증 수, 하는 경우에 hello 데이터가 기록 되 고 응용 프로그램에서 사용 하기 전에이 유효성 검사를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-324">If your application requires that that data be validated or authorized before it is ready toouse, you should perform this validation after hello data is written and before it is used by your application.</span></span> <span data-ttu-id="51252-325">또한이 연습 유출 된 SAS 악용 사용자 또는 사용자가 제대로 hello SAS를 획득 하거나 tooyour 계정 쓰여지는 손상 되거나 악의적인 데이터에 대 한 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-325">This practice also protects against corrupt or malicious data being written tooyour account, either by a user who properly acquired hello SAS, or by a user exploiting a leaked SAS.</span></span>
9. <span data-ttu-id="51252-326"><seg>
  **경우에 따라 SAS를 사용하지 마세요..**</seg></span><span class="sxs-lookup"><span data-stu-id="51252-326">**Don't always use SAS.**</span></span> <span data-ttu-id="51252-327">경우에 따라 저장소 계정에 대해 특정 작업과 관련 된 hello 위험 sa hello 이점을 보다 더 큽니다.</span><span class="sxs-lookup"><span data-stu-id="51252-327">Sometimes hello risks associated with a particular operation against your storage account outweigh hello benefits of SAS.</span></span> <span data-ttu-id="51252-328">이러한 작업에 대 한 비즈니스를 수행한 후 tooyour 저장소 계정에 기록 하는 중간 계층 서비스를 만드는 규칙 유효성 검사, 인증 및 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-328">For such operations, create a middle-tier service that writes tooyour storage account after performing business rule validation, authentication, and auditing.</span></span> <span data-ttu-id="51252-329">또한, 경우에 다른 방법으로 toomanage 액세스를 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-329">Also, sometimes it's simpler toomanage access in other ways.</span></span> <span data-ttu-id="51252-330">예를 들어 원하는 toomake 컨테이너의 모든 blob 공개적으로 읽을 수 만들면 컨테이너 공용, hello SAS tooevery 클라이언트 액세스를 위해 제공 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-330">For example, if you want toomake all blobs in a container publically readable, you can make hello container Public, rather than providing a SAS tooevery client for access.</span></span>
10. <span data-ttu-id="51252-331">**Storage Analytics toomonitor 응용 프로그램을 사용 합니다.**</span><span class="sxs-lookup"><span data-stu-id="51252-331">**Use Storage Analytics toomonitor your application.**</span></span> <span data-ttu-id="51252-332">로깅 및 메트릭 tooobserve tooan 정전 프로그램 SAS 공급자 서비스 또는 toohello 실수로 제거 저장 된 액세스 정책으로 인해 인증 오류가으로 가끔 치솟는 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-332">You can use logging and metrics tooobserve any spike in authentication failures due tooan outage in your SAS provider service or toohello inadvertent removal of a stored access policy.</span></span> <span data-ttu-id="51252-333">Hello 참조 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) 추가 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-333">See hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) for additional information.</span></span>

## <a name="sas-examples"></a><span data-ttu-id="51252-334">SAS 예제</span><span class="sxs-lookup"><span data-stu-id="51252-334">SAS examples</span></span>
<span data-ttu-id="51252-335">다음은 공유 액세스 서명의 두 유형(계정 SAS, 서비스 SAS)에 대한 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-335">Below are some examples of both types of shared access signatures, account SAS and service SAS.</span></span>

<span data-ttu-id="51252-336">toorun이 C# 예제에서는 프로젝트에서 NuGet 패키지를 다음 tooreference hello 필요:</span><span class="sxs-lookup"><span data-stu-id="51252-336">toorun these C# examples, you need tooreference hello following NuGet packages in your project:</span></span>

* <span data-ttu-id="51252-337">[.NET 용 azure 저장소 클라이언트 라이브러리](http://www.nuget.org/packages/WindowsAzure.Storage)을 버전 6.x 또는 이후 (toouse 계정 SAS).</span><span class="sxs-lookup"><span data-stu-id="51252-337">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x or later (toouse account SAS).</span></span>
* [<span data-ttu-id="51252-338">Azure 구성 관리자</span><span class="sxs-lookup"><span data-stu-id="51252-338">Azure Configuration Manager</span></span>](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

<span data-ttu-id="51252-339">Toocreate 및 테스트 SAS 참조 하는 방법을 보여 주는 추가 예에 대 한 [저장소에 대 한 Azure 코드 예제](https://azure.microsoft.com/documentation/samples/?service=storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-339">For additional examples that show how toocreate and test a SAS, see [Azure Code Samples for Storage](https://azure.microsoft.com/documentation/samples/?service=storage).</span></span>

### <a name="example-create-and-use-an-account-sas"></a><span data-ttu-id="51252-340">예제: SAS 계정 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="51252-340">Example: Create and use an account SAS</span></span>
<span data-ttu-id="51252-341">hello 다음 코드 예제에서는 Blob hello 및 파일 서비스를 사용할 수 있는 SA 계정을 만들고 클라이언트 권한 읽기, 쓰기 및 목록 사용 권한 부여 hello tooaccess 서비스 수준 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-341">hello following code example creates an account SAS that is valid for hello Blob and File services, and gives hello client permissions read, write, and list permissions tooaccess service-level APIs.</span></span> <span data-ttu-id="51252-342">hello 계정 SAS hello 요청 해야 HTTPS를 사용 하므로 hello 프로토콜 tooHTTPS를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-342">hello account SAS restricts hello protocol tooHTTPS, so hello request must be made with HTTPS.</span></span>

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

<span data-ttu-id="51252-343">toouse hello 계정 SAS tooaccess 서비스 수준 Api hello Blob 서비스에 대해, hello SAS를 사용 하 여 Blob 클라이언트 개체를 생성 및 저장소 계정에 대 한 Blob 저장소 끝점 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-343">toouse hello account SAS tooaccess service-level APIs for hello Blob service, construct a Blob client object using hello SAS and hello Blob storage endpoint for your storage account.</span></span>

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a><span data-ttu-id="51252-344">예제: 저장된 액세스 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="51252-344">Example: Create a stored access policy</span></span>
<span data-ttu-id="51252-345">hello 다음 코드는 저장 된 액세스 정책을 만듭니다 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="51252-345">hello following code creates a stored access policy on a container.</span></span> <span data-ttu-id="51252-346">서비스 hello 컨테이너에 대 한 SAS 또는 해당 blob에 대 한 hello 액세스 정책 toospecify 제약 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-346">You can use hello access policy toospecify constraints for a service SAS on hello container or its blobs.</span></span>

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a><span data-ttu-id="51252-347">예제: 컨테이너에 서비스 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="51252-347">Example: Create a service SAS on a container</span></span>
<span data-ttu-id="51252-348">hello 코드 다음 컨테이너에 대 한 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51252-348">hello following code creates a SAS on a container.</span></span> <span data-ttu-id="51252-349">기존 저장 된 액세스 정책의 hello 이름이 제공 된 경우 해당 정책 SAS hello와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-349">If hello name of an existing stored access policy is provided, that policy is associated with hello SAS.</span></span> <span data-ttu-id="51252-350">저장 된 액세스 정책이 없는 제공 hello 코드 hello 컨테이너에서 임시 SAS을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51252-350">If no stored access policy is provided, then hello code creates an ad-hoc SAS on hello container.</span></span>

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a><span data-ttu-id="51252-351">예제: Blob에 서비스 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="51252-351">Example: Create a service SAS on a blob</span></span>
<span data-ttu-id="51252-352">hello 코드 다음 blob에는 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51252-352">hello following code creates a SAS on a blob.</span></span> <span data-ttu-id="51252-353">기존 저장 된 액세스 정책의 hello 이름이 제공 된 경우 해당 정책 SAS hello와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-353">If hello name of an existing stored access policy is provided, that policy is associated with hello SAS.</span></span> <span data-ttu-id="51252-354">저장 된 액세스 정책이 없는 제공 hello 코드 hello blob에서 임시 SAS을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51252-354">If no stored access policy is provided, then hello code creates an ad-hoc SAS on hello blob.</span></span>

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a><span data-ttu-id="51252-355">결론</span><span class="sxs-lookup"><span data-stu-id="51252-355">Conclusion</span></span>
<span data-ttu-id="51252-356">공유 액세스 서명에 제한 된 권한 hello 계정 키 없어야 tooyour 저장소 계정 tooclients 제공 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51252-356">Shared access signatures are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="51252-357">따라서 서로 Azure 저장소를 사용 하 여 모든 응용 프로그램에 대 한 hello 보안 모델의 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="51252-357">As such, they are a vital part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="51252-358">여기에 나열 된 hello 모범 사례를 따르는 경우에 hello 응용 프로그램의 보안을 손상 시 키 지 않고 저장소 계정의 SAS tooprovide 보다 유연 하 게 액세스 tooresources 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51252-358">If you follow hello best practices listed here, you can use SAS tooprovide greater flexibility of access tooresources in your storage account, without compromising hello security of your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51252-359">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51252-359">Next Steps</span></span>
* [<span data-ttu-id="51252-360">익명 읽기 권한을 toocontainers 및 blob 관리</span><span class="sxs-lookup"><span data-stu-id="51252-360">Manage anonymous read access toocontainers and blobs</span></span>](../blobs/storage-manage-access-to-resources.md)
* [<span data-ttu-id="51252-361">공유 액세스 서명을 사용하여 액세스 위임</span><span class="sxs-lookup"><span data-stu-id="51252-361">Delegating Access with a Shared Access Signature</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="51252-362">테이블 및 큐 SAS 소개</span><span class="sxs-lookup"><span data-stu-id="51252-362">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
