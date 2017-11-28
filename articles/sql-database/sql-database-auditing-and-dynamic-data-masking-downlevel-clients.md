---
title: "aaaTable TDS 리디렉션, 감사 및 Azure SQL 데이터베이스에 대 한 IP 끝점 | Microsoft Docs"
description: "Azure SQL Database에서 테이블 감사를 구현할 때 감사, TDS 리디렉션 및 IP 끝점 변경 내용에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: 
ms.assetid: 4ef19ed1-e798-43a2-ad99-0e563f93ab53
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: giladm
ms.openlocfilehash: 966c23f92fab6fa459a515ad841bb2d5f75436aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database----downlevel-clients-support-and-ip-endpoint-changes-for-table-auditing"></a><span data-ttu-id="84cc3-103">SQL Database - 하위 클라이언트 지원 및 테이블 감사에 대한 IP 끝점 변경</span><span class="sxs-lookup"><span data-stu-id="84cc3-103">SQL Database -  Downlevel clients support and IP endpoint changes for Table Auditing</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84cc3-104">이 문서에만 tooTable 감사에는 적용 **이제 사용 되지 않는**합니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-104">This document applies only tooTable Auditing, which is **now deprecated**.</span></span><br>
> <span data-ttu-id="84cc3-105">Hello 새를 사용 하십시오 [Blob 감사](sql-database-auditing.md) 메서드를는 **없는** 하위 수준 클라이언트 연결 문자열 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-105">Please use hello new [Blob Auditing](sql-database-auditing.md) method, which **does not** require downlevel client connection string modifications.</span></span> <span data-ttu-id="84cc3-106">Blob 감사에 대한 추가 정보는 [SQL 데이터베이스 감사 시작](sql-database-auditing.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-106">Additional info on Blob Auditing can be found in [Get started with SQL database auditing](sql-database-auditing.md).</span></span>

<span data-ttu-id="84cc3-107">[데이터베이스 감사](sql-database-auditing.md)는 TDS 리디렉션을 지원하는 SQL 클라이언트와 함께 자동으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-107">[Database Auditing](sql-database-auditing.md) works automatically with SQL clients that support TDS redirection.</span></span> <span data-ttu-id="84cc3-108">Note hello Blob 감사 메서드를 사용 하는 경우 해당 리디렉션 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-108">Note that redirection does not apply when using hello Blob Auditing method.</span></span>

## <span data-ttu-id="84cc3-109"><a id="subheading-1"></a>하위 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="84cc3-109"><a id="subheading-1"></a>Downlevel clients support</span></span>
<span data-ttu-id="84cc3-110">TDS 7.4를 구현하는 모든 클라이언트는 리디렉션도 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-110">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="84cc3-111">예외 toothis 리디렉션 구현 되지 않은 Node.JS 용 hello 리디렉션 기능을 완벽 하 게 지원 되지 않으며 Tedious에 JDBC 4.0를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-111">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="84cc3-112">"하위 클라이언트"에 대 한 즉, TDS 버전 7.3 지원 하 고 아래-hello 연결 문자열에 FQDN 서버 hello 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-112">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="84cc3-113">Hello 연결 문자열에서 원래 서버 FQDN: <*서버 이름*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="84cc3-113">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="84cc3-114">Hello 연결 문자열에 수정 된 서버 FQDN: <*서버 이름*>.database. **보안**. windows.net</span><span class="sxs-lookup"><span data-stu-id="84cc3-114">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="84cc3-115">"하위 클라이언트"의 일부 목록에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-115">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="84cc3-116">.NET 4.0 이하</span><span class="sxs-lookup"><span data-stu-id="84cc3-116">.NET 4.0 and below,</span></span>
* <span data-ttu-id="84cc3-117">ODBC 10.0 이하</span><span class="sxs-lookup"><span data-stu-id="84cc3-117">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="84cc3-118">JDBC (JDBC TDS 7.4, TDS 리디렉션 기능을 완전히 지원 되지 않는 hello는 지원) 하는 중</span><span class="sxs-lookup"><span data-stu-id="84cc3-118">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="84cc3-119">Tedious(Node.JS용)</span><span class="sxs-lookup"><span data-stu-id="84cc3-119">Tedious (for Node.JS)</span></span>

<span data-ttu-id="84cc3-120">**설명:** hello 서버 FDQN 수정 위에 (임시 완화) 각 데이터베이스에는 구성에 대 한 요구가 단계 없이 SQL 서버 수준 감사 정책 적용에 대 한도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-120">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>

## <span data-ttu-id="84cc3-121"><a id="subheading-2"></a>감사를 사용하도록 설정할 때 IP 끝점 변경</span><span class="sxs-lookup"><span data-stu-id="84cc3-121"><a id="subheading-2"></a>IP endpoint changes when enabling Auditing</span></span>
<span data-ttu-id="84cc3-122">테이블에서 감사를 설정 하면 데이터베이스의 hello IP 끝점 변경 됩니다 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="84cc3-122">Please note that when you enable Table Auditing, hello IP endpoint of your database will change.</span></span> <span data-ttu-id="84cc3-123">엄격한 방화벽 설정이 있으면 해당 방화벽 설정을 적절하게 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="84cc3-123">If you have strict firewall settings, please update those firewall settings accordingly.</span></span>

<span data-ttu-id="84cc3-124">새 데이터베이스 IP 끝점 hello hello 데이터베이스 지역에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="84cc3-124">hello new database IP endpoint will depend on hello database region:</span></span>

| <span data-ttu-id="84cc3-125">데이터베이스 지역</span><span class="sxs-lookup"><span data-stu-id="84cc3-125">Database Region</span></span> | <span data-ttu-id="84cc3-126">가능한 IP 끝점</span><span class="sxs-lookup"><span data-stu-id="84cc3-126">Possible IP endpoints</span></span> |
| --- | --- |
| <span data-ttu-id="84cc3-127">중국 북부</span><span class="sxs-lookup"><span data-stu-id="84cc3-127">China North</span></span> |<span data-ttu-id="84cc3-128">139.217.29.176, 139.217.28.254</span><span class="sxs-lookup"><span data-stu-id="84cc3-128">139.217.29.176, 139.217.28.254</span></span> |
| <span data-ttu-id="84cc3-129">중국 동부</span><span class="sxs-lookup"><span data-stu-id="84cc3-129">China East</span></span> |<span data-ttu-id="84cc3-130">42.159.245.65, 42.159.246.245</span><span class="sxs-lookup"><span data-stu-id="84cc3-130">42.159.245.65, 42.159.246.245</span></span> |
| <span data-ttu-id="84cc3-131">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="84cc3-131">Australia East</span></span> |<span data-ttu-id="84cc3-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span><span class="sxs-lookup"><span data-stu-id="84cc3-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span></span> |
| <span data-ttu-id="84cc3-133">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="84cc3-133">Australia Southeast</span></span> |<span data-ttu-id="84cc3-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span><span class="sxs-lookup"><span data-stu-id="84cc3-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span></span> |
| <span data-ttu-id="84cc3-135">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="84cc3-135">Brazil South</span></span> |<span data-ttu-id="84cc3-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span><span class="sxs-lookup"><span data-stu-id="84cc3-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span></span> |
| <span data-ttu-id="84cc3-137">미국 중부</span><span class="sxs-lookup"><span data-stu-id="84cc3-137">Central US</span></span> |<span data-ttu-id="84cc3-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span><span class="sxs-lookup"><span data-stu-id="84cc3-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span></span> |
| <span data-ttu-id="84cc3-139">미국 중부 EUAP</span><span class="sxs-lookup"><span data-stu-id="84cc3-139">Central US EUAP</span></span> |<span data-ttu-id="84cc3-140">52.180.178.16, 52.180.176.190</span><span class="sxs-lookup"><span data-stu-id="84cc3-140">52.180.178.16, 52.180.176.190</span></span> |
| <span data-ttu-id="84cc3-141">동아시아</span><span class="sxs-lookup"><span data-stu-id="84cc3-141">East Asia</span></span> |<span data-ttu-id="84cc3-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span><span class="sxs-lookup"><span data-stu-id="84cc3-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span></span> |
| <span data-ttu-id="84cc3-143">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="84cc3-143">East US 2</span></span> |<span data-ttu-id="84cc3-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span><span class="sxs-lookup"><span data-stu-id="84cc3-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span></span> |
| <span data-ttu-id="84cc3-145">미국 동부</span><span class="sxs-lookup"><span data-stu-id="84cc3-145">East US</span></span> |<span data-ttu-id="84cc3-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span><span class="sxs-lookup"><span data-stu-id="84cc3-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span></span> |
| <span data-ttu-id="84cc3-147">미국 동부 EUAP</span><span class="sxs-lookup"><span data-stu-id="84cc3-147">East US EUAP</span></span> |<span data-ttu-id="84cc3-148">52.225.190.86, 52.225.191.187</span><span class="sxs-lookup"><span data-stu-id="84cc3-148">52.225.190.86, 52.225.191.187</span></span> |
| <span data-ttu-id="84cc3-149">인도 중부</span><span class="sxs-lookup"><span data-stu-id="84cc3-149">Central India</span></span> |<span data-ttu-id="84cc3-150">104.211.98.219, 104.211.103.71</span><span class="sxs-lookup"><span data-stu-id="84cc3-150">104.211.98.219, 104.211.103.71</span></span> |
| <span data-ttu-id="84cc3-151">인도 남부</span><span class="sxs-lookup"><span data-stu-id="84cc3-151">South India</span></span> |<span data-ttu-id="84cc3-152">104.211.227.102, 104.211.225.157</span><span class="sxs-lookup"><span data-stu-id="84cc3-152">104.211.227.102, 104.211.225.157</span></span> |
| <span data-ttu-id="84cc3-153">인도 서부</span><span class="sxs-lookup"><span data-stu-id="84cc3-153">West India</span></span> |<span data-ttu-id="84cc3-154">104.211.161.152, 104.211.162.21</span><span class="sxs-lookup"><span data-stu-id="84cc3-154">104.211.161.152, 104.211.162.21</span></span> |
| <span data-ttu-id="84cc3-155">일본 동부</span><span class="sxs-lookup"><span data-stu-id="84cc3-155">Japan East</span></span> |<span data-ttu-id="84cc3-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span><span class="sxs-lookup"><span data-stu-id="84cc3-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span></span> |
| <span data-ttu-id="84cc3-157">일본 서부</span><span class="sxs-lookup"><span data-stu-id="84cc3-157">Japan West</span></span> |<span data-ttu-id="84cc3-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span><span class="sxs-lookup"><span data-stu-id="84cc3-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span></span> |
| <span data-ttu-id="84cc3-159">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="84cc3-159">North Central US</span></span> |<span data-ttu-id="84cc3-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span><span class="sxs-lookup"><span data-stu-id="84cc3-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span></span> |
| <span data-ttu-id="84cc3-161">북유럽</span><span class="sxs-lookup"><span data-stu-id="84cc3-161">North Europe</span></span> |<span data-ttu-id="84cc3-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span><span class="sxs-lookup"><span data-stu-id="84cc3-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span></span> |
| <span data-ttu-id="84cc3-163">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="84cc3-163">South Central US</span></span> |<span data-ttu-id="84cc3-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span><span class="sxs-lookup"><span data-stu-id="84cc3-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span></span> |
| <span data-ttu-id="84cc3-165">동남아시아</span><span class="sxs-lookup"><span data-stu-id="84cc3-165">Southeast Asia</span></span> |<span data-ttu-id="84cc3-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span><span class="sxs-lookup"><span data-stu-id="84cc3-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span></span> |
| <span data-ttu-id="84cc3-167">서유럽</span><span class="sxs-lookup"><span data-stu-id="84cc3-167">West Europe</span></span> |<span data-ttu-id="84cc3-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span><span class="sxs-lookup"><span data-stu-id="84cc3-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span></span> |
| <span data-ttu-id="84cc3-169">미국 서부</span><span class="sxs-lookup"><span data-stu-id="84cc3-169">West US</span></span> |<span data-ttu-id="84cc3-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span><span class="sxs-lookup"><span data-stu-id="84cc3-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span></span> |
| <span data-ttu-id="84cc3-171">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="84cc3-171">West US 2</span></span> |<span data-ttu-id="84cc3-172">13.66.224.156, 13.66.227.8</span><span class="sxs-lookup"><span data-stu-id="84cc3-172">13.66.224.156, 13.66.227.8</span></span> |
| <span data-ttu-id="84cc3-173">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="84cc3-173">West Central US</span></span> |<span data-ttu-id="84cc3-174">52.161.29.186, 52.161.27.213</span><span class="sxs-lookup"><span data-stu-id="84cc3-174">52.161.29.186, 52.161.27.213</span></span> |
| <span data-ttu-id="84cc3-175">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="84cc3-175">Canada Central</span></span> |<span data-ttu-id="84cc3-176">13.88.248.106, 13.88.248.110</span><span class="sxs-lookup"><span data-stu-id="84cc3-176">13.88.248.106, 13.88.248.110</span></span> |
| <span data-ttu-id="84cc3-177">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="84cc3-177">Canada East</span></span> |<span data-ttu-id="84cc3-178">40.86.227.82, 40.86.225.194</span><span class="sxs-lookup"><span data-stu-id="84cc3-178">40.86.227.82, 40.86.225.194</span></span> |
| <span data-ttu-id="84cc3-179">영국 북부</span><span class="sxs-lookup"><span data-stu-id="84cc3-179">UK North</span></span> |<span data-ttu-id="84cc3-180">13.87.101.18, 13.87.100.232</span><span class="sxs-lookup"><span data-stu-id="84cc3-180">13.87.101.18, 13.87.100.232</span></span> |
| <span data-ttu-id="84cc3-181">영국 남부 2</span><span class="sxs-lookup"><span data-stu-id="84cc3-181">UK South 2</span></span> |<span data-ttu-id="84cc3-182">13.87.32.202, 13.87.32.226</span><span class="sxs-lookup"><span data-stu-id="84cc3-182">13.87.32.202, 13.87.32.226</span></span> |
