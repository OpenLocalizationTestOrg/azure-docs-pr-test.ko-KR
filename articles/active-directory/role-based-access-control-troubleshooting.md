---
title: "Azure RBAC 문제 해결 | Microsoft Docs"
description: "역할 기반 액세스 제어 리소스에 대해 발생하는 문제 또는 질문 사항에 대한 도움말을 봅니다."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="cfdb8-103">역할 기반 액세스 제어 문제 해결</span><span class="sxs-lookup"><span data-stu-id="cfdb8-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="cfdb8-104">이 문서에서는 역할과 함께 부여되는 특정 액세스 권한에 대한 일반적인 질문에 대한 답변을 제공합니다. 따라서 Azure Portal에서 역할을 사용할 때 예상되는 상황을 이해하고 액세스 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="cfdb8-105">이러한 세 가지 역할이 모든 리소스 유형에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="cfdb8-106">소유자</span><span class="sxs-lookup"><span data-stu-id="cfdb8-106">Owner</span></span>  
* <span data-ttu-id="cfdb8-107">참여자</span><span class="sxs-lookup"><span data-stu-id="cfdb8-107">Contributor</span></span>  
* <span data-ttu-id="cfdb8-108">판독기</span><span class="sxs-lookup"><span data-stu-id="cfdb8-108">Reader</span></span>  

<span data-ttu-id="cfdb8-109">소유자와 참여자 양쪽 모두 관리 환경에 대한 모든 권한을 가집니다. 하지만, 참여자의 경우 다른 사용자나 그룹에 액세스 권한을 부여할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="cfdb8-110">읽기 권한자 역할은 좀 더 복잡하므로 자세히 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="cfdb8-111">액세스를 부여하는 방법에 대한 세부 정보는 [역할 기반 액세스 제어 시작 문서](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="cfdb8-112">앱 서비스 워크로드</span><span class="sxs-lookup"><span data-stu-id="cfdb8-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="cfdb8-113">쓰기 액세스 기능</span><span class="sxs-lookup"><span data-stu-id="cfdb8-113">Write access capabilities</span></span>
<span data-ttu-id="cfdb8-114">사용자에게 단일 웹앱에 대한 읽기 전용 액세스를 부여하면 예상치 않게 일부 기능을 사용하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="cfdb8-115">다음 관리 기능을 사용하려면 참여자나 소유자에게 제공되는 웹앱에 대한 **쓰기** 권한이 필요하며, 읽기 전용 시나리오에서는 이러한 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="cfdb8-116">시작, 중지 등의 명령</span><span class="sxs-lookup"><span data-stu-id="cfdb8-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="cfdb8-117">일반 구성, 규모 설정, 백업 설정, 모니터링 설정 등의 설정 변경</span><span class="sxs-lookup"><span data-stu-id="cfdb8-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="cfdb8-118">게시 자격 증명과 앱 설정, 연결 문자열 등의 기타 암호 액세스</span><span class="sxs-lookup"><span data-stu-id="cfdb8-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="cfdb8-119">스트리밍 로그</span><span class="sxs-lookup"><span data-stu-id="cfdb8-119">Streaming logs</span></span>
* <span data-ttu-id="cfdb8-120">진단 로그 구성</span><span class="sxs-lookup"><span data-stu-id="cfdb8-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="cfdb8-121">콘솔(명령 프롬프트)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-121">Console (command prompt)</span></span>
* <span data-ttu-id="cfdb8-122">활성 및 최근 배포(로컬 Git 연속 배포의 경우)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="cfdb8-123">예상 소요 시간</span><span class="sxs-lookup"><span data-stu-id="cfdb8-123">Estimated spend</span></span>
* <span data-ttu-id="cfdb8-124">웹 테스트</span><span class="sxs-lookup"><span data-stu-id="cfdb8-124">Web tests</span></span>
* <span data-ttu-id="cfdb8-125">가상 네트워크(쓰기 권한이 있는 사용자가 이전에 가상 네트워크를 구성한 경우에만 읽기 권한자에게 표시됨)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="cfdb8-126">이러한 타일에 액세스할 수 없는 경우 관리자에게 웹앱에 대한 참가자 권한을 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="cfdb8-127">관련 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="cfdb8-127">Dealing with related resources</span></span>
<span data-ttu-id="cfdb8-128">웹앱에서 몇 가지 리소스가 상호 연동되는 경우 웹앱의 구조가 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="cfdb8-129">아래에는 웹 사이트 몇 개가 포함된 일반적인 리소스 그룹이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-129">Here is a typical resource group with a couple websites:</span></span>

![웹앱 리소스 그룹](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="cfdb8-131">따라서 사용자에게 웹앱에 대한 권한만 부여하면 Azure Portal에서 웹 사이트 블레이드의 기능을 대부분 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="cfdb8-132">다음 항목을 사용하려면 웹 사이트에 해당하는 **App Service 계획**에 대한 **쓰기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="cfdb8-133">웹앱의 가격 책정 계층 보기(무료 또는 표준)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="cfdb8-134">크기 조정 구성(인스턴스 수, 가상 컴퓨터 크기, 자동 크기 조정 설정)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="cfdb8-135">할당량(저장소, 대역폭, CPU)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="cfdb8-136">다음 항목을 사용하려면 웹 사이트를 포함하는 전체 **리소스 그룹**에 대한 **쓰기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="cfdb8-137">SSL 인증서 및 바인딩(SSL 인증서는 같은 리소스 그룹과 지리적 위치의 사이트 간에 공유될 수 있음)</span><span class="sxs-lookup"><span data-stu-id="cfdb8-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="cfdb8-138">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="cfdb8-138">Alert rules</span></span>  
* <span data-ttu-id="cfdb8-139">자동 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="cfdb8-139">Autoscale settings</span></span>  
* <span data-ttu-id="cfdb8-140">Application Insights 구성 요소</span><span class="sxs-lookup"><span data-stu-id="cfdb8-140">Application insights components</span></span>  
* <span data-ttu-id="cfdb8-141">웹 테스트</span><span class="sxs-lookup"><span data-stu-id="cfdb8-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="cfdb8-142">가상 컴퓨터 작업</span><span class="sxs-lookup"><span data-stu-id="cfdb8-142">Virtual machine workloads</span></span>
<span data-ttu-id="cfdb8-143">웹앱과 마찬가지로 가상 컴퓨터 블레이드의 일부 기능 역시 가상 컴퓨터 또는 리소스 그룹의 기타 리소스에 대한 쓰기 권한이 있어야 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="cfdb8-144">가상 컴퓨터는 도메인 이름, 가상 네트워크, 저장소 계정 및 경고 규칙과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="cfdb8-145">다음 항목을 사용하려면 **가상 컴퓨터**에 대한 **쓰기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="cfdb8-146">끝점</span><span class="sxs-lookup"><span data-stu-id="cfdb8-146">Endpoints</span></span>  
* <span data-ttu-id="cfdb8-147">IP 주소</span><span class="sxs-lookup"><span data-stu-id="cfdb8-147">IP addresses</span></span>  
* <span data-ttu-id="cfdb8-148">디스크</span><span class="sxs-lookup"><span data-stu-id="cfdb8-148">Disks</span></span>  
* <span data-ttu-id="cfdb8-149">확장</span><span class="sxs-lookup"><span data-stu-id="cfdb8-149">Extensions</span></span>  

<span data-ttu-id="cfdb8-150">다음 항목을 사용하려면 **가상 컴퓨터**와 가상 컴퓨터가 속한 **리소스 그룹**(도메인 이름 포함) 둘 다에 대한 **쓰기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="cfdb8-151">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="cfdb8-151">Availability set</span></span>  
* <span data-ttu-id="cfdb8-152">부하 분산된 집합</span><span class="sxs-lookup"><span data-stu-id="cfdb8-152">Load balanced set</span></span>  
* <span data-ttu-id="cfdb8-153">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="cfdb8-153">Alert rules</span></span>  

<span data-ttu-id="cfdb8-154">이러한 타일에 액세스할 수 없는 경우 관리자에게 리소스 그룹에 대한 참가자 권한을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="cfdb8-155">자세히 보기</span><span class="sxs-lookup"><span data-stu-id="cfdb8-155">See more</span></span>
* <span data-ttu-id="cfdb8-156">[역할 기반 액세스 제어](role-based-access-control-configure.md): Azure 포털에서 RBAC를 통해 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="cfdb8-157">[기본 제공 역할](role-based-access-built-in-roles.md): RBAC에서 표준이 되는 역할에 대한 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="cfdb8-158">[Azure RBAC에서 사용자 지정 역할](role-based-access-control-custom-roles.md): 액세스 요구 사항에 맞게 사용자 지정 역할을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="cfdb8-159">[액세스 변경 기록 보고서 만들기](role-based-access-control-access-change-history-report.md): RBAC에서 역할 할당 변경을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdb8-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

