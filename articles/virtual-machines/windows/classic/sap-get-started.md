---
title: "Windows 가상 컴퓨터에 SAP aaaUsing | Microsoft Docs"
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
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="9cc81-103">Azure의 Windows 가상 컴퓨터에서 SAP 사용</span><span class="sxs-lookup"><span data-stu-id="9cc81-103">Using SAP on Windows virtual machines in Azure</span></span>
<span data-ttu-id="9cc81-104">클라우드 컴퓨팅은 toolarge 및 다국적 회사를 중소 기업에서 점점 더 많은 중요도 hello IT 업계 내에서 취소 하는 널리 사용 되는 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="9cc81-105">Microsoft Azure는 hello 새로운 작업 방식을 폭넓게 제공 된 microsoft에서 클라우드 서비스 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="9cc81-106">이제 고객은 수 toorapidly 프로 비전 및 프로 비전 해제 응용 프로그램 클라우드 서비스로 제한 된 tootechnical 또는 예산 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="9cc81-107">하드웨어 인프라에 시간과 예산을 투자를 하는 대신 고객 및 사용자에 대 한 회사는 hello 응용 프로그램 및 비즈니스 프로세스의 장점에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="9cc81-108">Microsoft는 Microsoft Azure 가상 컴퓨터와 함께 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="9cc81-109">SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="9cc81-110">아래 hello 백서 tooplan 및 구현 SAP NetWeaver 기반 Azure에서 Windows 가상 컴퓨터에 응용 프로그램에 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="9cc81-111">[Linux 가상 컴퓨터](../../linux/classic/sap-get-started.md)에서 SAP NetWeaver 기반 응용 프로그램을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-111">You can also implement SAP NetWeaver based applications on [Linux virtual machines](../../linux/classic/sap-get-started.md).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a><span data-ttu-id="9cc81-112">Azure에서 SAP NetWeaver - HA</span><span class="sxs-lookup"><span data-stu-id="9cc81-112">SAP NetWeaver on Azure - HA</span></span>
<span data-ttu-id="9cc81-113">제목: Azure-SIOS datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터를 사용 하 여 클러스터링 SAP ASCS/SCS 인스턴스에에서 NetWeaver aaaSAP</span><span class="sxs-lookup"><span data-stu-id="9cc81-113">title: aaaSAP NetWeaver on Azure - Clustering SAP ASCS/SCS Instances using Windows Server Failover Cluster on Azure with SIOS DataKeeper</span></span>

<span data-ttu-id="9cc81-114">요약: '이 문서에서는 설명 방법을 toouse SIOS DataKeeper tooset Azure에서 항상 사용 가능한 SAP ASCS/SCS 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-114">Summary: 'This document describes how toouse SIOS DataKeeper tooset up a highly available SAP ASCS/SCS configuration on Azure.</span></span> <span data-ttu-id="9cc81-115">SAP는 공유 디스크를 필요로 하는 Windows Server 장애 조치 클러스터 구성으로 SAP ASCS/SCS 또는 Enqueue Replication Services와 같은 오류 구성 요소의 단일 지점을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-115">SAP protects their single point of failure components like SAP ASCS/SCS or Enqueue Replication Services with Windows Server Failover Cluster configurations that require shared disks.</span></span> <span data-ttu-id="9cc81-116">이러한 SAP 구성 요소는 SAP 시스템의 hello 기능에 필수적입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-116">These SAP components are essential for hello functionality of a SAP system.</span></span> <span data-ttu-id="9cc81-117">따라서 toobe 모드로 항상 사용 가능한 기능 요구 배치 toomake 있는지 완전 및 Hyper-v 환경에 대 한 Windows 클러스터 구성으로 작업 하는 것 처럼 해당 구성 요소는 서버 또는 VM의 실패를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-117">Therefore high-availability functionality needs toobe put in place toomake sure that those components can sustain a failure of a server or a VM as done with Windows Cluster configurations for bare-metal and Hyper-V environments.</span></span> <span data-ttu-id="9cc81-118">2015 년 8 월부터 Azure 자체 Windows hello에 필요한 공유 디스크 기반 이러한 주요 SAP 구성 요소에 필요한 항상 사용 가능한 구성으로 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-118">As of August 2015 Azure on itself cannot provide shared disks that would be required for hello Windows based highly available configurations required for these critical SAP components.</span></span> <span data-ttu-id="9cc81-119">그러나 hello Azure IaaS 플랫폼에서 사용 하 여 hello SIOS DataKeeper hello 제품, SAP ASCS/SCS 필요에 따라 Windows Server 장애 조치 클러스터 구성은 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-119">However with hello help of hello product DataKeeper by SIOS, Windows Server Failover Cluster configurations as needed for SAP ASCS/SCS can be built on hello Azure IaaS platform.</span></span> <span data-ttu-id="9cc81-120">이 문서는 tooinstall 공유 디스크 되는 Windows Server 장애 조치 클러스터 구성을 제공 하는 방식을 하 여 Azure에서 SIOS Datakeeper 단계-단계 접근 방식에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-120">This paper describes in a step-to-step approach how tooinstall a Windows Server Failover Cluster configuration with shared disk provided by SIOS Datakeeper in Azure.</span></span> <span data-ttu-id="9cc81-121">hello 용지를 최적의 방식으로 작동 하는 hello 고가용성 구성을 hello Azure, Windows와 SAP 측면에서 구성에 대 한 세부 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-121">hello paper will explain details in configurations on hello Azure, Windows and SAP side which make hello high availability configuration work in an optimal manner.</span></span> <span data-ttu-id="9cc81-122">hello 용지 보완 hello SAP 설치 설명서 및 SAP Note를 설치 및 배포에 SAP 소프트웨어에 대 한 기본 리소스 hello 플랫폼을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc81-122">hello paper complements hello SAP Installation Documentation and SAP Notes which represent hello primary resources for installations and deployments of SAP software on given platforms.</span></span>

<span data-ttu-id="9cc81-123">업데이트 날짜: 2015년 8월</span><span class="sxs-lookup"><span data-stu-id="9cc81-123">Updated: August 2015</span></span>

[<span data-ttu-id="9cc81-124">지금 이 가이드 다운로드</span><span class="sxs-lookup"><span data-stu-id="9cc81-124">Download this guide now</span></span>](http://go.microsoft.com/fwlink/?LinkId=613056)

