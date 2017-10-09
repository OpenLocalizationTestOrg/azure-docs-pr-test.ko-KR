---
title: "Azure에서 암호화를 사용 하 여 전송 중에 aaaProtect 개인 데이터 | Microsoft Docs"
description: "Azure tooprotect 개인 데이터에 암호화를 사용 하 여"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="8f38e-103">Azure 암호화 기술: 암호화를 사용하여 전송 중인 개인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="8f38e-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="8f38e-104">이 문서는 이해 하 고 전송 중에 Azure 암호화 기술을 toosecure 데이터를 사용 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="8f38e-105">개인 데이터의 개인 정보 보호 hello 보호 hello 네트워크를 통과할 때 여러 레이어로 된 방어 보안 전략의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="8f38e-106">전송 중에 암호화에는 디자인 된 tooprevent 전송 tooview 또는 사용 하 여 hello 데이터 수 없도록 차단 하는 공격자는입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="8f38e-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="8f38e-107">Scenario</span></span>

<span data-ttu-id="8f38e-108">Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="8f38e-109">toosupport 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력 독일, 덴마크 및 hello 영국</span><span class="sxs-lookup"><span data-stu-id="8f38e-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="8f38e-110">hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="8f38e-111">여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="8f38e-112">또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="8f38e-113">hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="8f38e-114">Hello world 주변에 있는 여행사 및 원격 사무실 hello 회사에서에서 고객의 개인 데이터 hello 데이터베이스에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="8f38e-115">고객 정보를 포함 하는 문서는 hello 네트워크 tooAzure 저장소를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="8f38e-116">문제 설명</span><span class="sxs-lookup"><span data-stu-id="8f38e-116">Problem statement</span></span>

<span data-ttu-id="8f38e-117">hello 회사에서 고객의의 hello 개인 정보를 보호 해야 하 고 Azure 서비스에서 전송 tooand 동안 직원의 개인 데이터는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="8f38e-118">회사 목표</span><span class="sxs-lookup"><span data-stu-id="8f38e-118">Company goal</span></span>

<span data-ttu-id="8f38e-119">회사 목표 tooensure hello 개인 데이터 디스크 끄기 때 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="8f38e-120">권한 없는 사람이 가로챌 hello 디스크 외부 개인 데이터를 렌더링 하 고 읽을 수 없는 형식에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="8f38e-121">암호화를 적용하는 경우 사용자 또는 관리자에게 쉽고 완전히 투명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="8f38e-122">솔루션</span><span class="sxs-lookup"><span data-stu-id="8f38e-122">Solutions</span></span>

<span data-ttu-id="8f38e-123">Azure 서비스는 여러 도구와 기술 toohelp 제공 전송 되는 개인 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="8f38e-124">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="8f38e-124">Azure Storage</span></span>

<span data-ttu-id="8f38e-125">Hello world, toohello Azure 데이터 센터에에서 모든 위치에 실제로 있을 수 있습니다 hello 클라이언트에서 hello 클라우드에 저장 된 데이터를 전송 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="8f38e-126">Hello에 다시 전달를 사용자가 해당 데이터를 검색할 때 방향이 반대입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="8f38e-127">데이터 hello를 통해 전송 되는 공용 인터넷 공격자의 목표가 인터 셉 션의 위험에 항상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="8f38e-128">개인 데이터의 중요 한 tooprotect hello 개인 정보 보호 위치 간에 이동 하는 것으로 전송 수준 암호화 toosecure를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8f38e-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="8f38e-129">HTTPS 프로토콜 hello hello 인터넷을 통해 안전 하 고 암호화 된 통신 채널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="8f38e-130">REST Api를 호출할 때 HTTPS 및 Azure 저장소의 사용된 tooaccess 개체 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="8f38e-131">사용 하는 경우 hello HTTPS 프로토콜의 사용 적용 [공유 액세스 서명](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate tooAzure 저장소 개체에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="8f38e-132">SAS에는 두 가지 유형, 즉 서비스 SAS와 계정 SAS가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="8f38e-133">서비스 SAS를 구성하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="8f38e-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="8f38e-134">서비스 SAS 대리자 액세스 tooa 리소스의 hello 저장소 서비스 (blob, 큐, 테이블 또는 파일 서비스) 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="8f38e-135">서비스 SAS tooconstruct 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="8f38e-136">Hello 서명 됨 버전 필드 지정</span><span class="sxs-lookup"><span data-stu-id="8f38e-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="8f38e-137">Hello 서명 됨 리소스 (Blob 및 파일 서비스에만 해당)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="8f38e-138">쿼리 매개 변수 tooOverride 응답 헤더 (Blob 서비스 및 파일 서비스에만 해당)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="8f38e-139">Hello 테이블 이름 (테이블 서비스에만 해당)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="8f38e-140">Hello 액세스 정책 지정</span><span class="sxs-lookup"><span data-stu-id="8f38e-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="8f38e-141">Hello 서명 유효성 간격 지정</span><span class="sxs-lookup"><span data-stu-id="8f38e-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="8f38e-142">권한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-142">Specify Permissions</span></span>

9. <span data-ttu-id="8f38e-143">IP 주소 또는 IP 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="8f38e-144">Hello HTTP 프로토콜을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="8f38e-145">테이블 액세스 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="8f38e-146">Hello 서명 됨 식별자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="8f38e-147">Hello 서명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-147">Specify hello Signature</span></span>

<span data-ttu-id="8f38e-148">자세한 지침은 [서비스 SAS 구성](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f38e-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="8f38e-149">계정 SAS를 구성하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="8f38e-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="8f38e-150">계정 SAS 액세스 tooresources 하나 이상의 hello 저장소 서비스에 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="8f38e-151">또한 액세스 tooread, 쓰기 및 삭제 작업을 blob 컨테이너, 테이블, 큐 및 서비스 SAS와 함께 사용할 수 없는 파일 공유를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="8f38e-152">계정 SAS 생성할 때 서비스 sa 비슷한 toothat 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="8f38e-153">자세한 지침은 [계정 SAS 구성](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f38e-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="8f38e-154">REST API를 호출할 때 HTTPS를 적용하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="8f38e-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="8f38e-155">저장소 계정에서 REST Api tooaccess 개체를 호출할 때 HTTPS tooenforce hello 사용을 활성화할 수 있습니다 필요한 전송 보안 hello 저장소 계정에 대 한.</span><span class="sxs-lookup"><span data-stu-id="8f38e-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="8f38e-156">Hello Azure 포털에서에서 선택 **저장소 계정 만들기**, 기존 저장소 계정을 선택 하거나 **설정** 차례로 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="8f38e-157">**보안 전송 필요** 아래에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![저장소 계정 만들기](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="8f38e-159">자세한 내용은 포함 하 여 tooenable 필수 전송 보안 프로그래밍 방식으로 참조 하는 방법 [전송 보안을 설정 해야](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="8f38e-160">Azure File Storage에서 데이터를 암호화하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="8f38e-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="8f38e-161">tooencrypt 데이터와 전송 중에 [Azure 파일 저장소](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), SMB를 사용할 수 있습니다 Windows 8, 8.1 및 10 및 Windows Server 2012 R2 및 Windows Server 2016 3.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="8f38e-162">Hello Azure 파일 서비스를 사용 하는 암호화 되지 않은 모든 연결 실패 "보안 전송 필요"를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="8f38e-163">SMB 2.1, SMB 3.0 암호화 없이 및 일부 버전의 Linux SMB 클라이언트 hello 사용 하는 시나리오를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="8f38e-164">Azure 클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="8f38e-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="8f38e-165">클라이언트 응용 프로그램과 Azure Storage 간에 전송되는 데이터를 보호하기 위한 또 다른 옵션은 [클라이언트 쪽 암호화](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="8f38e-166">Azure 저장소로 전송 하기 전에 hello 데이터는 암호화 및 hello 클라이언트 쪽에서 받은 후 hello 데이터를 암호 해독할 때 Azure 저장소에서 hello 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="8f38e-167">Azure 사이트 간 VPN</span><span class="sxs-lookup"><span data-stu-id="8f38e-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="8f38e-168">회사 네트워크 또는 사용자와 hello Azure 가상 네트워크 간에 데이터가 전송는 효과적인 방법은 tooprotect 개인 데이터는 toouse는 [사이트 간](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) 또는 [지점 및 사이트](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 가상 개인 네트워크 (VPN).</span><span class="sxs-lookup"><span data-stu-id="8f38e-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="8f38e-169">VPN 연결 hello 인터넷 간에 암호화 된 보안 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="8f38e-170">사이트 간 VPN 연결을 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="8f38e-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="8f38e-171">사이트 간 VPN hello 회사 네트워크 tooAzure에서 여러 사용자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="8f38e-172">hello Azure 포털에서에서 사이트 간 연결 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="8f38e-173">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-173">Create a virtual network.</span></span>

2. <span data-ttu-id="8f38e-174">DNS 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="8f38e-175">Hello 게이트웨이 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="8f38e-176">Hello VPN 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="8f38e-177">Hello 로컬 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="8f38e-178">VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="8f38e-179">Hello VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="8f38e-180">Hello VPN 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="8f38e-181">자세한 지침은에 어떻게 toocreate는 사이트 및 사이트 간 연결에 hello Azure 포털에서 참조 [hello Azure 포털에서에서 사이트-사이트 만들기 연결 합니다.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="8f38e-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="8f38e-182">지점 및 사이트 간 VPN 연결을 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="8f38e-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="8f38e-183">지점-사이트 VPN 개별 클라이언트 컴퓨터 tooa 가상 네트워크에서 보안 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="8f38e-184">집 이나 호텔 또는 회의 센터에서와 같은 원격 위치에서 tooconnect tooAzure을 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="8f38e-185">toocreate hello Azure 포털에서에서 지점 및 사이트 연결</span><span class="sxs-lookup"><span data-stu-id="8f38e-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="8f38e-186">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-186">Create a virtual network.</span></span>

2. <span data-ttu-id="8f38e-187">게이트웨이 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="8f38e-188">DNS 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-188">Specify a DNS server.</span></span> <span data-ttu-id="8f38e-189">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8f38e-189">(optional)</span></span>

4. <span data-ttu-id="8f38e-190">가상 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="8f38e-191">인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-191">Generate certificates.</span></span>

6. <span data-ttu-id="8f38e-192">Hello 클라이언트 주소 풀을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="8f38e-193">Hello 루트 인증서 공용 인증서 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="8f38e-194">생성 하 고 hello VPN 클라이언트 구성 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="8f38e-195">내보낸 클라이언트 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="8f38e-196">TooAzure를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="8f38e-197">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-197">Verify your connection.</span></span>

<span data-ttu-id="8f38e-198">자세한 내용은 참조 [지점 및 사이트 연결 tooa VNet 구성 인증서 인증을 사용 하 여: Azure 포털입니다.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="8f38e-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="8f38e-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="8f38e-199">SSL/TLS</span></span>

<span data-ttu-id="8f38e-200">다른 위치에서 SSL/TLS 프로토콜 tooexchange 데이터를 항상 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="8f38e-201">Toouse를 선택 하는 조직은 [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove 큰 데이터 집합 전용된 고속 WAN 링크를 통해 hello 데이터 hello 보호 하기 위해 다른 프로토콜 또는 SSL/TLS를 사용 하 여 응용 프로그램 수준에서 암호화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="8f38e-202">기본적으로 암호화</span><span class="sxs-lookup"><span data-stu-id="8f38e-202">Encryption by default</span></span>

<span data-ttu-id="8f38e-203">Microsoft Azure 클라우드 서비스의 고객 간에 전송 중에 암호화 tooprotect 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="8f38e-204">Hello Azure 포털을 통해 Azure 저장소와 상호 작용 하는, 하는 경우 HTTPS를 통해 모든 트랜잭션이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="8f38e-205">[전송 계층 보안](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS)는 hello 프로토콜 Microsoft 데이터 센터 toonegotiate tooMicrosoft 클라우드 서비스를 연결 하는 클라이언트 시스템을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="8f38e-206">TLS는 강력한 인증, 메시지 개인 정보 보호 및 무결성(메시지 변조, 가로채기 및 위조에 대한 검색 가능), 상호 운용성, 알고리즘 유연성, 배포 및 사용 편의성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="8f38e-207">또한 고객의 클라이언트 시스템과 Microsoft의 클라우드 서비스 간의 각 연결에서 고유한 키를 사용하도록 [PFS(Perfect Forward Secrecy)](https://en.wikipedia.org/wiki/Forward_secrecy)도 채택되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="8f38e-208">연결 tooMicrosoft 클라우드 서비스 활용 기반으로 하는 RSA 2048 비트 암호화 키 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="8f38e-209">TLS, RSA 2048 비트 키 길이 조합의 hello 및 PFS 훨씬 더 어려워집니다 다른 사용자에 대 한 Microsoft 클라우드 서비스와 고객 간에 전송 되는 데이터에 액세스 하 toointercept 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="8f38e-210">전송 중인 데이터는 항상 [Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview)에서 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="8f38e-211">또한 tooencrypting 데이터 사전 toostoring toopersistent 미디어 hello 데이터는 항상 전송에 보호 HTTPS를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="8f38e-212">HTTPS는 hello hello 데이터 레이크 저장소 REST 인터페이스에 지원 되는 유일한 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="8f38e-213">요약</span><span class="sxs-lookup"><span data-stu-id="8f38e-213">Summary</span></span>

<span data-ttu-id="8f38e-214">hello 회사 HTTPS 연결 tooAzure 저장소를 적용, 공유 액세스 서명을 사용 하 여 및 hello 저장소 계정에 필요한 전송 보안을 사용 하 여 이러한 데이터의 개인 데이터 및 hello의 개인 정보 보호 목표를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="8f38e-215">또한 SMB 3.0 연결을 사용하고 클라이언트 쪽 암호화를 구현하여 개인 데이터를 보호할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="8f38e-216">사이트 간 VPN 연결에는 Azure 가상 네트워크의 회사 네트워크 toohello hello 및 개별 사용자의 지점-사이트 VPN 연결 있는 개인 데이터 안전 하 게 통과할 수 안전한 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="8f38e-217">Microsoft의 기본 암호화 사례 개인 데이터의 hello 개인 정보를 추가로 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f38e-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f38e-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f38e-218">Next steps</span></span>

- [<span data-ttu-id="8f38e-219">Azure 데이터 보안 및 암호화 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8f38e-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="8f38e-220">VPN Gateway 계획 및 설계</span><span class="sxs-lookup"><span data-stu-id="8f38e-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="8f38e-221">VPN 게이트웨이 FAQ</span><span class="sxs-lookup"><span data-stu-id="8f38e-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="8f38e-222">Azure App Service에 대한 SSL 인증서 구입 및 구성</span><span class="sxs-lookup"><span data-stu-id="8f38e-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
