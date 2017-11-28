---
title: "Azure AD Connect 동기화: 기술 개념 | Microsoft Docs"
description: "Hello의 Azure AD Connect sync 기술 개념에 설명합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a><span data-ttu-id="1b4c1-103">Azure AD Connect Sync: 기술 개념</span><span class="sxs-lookup"><span data-stu-id="1b4c1-103">Azure AD Connect sync: Technical Concepts</span></span>
<span data-ttu-id="1b4c1-104">이 문서는 hello 항목의 요약 [이해 아키텍처](active-directory-aadconnectsync-technical-concepts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-104">This article is a summary of hello topic [Understanding architecture](active-directory-aadconnectsync-technical-concepts.md).</span></span>

<span data-ttu-id="1b4c1-105">Azure AD Connect 동기화는 견고한 메타 디렉터리 동기화 플랫폼상에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-105">Azure AD Connect sync builds upon a solid metadirectory synchronization platform.</span></span>
<span data-ttu-id="1b4c1-106">다음 섹션 hello 메타 디렉터리 동기화에 대 한 hello 개념을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-106">hello following sections introduce hello concepts for metadirectory synchronization.</span></span>
<span data-ttu-id="1b4c1-107">MIIS, ILM 및 FIM을 높이고 hello Azure Active Directory Sync Services hello 다음 플랫폼을 제공 연결 toodata 원본에 대 한 프로 비전 및 프로 비전 해제를 id의 hello 뿐만 아니라 데이터 소스 간의 데이터 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-107">Building upon MIIS, ILM, and FIM, hello Azure Active Directory Sync Services provides hello next platform for connecting toodata sources, synchronizing data between data sources, as well as hello provisioning and deprovisioning of identities.</span></span>

![기술 개념](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

<span data-ttu-id="1b4c1-109">hello FIM 동기화 서비스의 측면을 따라 hello에 대 한 자세한 정보를 제공 하는 다음 섹션 hello:</span><span class="sxs-lookup"><span data-stu-id="1b4c1-109">hello following sections provide more details about hello following aspects of hello FIM Synchronization Service:</span></span>

* <span data-ttu-id="1b4c1-110">커넥터</span><span class="sxs-lookup"><span data-stu-id="1b4c1-110">Connector</span></span>
* <span data-ttu-id="1b4c1-111">특성 이름</span><span class="sxs-lookup"><span data-stu-id="1b4c1-111">Attribute flow</span></span>
* <span data-ttu-id="1b4c1-112">커넥터 공간</span><span class="sxs-lookup"><span data-stu-id="1b4c1-112">Connector space</span></span>
* <span data-ttu-id="1b4c1-113">메타 버스</span><span class="sxs-lookup"><span data-stu-id="1b4c1-113">Metaverse</span></span>
* <span data-ttu-id="1b4c1-114">프로비전</span><span class="sxs-lookup"><span data-stu-id="1b4c1-114">Provisioning</span></span>

## <a name="connector"></a><span data-ttu-id="1b4c1-115">커넥터</span><span class="sxs-lookup"><span data-stu-id="1b4c1-115">Connector</span></span>
<span data-ttu-id="1b4c1-116">연결된 된 디렉터리를 사용 하는 toocommunicate hello 코드 모듈이 커넥터 (이전의 Ma (관리 에이전트)) 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-116">hello code modules that are used toocommunicate with a connected directory are called connectors (formerly known as  management agents (MAs)).</span></span>

<span data-ttu-id="1b4c1-117">이러한 작업은 Azure AD Connect 동기화를 실행 하는 hello 컴퓨터에 설치 됩니다. hello 커넥터는 전문된 에이전트 배포 hello에 의존 하지 않고 원격 시스템 프로토콜을 사용 하 여 에이전트 없는 능력 tooconverse hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-117">These are installed on hello computer running Azure AD Connect sync. hello connectors provide hello agentless ability tooconverse by using remote system protocols instead of relying on hello deployment of specialized agents.</span></span> <span data-ttu-id="1b4c1-118">따라서 특히 중요한 응용 프로그램 및 시스템을 다룰 때 위험성과 배포 시간이 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-118">This means decreased risk and deployment times, especially when dealing with critical applications and systems.</span></span>

<span data-ttu-id="1b4c1-119">위 hello 그림 hello 커넥터 hello 커넥터 공간과 동의어 이지만 hello 외부 시스템과 모든 통신을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-119">In hello picture above, hello connector is synonymous with hello connector space but encompasses all communication with hello external system.</span></span>

<span data-ttu-id="1b4c1-120">hello 커넥터는 처리에 대 한 모든 가져오기 및 내보내기 기능 toohello 시스템 toounderstand 어떻게 않아도 개발자 해제 tooconnect tooeach 시스템 선언적 프로비저닝 toocustomize 데이터 변환을 사용 하는 경우에 고유 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-120">hello connector is responsible for all import and export functionality toohello system and frees developers from needing toounderstand how tooconnect tooeach system natively when using declarative provisioning toocustomize data transformations.</span></span>

<span data-ttu-id="1b4c1-121">가져오기 및 내보내기 경우에 발생할 실행 되도록 예약 된 변경은 toohello 연결 된 데이터 소스를 자동으로 전파 되지 않습니다 이후 hello 시스템 내에서 발생 한 변경 내용 으로부터 단절 추가 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-121">Imports and exports only occur when scheduled, allowing for further insulation from changes occurring within hello system, since changes do not automatically propagate toohello connected data source.</span></span> <span data-ttu-id="1b4c1-122">또한 개발자는 toovirtually 모든 데이터 원본 연결 하기 위한 자체의 커넥터를 만들 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-122">In addition, developers may also create their own connectors for connecting toovirtually any data source.</span></span>

## <a name="attribute-flow"></a><span data-ttu-id="1b4c1-123">특성 이름</span><span class="sxs-lookup"><span data-stu-id="1b4c1-123">Attribute flow</span></span>
<span data-ttu-id="1b4c1-124">hello 메타 버스는 인접 커넥터 공간에서 모든 조인 된 id의 hello 통합 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-124">hello metaverse is hello consolidated view of all joined identities from neighboring connector spaces.</span></span> <span data-ttu-id="1b4c1-125">위 hello 그림 특성 흐름은 인바운드 및 아웃 바운드 흐름에 대 한 화살촉이 있는 선으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-125">In hello figure above, attribute flow is depicted by lines with arrowheads for both inbound and outbound flow.</span></span> <span data-ttu-id="1b4c1-126">특성 흐름은 복사 나 tooanother 하나의 시스템에서에서 데이터 변환을의 hello 프로세스 및 모든 특성 흐름 (인바운드 또는 아웃 바운드).</span><span class="sxs-lookup"><span data-stu-id="1b4c1-126">Attribute flow is hello process of copying or transforming data from one system tooanother and all attribute flows (inbound or outbound).</span></span>

<span data-ttu-id="1b4c1-127">특성 흐름 발생 hello 커넥터 공간과 메타 버스 hello 간의 양방향으로 동기화 (전체 또는 델타) 작업은 예약 된 toorun 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-127">Attribute flow occurs between hello connector space and hello metaverse bi-directionally when synchronization (full or delta) operations are scheduled toorun.</span></span>

<span data-ttu-id="1b4c1-128">특성 흐름은 이러한 동기화가 실행되는 경우에만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-128">Attribute flow only occurs when these synchronizations are run.</span></span> <span data-ttu-id="1b4c1-129">특성 흐름은 동기화 규칙에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-129">Attribute flows are defined in Synchronization Rules.</span></span> <span data-ttu-id="1b4c1-130">인바운드 (위 hello 그림의 ISR) 또는 아웃 바운드 (위 hello 그림에서 OSR) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-130">These can be inbound (ISR in hello picture above) or outbound (OSR in hello picture above).</span></span>

## <a name="connected-system"></a><span data-ttu-id="1b4c1-131">연결된 시스템</span><span class="sxs-lookup"><span data-stu-id="1b4c1-131">Connected system</span></span>
<span data-ttu-id="1b4c1-132">연결 된 시스템 (즉, 연결 된 디렉터리)가 참조 toohello 원격 시스템 Azure AD Connect 동기화 tooand 읽기 및 쓰기에서 identity 데이터 tooand 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-132">Connected system (aka connected directory) is referring toohello remote system Azure AD Connect sync has connected tooand reading and writing identity data tooand from.</span></span>

## <a name="connector-space"></a><span data-ttu-id="1b4c1-133">커넥터 공간</span><span class="sxs-lookup"><span data-stu-id="1b4c1-133">Connector space</span></span>
<span data-ttu-id="1b4c1-134">각 연결 된 데이터 원본 커넥터 공간의 hello의 hello 개체 및 특성의 필터링된 된 하위 집합으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-134">Each connected data source is represented as a filtered subset of hello objects and attributes in hello connector space.</span></span>
<span data-ttu-id="1b4c1-135">이 hello 필요 toocontact hello 원격 시스템 하지 않고 로컬 hello 동기화 서비스 toooperate hello 개체를 동기화 할 때와 상호 작용 tooimports 제한를 통해만 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-135">This allows hello sync service toooperate locally without hello need toocontact hello remote system when synchronizing hello objects and restricts interaction tooimports and exports only.</span></span>

<span data-ttu-id="1b4c1-136">Hello 데이터 소스와 hello 커넥터가 hello 기능 tooprovide (델타 가져오기) 변경 내용 목록은 때 다음 hello 운영 효율성 증가 크게 hello 마지막 폴링 이후 변경 된 내용만 주기로 교환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-136">When hello data source and hello connector have hello ability tooprovide a list of changes (a delta import), then hello operational efficiency increases dramatically as only changes since hello last polling cycle are exchanged.</span></span> <span data-ttu-id="1b4c1-137">hello 커넥터 공간 해당 hello 커넥터 일정 가져옵니다 요구 및 내보내기에 의해 자동으로 전파 된 변경 내용에서 연결 된 데이터 원본 hello을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-137">hello connector space insulates hello connected data source from changes propagating automatically by requiring that hello connector schedule imports and exports.</span></span> <span data-ttu-id="1b4c1-138">이러한 추가 된 보호 테스트, 미기 보기 또는 hello 다음 업데이트를 확인 하는 동안을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-138">This added insurance grants you peace of mind while testing, previewing, or confirming hello next update.</span></span>

## <a name="metaverse"></a><span data-ttu-id="1b4c1-139">메타 버스</span><span class="sxs-lookup"><span data-stu-id="1b4c1-139">Metaverse</span></span>
<span data-ttu-id="1b4c1-140">hello 메타 버스는 인접 커넥터 공간에서 모든 조인 된 id의 hello 통합 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-140">hello metaverse is hello consolidated view of all joined identities from neighboring connector spaces.</span></span>

<span data-ttu-id="1b4c1-141">을 identities 함께 연결 되 고 가져오기 흐름 매핑을 통해 다양 한 특성에 대 한 권한이 할당 되므로 hello 중앙 메타 버스 개체는 여러 시스템에서 tooaggregate 정보를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-141">As identities are linked together and authority is assigned for various attributes through import flow mappings, hello central metaverse object begins tooaggregate information from multiple systems.</span></span> <span data-ttu-id="1b4c1-142">이 개체 특성 흐름에서 매핑은 정보 toooutbound 시스템을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-142">From this object attribute flow, mappings carry information toooutbound systems.</span></span>

<span data-ttu-id="1b4c1-143">개체는 신뢰할 수 있는 시스템 hello 메타 버스에 투영할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-143">Objects are created when an authoritative system projects them into hello metaverse.</span></span> <span data-ttu-id="1b4c1-144">모든 연결이 제거 되는 즉시 hello 메타 버스 개체가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-144">As soon as all connections are removed, hello metaverse object is deleted.</span></span>

<span data-ttu-id="1b4c1-145">Hello 메타 버스의 개체를 직접 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-145">Objects in hello metaverse cannot be edited directly.</span></span> <span data-ttu-id="1b4c1-146">Hello 개체의 모든 데이터는 특성 흐름을 통해 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-146">All data in hello object must be contributed through attribute flow.</span></span> <span data-ttu-id="1b4c1-147">hello 메타 버스에는 각 커넥터 공간과 영구 커넥터 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-147">hello metaverse maintains persistent connectors with each connector space.</span></span> <span data-ttu-id="1b4c1-148">이러한 커넥터는 각 동기화 실행에 대해 다시 평가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-148">These connectors do not require reevaluation for each synchronization run.</span></span> <span data-ttu-id="1b4c1-149">즉, Azure AD Connect 동기화 하지 않았는지 toolocate hello 일치 하는 원격 개체 때마다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-149">This means that Azure AD Connect sync does not have toolocate hello matching remote object each time.</span></span> <span data-ttu-id="1b4c1-150">따라서 일반적으로 수 hello 개체를 상호 연결 하는 일을 담당 하는 비용이 드는 에이전트가 tooprevent 변경 tooattributes hello 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-150">This avoids hello need for costly agents tooprevent changes tooattributes that would normally be responsible for correlating hello objects.</span></span>

<span data-ttu-id="1b4c1-151">때 프로세스 toobe 관리, Azure AD Connect 동기화를 사용 해야 하는 기존 개체를 가질 수 있는 새 데이터 원본을 검색할는 조인 규칙 tooevaluate 잠재적 대상을 어떤 tooestablish 링크 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-151">When discovering new data sources that may have preexisting objects that need toobe managed, Azure AD Connect sync uses a process called a join rule tooevaluate potential candidates with which tooestablish a link.</span></span>
<span data-ttu-id="1b4c1-152">이 평가가 다시 수행 되지 hello 링크가 설정 되 고 hello 원격 연결 된 데이터 원본과 hello 메타 버스 간에 정상 특성 흐름이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-152">Once hello link is established, this evaluation does not reoccur and normal attribute flow can occur between hello remote connected data source and hello metaverse.</span></span>

## <a name="provisioning"></a><span data-ttu-id="1b4c1-153">프로비전</span><span class="sxs-lookup"><span data-stu-id="1b4c1-153">Provisioning</span></span>
<span data-ttu-id="1b4c1-154">신뢰할 수 있는 소스 프로젝트 때 다운스트림 연결된 데이터 원본을 나타내는 다른 커넥터에서 hello 메타 버스 새 커넥터 공간 개체에 새 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-154">When an authoritative source projects a new object into hello metaverse a new connector space object can be created in another Connector representing a downstream connected data source.</span></span>

<span data-ttu-id="1b4c1-155">그러면 고유하게 링크가 설정되고 특성 흐름이 양방향으로 진행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-155">This inherently establishes a link, and attribute flow can proceed bi-directionally.</span></span>

<span data-ttu-id="1b4c1-156">새 커넥터 공간 개체를 만든 toobe 필요 함을 확인 하는 규칙 경우 때마다 프로 비전 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-156">Whenever a rule determines that a new connector space object needs toobe created, it is called provisioning.</span></span> <span data-ttu-id="1b4c1-157">그러나를 하기 때문에이 작업만 hello 커넥터 공간 내에서 그는 적용 되지 않으므로 hello 연결 된 데이터 소스에 내보내기를 수행 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c1-157">However, because this operation only takes place within hello connector space, it does not carry over into hello connected data source until an export is performed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b4c1-158">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1b4c1-158">Additional Resources</span></span>
* [<span data-ttu-id="1b4c1-159">Azure AD Connect Sync: 사용자 지정 동기화 옵션</span><span class="sxs-lookup"><span data-stu-id="1b4c1-159">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="1b4c1-160">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="1b4c1-160">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
