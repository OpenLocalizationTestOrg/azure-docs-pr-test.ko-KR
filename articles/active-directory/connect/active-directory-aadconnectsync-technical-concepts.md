---
title: "Azure AD Connect 동기화: 기술 개념 | Microsoft Docs"
description: "Azure AD Connect 동기화의 기술 개념에 대해 설명합니다."
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
ms.openlocfilehash: 6cf8debc6443bb60fc5f601ea4aa392eb2f13a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a><span data-ttu-id="e1bf8-103">Azure AD Connect Sync: 기술 개념</span><span class="sxs-lookup"><span data-stu-id="e1bf8-103">Azure AD Connect sync: Technical Concepts</span></span>
<span data-ttu-id="e1bf8-104">이 문서에서는 [아키텍처 이해](active-directory-aadconnectsync-technical-concepts.md)항목을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-104">This article is a summary of the topic [Understanding architecture](active-directory-aadconnectsync-technical-concepts.md).</span></span>

<span data-ttu-id="e1bf8-105">Azure AD Connect 동기화는 견고한 메타 디렉터리 동기화 플랫폼상에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-105">Azure AD Connect sync builds upon a solid metadirectory synchronization platform.</span></span>
<span data-ttu-id="e1bf8-106">다음 섹션에서는 메타 디렉터리 동기화에 대한 개념을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-106">The following sections introduce the concepts for metadirectory synchronization.</span></span>
<span data-ttu-id="e1bf8-107">MIIS, ILM 및 FIM을 바탕으로 구성된 Azure Active Directory 동기화 서비스는 데이터 원본에 연결, 데이터 원본 사이에 데이터 동기화 및 ID의 프로비전 및 프로비전 해제를 위한 차세대 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-107">Building upon MIIS, ILM, and FIM, the Azure Active Directory Sync Services provides the next platform for connecting to data sources, synchronizing data between data sources, as well as the provisioning and deprovisioning of identities.</span></span>

![기술 개념](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

<span data-ttu-id="e1bf8-109">다음 섹션에서는 FIM 동기화 서비스의 다음과 같은 측면에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-109">The following sections provide more details about the following aspects of the FIM Synchronization Service:</span></span>

* <span data-ttu-id="e1bf8-110">커넥터</span><span class="sxs-lookup"><span data-stu-id="e1bf8-110">Connector</span></span>
* <span data-ttu-id="e1bf8-111">특성 이름</span><span class="sxs-lookup"><span data-stu-id="e1bf8-111">Attribute flow</span></span>
* <span data-ttu-id="e1bf8-112">커넥터 공간</span><span class="sxs-lookup"><span data-stu-id="e1bf8-112">Connector space</span></span>
* <span data-ttu-id="e1bf8-113">메타 버스</span><span class="sxs-lookup"><span data-stu-id="e1bf8-113">Metaverse</span></span>
* <span data-ttu-id="e1bf8-114">프로비전</span><span class="sxs-lookup"><span data-stu-id="e1bf8-114">Provisioning</span></span>

## <a name="connector"></a><span data-ttu-id="e1bf8-115">커넥터</span><span class="sxs-lookup"><span data-stu-id="e1bf8-115">Connector</span></span>
<span data-ttu-id="e1bf8-116">연결된 디렉터리와 통신하는 데 사용되는 코드 모듈을 커넥터(이전의 MA(관리 에이전트))라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-116">The code modules that are used to communicate with a connected directory are called connectors (formerly known as  management agents (MAs)).</span></span>

<span data-ttu-id="e1bf8-117">이러한 작업은 Azure AD Connect 동기화를 실행하는 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-117">These are installed on the computer running Azure AD Connect sync.</span></span>
<span data-ttu-id="e1bf8-118">커넥터는 특수 에이전트의 배포에 의존하지 않고 원격 시스템 프로토콜을 사용하여 대화할 수 있는 에이전트 없는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-118">The connectors provide the agentless ability to converse by using remote system protocols instead of relying on the deployment of specialized agents.</span></span> <span data-ttu-id="e1bf8-119">따라서 특히 중요한 응용 프로그램 및 시스템을 다룰 때 위험성과 배포 시간이 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-119">This means decreased risk and deployment times, especially when dealing with critical applications and systems.</span></span>

<span data-ttu-id="e1bf8-120">위 그림에서 커넥터는 커넥터 공간와 동의어 이지만 외부 시스템과의 모든 통신을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-120">In the picture above, the connector is synonymous with the connector space but encompasses all communication with the external system.</span></span>

<span data-ttu-id="e1bf8-121">커넥터는 모든 가져오기 및 시스템에 내보내기 기능을 책임지며, 개발자가 선언적 프로비전을 사용하여 데이터 변환을 사용자 지정하는 경우 기본적으로 각 시스템에 연결하는 방법을 이해할 필요가 없게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-121">The connector is responsible for all import and export functionality to the system and frees developers from needing to understand how to connect to each system natively when using declarative provisioning to customize data transformations.</span></span>

<span data-ttu-id="e1bf8-122">가져오기 및 내보내기가 예약된 경우에만 발생하므로 변경 내용이 연결된 데이터 원본에 자동으로 전파되지 않아서 변경이 추가로 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-122">Imports and exports only occur when scheduled, allowing for further insulation from changes occurring within the system, since changes do not automatically propagate to the connected data source.</span></span> <span data-ttu-id="e1bf8-123">또한 개발자는 거의 모든 데이터 원본에 연결하기 위해 자체 커넥터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-123">In addition, developers may also create their own connectors for connecting to virtually any data source.</span></span>

## <a name="attribute-flow"></a><span data-ttu-id="e1bf8-124">특성 이름</span><span class="sxs-lookup"><span data-stu-id="e1bf8-124">Attribute flow</span></span>
<span data-ttu-id="e1bf8-125">메타 버스는 인접 커넥터 공간에서 조인된 모든 ID의 통합된 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-125">The metaverse is the consolidated view of all joined identities from neighboring connector spaces.</span></span> <span data-ttu-id="e1bf8-126">위 그림에서는 특성 흐름이 인바운드 및 아웃바운드 흐름에 대해 화살촉이 있는 선으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-126">In the figure above, attribute flow is depicted by lines with arrowheads for both inbound and outbound flow.</span></span> <span data-ttu-id="e1bf8-127">특성 흐름은 한 시스템에서 다른 시스템으로 데이터 복사 또는 변환 프로세스이며 모든 특성 흐름(인바운드 또는 아웃바운드)입니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-127">Attribute flow is the process of copying or transforming data from one system to another and all attribute flows (inbound or outbound).</span></span>

<span data-ttu-id="e1bf8-128">특성 흐름은 동기화(전체 또는 델타) 작업이 예정되어 있을 때 커넥터 공간과 메타 버스 사이에서 양방향으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-128">Attribute flow occurs between the connector space and the metaverse bi-directionally when synchronization (full or delta) operations are scheduled to run.</span></span>

<span data-ttu-id="e1bf8-129">특성 흐름은 이러한 동기화가 실행되는 경우에만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-129">Attribute flow only occurs when these synchronizations are run.</span></span> <span data-ttu-id="e1bf8-130">특성 흐름은 동기화 규칙에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-130">Attribute flows are defined in Synchronization Rules.</span></span> <span data-ttu-id="e1bf8-131">이러한 흐름은 인바운드(위 그림의 ISR) 또는 아웃바운드(위 그림의 OSR)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-131">These can be inbound (ISR in the picture above) or outbound (OSR in the picture above).</span></span>

## <a name="connected-system"></a><span data-ttu-id="e1bf8-132">연결된 시스템</span><span class="sxs-lookup"><span data-stu-id="e1bf8-132">Connected system</span></span>
<span data-ttu-id="e1bf8-133">연결된 시스템(연결된 디렉터리)은 Azure AD Connect Sync가 연결된 원격 시스템을 뜻하며 ID 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-133">Connected system (aka connected directory) is referring to the remote system Azure AD Connect sync has connected to and reading and writing identity data to and from.</span></span>

## <a name="connector-space"></a><span data-ttu-id="e1bf8-134">커넥터 공간</span><span class="sxs-lookup"><span data-stu-id="e1bf8-134">Connector space</span></span>
<span data-ttu-id="e1bf8-135">연결된 각 데이터 원본은 커넥터 공간 내 개체 및 특성의 필터링된 하위 집합으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-135">Each connected data source is represented as a filtered subset of the objects and attributes in the connector space.</span></span>
<span data-ttu-id="e1bf8-136">따라서 개체를 동기화할 때 원격 시스템에 연결할 필요 없이 동기화 서비스가 로컬에서 작동되며, 상호 작용이 가져오기 및 내보내기로만 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-136">This allows the sync service to operate locally without the need to contact the remote system when synchronizing the objects and restricts interaction to imports and exports only.</span></span>

<span data-ttu-id="e1bf8-137">데이터 원본 및 커넥터가 변경 내용 목록(델타 가져오기)을 제공할 수 있는 능력이 있는 경우 운영 효율성이 크게 증가합니다. 마지막 폴링 주기 이후의 변경 내용만 교환되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-137">When the data source and the connector have the ability to provide a list of changes (a delta import), then the operational efficiency increases dramatically as only changes since the last polling cycle are exchanged.</span></span> <span data-ttu-id="e1bf8-138">커넥터 공간은 커넥터 일정 가져오기와 내보내기를 요구하여 연결된 데이터 원본이 변경 내용을 자동으로 전파하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-138">The connector space insulates the connected data source from changes propagating automatically by requiring that the connector schedule imports and exports.</span></span> <span data-ttu-id="e1bf8-139">추가된 이 보험은 테스트, 미리보기 또는 다음 업데이트를 확인하는 동안 마음의 평화를 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-139">This added insurance grants you peace of mind while testing, previewing, or confirming the next update.</span></span>

## <a name="metaverse"></a><span data-ttu-id="e1bf8-140">메타 버스</span><span class="sxs-lookup"><span data-stu-id="e1bf8-140">Metaverse</span></span>
<span data-ttu-id="e1bf8-141">메타 버스는 인접 커넥터 공간에서 조인된 모든 ID의 통합된 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-141">The metaverse is the consolidated view of all joined identities from neighboring connector spaces.</span></span>

<span data-ttu-id="e1bf8-142">ID가 서로 연결되어 있고 가져오기 흐름 매핑을 통해 기관이 다양한 특성에 할당되므로 중앙 메타 버스 개체가 여러 시스템으로부터 정보를 집계하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-142">As identities are linked together and authority is assigned for various attributes through import flow mappings, the central metaverse object begins to aggregate information from multiple systems.</span></span> <span data-ttu-id="e1bf8-143">이 개체 특성 흐름으로부터 매핑이 아웃바운드 시스템에 정보를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-143">From this object attribute flow, mappings carry information to outbound systems.</span></span>

<span data-ttu-id="e1bf8-144">권한이 있는 시스템이 메타 버스에 정보를 프로젝션하면 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-144">Objects are created when an authoritative system projects them into the metaverse.</span></span> <span data-ttu-id="e1bf8-145">모든 연결이 제거되는 즉시 메타 버스 개체가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-145">As soon as all connections are removed, the metaverse object is deleted.</span></span>

<span data-ttu-id="e1bf8-146">메타버스의 개체는 직접 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-146">Objects in the metaverse cannot be edited directly.</span></span> <span data-ttu-id="e1bf8-147">개체의 모든 데이터는 특성 흐름을 통해 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-147">All data in the object must be contributed through attribute flow.</span></span> <span data-ttu-id="e1bf8-148">메타버스는 각 커넥터 공간을 가진 영구 커넥터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-148">The metaverse maintains persistent connectors with each connector space.</span></span> <span data-ttu-id="e1bf8-149">이러한 커넥터는 각 동기화 실행에 대해 다시 평가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-149">These connectors do not require reevaluation for each synchronization run.</span></span> <span data-ttu-id="e1bf8-150">즉 Azure AD Connect Sync는 매번 일치하는 원격 개체를 찾을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-150">This means that Azure AD Connect sync does not have to locate the matching remote object each time.</span></span> <span data-ttu-id="e1bf8-151">이렇게 하면 일반적으로 개체를 연결해야 하는 특성이 변경되지 않도록 하기 위해 비용이 많이 드는 에이전트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-151">This avoids the need for costly agents to prevent changes to attributes that would normally be responsible for correlating the objects.</span></span>

<span data-ttu-id="e1bf8-152">관리해야 하는 기존 개체가 포함되어 있을 수 있는 새 데이터 원본을 검색할 때 Azure AD Connect 동기화는 조인 규칙이라는 프로세스를 사용하여 링크를 설정하는 데 사용할 잠재적인 후보를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-152">When discovering new data sources that may have preexisting objects that need to be managed, Azure AD Connect sync uses a process called a join rule to evaluate potential candidates with which to establish a link.</span></span>
<span data-ttu-id="e1bf8-153">링크가 설정되면 이 평가가 다시 발생하지 않으며 일반 특성 흐름이 연결된 원격 데이터 원본과 메타 버스 간에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-153">Once the link is established, this evaluation does not reoccur and normal attribute flow can occur between the remote connected data source and the metaverse.</span></span>

## <a name="provisioning"></a><span data-ttu-id="e1bf8-154">프로비전</span><span class="sxs-lookup"><span data-stu-id="e1bf8-154">Provisioning</span></span>
<span data-ttu-id="e1bf8-155">권한이 있는 원본이 새 개체를 메타 버스에 프로젝션하면 새 커넥터 공간 개체를 다른 커넥터에 생성하여 다운스트림에 연결된 데이터 소스를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-155">When an authoritative source projects a new object into the metaverse a new connector space object can be created in another Connector representing a downstream connected data source.</span></span>

<span data-ttu-id="e1bf8-156">그러면 고유하게 링크가 설정되고 특성 흐름이 양방향으로 진행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-156">This inherently establishes a link, and attribute flow can proceed bi-directionally.</span></span>

<span data-ttu-id="e1bf8-157">규칙이 새 커넥터 공간 개체를 만들어야 한다고 결정할 때마다 프로버전이라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-157">Whenever a rule determines that a new connector space object needs to be created, it is called provisioning.</span></span> <span data-ttu-id="e1bf8-158">그러나 이 작업은 커넥터 공간 내에서만 발생하기 때문에 내보내기가 실행될 때까지 연결된 데이터 원본으로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-158">However, because this operation only takes place within the connector space, it does not carry over into the connected data source until an export is performed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1bf8-159">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e1bf8-159">Additional Resources</span></span>
* [<span data-ttu-id="e1bf8-160">Azure AD Connect Sync: 사용자 지정 동기화 옵션</span><span class="sxs-lookup"><span data-stu-id="e1bf8-160">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="e1bf8-161">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="e1bf8-161">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
