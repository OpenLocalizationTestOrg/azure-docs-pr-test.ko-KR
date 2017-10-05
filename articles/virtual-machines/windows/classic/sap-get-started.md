---
title: "Windows 가상 컴퓨터에서 SAP 사용 | Microsoft Docs"
description: "Microsoft Azure의 Windows VM(가상 컴퓨터)에서 SAP를 사용하는 방법을 알아봅니다."
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 1d6326d5f79ea4e975abd1aa90b0d4a635f4c31a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="af7c3-103">Azure의 Windows 가상 컴퓨터에서 SAP 사용</span><span class="sxs-lookup"><span data-stu-id="af7c3-103">Using SAP on Windows virtual machines in Azure</span></span>
<span data-ttu-id="af7c3-104">클라우드 컴퓨팅은 중소 기업에서 대기업 및 다국적 기업까지 IT 업계 내에서 점점 더 중요해지는 널리 사용되는 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="af7c3-105">Microsoft Azure는 다양한 새로운 가능성을 제공하는 Microsoft의 클라우드 서비스 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="af7c3-106">이제 고객은 클라우드 서비스로 응용 프로그램을 신속하게 프로비전 및 프로비전 해제할 수 있으므로 기술 또는 예산 제한에 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="af7c3-107">하드웨어 인프라에 시간과 예산을 투자하는 대신 기업은 고객 및 사용자를 위한 응용 프로그램, 비즈니스 프로세스 및 그 이점에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="af7c3-108">Microsoft는 Microsoft Azure 가상 컴퓨터와 함께 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="af7c3-109">SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="af7c3-110">아래 백서는 Azure의 Windows 가상 컴퓨터에서 SAP NetWeaver 기반 응용 프로그램을 계획하고 구현하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="af7c3-111">[Linux 가상 컴퓨터](../../linux/classic/sap-get-started.md)에서 SAP NetWeaver 기반 응용 프로그램을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-111">You can also implement SAP NetWeaver based applications on [Linux virtual machines](../../linux/classic/sap-get-started.md).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a><span data-ttu-id="af7c3-112">Azure에서 SAP NetWeaver - HA</span><span class="sxs-lookup"><span data-stu-id="af7c3-112">SAP NetWeaver on Azure - HA</span></span>
<span data-ttu-id="af7c3-113">제목: Azure에서 SAP NetWeaver - SIOS Datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터를 사용하여 SAP ASCS/SCS 인스턴스 클러스터링</span><span class="sxs-lookup"><span data-stu-id="af7c3-113">Title: SAP NetWeaver on Azure - Clustering SAP ASCS/SCS Instances using Windows Server Failover Cluster on Azure with SIOS DataKeeper</span></span>

<span data-ttu-id="af7c3-114">요약: '이 문서에서는 SIOS DataKeeper를 사용하여 Azure에서 고가용성 SAP ASCS/SCS 구성을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-114">Summary: 'This document describes how to use SIOS DataKeeper to set up a highly available SAP ASCS/SCS configuration on Azure.</span></span> <span data-ttu-id="af7c3-115">SAP는 공유 디스크를 필요로 하는 Windows Server 장애 조치 클러스터 구성으로 SAP ASCS/SCS 또는 Enqueue Replication Services와 같은 오류 구성 요소의 단일 지점을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-115">SAP protects their single point of failure components like SAP ASCS/SCS or Enqueue Replication Services with Windows Server Failover Cluster configurations that require shared disks.</span></span> <span data-ttu-id="af7c3-116">이러한 SAP 구성 요소는 SAP 시스템의 기능에 필수적입니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-116">These SAP components are essential for the functionality of a SAP system.</span></span> <span data-ttu-id="af7c3-117">따라서 고가용성 기능은 해당 구성 요소가 나금속 및 Hyper-V 환경에 대한 Windows 클러스터 구성으로 실행된 것처럼 서버 또는 VM의 오류를 유지할 수 있는지 확인하기 위해 작동되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-117">Therefore high-availability functionality needs to be put in place to make sure that those components can sustain a failure of a server or a VM as done with Windows Cluster configurations for bare-metal and Hyper-V environments.</span></span> <span data-ttu-id="af7c3-118">2015년 8월을 기준으로 Azure 자체는 중요한 SAP 구성 요소에 필요한 Windows 기반 고가용성 구성을 위해 필요한 공유 디스크를 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-118">As of August 2015 Azure on itself cannot provide shared disks that would be required for the Windows based highly available configurations required for these critical SAP components.</span></span> <span data-ttu-id="af7c3-119">그러나 SIOS로 DataKeeper 제품의 도움을 받아 SAP ASCS/SCS의 필요에 따라 Windows Server 장애 조치 클러스터 구성은 Azure IaaS 플랫폼에서 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-119">However with the help of the product DataKeeper by SIOS, Windows Server Failover Cluster configurations as needed for SAP ASCS/SCS can be built on the Azure IaaS platform.</span></span> <span data-ttu-id="af7c3-120">이 문서는 Azure에서 SIOS Datakeeper에서 제공하는 공유 디스크와 Windows Server 장애 조치 클러스터 구성을 설치하는 방법을 단계별 접근 방식으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-120">This paper describes in a step-to-step approach how to install a Windows Server Failover Cluster configuration with shared disk provided by SIOS Datakeeper in Azure.</span></span> <span data-ttu-id="af7c3-121">이 문서에서는 고가용성 구성이 최적의 방식으로 작동하는 Azure, Windows와 SAP 측면에서 구성에 대한 세부 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-121">The paper will explain details in configurations on the Azure, Windows and SAP side which make the high availability configuration work in an optimal manner.</span></span> <span data-ttu-id="af7c3-122">이 문서는 지정된 플랫폼에서 SAP 소프트웨어 설치 및 배포에 대한 기본 리소스를 나타내는 SAP 설치 설명서 및 SAP 정보를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="af7c3-122">The paper complements the SAP Installation Documentation and SAP Notes which represent the primary resources for installations and deployments of SAP software on given platforms.</span></span>

<span data-ttu-id="af7c3-123">업데이트 날짜: 2015년 8월</span><span class="sxs-lookup"><span data-stu-id="af7c3-123">Updated: August 2015</span></span>

[<span data-ttu-id="af7c3-124">지금 이 가이드 다운로드</span><span class="sxs-lookup"><span data-stu-id="af7c3-124">Download this guide now</span></span>](http://go.microsoft.com/fwlink/?LinkId=613056)

