---
title: "Azure Linux 가상 컴퓨터 DotNet Core 자습서 1 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b3652e86-0c44-4ac9-8cd1-27abdeaea4d4
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 928d90f4bee593f04a41254b5f37d9328e59e05e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automating-application-deployments-to-linux-virtual-machines"></a><span data-ttu-id="d1d06-103">Linux 가상 컴퓨터에 대한 응용 프로그램 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="d1d06-103">Automating application deployments to Linux Virtual Machines</span></span> 

<span data-ttu-id="d1d06-104">네 부분으로 구성된 이 시리즈에서는 Azure Resource Manage 템플릿을 사용하여 Azure 리소스 및 응용 프로그램을 배포 및 구성하는 과정을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-104">This four-part series details deploying and configuring Azure resource and applications using Azure Resource Manage templates.</span></span> <span data-ttu-id="d1d06-105">이 시리즈에서는 샘플 템플릿이 배포되고 배포 템플릿이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-105">In this series, a sample template is deployed and the deployment template examined.</span></span> <span data-ttu-id="d1d06-106">이 시리즈의 목적은 Azure 리소스 간 관계를 익히고 완전히 통합된 Azure Resource Manager 템플릿을 배포하는 과정을 경험해보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-106">The goal of this series is to educate on the relationship between Azure resources, and to provide hands on experience deploying fully integrated Azure Resource Manager templates.</span></span> <span data-ttu-id="d1d06-107">이 문서에서는 Azure Resource Manager에 대한 기본적인 지식이 있다고 가정하므로 이 자습서를 시작하기 전에 기본적인 Azure Resource Manager 개념을 숙지하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-107">This document assumes a basic level of knowledge with Azure Resource Manager, before starting this tutorial familiarize yourself with basic Azure Resource Manager concepts.</span></span> 

## <a name="music-store-application"></a><span data-ttu-id="d1d06-108">Music Store 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d1d06-108">Music store application</span></span>
<span data-ttu-id="d1d06-109">이 시리즈에 사용된 샘플은 Music Store 쇼핑 환경을 시뮬레이트하는 .Net Core 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-109">The sample used in this series is a .Net Core application simulating a Music Store shopping experience.</span></span> <span data-ttu-id="d1d06-110">이 응용 프로그램은 Linux 또는 Windows 가상 시스템에 배포할 수 있으며 둘 다에 대해 샘플 배포가 만들어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-110">This application can be deployed to either a Linux or Windows virtual system, sample deployments have been created for both.</span></span> <span data-ttu-id="d1d06-111">이 응용 프로그램에는 웹 응용 프로그램 및 SQL Database가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-111">The application includes a web application and a SQL database.</span></span> <span data-ttu-id="d1d06-112">이 시리즈의 문서를 읽기 전에 이 페이지에 있는 배포 단추를 사용하여 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-112">Before reading the articles in this series, deploy the application using the deployment button found on this page.</span></span> <span data-ttu-id="d1d06-113">완전히 배포하면 응용 프로그램/Azure 아키텍처가 다음 다이어그램과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-113">When fully deployed, the application / Azure architecture looks like the following diagram.</span></span> 

<span data-ttu-id="d1d06-114">Music Store Resource Manager 템플릿은 [Music Store Linux 템플릿](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)</span><span class="sxs-lookup"><span data-stu-id="d1d06-114">The Music Store Resource Manager template can be found here, [Music Store Linux Template](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)</span></span>

![Music Store 응용 프로그램](./media/dotnet-core-1-landing/music-store.png)

<span data-ttu-id="d1d06-116">관련된 템플릿 JSON을 포함하여 이러한 각 구성 요소는 다음 네 가지 문서에서 검토됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-116">Each of these components, including the associate template JSON is examined in the following four articles.</span></span>

* <span data-ttu-id="d1d06-117">[**응용 프로그램 아키텍처**](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – 웹 사이트 및 데이터베이스와 같은 응용 프로그램 구성 요소는 가상 컴퓨터 및 Azure SQL Database와 같은 Azure 컴퓨터 리소스에 호스트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-117">[**Application Architecture**](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – Application components such as web sites and databases need to be hosted on Azure computer resources such as virtual machines and Azure SQL databases.</span></span> <span data-ttu-id="d1d06-118">이 문서에서는 계산 요구를 Azure 리소스에 매핑하고 이러한 리소스를 Azure Resource Manager 템플릿을 통해 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-118">This document walks through mapping compute need, to Azure resources, and deploying these resources with an Azure Resource Manager template.</span></span> 
* <span data-ttu-id="d1d06-119">[**액세스 및 보안**](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – Azure에서 응용 프로그램을 호스트할 때 응용 프로그램에 액세스되는 방법과 응용 프로그램 구성 요소가 서로 액세스하는 방법을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-119">[**Access and Security**](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – When hosting applications in Azure, it is necessary to consider how the application is accessed, and how different application components access each other.</span></span> <span data-ttu-id="d1d06-120">이 문서에서는 응용 프로그램에 대한 인터넷 액세스와 응용 프로그램 구성 요소 간 액세스를 제공하고 보안을 유지하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-120">This document details providing and securing internet access to an application and access between application components.</span></span>
* <span data-ttu-id="d1d06-121">[**가용성 및 크기 조정**](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – 가용성 및 크기 조정은 인프라 가동 중지 시간 동안 응용 프로그램이 실행 상태를 유지하는 능력과 응용 프로그램 요구에 맞게 계산 리소스의 규모를 조정하는 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-121">[**Availability and Scale**](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – Availability and scale refer to the applications ability to stay running during infrastructure downtime, and the ability to scale compute resources to meet application demand.</span></span> <span data-ttu-id="d1d06-122">이 문서에서는 부하 분산되고 가용성이 높은 응용 프로그램을 배포하는 데 필요한 구성 요소에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-122">This document details the components needed to deploy a load balanced and highly available application.</span></span>
* <span data-ttu-id="d1d06-123">[**응용 프로그램 배포**](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -Azure 가상 컴퓨터에 응용 프로그램을 배포할 때 응용 프로그램 이진 파일이 가상 컴퓨터에 설치되는 방법을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-123">[**Application Deployment**](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - When deploying applications onto Azure Virtual Machines, the method by which the application binaries are installed on the Virtual Machine must be considered.</span></span> <span data-ttu-id="d1d06-124">이 문서에서는 Azure 가상 컴퓨터 사용자 지정 스크립트 확장을 사용하여 응용 프로그램 설치를 자동화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-124">This document details automating application installation using Azure Virtual Machine Custom Script Extensions.</span></span>

<span data-ttu-id="d1d06-125">Azure Resource Manager 템플릿을 개발할 때의 목표는 Azure 인프라의 배포와 이 Azure 인프라에 호스트되는 응용 프로그램의 설치 및 구성을 자동화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-125">The goal when developing Azure Resource Manager templates is to automate the deployment of Azure Infrastructure, and the installation and configuration of any applications being hosted on this Azure infrastructure.</span></span> <span data-ttu-id="d1d06-126">이러한 문서를 따라 작업하면서 이러한 작업의 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-126">Working through these articles provides an example of this experience.</span></span>

## <a name="deploy-the-music-store-application"></a><span data-ttu-id="d1d06-127">Music Store 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="d1d06-127">Deploy the music store application</span></span>
<span data-ttu-id="d1d06-128">이 단추를 사용하여 Music Store 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-128">The Music Store application can be deployed using this button.</span></span>

<span data-ttu-id="d1d06-129"><a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a></span><span class="sxs-lookup"><span data-stu-id="d1d06-129"><a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a></span></span>

<span data-ttu-id="d1d06-130">Azure Resource Manager 템플릿에는 다음 매개 변수 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-130">The Azure Resource Manager template requires the following parameter values.</span></span>

| <span data-ttu-id="d1d06-131">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="d1d06-131">Parameter Name</span></span> | <span data-ttu-id="d1d06-132">설명</span><span class="sxs-lookup"><span data-stu-id="d1d06-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1d06-133">SSHKEYDATA</span><span class="sxs-lookup"><span data-stu-id="d1d06-133">SSHKEYDATA</span></span> |<span data-ttu-id="d1d06-134">가상 컴퓨터에 대한 액세스를 보호하는 데 사용되는 SSH 키 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-134">SSH key data used to secure access to the Virtual Machine.</span></span> <span data-ttu-id="d1d06-135">SSH 키 쌍을 만드는 방법에 대한 자세한 내용은 [Azure에서 Linux VM에 대한 SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1d06-135">For information on creating an SSH key pair, see [Creating SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> |
| <span data-ttu-id="d1d06-136">ADMINUSERNAME</span><span class="sxs-lookup"><span data-stu-id="d1d06-136">ADMINUSERNAME</span></span> |<span data-ttu-id="d1d06-137">가상 컴퓨터와 Azure SQL Database에 사용되는 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-137">Admin user name that is used on the virtual machine and the Azure SQL Database.</span></span> |
| <span data-ttu-id="d1d06-138">SQLADMINPASSWORD</span><span class="sxs-lookup"><span data-stu-id="d1d06-138">SQLADMINPASSWORD</span></span> |<span data-ttu-id="d1d06-139">Azure SQL Database에 사용되는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-139">Password that is used on the Azure SQL Database.</span></span> |
| <span data-ttu-id="d1d06-140">NUMBEROFINSTANCES</span><span class="sxs-lookup"><span data-stu-id="d1d06-140">NUMBEROFINSTANCES</span></span> |<span data-ttu-id="d1d06-141">만들 가상 컴퓨터의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-141">The number of virtual machines to be created.</span></span> <span data-ttu-id="d1d06-142">이러한 각 가상 컴퓨터는 Music Store 웹 응용 프로그램을 호스트하며 모든 트래픽의 부하가 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-142">Each of these virtual machines host the Music Store web application, and all traffic is load balanced across them.</span></span> |
| <span data-ttu-id="d1d06-143">PUBLICIPADDRESSDNSNAME</span><span class="sxs-lookup"><span data-stu-id="d1d06-143">PUBLICIPADDRESSDNSNAME</span></span> |<span data-ttu-id="d1d06-144">공용 IP 주소와 연결된 전역 고유 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-144">Globally unique DNS name associated with the Public IP address.</span></span> |

<span data-ttu-id="d1d06-145">템플릿 배포가 완료되면 인터넷 브라우저를 사용하여 이 공용 IP 주소로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-145">When the template deployment has completed, browse to the public IP Address using any internet browser.</span></span> <span data-ttu-id="d1d06-146">.NET Core Music 사이트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d1d06-146">The .Net Core Music site will be presented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1d06-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1d06-147">Next steps</span></span>
<hr>

[<span data-ttu-id="d1d06-148">1단계 - Azure Resource Manager 템플릿을 사용하는 응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="d1d06-148">Step 1 - Application Architecture with Azure Resource Manager Templates</span></span>](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="d1d06-149">2단계 - Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="d1d06-149">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="d1d06-150">3단계 - Azure Resource Manager 템플릿의 가용성 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d1d06-150">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="d1d06-151">4단계 - Azure Resource Manager 템플릿을 사용한 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="d1d06-151">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

