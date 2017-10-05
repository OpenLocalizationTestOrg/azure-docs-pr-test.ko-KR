---
title: "Azure 보안 서비스 및 기술 | Microsoft Docs"
description: "이 문서는 엄선된 Azure 보안 서비스 및 기술 목록입니다."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: a5a7f60a-97e2-49b4-a8c5-7c010ff27ef8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/02/2016
ms.author: yurid
ms.openlocfilehash: 0bea62a43cf6cac9132fe64f2d6c54e52def4c55
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-security-services-and-technologies"></a><span data-ttu-id="79ac4-103">Azure 보안 서비스 및 기술</span><span class="sxs-lookup"><span data-stu-id="79ac4-103">Azure Security Services and Technologies</span></span>
<span data-ttu-id="79ac4-104">현재 및 미래 Azure 고객들과 이야기를 나눌 때 우리는 이런 질문을 자주 받습니다. “Azure가 제공하는 모든 보안 관련 서비스 및 기술 목록을 구비하고 계십니까?”</span><span class="sxs-lookup"><span data-stu-id="79ac4-104">In our discussions with current and future Azure customers, we’re often asked “do you have a list of all the security related services and technologies that Azure has to offer?”</span></span>

<span data-ttu-id="79ac4-105">클라우드 서비스 공급자 기술 옵션을 평가할 때, 사용 가능한 목록을 갖고 있다면 시간이 맞을 때 더 자세히 알아보는 데 유용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ac4-105">We understand that when you’re evaluating your cloud service provider technical options, it’s helpful to have such a list available that you can use to dig down deeper when the time is right for you.</span></span>

<span data-ttu-id="79ac4-106">다음은 우리가 목록을 제공하기 위해 기울이는 초기 노력입니다.</span><span class="sxs-lookup"><span data-stu-id="79ac4-106">The following is our initial effort at providing a list.</span></span> <span data-ttu-id="79ac4-107">시간이 지남에 따라 이 목록은 Azure와 마찬가지로 변경되고 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="79ac4-107">Over time, this list will change and grow, just as Azure does.</span></span> <span data-ttu-id="79ac4-108">목록은 분류되며, 범주 목록 또한 시간이 지남에 따라 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="79ac4-108">The list is categorized, and the list of categories will also grow over time.</span></span> <span data-ttu-id="79ac4-109">보안 관련 서비스 및 기술을 최신 상태로 유지할 수 있도록 정기적으로 이 페이지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="79ac4-109">Make sure to check this page on a regular basis to stay up-to-date on our security-related services and technologies.</span></span>

## <a name="azure-security---general"></a><span data-ttu-id="79ac4-110">Azure 보안-일반</span><span class="sxs-lookup"><span data-stu-id="79ac4-110">Azure Security - General</span></span>
* [<span data-ttu-id="79ac4-111">Azure 보안 센터</span><span class="sxs-lookup"><span data-stu-id="79ac4-111">Azure Security Center</span></span>](https://azure.microsoft.com/documentation/services/security-center/)
* [<span data-ttu-id="79ac4-112">Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="79ac4-112">Azure Key Vault</span></span>](https://azure.microsoft.com/documentation/services/key-vault/)
* [<span data-ttu-id="79ac4-113">Azure 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-113">Azure Disk Encryption</span></span>](azure-security-disk-encryption.md)
* [<span data-ttu-id="79ac4-114">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="79ac4-114">Log Analytics</span></span>](../log-analytics/log-analytics-overview.md)
* [<span data-ttu-id="79ac4-115">Azure Dev/Test Labs</span><span class="sxs-lookup"><span data-stu-id="79ac4-115">Azure Dev/Test Labs</span></span>](https://azure.microsoft.com/documentation/services/devtest-lab/)

## <a name="azure-storage-security"></a><span data-ttu-id="79ac4-116">Azure 저장소 보안</span><span class="sxs-lookup"><span data-stu-id="79ac4-116">Azure Storage Security</span></span>
* [<span data-ttu-id="79ac4-117">Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-117">Azure Storage Service Encryption</span></span>](../storage/common/storage-service-encryption.md)
* [<span data-ttu-id="79ac4-118">StorSimple 암호화된 하이브리드 저장소</span><span class="sxs-lookup"><span data-stu-id="79ac4-118">StorSimple Encrypted Hybrid Storage</span></span>](https://azure.microsoft.com/documentation/services/storsimple/)
* [<span data-ttu-id="79ac4-119">Azure 클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-119">Azure Client-Side Encryption</span></span>](../storage/common/storage-client-side-encryption.md)
* [<span data-ttu-id="79ac4-120">Azure 저장소 공유 액세스 서명</span><span class="sxs-lookup"><span data-stu-id="79ac4-120">Azure Storage Shared Access Signatures</span></span>](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="79ac4-121">Azure 저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="79ac4-121">Azure Storage Account Keys</span></span>](../storage/common/storage-create-storage-account.md)
* [<span data-ttu-id="79ac4-122">SMB 3.0 암호화를 사용한 Azure 파일 공유</span><span class="sxs-lookup"><span data-stu-id="79ac4-122">Azure File shares with SMB 3.0 Encryption</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="79ac4-123">Azure 저장소 분석</span><span class="sxs-lookup"><span data-stu-id="79ac4-123">Azure Storage Analytics</span></span>](https://msdn.microsoft.com/library/hh343270.aspx)

## <a name="azure-database-security"></a><span data-ttu-id="79ac4-124">Azure 데이터베이스 보안</span><span class="sxs-lookup"><span data-stu-id="79ac4-124">Azure Database Security</span></span>
* [<span data-ttu-id="79ac4-125">Azure SQL 방화벽</span><span class="sxs-lookup"><span data-stu-id="79ac4-125">Azure SQL Firewall</span></span>](../sql-database/sql-database-firewall-configure.md)
* [<span data-ttu-id="79ac4-126">Azure SQL 셀 수준 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-126">Azure SQL Cell Level Encryption</span></span>](https://blogs.msdn.microsoft.com/sqlsecurity/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database/)
* [<span data-ttu-id="79ac4-127">Azure SQL 연결 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-127">Azure SQL Connection Encryption</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="79ac4-128">Azure SQL 인증</span><span class="sxs-lookup"><span data-stu-id="79ac4-128">Azure SQL Authentication</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="79ac4-129">Azure SQL 항상 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-129">Azure SQL Always Encryption</span></span>](https://msdn.microsoft.com/library/mt163865.aspx)
* [<span data-ttu-id="79ac4-130">Azure SQL 열 수준 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-130">Azure SQL Column Level Encryption</span></span>](https://msdn.microsoft.com/library/ms179331.aspx)
* [<span data-ttu-id="79ac4-131">Azure SQL 투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="79ac4-131">Azure SQL Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/dn948096.aspx)
* [<span data-ttu-id="79ac4-132">Azure SQL 데이터베이스 감사</span><span class="sxs-lookup"><span data-stu-id="79ac4-132">Azure SQL Database Auditing</span></span>](../sql-database/sql-database-auditing.md)

## <a name="azure-identity-and-access-management"></a><span data-ttu-id="79ac4-133">Azure ID 및 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="79ac4-133">Azure Identity and Access Management</span></span>
* [<span data-ttu-id="79ac4-134">Azure 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="79ac4-134">Azure Role Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
* [<span data-ttu-id="79ac4-135">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79ac4-135">Azure Active Directory</span></span>](../active-directory/active-directory-whatis.md)
* [<span data-ttu-id="79ac4-136">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="79ac4-136">Azure Active Directory B2C</span></span>](../active-directory-b2c/active-directory-b2c-get-started.md)
* [<span data-ttu-id="79ac4-137">Azure Active Directory 도메인 서비스</span><span class="sxs-lookup"><span data-stu-id="79ac4-137">Azure Active Directory Domain Services</span></span>](../active-directory-domain-services/active-directory-ds-overview.md)
* [<span data-ttu-id="79ac4-138">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="79ac4-138">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="backup-and-disaster-recovery"></a><span data-ttu-id="79ac4-139">백업 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="79ac4-139">Backup and Disaster Recovery</span></span>
* [<span data-ttu-id="79ac4-140">Azure 백업</span><span class="sxs-lookup"><span data-stu-id="79ac4-140">Azure Backup</span></span>](https://azure.microsoft.com/documentation/services/backup/)
* [<span data-ttu-id="79ac4-141">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="79ac4-141">Azure Site Recovery</span></span>](https://azure.microsoft.com/documentation/services/site-recovery/)

## <a name="azure-networking"></a><span data-ttu-id="79ac4-142">Azure 네트워킹</span><span class="sxs-lookup"><span data-stu-id="79ac4-142">Azure Networking</span></span>
* [<span data-ttu-id="79ac4-143">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="79ac4-143">Network Security Groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="79ac4-144">Azure VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="79ac4-144">Azure VPN Gateway</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="79ac4-145">Azure 응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="79ac4-145">Azure Application Gateway</span></span>](../application-gateway/application-gateway-introduction.md)
* [<span data-ttu-id="79ac4-146">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="79ac4-146">Azure Load Balancer</span></span>](../load-balancer/load-balancer-overview.md)
* [<span data-ttu-id="79ac4-147">Azure express 경로</span><span class="sxs-lookup"><span data-stu-id="79ac4-147">Azure ExpressRoute</span></span>](../expressroute/expressroute-introduction.md)
* [<span data-ttu-id="79ac4-148">Azure 트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="79ac4-148">Azure Traffic Manager</span></span>](../traffic-manager/traffic-manager-overview.md)
* [<span data-ttu-id="79ac4-149">Azure 응용 프로그램 프록시</span><span class="sxs-lookup"><span data-stu-id="79ac4-149">Azure Application Proxy</span></span>](../active-directory/active-directory-application-proxy-enable.md)
