---
title: "Azure Storage에서 SAS(공유 액세스 서명) 사용 | Microsoft 문서"
description: "SAS(공유 액세스 서명)를 사용하여 Blob, 큐, 테이블 및 파일을 비롯한 Azure Storage 리소스에 대한 액세스 권한을 위임하는 방법을 알아봅니다."
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
ms.openlocfilehash: ae944eae4e62132e47bf9069d83817a1a6779ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-shared-access-signatures-sas"></a><span data-ttu-id="37b26-103">SAS(공유 액세스 서명) 사용</span><span class="sxs-lookup"><span data-stu-id="37b26-103">Using shared access signatures (SAS)</span></span>

<span data-ttu-id="37b26-104">SAS(공유 액세스 서명)를 사용하면 계정 키를 노출하지 않고 다른 클라이언트에게 저장소 계정의 개체에 대한 제한된 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-104">A shared access signature (SAS) provides you with a way to grant limited access to objects in your storage account to other clients, without exposing your account key.</span></span> <span data-ttu-id="37b26-105">이 문서에서는 SAS 모델의 개요를 설명하고 SAS 모범 사례를 검토하고 몇 가지 예를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-105">In this article, we provide an overview of the SAS model, review SAS best practices, and look at some examples.</span></span>

<span data-ttu-id="37b26-106">여기에 제시된 것 이외의 SAS를 사용하는 추가 코드 예제는 [.NET에서 Azure Blob Storage 시작](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) 및 [Azure 코드 샘플](https://azure.microsoft.com/documentation/samples/?service=storage) 라이브러리에서 사용할 수 있는 다른 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-106">For additional code examples using SAS beyond those presented here, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) and other samples available in the [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage) library.</span></span> <span data-ttu-id="37b26-107">GitHub에서 샘플 응용 프로그램을 다운로드하고 실행하거나 코드를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-107">You can download the sample applications and run them, or browse the code on GitHub.</span></span>

## <a name="what-is-a-shared-access-signature"></a><span data-ttu-id="37b26-108">공유 액세스 서명이란?</span><span class="sxs-lookup"><span data-stu-id="37b26-108">What is a shared access signature?</span></span>
<span data-ttu-id="37b26-109">공유 액세스 서명은 저장소 계정의 리소스에 대한 위임된 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-109">A shared access signature provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="37b26-110">SAS로 계정 키를 공유하지 않고 저장 계정의 리소스에 대한 클라이언트의 액세스를 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-110">With a SAS, you can grant clients access to resources in your storage account, without sharing your account keys.</span></span> <span data-ttu-id="37b26-111">이는 응용 프로그램에서 공유 액세스 서명을 사용하는 중요한 점입니다. SAS는 선택키를 손상시키지 않고 저장 리소스를 공유할 수 있는 보안 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-111">This is the key point of using shared access signatures in your applications--a SAS is a secure way to share your storage resources without compromising your account keys.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

<span data-ttu-id="37b26-112">SAS가 있는 클라이언트에게 허용하는 액세스 유형에 대해 SAS는 세부적인 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-112">A SAS gives you granular control over the type of access you grant to clients who have the SAS, including:</span></span>

* <span data-ttu-id="37b26-113">SAS가 유효한 경우 시작 시간 및 만료 시간을 포함하는 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-113">The interval over which the SAS is valid, including the start time and the expiry time.</span></span>
* <span data-ttu-id="37b26-114">SAS에서 부여된 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-114">The permissions granted by the SAS.</span></span> <span data-ttu-id="37b26-115">예를 들어 blob의 SAS는 해당 blob에 읽기 및 쓰기 권한을 부여할 수 있지만 삭제 권한은 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-115">For example, a SAS for a blob might grant read and write permissions to that blob, but not delete permissions.</span></span>
* <span data-ttu-id="37b26-116">Azure Storage가 SAS를 수락하는 선택적 IP 주소 또는 IP 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-116">An optional IP address or range of IP addresses from which Azure Storage will accept the SAS.</span></span> <span data-ttu-id="37b26-117">예를 들어 조직에 속한 IP 주소 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-117">For example, you might specify a range of IP addresses belonging to your organization.</span></span>
* <span data-ttu-id="37b26-118">Azure Storage가 SAS을 수락하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-118">The protocol over which Azure Storage will accept the SAS.</span></span> <span data-ttu-id="37b26-119">HTTPS를 사용하여 클라이언트에 대한 액세스를 제한하려면 이 선택적 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-119">You can use this optional parameter to restrict access to clients using HTTPS.</span></span>

## <a name="when-should-you-use-a-shared-access-signature"></a><span data-ttu-id="37b26-120">공유 액세스 서명은 언제 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="37b26-120">When should you use a shared access signature?</span></span>
<span data-ttu-id="37b26-121">저장소 계정의 액세스 키가 없는 클라이언트에게 저장소 계정의 리소스에 대한 액세스 권한을 제공하려는 경우에 SAS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-121">You can use a SAS when you want to provide access to resources in your storage account to any client not possessing your storage account's access keys.</span></span> <span data-ttu-id="37b26-122">저장소 계정 키는 기본 키와 보조 액세스 키를 모두 포함하여, 계정과 계정에 있는 모든 리소스에 대한 관리 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-122">Your storage account includes both a primary and secondary access key, both of which grant administrative access to your account, and all resources within it.</span></span> <span data-ttu-id="37b26-123">이러한 키를 노출하면 계정도 악의적이거나 잘못된 용도로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-123">Exposing either of these keys opens your account to the possibility of malicious or negligent use.</span></span> <span data-ttu-id="37b26-124">공유 액세스 서명은 클라이언트가 계정 키를 사용하지 않고 명시적으로 부여된 권한에 따라 저장소 계정에서 데이터를 읽고, 쓰고, 삭제하도록 허용하는 안전한 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-124">Shared access signatures provide a safe alternative that allows clients to read, write, and delete data in your storage account according to the permissions you've explicitly granted, and without need for an account key.</span></span>

<span data-ttu-id="37b26-125">SAS가 유용한 일반적인 시나리오로는 다른 사용자가 저장소 계정에서 데이터를 읽고 쓰는 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-125">A common scenario where a SAS is useful is a service where users read and write their own data to your storage account.</span></span> <span data-ttu-id="37b26-126">저장소 계정에 사용자 데이터를 저장하는 시나리오에는 다음과 같은 두 가지 일반적인 디자인 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-126">In a scenario where a storage account stores user data, there are two typical design patterns:</span></span>

1. <span data-ttu-id="37b26-127">클라이언트는 인증을 수행하는 프런트 엔드 프록시 서비스를 통해 데이터를 업로드하고 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-127">Clients upload and download data via a front-end proxy service, which performs authentication.</span></span> <span data-ttu-id="37b26-128">프런트 엔드 프록시 서비스는 비즈니스 규칙의 유효성을 검사할 수 있다는 장점이 있지만, 데이터의 양이 많거나 트랜잭션 볼륨이 높은 경우 수요에 맞게 확장 가능한 서비스를 구축하려면 많은 비용이 필요하거나 어려움이 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-128">This front-end proxy service has the advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale to match demand may be expensive or difficult.</span></span>

  ![시나리오 다이어그램: 프런트 엔드 프록시 서비스][sas-storage-fe-proxy-service]

1. <span data-ttu-id="37b26-130">간단한 서비스에서 필요에 따라 클라이언트를 인증한 다음 SAS를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-130">A lightweight service authenticates the client as needed and then generates a SAS.</span></span> <span data-ttu-id="37b26-131">클라이언트는 SAS를 수신한 후 SAS에 정의된 권한을 사용하여 SAS에 허용된 간격으로 저장소 계정 리소스에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-131">Once the client receives the SAS, they can access storage account resources directly with the permissions defined by the SAS and for the interval allowed by the SAS.</span></span> <span data-ttu-id="37b26-132">SAS를 사용하면 프런트 엔드 프록시 서비스를 통해 모든 데이터를 라우팅할 필요성이 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-132">The SAS mitigates the need for routing all data through the front-end proxy service.</span></span>

  ![시나리오 다이어그램: SAS 공급자 서비스][sas-storage-provider-service]

<span data-ttu-id="37b26-134">대부분의 실제 서비스에서는 이러한 두 가지 방법을 혼합하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-134">Many real-world services may use a hybrid of these two approaches.</span></span> <span data-ttu-id="37b26-135">예를 들어 일부 데이터는 프런트 엔드 프록시를 통해 처리 및 확인하고 일부 데이터는 SAS를 사용하여 직접 저장하거나 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-135">For example, some data might be processed and validated via the front-end proxy, while other data is saved and/or read directly using SAS.</span></span>

<span data-ttu-id="37b26-136">또한 특정 시나리오에서는 SAS를 사용하여 복사 작업의 원본 개체를 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-136">Additionally, you will need to use a SAS to authenticate the source object in a copy operation in certain scenarios:</span></span>

* <span data-ttu-id="37b26-137">다른 저장소 계정에 있는 다른 Blob에 Blob을 복사하는 경우 SAS를 사용하여 원본 Blob을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-137">When you copy a blob to another blob that resides in a different storage account, you must use a SAS to authenticate the source blob.</span></span> <span data-ttu-id="37b26-138">필요에 따라 SAS를 사용하여 대상 Blob도 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-138">You can optionally use a SAS to authenticate the destination blob as well.</span></span>
* <span data-ttu-id="37b26-139">다른 저장소 계정에 있는 다른 파일에 파일을 복사하는 경우 SAS를 사용하여 원본 파일을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-139">When you copy a file to another file that resides in a different storage account, you must use a SAS to authenticate the source file.</span></span> <span data-ttu-id="37b26-140">필요에 따라 SAS를 사용하여 대상 파일도 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-140">You can optionally use a SAS to authenticate the destination file as well.</span></span>
* <span data-ttu-id="37b26-141">Blob을 파일에 복사하거나 파일을 Blob에 복사하는 경우 원본 및 대상 개체가 동일한 저장소 계정 내에 있더라도 SAS를 사용하여 원본 개체를 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-141">When you copy a blob to a file, or a file to a blob, you must use a SAS to authenticate the source object, even if the source and destination objects reside within the same storage account.</span></span>

## <a name="types-of-shared-access-signatures"></a><span data-ttu-id="37b26-142">공유 액세스 서명의 유형</span><span class="sxs-lookup"><span data-stu-id="37b26-142">Types of shared access signatures</span></span>
<span data-ttu-id="37b26-143">두 가지 유형의 공유 액세스 서명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-143">You can create two types of shared access signatures:</span></span>

* <span data-ttu-id="37b26-144">**서비스 SAS**</span><span class="sxs-lookup"><span data-stu-id="37b26-144">**Service SAS.**</span></span> <span data-ttu-id="37b26-145">서비스 SAS는 저장소 서비스(Blob, 큐, 테이블, 파일 서비스) 중 하나의 리소스에만 액세스 권한을 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-145">The service SAS delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service.</span></span> <span data-ttu-id="37b26-146">서비스 SAS 토큰을 구성하는 방법에 대한 자세한 내용은 [서비스 SAS 구성](https://msdn.microsoft.com/library/dn140255.aspx) 및 [서비스 SAS 예제](https://msdn.microsoft.com/library/dn140256.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-146">See [Constructing a Service SAS](https://msdn.microsoft.com/library/dn140255.aspx) and [Service SAS Examples](https://msdn.microsoft.com/library/dn140256.aspx) for in-depth information about constructing the service SAS token.</span></span>
* <span data-ttu-id="37b26-147">**계정 SAS**</span><span class="sxs-lookup"><span data-stu-id="37b26-147">**Account SAS.**</span></span> <span data-ttu-id="37b26-148">계정 SAS는 하나 이상의 저장소 서비스에서 리소스에 대한 액세스 권한을 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-148">The account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="37b26-149">서비스 SAS를 통해 사용 가능한 모든 작업은 계정 SAS를 통해서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-149">All of the operations available via a service SAS are also available via an account SAS.</span></span> <span data-ttu-id="37b26-150">또한 계정 SAS를 사용하면 **서비스 속성 가져오기/설정**, **서비스 통계 가져오기**와 같은 특정 서비스에 적용되는 작업에 대한 액세스 권한을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-150">Additionally, with the account SAS, you can delegate access to operations that apply to a given service, such as **Get/Set Service Properties** and **Get Service Stats**.</span></span> <span data-ttu-id="37b26-151">또한 서비스 SAS로 허용되지 않는 Blob 컨테이너, 테이블, 큐, 파일 공유에서 읽기, 쓰기, 삭제 작업에 대한 액세스 권한을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-151">You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="37b26-152">계정 SAS 토큰을 구성하는 방법에 대한 자세한 내용은 [계정 SAS 구성](https://msdn.microsoft.com/library/mt584140.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-152">See [Constructing an Account SAS](https://msdn.microsoft.com/library/mt584140.aspx) for in-depth information about constructing the account SAS token.</span></span>

## <a name="how-a-shared-access-signature-works"></a><span data-ttu-id="37b26-153">공유 액세스 서명 사용 방법</span><span class="sxs-lookup"><span data-stu-id="37b26-153">How a shared access signature works</span></span>
<span data-ttu-id="37b26-154">공유 액세스 서명은 하나 이상의 저장소 리소스를 가리키는 서명된 URI이며 쿼리 매개 변수의 특별 집합이 포함된 토큰이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-154">A shared access signature is a signed URI that points to one or more storage resources and includes a token that contains a special set of query parameters.</span></span> <span data-ttu-id="37b26-155">토큰은 클라이언트가 리소스를 액세스하는 방식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-155">The token indicates how the resources may be accessed by the client.</span></span> <span data-ttu-id="37b26-156">이러한 쿼리 매개 변수 중 하나인 서명은 SAS 매개 변수에서 구성되고 계정 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-156">One of the query parameters, the signature, is constructed from the SAS parameters and signed with the account key.</span></span> <span data-ttu-id="37b26-157">이 서명은 Azure 저장소에서 SAS를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-157">This signature is used by Azure Storage to authenticate the SAS.</span></span>

<span data-ttu-id="37b26-158">다음은 리소스 URI과 SAS 토큰을 표시하는 SAS URI의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-158">Here's an example of a SAS URI, showing the resource URI and the SAS token:</span></span>

![SAS URI의 구성 요소][sas-storage-uri]

<span data-ttu-id="37b26-160">SAS 토큰은 *클라이언트* 쪽에서 생성된 문자열입니다. 코드 예제는 [SAS 예제](#sas-examples) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-160">The SAS token is a string you generate on the *client* side (see the [SAS examples](#sas-examples) section for code examples).</span></span> <span data-ttu-id="37b26-161">저장소 클라이언트 라이브러리를 사용하여 생성하는 SAS 토큰은 어떤 방식으로든 Azure Storage에 의해 추적되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-161">A SAS token you generate with the storage client library, for example, is not tracked by Azure Storage in any way.</span></span> <span data-ttu-id="37b26-162">클라이언트 쪽에서 SAS 토큰 개수를 제한 없이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-162">You can create an unlimited number of SAS tokens on the client side.</span></span>

<span data-ttu-id="37b26-163">클라이언트가 Azure Storage에 SAS URI를 요청의 일부로 제공하는 경우 서비스는 SAS 매개 변수와 서명을 확인하여 요청을 인증하기에 유효한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-163">When a client provides a SAS URI to Azure Storage as part of a request, the service checks the SAS parameters and signature to verify that it is valid for authenticating the request.</span></span> <span data-ttu-id="37b26-164">서비스에서 서명이 유효하다고 확인한 경우 요청이 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-164">If the service verifies that the signature is valid, then the request is authenticated.</span></span> <span data-ttu-id="37b26-165">그렇지 않은 경우 오류 코드 403(금지됨) 요청이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-165">Otherwise, the request is declined with error code 403 (Forbidden).</span></span>

## <a name="shared-access-signature-parameters"></a><span data-ttu-id="37b26-166">공유 액세스 서명 매개 변수</span><span class="sxs-lookup"><span data-stu-id="37b26-166">Shared access signature parameters</span></span>
<span data-ttu-id="37b26-167">계정 SAS 및 서비스 SAS 토큰에는 일반적인 매개 변수 몇 개가 포함되며 다른 몇 가지 매개 변수도 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-167">The account SAS and service SAS tokens include some common parameters, and also take a few parameters that that are different.</span></span>

### <a name="parameters-common-to-account-sas-and-service-sas-tokens"></a><span data-ttu-id="37b26-168">계정 SAS 및 서비스 SAS 토큰에 일반적인 매개 변수</span><span class="sxs-lookup"><span data-stu-id="37b26-168">Parameters common to account SAS and service SAS tokens</span></span>
* <span data-ttu-id="37b26-169">**Api 버전** 요청을 실행하기 위해 사용할 저장소 서비스 버전을 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-169">**Api version** An optional parameter that specifies the storage service version to use to execute the request.</span></span>
* <span data-ttu-id="37b26-170">**서비스 버전** 요청을 인증하기 위해 사용할 저장소 서비스 버전을 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-170">**Service version** A required parameter that specifies the storage service version to use to authenticate the request.</span></span>
* <span data-ttu-id="37b26-171">**시작 시간.**</span><span class="sxs-lookup"><span data-stu-id="37b26-171">**Start time.**</span></span> <span data-ttu-id="37b26-172">SAS가 유효해지는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-172">This is the time at which the SAS becomes valid.</span></span> <span data-ttu-id="37b26-173">공유 액세스 서명의 시작 시간은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-173">The start time for a shared access signature is optional.</span></span> <span data-ttu-id="37b26-174">시작 시간이 생략된 경우 SAS가 즉시 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-174">If a start time is omitted, the SAS is effective immediately.</span></span> <span data-ttu-id="37b26-175">시작 시간은 특정 UTC 지정자("Z")를 이용하여 UTC(협정 세계시)로 표시해야 합니다(예: `1994-11-05T13:15:30Z`).</span><span class="sxs-lookup"><span data-stu-id="37b26-175">The start time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z`.</span></span>
* <span data-ttu-id="37b26-176">**만료 시간.**</span><span class="sxs-lookup"><span data-stu-id="37b26-176">**Expiry time.**</span></span> <span data-ttu-id="37b26-177">SAS가 더 이상 유효하지 않게 되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-177">This is the time after which the SAS is no longer valid.</span></span> <span data-ttu-id="37b26-178">모범 사례에 따라 SAS의 만료 시간을 지정하거나 만료 시간을 저장된 액세스 정책과 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-178">Best practices recommend that you either specify an expiry time for a SAS, or associate it with a stored access policy.</span></span> <span data-ttu-id="37b26-179">만료 시간은 특정 UTC 지정자("Z")를 이용하여 UTC(협정 세계시)로 표시해야 합니다(예: `1994-11-05T13:15:30Z`). 자세한 내용은 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-179">The expiry time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z` (see more below).</span></span>
* <span data-ttu-id="37b26-180">**사용 권한**</span><span class="sxs-lookup"><span data-stu-id="37b26-180">**Permissions.**</span></span> <span data-ttu-id="37b26-181">SAS에 지정된 사용 권한은 클라이언트가 SAS를 사용하여 저장소 리소스에 대해 수행할 수 있는 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-181">The permissions specified on the SAS indicate what operations the client can perform against the storage resource using the SAS.</span></span> <span data-ttu-id="37b26-182">사용 가능한 권한은 계정 SAS와 서비스 SAS가 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-182">Available permissions differ for an account SAS and a service SAS.</span></span>
* <span data-ttu-id="37b26-183">**IP**</span><span class="sxs-lookup"><span data-stu-id="37b26-183">**IP.**</span></span> <span data-ttu-id="37b26-184">요청을 수락할 Azure 외부(Express 경로에 대한 [라우팅 세션 구성 상태](../expressroute/expressroute-workflows.md#routing-session-configuration-state) 섹션 참조)의 IP 주소 또는 IP 주소 범위를 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-184">An optional parameter that specifies an IP address or a range of IP addresses outside of Azure (see the section [Routing session configuration state](../expressroute/expressroute-workflows.md#routing-session-configuration-state) for Express Route) from which to accept requests.</span></span>
* <span data-ttu-id="37b26-185">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="37b26-185">**Protocol.**</span></span> <span data-ttu-id="37b26-186">요청에 허용되는 프로토콜을 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-186">An optional parameter that specifies the protocol permitted for a request.</span></span> <span data-ttu-id="37b26-187">기본값인 HTTPS 및 HTTP(`https,http`) 또는 HTTPS만(`https`) 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-187">Possible values are both HTTPS and HTTP (`https,http`), which is the default value, or HTTPS only (`https`).</span></span> <span data-ttu-id="37b26-188">HTTP만은 허용되는 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-188">Note that HTTP only is not a permitted value.</span></span>
* <span data-ttu-id="37b26-189">**서명**</span><span class="sxs-lookup"><span data-stu-id="37b26-189">**Signature.**</span></span> <span data-ttu-id="37b26-190">서명은 토큰의 일부로 지정된 다음 암호화된 다른 매개 변수에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-190">The signature is constructed from the other parameters specified as part token and then encrypted.</span></span> <span data-ttu-id="37b26-191">서명은 SAS 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-191">It's used to authenticate the SAS.</span></span>

### <a name="parameters-for-a-service-sas-token"></a><span data-ttu-id="37b26-192">서비스 SAS 토큰의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="37b26-192">Parameters for a service SAS token</span></span>
* <span data-ttu-id="37b26-193">**저장소 리소스**</span><span class="sxs-lookup"><span data-stu-id="37b26-193">**Storage resource.**</span></span> <span data-ttu-id="37b26-194">서비스 SAS를 사용하여 액세스 권한을 위임할 수 있는 저장소 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-194">Storage resources for which you can delegate access with a service SAS include:</span></span>
  * <span data-ttu-id="37b26-195">컨테이너 및 Blob</span><span class="sxs-lookup"><span data-stu-id="37b26-195">Containers and blobs</span></span>
  * <span data-ttu-id="37b26-196">파일 공유 및 파일</span><span class="sxs-lookup"><span data-stu-id="37b26-196">File shares and files</span></span>
  * <span data-ttu-id="37b26-197">큐</span><span class="sxs-lookup"><span data-stu-id="37b26-197">Queues</span></span>
  * <span data-ttu-id="37b26-198">테이블 및 테이블 엔터티 범위</span><span class="sxs-lookup"><span data-stu-id="37b26-198">Tables and ranges of table entities.</span></span>

### <a name="parameters-for-an-account-sas-token"></a><span data-ttu-id="37b26-199">계정 SAS 토큰의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="37b26-199">Parameters for an account SAS token</span></span>
* <span data-ttu-id="37b26-200">**서비스**</span><span class="sxs-lookup"><span data-stu-id="37b26-200">**Service or services.**</span></span> <span data-ttu-id="37b26-201">계정 SAS는 하나 이상의 저장소 서비스에 대한 액세스 권한을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-201">An account SAS can delegate access to one or more of the storage services.</span></span> <span data-ttu-id="37b26-202">예를 들어 Blob 및 파일 서비스에 대한 액세스 권한을 위임하는 계정 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-202">For example, you can create an account SAS that delegates access to the Blob and File service.</span></span> <span data-ttu-id="37b26-203">또는 4개 서비스(Blob, 큐, 테이블, 파일) 전체에 대한 액세스 권한을 위임하는 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-203">Or you can create a SAS that delegates access to all four services (Blob, Queue, Table, and File).</span></span>
* <span data-ttu-id="37b26-204">**저장소 리소스 유형**</span><span class="sxs-lookup"><span data-stu-id="37b26-204">**Storage resource types.**</span></span> <span data-ttu-id="37b26-205">계정 SAS는 특정 리소스가 아닌 하나 이상의 클래스의 저장소 리소스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-205">An account SAS applies to one or more classes of storage resources, rather than a specific resource.</span></span> <span data-ttu-id="37b26-206">계정 SAS를 만들어 다음에 대한 액세스 권한을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-206">You can create an account SAS to delegate access to:</span></span>
  * <span data-ttu-id="37b26-207">저장소 계정 리소스에 대해 호출되는 서비스 수준 API.</span><span class="sxs-lookup"><span data-stu-id="37b26-207">Service-level APIs, which are called against the storage account resource.</span></span> <span data-ttu-id="37b26-208">예를 들면 **서비스 속성 가져오기/설정**, **서비스 통계 가져오기**, **컨테이너/큐/테이블/공유 나열**이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-208">Examples include **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.</span></span>
  * <span data-ttu-id="37b26-209">각 서비스(Blob 컨테이너, 큐, 테이블, 파일 공유)의 컨테이너 개체에 대해 호출되는 컨테이너 수준 API입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-209">Container-level APIs, which are called against the container objects for each service: blob containers, queues, tables, and file shares.</span></span> <span data-ttu-id="37b26-210">예를 들어 **컨테이너 만들기/삭제**, **큐 만들기/삭제**, **테이블 만들기/삭제**, **공유 만들기/삭제**, **Blob/파일 및 디렉터리 나열**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-210">Examples include **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share**, and **List Blobs/Files and Directories**.</span></span>
  * <span data-ttu-id="37b26-211">Blob, 큐 메시지, 테이블 엔터티, 파일에 대해 호출되는 개체 수준 API.</span><span class="sxs-lookup"><span data-stu-id="37b26-211">Object-level APIs, which are called against blobs, queue messages, table entities, and files.</span></span> <span data-ttu-id="37b26-212">예를 들어 **Blob 배치**, **쿼리 엔터티**, **메시지 가져오기**, **파일 만들기**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-212">For example, **Put Blob**, **Query Entity**, **Get Messages**, and **Create File**.</span></span>

## <a name="examples-of-sas-uris"></a><span data-ttu-id="37b26-213">SAS URI의 예</span><span class="sxs-lookup"><span data-stu-id="37b26-213">Examples of SAS URIs</span></span>

### <a name="service-sas-uri-example"></a><span data-ttu-id="37b26-214">서비스 SAS URI 예</span><span class="sxs-lookup"><span data-stu-id="37b26-214">Service SAS URI example</span></span>

<span data-ttu-id="37b26-215">다음은 Blob에 대한 읽기 및 쓰기 권한을 제공하는 서비스 SAS URI의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-215">Here is an example of a service SAS URI that provides read and write permissions to a blob.</span></span> <span data-ttu-id="37b26-216">테이블에서는 URI의 각 부분이 SAS에서 어떤 역할을 하는지를 이해할 수 있도록 세분화했습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-216">The table breaks down each part of the URI to understand how it contributes to the SAS:</span></span>

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| <span data-ttu-id="37b26-217">이름</span><span class="sxs-lookup"><span data-stu-id="37b26-217">Name</span></span> | <span data-ttu-id="37b26-218">SAS 부분</span><span class="sxs-lookup"><span data-stu-id="37b26-218">SAS portion</span></span> | <span data-ttu-id="37b26-219">설명</span><span class="sxs-lookup"><span data-stu-id="37b26-219">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="37b26-220">Blob URI</span><span class="sxs-lookup"><span data-stu-id="37b26-220">Blob URI</span></span> |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |<span data-ttu-id="37b26-221">Blob의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-221">The address of the blob.</span></span> <span data-ttu-id="37b26-222">HTTPS를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-222">Note that using HTTPS is highly recommended.</span></span> |
| <span data-ttu-id="37b26-223">저장소 서비스 버전</span><span class="sxs-lookup"><span data-stu-id="37b26-223">Storage services version</span></span> |`sv=2015-04-05` |<span data-ttu-id="37b26-224">2012-02-12 이후의 저장소 서비스 버전의 경우 이 매개 변수는 사용할 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-224">For storage services version 2012-02-12 and later, this parameter indicates the version to use.</span></span> |
| <span data-ttu-id="37b26-225">시작 시간</span><span class="sxs-lookup"><span data-stu-id="37b26-225">Start time</span></span> |`st=2015-04-29T22%3A18%3A26Z` |<span data-ttu-id="37b26-226">UTC 시간으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-226">Specified in UTC time.</span></span> <span data-ttu-id="37b26-227">SAS를 즉시 유효화하려면 시작 시간을 생략하십시오.</span><span class="sxs-lookup"><span data-stu-id="37b26-227">If you want the SAS to be valid immediately, omit the start time.</span></span> |
| <span data-ttu-id="37b26-228">만료 시간</span><span class="sxs-lookup"><span data-stu-id="37b26-228">Expiry time</span></span> |`se=2015-04-30T02%3A23%3A26Z` |<span data-ttu-id="37b26-229">UTC 시간으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-229">Specified in UTC time.</span></span> |
| <span data-ttu-id="37b26-230">리소스</span><span class="sxs-lookup"><span data-stu-id="37b26-230">Resource</span></span> |`sr=b` |<span data-ttu-id="37b26-231">Blob의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-231">The resource is a blob.</span></span> |
| <span data-ttu-id="37b26-232">권한</span><span class="sxs-lookup"><span data-stu-id="37b26-232">Permissions</span></span> |`sp=rw` |<span data-ttu-id="37b26-233">SAS에서 부여하는 권한에는 읽기 및 쓰기가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-233">The permissions granted by the SAS include Read (r) and Write (w).</span></span> |
| <span data-ttu-id="37b26-234">IP 범위</span><span class="sxs-lookup"><span data-stu-id="37b26-234">IP range</span></span> |`sip=168.1.5.60-168.1.5.70` |<span data-ttu-id="37b26-235">요청을 수락할 IP 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-235">The range of IP addresses from which a request will be accepted.</span></span> |
| <span data-ttu-id="37b26-236">프로토콜</span><span class="sxs-lookup"><span data-stu-id="37b26-236">Protocol</span></span> |`spr=https` |<span data-ttu-id="37b26-237">HTTPS를 사용하는 요청만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-237">Only requests using HTTPS are permitted.</span></span> |
| <span data-ttu-id="37b26-238">서명</span><span class="sxs-lookup"><span data-stu-id="37b26-238">Signature</span></span> |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |<span data-ttu-id="37b26-239">Blob에 대한 액세스 권한을 인증하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-239">Used to authenticate access to the blob.</span></span> <span data-ttu-id="37b26-240">이 서명은 SHA256 알고리즘을 사용하여 서명할 문자열과 키를 통해 계산되고 Base64 인코딩을 사용하여 인코드되는 HMAC입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-240">The signature is an HMAC computed over a string-to-sign and key using the SHA256 algorithm, and then encoded using Base64 encoding.</span></span> |

### <a name="account-sas-uri-example"></a><span data-ttu-id="37b26-241">계정 SAS URI 예</span><span class="sxs-lookup"><span data-stu-id="37b26-241">Account SAS URI example</span></span>

<span data-ttu-id="37b26-242">다음은 토큰에 동일한 일반적 매개 변수를 사용하는 계정 SAS의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-242">Here is an example of an account SAS that uses the same common parameters on the token.</span></span> <span data-ttu-id="37b26-243">이러한 매개 변수는 위에서 설명했으므로 여기에서는 설명을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-243">Since these parameters are described above, they are not described here.</span></span> <span data-ttu-id="37b26-244">계정 SAS에 해당하는 매개 변수만 아래 표에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-244">Only the parameters that are specific to account SAS are described in the table below.</span></span>

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| <span data-ttu-id="37b26-245">이름</span><span class="sxs-lookup"><span data-stu-id="37b26-245">Name</span></span> | <span data-ttu-id="37b26-246">SAS 부분</span><span class="sxs-lookup"><span data-stu-id="37b26-246">SAS portion</span></span> | <span data-ttu-id="37b26-247">설명</span><span class="sxs-lookup"><span data-stu-id="37b26-247">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="37b26-248">리소스 URI</span><span class="sxs-lookup"><span data-stu-id="37b26-248">Resource URI</span></span> |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |<span data-ttu-id="37b26-249">서비스 속성을 가져오거나(GET으로 호출할 경우) 서비스 속성을 설정하기 위한(SET으로 호출하는 경우) 매개 변수를 사용하는 Blob service 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-249">The Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).</span></span> |
| <span data-ttu-id="37b26-250">Services</span><span class="sxs-lookup"><span data-stu-id="37b26-250">Services</span></span> |`ss=bf` |<span data-ttu-id="37b26-251">SAS는 Blob 및 파일 서비스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-251">The SAS applies to the Blob and File services</span></span> |
| <span data-ttu-id="37b26-252">리소스 유형</span><span class="sxs-lookup"><span data-stu-id="37b26-252">Resource types</span></span> |`srt=s` |<span data-ttu-id="37b26-253">SAS는 서비스 수준 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-253">The SAS applies to service-level operations.</span></span> |
| <span data-ttu-id="37b26-254">권한</span><span class="sxs-lookup"><span data-stu-id="37b26-254">Permissions</span></span> |`sp=rw` |<span data-ttu-id="37b26-255">사용 권한으로 읽기 및 쓰기 작업에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-255">The permissions grant access to read and write operations.</span></span> |

<span data-ttu-id="37b26-256">사용 권한이 서비스 수준으로 제한된 경우 이 SAS로 액세스 가능한 작업은 **Blob service 속성 가져오기**(읽기) 및 **Blob service 속성 설정**(쓰기)입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-256">Given that permissions are restricted to the service level, accessible operations with this SAS are **Get Blob Service Properties** (read) and **Set Blob Service Properties** (write).</span></span> <span data-ttu-id="37b26-257">하지만 다른 리소스 URI를 사용하면 동일한 SAS 토큰을 사용하여 **Blob 서비스 통계 가져오기** (읽기)에 대한 액세스 권한을 위임할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-257">However, with a different resource URI, the same SAS token could also be used to delegate access to **Get Blob Service Stats** (read).</span></span>

## <a name="controlling-a-sas-with-a-stored-access-policy"></a><span data-ttu-id="37b26-258">저장된 액세스 정책을 사용하여 SAS 관리</span><span class="sxs-lookup"><span data-stu-id="37b26-258">Controlling a SAS with a stored access policy</span></span>
<span data-ttu-id="37b26-259">공유 액세스 서명은 다음 두 가지 형식 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-259">A shared access signature can take one of two forms:</span></span>

* <span data-ttu-id="37b26-260">**임시 SAS:** 임시 SAS를 만들 때 SAS의 시작 시간, 만료 시간 및 사용 권한이 SAS URI에 모두 지정되거나 시작 시간이 생략되는 경우에는 암시적으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-260">**Ad hoc SAS:** When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified in the SAS URI (or implied, in the case where start time is omitted).</span></span> <span data-ttu-id="37b26-261">이 SAS 유형은 계정 SAS 또는 서비스 SAS로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-261">This type of SAS can be created as an account SAS or a service SAS.</span></span>
* <span data-ttu-id="37b26-262">**저장된 액세스 정책 사용 SAS:** 저장된 액세스 정책은 리소스 컨테이너(Blob 컨테이너, 테이블, 큐 또는 파일 공유)에서 정의되며, 하나 이상의 공유 액세스 서명에 대한 제약 조건을 관리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-262">**SAS with stored access policy:** A stored access policy is defined on a resource container--a blob container, table, queue, or file share--and can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="37b26-263">SAS를 공유 액세스 정책과 연결할 경우 SAS는 저장된 액세스 정책에 대해 정의된 제약 조건(시작 시간, 만료 시간 및 사용 권한)을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-263">When you associate a SAS with a stored access policy, the SAS inherits the constraints--the start time, expiry time, and permissions--defined for the stored access policy.</span></span>

> [!NOTE]
> <span data-ttu-id="37b26-264">현재, 계정 SAS는 애드혹 SAS여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-264">Currently, an account SAS must be an ad hoc SAS.</span></span> <span data-ttu-id="37b26-265">저장된 액세스 정책은 아직 계정 SAS에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-265">Stored access policies are not yet supported for account SAS.</span></span>

<span data-ttu-id="37b26-266">두 형식의 차이점은 주요 시나리오인 해지에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-266">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="37b26-267">SAS URI는 URL이므로 원래 작성자에 관계없이 SAS를 가져오는 모든 사용자가 이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-267">Because a SAS URI is a URL, anyone that obtains the SAS can use it, regardless of who originally created it.</span></span> <span data-ttu-id="37b26-268">SAS가 공개적으로 게시된 경우 전 세계의 모든 사용자가 SAS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-268">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="37b26-269">SAS는 다음 네 가지 중 하나에 해당할 때까지 소유하고 있는 모든 사용자에게 리소스에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-269">A SAS grants access to resources to anyone possessing it until one of four things happens:</span></span>

1. <span data-ttu-id="37b26-270">SAS에 지정된 만료 시간에 도달한 경우</span><span class="sxs-lookup"><span data-stu-id="37b26-270">The expiry time specified on the SAS is reached.</span></span>
2. <span data-ttu-id="37b26-271">SAS에서 참조되는 저장된 액세스 정책에 지정된 만료 시간에 도달한 경우(저장된 액세스 정책을 참조하고 이 정책에 만료 시간이 지정된 경우).</span><span class="sxs-lookup"><span data-stu-id="37b26-271">The expiry time specified on the stored access policy referenced by the SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span></span> <span data-ttu-id="37b26-272">시간 간격이 경과하거나 저장된 액세스 정책에서 만료 시간을 과거의 시간으로 수정한 경우에 발생할 수 있으며 이는 SAS를 해지하는 한 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-272">This can occur either because the interval elapses, or because you've modified the stored access policy with an expiry time in the past, which is one way to revoke the SAS.</span></span>
3. <span data-ttu-id="37b26-273">SAS에서 참조되는 저장된 액세스 정책을 삭제한 경우(SAS를 해지하는 다른 방법).</span><span class="sxs-lookup"><span data-stu-id="37b26-273">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="37b26-274">동일한 이름을 사용하여 저장된 액세스 정책을 다시 만들면 저장된 액세스 정책에 연결된 사용 권한에 따라 모든 기존 SAS 토큰이 다시 유효해집니다(SAS의 만료 시간이 경과하지 않은 것으로 가정).</span><span class="sxs-lookup"><span data-stu-id="37b26-274">Note that if you recreate the stored access policy with exactly the same name, all existing SAS tokens will again be valid according to the permissions associated with that stored access policy (assuming that the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="37b26-275">SAS를 해지하기 위해 만료 시간을 미래의 시간으로 지정하여 액세스 정책을 다시 만들 경우 다른 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-275">If you are intending to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>
4. <span data-ttu-id="37b26-276">SAS를 만드는 데 사용된 계정 키를 다시 생성한 경우.</span><span class="sxs-lookup"><span data-stu-id="37b26-276">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="37b26-277">계정 키를 다시 생성하면 해당 키를 사용하는 모든 응용 프로그램 구성 요소는 다른 유효한 계정 키 또는 새로 생성된 계정 키를 사용하도록 업데이트될 때까지 인증되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-277">Regenerating an account key will cause all application components using that key to fail to authenticate until they're updated to use either the other valid account key or the newly regenerated account key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37b26-278">공유 액세스 서명 URI는 서명을 만드는 데 사용된 계정 키 및 저장된 관련 액세스 정책(있는 경우)에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-278">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="37b26-279">저장된 액세스 정책을 지정하지 않는 경우 공유 액세스 서명을 해지하는 방법은 계정 키를 변경하는 것뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-279">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

## <a name="authenticating-from-a-client-application-with-a-sas"></a><span data-ttu-id="37b26-280">SAS를 사용하여 클라이언트 응용 프로그램 인증</span><span class="sxs-lookup"><span data-stu-id="37b26-280">Authenticating from a client application with a SAS</span></span>
<span data-ttu-id="37b26-281">SAS를 소유하는 클라이언트는 SAS를 사용하여 계정 키를 소유하지 않는 저장소 계정에 대해 요청을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-281">A client who is in possession of a SAS can use the SAS to authenticate a request against a storage account for which they do not possess the account keys.</span></span> <span data-ttu-id="37b26-282">SAS는 연결 문자열에 포함되거나 적절한 생성자 또는 메서드에서 직접 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-282">A SAS can be included in a connection string, or used directly from the appropriate constructor or method.</span></span>

### <a name="using-a-sas-in-a-connection-string"></a><span data-ttu-id="37b26-283">연결 문자열에서 SAS 사용</span><span class="sxs-lookup"><span data-stu-id="37b26-283">Using a SAS in a connection string</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a><span data-ttu-id="37b26-284">생성자 또는 메서드에서 SAS 사용</span><span class="sxs-lookup"><span data-stu-id="37b26-284">Using a SAS in a constructor or method</span></span>
<span data-ttu-id="37b26-285">여러 Azure Storage 클라이언트 라이브러리 생성자와 메서드 오버로드는 SAS 매개 변수를 제공하므로 SAS를 사용하는 서비스에 대한 요청을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-285">Several Azure Storage client library constructors and method overloads offer a SAS parameter, so that you can authenticate a request to the service with a SAS.</span></span>

<span data-ttu-id="37b26-286">예를 들어, 여기서 블록 blob에 대한 참조를 만드는 데 SAS URI가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-286">For example, here a SAS URI is used to create a reference to a block blob.</span></span> <span data-ttu-id="37b26-287">SAS는 요청에 필요한 유일한 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-287">The SAS provides the only credentials needed for the request.</span></span> <span data-ttu-id="37b26-288">그런 다음 블록 blob 참조는 쓰기 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-288">The block blob reference is then used for a write operation:</span></span>

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with the specified name to the container.
// If the blob does not exist, it will be created. If it does exist, it will be overwritten.
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

## <a name="best-practices-when-using-sas"></a><span data-ttu-id="37b26-289">SAS를 사용하는 경우 모범 사례</span><span class="sxs-lookup"><span data-stu-id="37b26-289">Best practices when using SAS</span></span>
<span data-ttu-id="37b26-290">응용 프로그램에서 공유 액세스 서명을 사용할 경우 다음과 같은 두 가지 잠재적 위험에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-290">When you use shared access signatures in your applications, you need to be aware of two potential risks:</span></span>

* <span data-ttu-id="37b26-291">SAS가 누설될 경우 SAS를 획득한 모든 사용자가 SAS를 사용하여 저장소 계정을 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-291">If a SAS is leaked, it can be used by anyone who obtains it, which can potentially compromise your storage account.</span></span>
* <span data-ttu-id="37b26-292">클라이언트 응용 프로그램에 제공된 SAS가 만료되어 응용 프로그램이 서비스에서 새 SAS를 검색할 수 없는 경우 응용 프로그램의 기능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-292">If a SAS provided to a client application expires and the application is unable to retrieve a new SAS from your service, then the application's functionality may be hindered.</span></span>

<span data-ttu-id="37b26-293">다음은 공유 액세스 서명을 사용하여 이러한 위험을 완화하는 데 도움이 될 수 있는 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-293">The following recommendations for using shared access signatures can help mitigate these risks:</span></span>

1. <span data-ttu-id="37b26-294">**항상 HTTPS를 사용하여** SAS를 만들거나 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-294">**Always use HTTPS** to create or distribute a SAS.</span></span> <span data-ttu-id="37b26-295">HTTP를 통해 SAS를 전달할 경우 SAS가 노출되면 메시지 가로채기(man-in-the-middle) 공격을 수행하는 공격자가 SAS를 읽은 다음 의도된 사용자처럼 SAS를 사용할 수 있으므로, 악의적인 사용자가 중요한 데이터를 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-295">If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack is able to read the SAS and then use it just as the intended user could have, potentially compromising sensitive data or allowing for data corruption by the malicious user.</span></span>
2. <span data-ttu-id="37b26-296">**저장된 액세스 정책을 최대한 참조합니다.**</span><span class="sxs-lookup"><span data-stu-id="37b26-296">**Reference stored access policies where possible.**</span></span> <span data-ttu-id="37b26-297">저장된 액세스 정책을 사용하면 저장소 계정 키를 다시 생성할 필요 없이 사용 권한을 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-297">Stored access policies give you the option to revoke permissions without having to regenerate the storage account keys.</span></span> <span data-ttu-id="37b26-298">만료 시간을 매우 길게(또는 무제한) 설정하고 정기적으로 업데이트하여 만료 시간을 미래의 시간으로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-298">Set the expiration on these very far in the future (or infinite) and make sure it's regularly updated to move it farther into the future.</span></span>
3. <span data-ttu-id="37b26-299">**임시 SAS의 경우 짧은 만료 시간을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="37b26-299">**Use near-term expiration times on an ad hoc SAS.**</span></span> <span data-ttu-id="37b26-300">그러면 SAS가 손상되더라도 단기적으로만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-300">In this way, even if a SAS is compromised, it's valid only for a short time.</span></span> <span data-ttu-id="37b26-301">이 방법은 저장된 액세스 정책을 참조할 수 없는 경우에 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-301">This practice is especially important if you cannot reference a stored access policy.</span></span> <span data-ttu-id="37b26-302">또한 짧은 만료 시간은 업로드할 수 있는 시간을 제한하여 Blob에 쓸 수 있는 데이터의 양을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-302">Near-term expiration times also limit the amount of data that can be written to a blob by limiting the time available to upload to it.</span></span>
4. <span data-ttu-id="37b26-303">**필요한 경우 클라이언트가 SAS를 자동으로 갱신하도록 허용합니다.**</span><span class="sxs-lookup"><span data-stu-id="37b26-303">**Have clients automatically renew the SAS if necessary.**</span></span> <span data-ttu-id="37b26-304">클라이언트는 만료일 이전에 SAS를 갱신하여 SAS를 제공하는 서비스를 사용할 수 없을 때 다시 시도할 수 있는 시간적 여유를 확보해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-304">Clients should renew the SAS well before the expiration, in order to allow time for retries if the service providing the SAS is unavailable.</span></span> <span data-ttu-id="37b26-305">만료 기간 내에 완료할 수 있는 즉각적인 소규모 단기 작업에 SAS를 사용할 경우에는 SAS를 갱신할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-305">If your SAS is meant to be used for a small number of immediate, short-lived operations that are expected to be completed within the expiration period, then this may be unnecessary as the SAS is not expected to be renewed.</span></span> <span data-ttu-id="37b26-306">하지만 클라이언트가 SAS를 통해 일상 요청을 수행하는 경우에는 중간에 만료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-306">However, if you have client that is routinely making requests via SAS, then the possibility of expiration comes into play.</span></span> <span data-ttu-id="37b26-307">따라서 이전에 언급한 SAS 단기 실행 요구 사항과 클라이언트가 조기에 갱신을 요청하여 갱신 이전에 SAS가 만료되어 가동 중단이 발생하는 것을 방지해야 하는 요구 사항을 적절하게 조율하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-307">The key consideration is to balance the need for the SAS to be short-lived (as previously stated) with the need to ensure that the client is requesting renewal early enough (to avoid disruption due to the SAS expiring prior to successful renewal).</span></span>
5. <span data-ttu-id="37b26-308">**SAS 시작 시간에 유의하세요.**</span><span class="sxs-lookup"><span data-stu-id="37b26-308">**Be careful with SAS start time.**</span></span> <span data-ttu-id="37b26-309">SAS 시작 시간을 **지금**으로 설정한 경우 클럭 오차(컴퓨터의 차이에 따른 현재 시간의 차이)로 인해 처음 몇 분 동안 간헐적으로 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-309">If you set the start time for a SAS to **now**, then due to clock skew (differences in current time according to different machines), failures may be observed intermittently for the first few minutes.</span></span> <span data-ttu-id="37b26-310">일반적으로 시작 시간을 최소 15분 이전으로 설정하거나</span><span class="sxs-lookup"><span data-stu-id="37b26-310">In general, set the start time to be at least 15 minutes in the past.</span></span> <span data-ttu-id="37b26-311">설정하지 않습니다. 그러면 시작 시간이 즉시 유효해집니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-311">Or, don't set it at all, which will make it valid immediately in all cases.</span></span> <span data-ttu-id="37b26-312">이는 만료 시간에도 일반적으로 적용됩니다. 요청 방향에서 최대 15분의 클럭 오차가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-312">The same generally applies to expiry time as well--remember that you may observe up to 15 minutes of clock skew in either direction on any request.</span></span> <span data-ttu-id="37b26-313">2012-02-12 이전 REST 버전을 사용하는 클라이언트의 경우 저장된 액세스 정책을 참조하지 않는 SAS의 최대 기간은 1시간이고, 이 시간보다 더 긴 기간을 지정하는 정책은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-313">For clients using a REST version prior to 2012-02-12, the maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.</span></span>
6. <span data-ttu-id="37b26-314">**액세스할 리소스를 구체적으로 지정하세요.**</span><span class="sxs-lookup"><span data-stu-id="37b26-314">**Be specific with the resource to be accessed.**</span></span> <span data-ttu-id="37b26-315">보안을 위한 최적의 방법은 사용자에게 필요한 최소 권한을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-315">A security best practice is to provide a user with the minimum required privileges.</span></span> <span data-ttu-id="37b26-316">사용자가 단일 엔터티에 대한 읽기 권한만 필요한 경우 해당 엔터티에 대한 읽기 권한만 부여하고 모든 엔터티에 대한 읽기/쓰기/삭제 권한은 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-316">If a user only needs read access to a single entity, then grant them read access to that single entity, and not read/write/delete access to all entities.</span></span> <span data-ttu-id="37b26-317">또한 SAS가 공격자의 수중에 넘어갈 가능성이 낮아지므로 SAS가 손상될 경우 손해가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-317">This also helps lessen the damage if a SAS is compromised because the SAS has less power in the hands of an attacker.</span></span>
7. <span data-ttu-id="37b26-318">**SAS 사용 작업을 포함한 모든 사용량에 대한 요금이 계정에 청구됩니다.**</span><span class="sxs-lookup"><span data-stu-id="37b26-318">**Understand that your account will be billed for any usage, including that done with SAS.**</span></span> <span data-ttu-id="37b26-319">Blob에 쓰기 권한을 제공한 경우 사용자가 200GB Blob을 업로드하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-319">If you provide write access to a blob, a user may choose to upload a 200GB blob.</span></span> <span data-ttu-id="37b26-320">사용자에게 읽기 권한도 제공한 경우 사용자가 이 Blob을 10번 다운로드하도록 선택하여 2TB의 발신 비용이 청구될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-320">If you've given them read access as well, they may choose to download it 10 times, incurring 2 TB in egress costs for you.</span></span> <span data-ttu-id="37b26-321">또한 제한된 권한을 제공하여 악의적인 사용자의 작업 가능성을 낮추세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-321">Again, provide limited permissions to help mitigate the potential actions of malicious users.</span></span> <span data-ttu-id="37b26-322">단기 실행 SAS를 사용하여 이 위협을 줄이세요. 이때 종료 시간의 클럭 오차에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-322">Use short-lived SAS to reduce this threat (but be mindful of clock skew on the end time).</span></span>
8. <span data-ttu-id="37b26-323">**SAS를 사용하여 작성된 데이터의 유효성을 검사하세요.**</span><span class="sxs-lookup"><span data-stu-id="37b26-323">**Validate data written using SAS.**</span></span> <span data-ttu-id="37b26-324">클라이언트 응용 프로그램이 저장소 계정에 데이터를 쓸 경우 해당 데이터에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-324">When a client application writes data to your storage account, keep in mind that there can be problems with that data.</span></span> <span data-ttu-id="37b26-325">데이터를 사용할 준비가 되기 이전에 응용 프로그램에서 데이터의 유효성을 검사하거나 권한을 부여해야 하는 경우 데이터를 작성한 이후 응용 프로그램에서 데이터를 사용하기 이전에 유효성 검사를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-325">If your application requires that that data be validated or authorized before it is ready to use, you should perform this validation after the data is written and before it is used by your application.</span></span> <span data-ttu-id="37b26-326">그러면 SAS를 적절한 방법으로 습득한 사용자나 누설된 SAS를 악용하는 사용자로 인해 계정이 손상되거나 데이터에 악의적인 데이터가 기록되는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-326">This practice also protects against corrupt or malicious data being written to your account, either by a user who properly acquired the SAS, or by a user exploiting a leaked SAS.</span></span>
9. <span data-ttu-id="37b26-327"><seg>
  **경우에 따라 SAS를 사용하지 마세요..**</seg></span><span class="sxs-lookup"><span data-stu-id="37b26-327">**Don't always use SAS.**</span></span> <span data-ttu-id="37b26-328">저장소 계정에 대한 특정 작업 관련 위험이 SAS의 이점을 능가하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-328">Sometimes the risks associated with a particular operation against your storage account outweigh the benefits of SAS.</span></span> <span data-ttu-id="37b26-329">그런 작업에 대해서는 비즈니스 규칙 유효성 검사, 인증 및 감사를 수행한 이후에 저장소 계정에 쓰는 중간 계층 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-329">For such operations, create a middle-tier service that writes to your storage account after performing business rule validation, authentication, and auditing.</span></span> <span data-ttu-id="37b26-330">또한 다른 방법으로 액세스를 관리하는 것이 더 간단한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-330">Also, sometimes it's simpler to manage access in other ways.</span></span> <span data-ttu-id="37b26-331">예를 들어 컨테이너의 모든 Blob을 공개적으로 읽기 가능하도록 설정하려면 모든 클라이언트가 액세스하도록 SAS를 제공하는 대신에 컨테이너를 공용으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-331">For example, if you want to make all blobs in a container publically readable, you can make the container Public, rather than providing a SAS to every client for access.</span></span>
10. <span data-ttu-id="37b26-332">**저장소 분석을 사용하여 응용 프로그램을 모니터링합니다.**</span><span class="sxs-lookup"><span data-stu-id="37b26-332">**Use Storage Analytics to monitor your application.**</span></span> <span data-ttu-id="37b26-333">로깅 및 메트릭을 사용하여 SAS 공급자 서비스의 가동 중단이나 저장된 액세스 정책의 잘못된 제거로 인한 인증 오류의 급격한 증가를 관찰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-333">You can use logging and metrics to observe any spike in authentication failures due to an outage in your SAS provider service or to the inadvertent removal of a stored access policy.</span></span> <span data-ttu-id="37b26-334">자세한 내용은 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) (영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="37b26-334">See the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) for additional information.</span></span>

## <a name="sas-examples"></a><span data-ttu-id="37b26-335">SAS 예제</span><span class="sxs-lookup"><span data-stu-id="37b26-335">SAS examples</span></span>
<span data-ttu-id="37b26-336">다음은 공유 액세스 서명의 두 유형(계정 SAS, 서비스 SAS)에 대한 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-336">Below are some examples of both types of shared access signatures, account SAS and service SAS.</span></span>

<span data-ttu-id="37b26-337">이러한 C# 예제를 실행하려면 프로젝트에서 다음 NuGet 패키지를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-337">To run these C# examples, you need to reference the following NuGet packages in your project:</span></span>

* <span data-ttu-id="37b26-338">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), 버전 6.x 이상(계정 SAS 사용을 위해).</span><span class="sxs-lookup"><span data-stu-id="37b26-338">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x or later (to use account SAS).</span></span>
* [<span data-ttu-id="37b26-339">Azure 구성 관리자</span><span class="sxs-lookup"><span data-stu-id="37b26-339">Azure Configuration Manager</span></span>](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

<span data-ttu-id="37b26-340">SAS를 만들고 테스트하는 방법을 보여 주는 추가 예제는 [저장소에 대한 Azure 코드 샘플](https://azure.microsoft.com/documentation/samples/?service=storage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b26-340">For additional examples that show how to create and test a SAS, see [Azure Code Samples for Storage](https://azure.microsoft.com/documentation/samples/?service=storage).</span></span>

### <a name="example-create-and-use-an-account-sas"></a><span data-ttu-id="37b26-341">예제: SAS 계정 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="37b26-341">Example: Create and use an account SAS</span></span>
<span data-ttu-id="37b26-342">다음 코드 예제는 Blob 및 파일 공유에 유효한 계정 SAS를 만들며 클라이언트가 읽기, 쓰기, 목록 권한을 사용하여 서비스 수준 API에 액세스할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-342">The following code example creates an account SAS that is valid for the Blob and File services, and gives the client permissions read, write, and list permissions to access service-level APIs.</span></span> <span data-ttu-id="37b26-343">계정 SAS는 프로토콜을 HTTPS로 제한하므로 반드시 HTTPS로 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-343">The account SAS restricts the protocol to HTTPS, so the request must be made with HTTPS.</span></span>

```csharp
static string GetAccountSASToken()
{
    // To create the account SAS, you need to use your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for the account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return the SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

<span data-ttu-id="37b26-344">계정 SAS를 사용하여 Blob 서비스에 대한 서비스 수준 API에 액세스하려면 SAS를 사용하는 Blob 클라이언트 개체와 저장소 계정의 Blob 저장소 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-344">To use the account SAS to access service-level APIs for the Blob service, construct a Blob client object using the SAS and the Blob storage endpoint for your storage account.</span></span>

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using the SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and the account name to create a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set the service properties for the Blob client created with the SAS.
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

    // The permissions granted by the account SAS also permit you to retrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a><span data-ttu-id="37b26-345">예제: 저장된 액세스 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="37b26-345">Example: Create a stored access policy</span></span>
<span data-ttu-id="37b26-346">다음 코드는 컨테이너에 저장된 액세스 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-346">The following code creates a stored access policy on a container.</span></span> <span data-ttu-id="37b26-347">액세스 정책을 사용하여 컨테이너나 해당 Blob에 서비스 SAS에 대한 제약 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-347">You can use the access policy to specify constraints for a service SAS on the container or its blobs.</span></span>

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // The access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
        // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get the container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a><span data-ttu-id="37b26-348">예제: 컨테이너에 서비스 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="37b26-348">Example: Create a service SAS on a container</span></span>
<span data-ttu-id="37b26-349">다음 코드는 컨테이너에 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-349">The following code creates a SAS on a container.</span></span> <span data-ttu-id="37b26-350">기존에 저장된 액세스 정책의 이름을 제공하는 경우 해당 정책은 SAS와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-350">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span></span> <span data-ttu-id="37b26-351">저장된 액세스 정책이 제공되지 않는 경우 코드는 컨테이너에서 임시 SAS을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-351">If no stored access policy is provided, then the code creates an ad-hoc SAS on the container.</span></span>

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate the shared access signature on the container, setting the constraints directly on the signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the container. In this case, all of the constraints for the
        // shared access signature are specified on the stored access policy, which is provided by name.
        // It is also possible to specify some constraints on an ad-hoc SAS and others on the stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a><span data-ttu-id="37b26-352">예제: Blob에 서비스 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="37b26-352">Example: Create a service SAS on a blob</span></span>
<span data-ttu-id="37b26-353">다음 코드는 Blob에 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-353">The following code creates a SAS on a blob.</span></span> <span data-ttu-id="37b26-354">기존에 저장된 액세스 정책의 이름을 제공하는 경우 해당 정책은 SAS와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-354">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span></span> <span data-ttu-id="37b26-355">저장된 액세스 정책이 제공되지 않는 경우 코드는 Blob에서 임시 SAS을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-355">If no stored access policy is provided, then the code creates an ad-hoc SAS on the blob.</span></span>

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference to a blob within the container.
    // Note that the blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate the shared access signature on the blob, setting the constraints directly on the signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the blob. In this case, all of the constraints for the
        // shared access signature are specified on the container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a><span data-ttu-id="37b26-356">결론</span><span class="sxs-lookup"><span data-stu-id="37b26-356">Conclusion</span></span>
<span data-ttu-id="37b26-357">공유 액세스 서명은 계정 키가 필요하지 않은 클라이언트에게 저장소 계정에 대한 제한된 권한을 제공하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-357">Shared access signatures are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="37b26-358">일반적으로 공유 액세스 서명은 Azure 저장소를 사용하는 응용 프로그램에 대한 보안 모델의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-358">As such, they are a vital part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="37b26-359">여기에 나열된 모범 사례를 따를 경우 SAS를 사용하여 응용 프로그램의 보안을 훼손하지 않으면서 저장소 계정에 있는 리소스에 유연하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b26-359">If you follow the best practices listed here, you can use SAS to provide greater flexibility of access to resources in your storage account, without compromising the security of your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37b26-360">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37b26-360">Next Steps</span></span>
* [<span data-ttu-id="37b26-361">컨테이너 및 Blob에 대한 익명 읽기 권한 관리</span><span class="sxs-lookup"><span data-stu-id="37b26-361">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="37b26-362">공유 액세스 서명을 사용하여 액세스 위임</span><span class="sxs-lookup"><span data-stu-id="37b26-362">Delegating Access with a Shared Access Signature</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="37b26-363">테이블 및 큐 SAS 소개</span><span class="sxs-lookup"><span data-stu-id="37b26-363">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png
