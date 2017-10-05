---
title: "Azure PowerShell 샘플 - App Service | Microsoft Docs"
description: "Azure PowerShell 샘플 - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="c608d-103">Azure PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="c608d-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="c608d-104">다음 테이블은 Azure PowerShell을 사용하여 빌드된 bash 셸에 대한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="c608d-105">**앱 만들기**</span><span class="sxs-lookup"><span data-stu-id="c608d-105">**Create app**</span></span>||
| [<span data-ttu-id="c608d-106">GitHub의 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c608d-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c608d-107">GitHub의 코드를 가져오는 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="c608d-108">GitHub의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c608d-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c608d-109">연속적으로 GitHub의 코드를 배포하는 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="c608d-110">FTP를 사용하여 웹앱 만들기 및 코드 배포</span><span class="sxs-lookup"><span data-stu-id="c608d-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c608d-111">FTP를 사용하여 로컬 디렉터리에서 Azure 웹앱을 만들고 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="c608d-112">웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="c608d-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c608d-113">Azure 웹앱을 만들고 로컬 Git 리포지토리의 코드 푸시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="c608d-114">웹앱 만들기 및 스테이징 환경에 코드 배포</span><span class="sxs-lookup"><span data-stu-id="c608d-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c608d-115">코드 변경 내용을 준비하기 위해 배포 슬롯을 사용하여 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="c608d-116">**앱 구성**</span><span class="sxs-lookup"><span data-stu-id="c608d-116">**Configure app**</span></span>||
| [<span data-ttu-id="c608d-117">웹앱에 사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="c608d-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c608d-118">Azure 웹앱을 만들고 여기에 사용자 지정 도메인 이름을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="c608d-119">웹앱에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="c608d-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c608d-120">Azure 웹앱을 만들고 여기에 사용자 지정 도메인 이름의 SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="c608d-121">**앱 크기 조정**</span><span class="sxs-lookup"><span data-stu-id="c608d-121">**Scale app**</span></span>||
| [<span data-ttu-id="c608d-122">수동 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c608d-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c608d-123">Azure 웹앱을 만들고 2개의 인스턴스로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="c608d-124">고가용성 아키텍처로 전 세계 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c608d-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c608d-125">두 개의 지역에 두 개의 Azure 웹앱을 만들고 Azure Traffic Manager를 사용하여 단일 끝점을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="c608d-126">**리소스에 앱 연결**</span><span class="sxs-lookup"><span data-stu-id="c608d-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="c608d-127">SQL Database에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="c608d-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c608d-128">Azure 웹앱 및 SQL Database를 만들고 앱 설정에 데이터베이스 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="c608d-129">저장소 계정에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="c608d-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c608d-130">Azure 웹앱 및 저장소 계정을 만들고 앱 설정에 저장소 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="c608d-131">**앱 모니터링**</span><span class="sxs-lookup"><span data-stu-id="c608d-131">**Monitor app**</span></span>||
| [<span data-ttu-id="c608d-132">웹 서버 로그로 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="c608d-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c608d-133">Azure 웹앱을 만들고 로깅을 사용하도록 설정하고 로그를 로컬 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c608d-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
