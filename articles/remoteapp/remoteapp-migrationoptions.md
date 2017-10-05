---
title: "Azure RemoteApp에서 마이그레이션하기 위한 옵션 | Microsoft Docs"
description: "Azure RemoteApp에서 마이그레이션하기 위한 옵션에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="a2168-103">Azure RemoteApp에서 마이그레이션하기 위한 옵션</span><span class="sxs-lookup"><span data-stu-id="a2168-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a2168-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a2168-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="a2168-106">[사용 중지 알림](https://go.microsoft.com/fwlink/?linkid=821148) 또는 평가를 완료했기 때문에 Azure RemoteApp 사용을 중단했으면 Azure RemoteApp을 다른 앱 서비스로 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="a2168-107">마이그레이션에는 두 가지 방식, 즉 자체 관리형 솔루션(종종 IaaS(Infrastructure as a Service)라고 함) 배포 또는 완전 관리형 제품(종종 PaaS(Platform as a Service)/SaaS(Software as a Service)라고 함)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="a2168-108">자체 관리형 IaaS는 VM(가상 컴퓨터) 또는 실제 시스템에 직접 배포되어 사용자가 관리, 운영 및 소유하는 자체(DIY) 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="a2168-109">다른 한편으로 완전 관리형 PaaS/SaaS 제품은 Azure RemoteApp과 매우 비슷합니다. 즉 파트너는 운영 및 서비스를 처리하는 원격 솔루션 위에 서비스 계층을 제공하는 반면 고객은 이미지 및 앱 관리를 일부 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="a2168-110">[마이그레이션 옵션에 대한 Azure RemoteApp 웨비나를 보거나](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp) 자세한 내용을 읽어보세요(다른 호스트 옵션 예제 포함).</span><span class="sxs-lookup"><span data-stu-id="a2168-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="a2168-111">자체 관리형 솔루션(IaaS)</span><span class="sxs-lookup"><span data-stu-id="a2168-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="a2168-112">**IaaS의 RDS**</span><span class="sxs-lookup"><span data-stu-id="a2168-112">**RDS on IaaS**</span></span>
<span data-ttu-id="a2168-113">RemoteApp이나 온-프레미스 또는 호스팅된 환경에 속한 데스크톱(예: Azure VM)을 사용하면 네이티브 세션 기반 원격 데스크톱 서비스(Windows Server) 배포본을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="a2168-114">RDS 배포에 이미 익숙하고 기존 기술 전문 지식을 갖춘 고객에게는 IaaS에 대한 RDS 배포가 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="a2168-115">이 배포 옵션을 사용하려면 RDS 클라이언트 액세스 라이선스로서 SA(Software Assurance)가 있는 볼륨 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="a2168-116">Azure VM에 RDS를 배포하는 것은 템플릿을 배포/패치하는 것보다 쉽습니다([개요](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) 참조 및 [가져오기](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="a2168-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="a2168-117">더 많은 사용자 지정 및 구성 옵션이 있지만 [크기 자동 조정 스크립트](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76)를 사용하면 Azure RemoteApp 내에서 Azure 클래식 배포 모델 리소스(Azure Resource Model 리소스가 아님)와 동일한 탄력적인 크기 조정 기능을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="a2168-118">Azure VM에 RDS를 배포하는 경우 Azure RemoteApp을 지원했던 것처럼 전문적인 [Azure 지원](https://azure.microsoft.com/support/plans/)을 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="a2168-119">[Azure 지원](https://azure.microsoft.com/support/plans/)에 문의하여 기존 사용량에 기반한 견적 비용을 확인하거나 곧 출시될 비용 계산기를 통해 직접 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="a2168-120">또한 N 계열 VM(현재 비공개 미리 보기로 있음)을 사용하면 vGPU를 추가할 수 있습니다. vGPU를 추가하는 방법과 [Windows Server 2016의 RDS 향상 기능 활용](https://myignite.microsoft.com/videos/2794) 방법을 자세히 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="a2168-121">[Windows Server 2012 R2](http://aka.ms/rdsonazure) 및 [Windows Server 2016](http://aka.ms/rdsonazure2016)에 대한 단계별 배포 가이드를 통해 배포를 지원하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="a2168-122">[원격 데스크톱 블로그](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services)에서 최신 소식을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="a2168-123">**IaaS의 Citrix**</span><span class="sxs-lookup"><span data-stu-id="a2168-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="a2168-124">세션 기반 XenApp 또는 XenDesktop의 네이티브 Citrix 배포본은 온-프레미스 또는 호스팅된 환경(예: Azure VM)에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="a2168-125">자세한 내용은 [Azure에서 Citrix XA 7.6](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx) 단계별 배포 가이드를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="a2168-126">가격 계산기를 포함하여 [Azure에서 Citrix](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="a2168-127">[Citrix 연락처](http://citrix.com/English/contact/index.asp)를 사용하면 옵션에 대해 논의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="a2168-128">완전 관리형 제품(PaaS/SaaS)</span><span class="sxs-lookup"><span data-stu-id="a2168-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="a2168-129">Citrix XenApp Essentials(2017년 4월 출시)</span><span class="sxs-lookup"><span data-stu-id="a2168-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="a2168-130">이제 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials)에서 구입 가능한 Citrix XenApp Essentials는 단순하고 규범적이며 사용하기 쉬운 Microsoft Azure RemoteApp 비전과 Citrix 클라우드 플랫폼의 강력한 기능 및 유연성을 결합한 새로운 응용 프로그램 가상화 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-130">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="a2168-131">기존 Azure RemoteApp 고객은 [평가판 등록](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/)이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="a2168-132">참고: Citrix 사용자 서비스 요금만 무료이며 Azure 계산 및 저장소 비용은 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="a2168-133">자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="a2168-133">Learn More:</span></span>
- [<span data-ttu-id="a2168-134">Azure RemoteApp에서 Citrix XenApp Essentials로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="a2168-134">Migrate from Azure RemoteApp to Citrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="a2168-135">Citrix 및 Microsoft</span><span class="sxs-lookup"><span data-stu-id="a2168-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="a2168-136">[Citrix XenApp Essentials 프레젠테이션](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="a2168-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="a2168-137">Citrix 클라우드 XenApp 서비스 및 XenDesktop 서비스</span><span class="sxs-lookup"><span data-stu-id="a2168-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="a2168-138">[Citrix 클라우드 XenApp 서비스 및 XenDesktop 서비스](https://www.citrix.com/products/citrix-cloud/services.html)는 앱 및 데스크톱의 제공을 위한 최상의 솔루션이며 고급 관리 및 모니터링 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="a2168-139">Conexlink(플랫폼 이름: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="a2168-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="a2168-140">[MyCloudIT](https://mycloudit.com)는 IT 회사에서 Microsoft Azure Cloud의 원격 데스크톱, 원격 응용 프로그램 및 인프라에 대한 마이그레이션 및 배포를 단순화, 최적화 및 확장할 수 있도록 하는 자동화 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="a2168-141">MyCloudIT 플랫폼을 사용하면 배포 시간을 95% 단축하며, Azure 비용을 30% 절감하고, 몇몇의 키 입력으로 고객의 전체 IT 인프라를 클라우드로 옮길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-141">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="a2168-142">이제 파트너는 하나의 전역 대시보드에서 고객을 관리하고, 이전과는 완전히 다르게 전 세계의 최종 사용자에게 서비스를 제공하며, 추가 오버 헤드 또는 광범위한 Azure 교육을 추가하지 않고도 수익을 올릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-142">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="a2168-143">기본 위치: 미국 텍사스주 댈러스</span><span class="sxs-lookup"><span data-stu-id="a2168-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="a2168-144">작업 영역: 전 세계</span><span class="sxs-lookup"><span data-stu-id="a2168-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="a2168-145">파트너 관계 상태: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="a2168-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="a2168-146">Microsoft 클라우드 서비스 공급자: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a2168-147">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a2168-148">Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="a2168-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="a2168-149">Brian Garoutte, 비즈니스 개발 부사장</span><span class="sxs-lookup"><span data-stu-id="a2168-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="a2168-150">전화 번호: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="a2168-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="a2168-151">메일: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="a2168-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="a2168-152">프레임</span><span class="sxs-lookup"><span data-stu-id="a2168-152">Frame</span></span>

<span data-ttu-id="a2168-153">엔터프라이즈 및 정부의 IT 조직, 관리되는 서비스 공급자 및 소프트웨어 공급 업체는 프레임을 선택하여 클라우드에서 자신의 안전한 소프트웨어 정의 작업 영역을 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="a2168-154">작은 조직에서 대규모 조직까지 프레임을 사용하면 사용자가 매우 쉽게 모든 장치의 모든 브라우저에서 Windows 응용 프로그램에 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-154">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="a2168-155">프레임 플랫폼은 Azure 인프라와 RDS 라이선스를 비롯하여 관리자가 클라우드에서 응용 프로그램을 배포하는 데 필요한 모든 항목을 포함합니다(사용자 고유의 Azure 계정 및 라이선스를 가져오는 것은 선택 사항임).</span><span class="sxs-lookup"><span data-stu-id="a2168-155">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="a2168-156">[Azure의 프레임](https://www.fra.me/ara)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="a2168-157">기본 위치: 샌마티오, 캘리포니아, 미국</span><span class="sxs-lookup"><span data-stu-id="a2168-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="a2168-158">작업 영역: 전 세계</span><span class="sxs-lookup"><span data-stu-id="a2168-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="a2168-159">Microsoft 파트너: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="a2168-160">전화 번호: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="a2168-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="a2168-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="a2168-161">Awingu</span></span>
<span data-ttu-id="a2168-162">Awingu에서는 html5 브라우저에서 레거시 앱, SaaS 및 문서를 실행하는 간단한 온라인 작업 영역 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="a2168-163">따라서 모든 종류의 장치에서 모든 응용 프로그램을 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="a2168-164">SaaS 서비스에 대해 광범위한 op Single Sign-On 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="a2168-165">또한 다양한 파일 시스템(클라우드 포함)을 작업 영역에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="a2168-166">전체 이동성 옆에 있는 Awingu의 풍부한 온라인 작업 영역에서는 세분화된 제어(예: 다운로드/업로드), 전체 사용 감사, Multi-Factor Authentication(예: Azure MFA), 세션 기록 등으로 최적 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-166">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="a2168-167">기본적으로 Awingu를 사용하면 문서 및 응용 프로그램 세션 공유에서 안전한 공동 작업을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="a2168-168">Awingu의 솔루션은 다중 테넌트, 다중 AD 및 오픈 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="a2168-169">중소기업 및 대기업, 클라우드 서비스 공급자 및 [ISV](http://www.isv2saas.com)에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="a2168-170">이러한 고객은 사용 편의성, 설치 편의성 및 낮은 TCO를 높이 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-170">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="a2168-171">Awingu 올인원은 2명의 기본 제공 동시 사용자가 있는 [Azure Marketplace에서 사용 가능](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-171">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="a2168-172">추가 라이선스는 [광범위한 배포자 및 판매점](http://www.awingu.com/reseller)을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="a2168-173">[Azure RemoteApp의 대안으로 Awingu 사용](http://alternative-for-azure-remoteapp.awingu.com/)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-173">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="a2168-174">기본 위치: 벨기에</span><span class="sxs-lookup"><span data-stu-id="a2168-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="a2168-175">운영 지역: EMEA, 북미 및 브라질</span><span class="sxs-lookup"><span data-stu-id="a2168-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="a2168-176">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="a2168-177">**전역**:</span><span class="sxs-lookup"><span data-stu-id="a2168-177">**Global**:</span></span>
> 
> <span data-ttu-id="a2168-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="a2168-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="a2168-179">메일: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="a2168-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="a2168-180">전화 번호: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="a2168-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="a2168-181">**벨기에 HQ**:</span><span class="sxs-lookup"><span data-stu-id="a2168-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="a2168-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="a2168-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="a2168-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="a2168-183">9000 Gent</span></span>
> 
> <span data-ttu-id="a2168-184">메일: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="a2168-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="a2168-185">전화 번호: + 32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="a2168-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="a2168-186">**USA**:</span><span class="sxs-lookup"><span data-stu-id="a2168-186">**USA**:</span></span>
> 
> <span data-ttu-id="a2168-187">7층, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="a2168-187">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="a2168-188">뉴욕, NY 10036</span><span class="sxs-lookup"><span data-stu-id="a2168-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="a2168-189">메일: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="a2168-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="a2168-190">Microsoft 호스티드 서비스 공급자</span><span class="sxs-lookup"><span data-stu-id="a2168-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="a2168-191">호스팅 파트너는 일반적으로 완전히 관리되는 호스트된 Windows 데스크톱 및 응용 프로그램 서비스를 제공합니다. 여기에는 Azure 리소스, 운영 체제, 응용 프로그램 및 기술 지원팀이 포함되며, Microsoft 및 기타 소프트웨어 공급자와 함께 파트너의 라이선스 계약을 통해 SAL(Subscriber Access License)의 재판매를 허용하는 서비스 공급자 라이선스 계약을 체결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="a2168-192">다음 정보는 Azure RemoteApp 마이그레이션으로 고객을 지원하는 데 전문화된 일부 호스팅 업체의 세부 정보 및 연락처 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-192">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="a2168-193">IaaS 학습 경로 및 평가에서 RDS를 완료한 [호스티드 서비스 공급자의 현재 목록](http://aka.ms/rdsonazurecertified)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-193">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="a2168-194">Citrix 서비스 공급자 프로그램</span><span class="sxs-lookup"><span data-stu-id="a2168-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="a2168-195">Citrix 서비스 공급자 프로그램을 사용하면 서비스 공급자가 가상 클라우드 컴퓨팅의 단순성을 SMB에 제공하여 간편한 종량제 모델에서 원하는 서비스를 손쉽게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-195">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="a2168-196">Citrix 서비스 공급자는 모든 장치에서 어디서든 액세스 가능, 광범위한 응용 프로그램 지원, 풍부한 경험, 보안 강화 및 향상된 확장성을 통해 Microsoft SPLA 비즈니스를 성장시키고 RDS 플랫폼 투자를 확대합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="a2168-197">이에 따라 Citrix 서비스 공급자는 구독자를 더 많이 유치하며, 고객 만족도를 높이고, 운영 비용을 절감합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="a2168-198">[자세한 정보](http://www.citrix.com/products/service-providers.html) 또는 [파트너 찾기](https://www.citrix.com/buy/partnerlocator.html)</span><span class="sxs-lookup"><span data-stu-id="a2168-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="a2168-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="a2168-199">Acuutech</span></span>
<span data-ttu-id="a2168-200">[Acuutech](http://www.acuutech.com)는 호스팅된 데스크톱 솔루션을 제공하고, Azure 및 자체 데이터 센터의 전역 클라이언트에 기반하여 Microsoft 기술로 구현되는 완벽한 데스크톱 및 ISV 응용 프로그램 환경을 배포하는 것을 전문적으로 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="a2168-201">기본 위치: 영국 런던, 싱가포르, 미국 텍사스주 휴스턴</span><span class="sxs-lookup"><span data-stu-id="a2168-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="a2168-202">작업 영역: 전 세계</span><span class="sxs-lookup"><span data-stu-id="a2168-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="a2168-203">파트너 관계 상태: Gold</span><span class="sxs-lookup"><span data-stu-id="a2168-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="a2168-204">Microsoft 클라우드 서비스 공급자: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a2168-205">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a2168-206">Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="a2168-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="a2168-207">**영국**:</span><span class="sxs-lookup"><span data-stu-id="a2168-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="a2168-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="a2168-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="a2168-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="a2168-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="a2168-210">전화 번호: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="a2168-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="a2168-211">**싱가포르**:</span><span class="sxs-lookup"><span data-stu-id="a2168-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="a2168-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="a2168-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="a2168-213">The Globe, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="a2168-213">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="a2168-214">전화 번호: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="a2168-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="a2168-215">**북아메리카**</span><span class="sxs-lookup"><span data-stu-id="a2168-215">**North America**:</span></span>
>   
> <span data-ttu-id="a2168-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="a2168-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="a2168-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="a2168-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="a2168-218">전화 번호: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="a2168-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="a2168-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="a2168-219">ASPEX</span></span>
<span data-ttu-id="a2168-220">[ASPEX](http://www.aspex.be/en)는 ISV(Independent Software Vendor)에서 클라우드로 전환하여 현재의 클라우드 설정을 최적화하는 것을 전문적으로 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="a2168-221">ASPEX에서는 광범위한 관리, 개발 및 컨설팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="a2168-222">기본 위치: 벨기에 앤트워프</span><span class="sxs-lookup"><span data-stu-id="a2168-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="a2168-223">작업 영역: 서유럽</span><span class="sxs-lookup"><span data-stu-id="a2168-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="a2168-224">파트너 관계 상태: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="a2168-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="a2168-225">Microsoft 클라우드 서비스 공급자: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a2168-226">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a2168-227">Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="a2168-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="a2168-228">전화 번호: +3232202198</span><span class="sxs-lookup"><span data-stu-id="a2168-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="a2168-229">메일: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="a2168-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="a2168-230">웹: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="a2168-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="a2168-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="a2168-231">Caase.com</span></span>
<span data-ttu-id="a2168-232">[Caase.com](http://www.caase.com/)은 기업, 지방 정부, 비정부 단체 및 의료 기관이 Microsoft Cloud에서 보다 스마트한 방식으로 업무를 처리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in the Microsoft Cloud.</span></span> <span data-ttu-id="a2168-233">어떤 장치를 사용하더라도 낮은 IT 비용으로 어디서든 생산적이고 안전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="a2168-234">Caase.com은 진정한 Microsoft Office365, Azure, Enterprise Mobility + Security 및 Windows 전문가입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="a2168-235">컨설팅, 마이그레이션 서비스, 채택 프로그램, 교육, 관리 및 지원 Caase.com은 고객사 직원, 파트너 및 공급 업체 모두를 위한 최적화되고 안전한 플랫폼을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="a2168-236">Caase.com은 Azure 원격 작업 영역(모바일 작업 영역) 및 디지털 작업 영역(소셜 인트라넷)의 최고 전문가입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-236">Caase.com is the mastermind of the Azure Remote Workspace (mobile workplace) and the Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="a2168-237">기술 적용을 통해 완성된 이 두 가지 솔루션은 Microsoft Cloud를 활용하면서 가장 즐겁고 성공적이며 효과적인 경험을 가능하게 하는 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-237">Both solutions – accomplished with adoption – are the foundation which ensures that the users of these solutions have the most pleasant, successful and effective experience in their route to the Microsoft Cloud.</span></span>
<span data-ttu-id="a2168-238">http://caase.com/over-ons/에서 네덜란드어 번역 및 관련 동영상을 참고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="a2168-239">운영 지역: 네덜란드 기반의 글로벌 환경</span><span class="sxs-lookup"><span data-stu-id="a2168-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="a2168-240">파트너 관계 상태: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="a2168-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="a2168-241">Microsoft 클라우드 서비스 공급자: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a2168-242">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a2168-243">Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](http://caase.com/diensten/microsoft-azure/)</span><span class="sxs-lookup"><span data-stu-id="a2168-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="a2168-244">네덜란드:</span><span class="sxs-lookup"><span data-stu-id="a2168-244">Netherlands:</span></span>
> 
> <span data-ttu-id="a2168-245">Rigtersbleek-Zandvoort 10(De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="a2168-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="a2168-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="a2168-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="a2168-247">전화: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="a2168-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="a2168-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="a2168-248">Nerdio</span></span>
<span data-ttu-id="a2168-249">[Nerdio for Azure](http://getnerdio.com/nfa/)는 Microsoft 클라우드의 완벽한 IT 환경을 위해 대단히 간단한 프로비저닝, 관리 및 최적화를 제공하는 IT 자동화 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in the Microsoft cloud.</span></span> <span data-ttu-id="a2168-250">가상 데스크톱, 원격 응용 프로그램 및 서버를 한두 시간 내에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="a2168-251">Nerdio Admin Portal에서 세 번 이하의 클릭으로 환경을 관리하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-251">Administer the environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="a2168-252">지능형 자동 크기 조정을 사용하고 Azure IaaS 리소스에서 40~60%를 절약하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-252">Use intelligent auto-scaling and save 40 to 60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="a2168-253">기본 위치: 시카고, IL 운영 지역: 전세계 파트너 등급: [골드](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft 클라우드 서비스 공급자: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a2168-254">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a2168-255">Azure RemoteApp 마이그레이션 솔루션: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="a2168-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="a2168-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="a2168-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="a2168-257">Suite 212</span></span>
> 
> <span data-ttu-id="a2168-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="a2168-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="a2168-259">미국</span><span class="sxs-lookup"><span data-stu-id="a2168-259">USA</span></span>
> 
> <span data-ttu-id="a2168-260">(844) 4NERDIO ext.</span><span class="sxs-lookup"><span data-stu-id="a2168-260">(844) 4NERDIO ext.</span></span> <span data-ttu-id="a2168-261">6</span><span class="sxs-lookup"><span data-stu-id="a2168-261">6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="a2168-262">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="a2168-262">**SaaSplaza**</span></span>
<span data-ttu-id="a2168-263">[SaaSplaza](http://www.saasplaza.com/)는 모든 Microsoft Dynamics 포트폴리오(NAV, AX, GP, SL, CRM) 개인 및 공용 클라우드(Azure)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-263">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="a2168-264">기본 위치: 네덜란드</span><span class="sxs-lookup"><span data-stu-id="a2168-264">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="a2168-265">작업 영역: 전 세계</span><span class="sxs-lookup"><span data-stu-id="a2168-265">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="a2168-266">파트너 관계 상태: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="a2168-266">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="a2168-267">Microsoft 클라우드 서비스 공급자: 예</span><span class="sxs-lookup"><span data-stu-id="a2168-267">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a2168-268">세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다</span><span class="sxs-lookup"><span data-stu-id="a2168-268">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a2168-269">**EMEA**</span><span class="sxs-lookup"><span data-stu-id="a2168-269">**EMEA**:</span></span>
> 
> <span data-ttu-id="a2168-270">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="a2168-270">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="a2168-271">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="a2168-271">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="a2168-272">네덜란드</span><span class="sxs-lookup"><span data-stu-id="a2168-272">The Netherlands</span></span>
> 
> <span data-ttu-id="a2168-273">전화 번호: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="a2168-273">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="a2168-274">**아메리카**</span><span class="sxs-lookup"><span data-stu-id="a2168-274">**Americas**:</span></span>
> 
> <span data-ttu-id="a2168-275">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="a2168-275">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="a2168-276">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="a2168-276">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="a2168-277">샌디에이고</span><span class="sxs-lookup"><span data-stu-id="a2168-277">San Diego</span></span>
> 
> <span data-ttu-id="a2168-278">미국</span><span class="sxs-lookup"><span data-stu-id="a2168-278">United States</span></span>
> 
> <span data-ttu-id="a2168-279">전화 번호: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="a2168-279">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="a2168-280">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="a2168-280">**APAC**:</span></span>
> 
> <span data-ttu-id="a2168-281">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="a2168-281">105 Cecil Street</span></span>
>    
> <span data-ttu-id="a2168-282">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="a2168-282">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="a2168-283">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="a2168-283">Singapore 069534</span></span>
> 
> <span data-ttu-id="a2168-284">싱가포르</span><span class="sxs-lookup"><span data-stu-id="a2168-284">Singapore</span></span>
>   
> <span data-ttu-id="a2168-285">전화 번호 - 싱가포르: + 65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="a2168-285">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="a2168-286">전화 번호 - 오스트레일리아: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="a2168-286">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="a2168-287">전화 번호 - 뉴질랜드: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="a2168-287">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="a2168-288">도움이 더 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="a2168-288">Need more help?</span></span>
<span data-ttu-id="a2168-289">여전히 도움이 필요하거나 추가 질문이 있나요?</span><span class="sxs-lookup"><span data-stu-id="a2168-289">Still need help choosing or have further questions?</span></span> <span data-ttu-id="a2168-290">다음 방법 중 하나를 사용하여 도움을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-290">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="a2168-291">[arainfo@microsoft.com](mailto:arainfo@microsoft.com)으로 메일을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-291">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="a2168-292">[Azure 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-292">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="a2168-293">[Azure 지원 사례](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)를 열면서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a2168-293">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="a2168-294">전화로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a2168-294">Call us.</span></span> <span data-ttu-id="a2168-295">[해당 지역 영업 담당자 전화번호 찾기](https://azure.microsoft.com/overview/sales-number/)</span><span class="sxs-lookup"><span data-stu-id="a2168-295">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

