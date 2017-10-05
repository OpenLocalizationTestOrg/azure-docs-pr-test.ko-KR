---
title: "Azure CLI 샘플 - App Service | Microsoft Docs"
description: "Azure CLI 샘플 - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 6718694af487929d193dae54ecb2d85ece64887a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cli-samples"></a><span data-ttu-id="8af24-103">Azure CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="8af24-103">Azure CLI Samples</span></span>

<span data-ttu-id="8af24-104">다음 테이블은 Azure CLI를 사용하여 빌드된 bash 셸에 대한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="8af24-105">**앱 만들기**</span><span class="sxs-lookup"><span data-stu-id="8af24-105">**Create app**</span></span>||
| [<span data-ttu-id="8af24-106">웹앱 만들기 및 GitHub에서 코드 배포</span><span class="sxs-lookup"><span data-stu-id="8af24-106">Create a web app and deploy code from GitHub</span></span>](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-107">Azure 웹앱을 만들고 공용 GitHub 리포지토리에서 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-107">Creates an Azure web app and deploys code from a public GitHub repository.</span></span> |
| [<span data-ttu-id="8af24-108">GitHub의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8af24-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-109">사용자가 소유한 GitHub 리포지토리에서 연속 게시를 통해 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-109">Creates an Azure web app with continuous publishing from a GitHub repository you own.</span></span> |
| [<span data-ttu-id="8af24-110">웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="8af24-110">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-111">Azure 웹앱을 만들고 로컬 Git 리포지토리의 코드 푸시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-111">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="8af24-112">웹앱 만들기 및 스테이징 환경에 코드 배포</span><span class="sxs-lookup"><span data-stu-id="8af24-112">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-113">코드 변경 내용을 준비하기 위해 배포 슬롯을 사용하여 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-113">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
| [<span data-ttu-id="8af24-114">Docker 컨테이너에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8af24-114">Create an ASP.NET Core web app in a Docker container</span></span>](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-115">Linux에서 Azure 웹앱을 만들고 Docker Hub의 Docker 이미지를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-115">Creates an Azure web app on Linux and loads a Docker image from Docker Hub.</span></span> |
|<span data-ttu-id="8af24-116">**앱 구성**</span><span class="sxs-lookup"><span data-stu-id="8af24-116">**Configure app**</span></span>||
| [<span data-ttu-id="8af24-117">웹앱에 사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="8af24-117">Map a custom domain to a web app</span></span>](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-118">Azure 웹앱을 만들고 여기에 사용자 지정 도메인 이름을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="8af24-119">웹앱에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="8af24-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-120">Azure 웹앱을 만들고 여기에 사용자 지정 도메인 이름의 SSL 인증서를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="8af24-121">**앱 크기 조정**</span><span class="sxs-lookup"><span data-stu-id="8af24-121">**Scale app**</span></span>||
| [<span data-ttu-id="8af24-122">수동 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8af24-122">Scale a web app manually</span></span>](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-123">Azure 웹앱을 만들고 2개의 인스턴스로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="8af24-124">고가용성 아키텍처로 전 세계 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8af24-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-125">두 개의 지역에 두 개의 Azure 웹앱을 만들고 Azure Traffic Manager를 사용하여 단일 끝점을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="8af24-126">**리소스에 앱 연결**</span><span class="sxs-lookup"><span data-stu-id="8af24-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="8af24-127">SQL Database에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="8af24-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-128">Azure 웹앱 및 SQL Database를 만들고 앱 설정에 데이터베이스 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="8af24-129">저장소 계정에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="8af24-129">Connect a web app to a storage account</span></span>](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="8af24-130">Azure 웹앱 및 저장소 계정을 만들고 앱 설정에 저장소 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
| [<span data-ttu-id="8af24-131">Redis Cache에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="8af24-131">Connect a web app to a redis cache</span></span>](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-132">Azure 웹앱 및 Redis Cache를 만들고 앱 설정에 Redis 연결 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-132">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.)</span></span> |
| [<span data-ttu-id="8af24-133">웹앱을 Cosmos DB에 연결</span><span class="sxs-lookup"><span data-stu-id="8af24-133">Connect a web app to Cosmos DB</span></span>](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-134">Azure Web App 및 Cosmos DB를 만든 다음 앱 설정에 Cosmos DB 연결 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-134">Creates an Azure web app and a Cosmos DB, then adds the Cosmos DB connection details to the app settings.</span></span> |
|<span data-ttu-id="8af24-135">**앱 모니터링**</span><span class="sxs-lookup"><span data-stu-id="8af24-135">**Monitor app**</span></span>||
| [<span data-ttu-id="8af24-136">웹 서버 로그로 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="8af24-136">Monitor a web app with web server logs</span></span>](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="8af24-137">Azure 웹앱을 만들고 로깅을 사용하도록 설정하고 로그를 로컬 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8af24-137">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |