---
title: "Azure SQL Database의 테이블 감사, TDS 리디렉션 및 IP 끝점 | Microsoft Docs"
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
ms.openlocfilehash: d4a7e6658ec65a70bd7e07859e2a69acee58b7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database----downlevel-clients-support-and-ip-endpoint-changes-for-table-auditing"></a><span data-ttu-id="ad731-103">SQL Database - 하위 클라이언트 지원 및 테이블 감사에 대한 IP 끝점 변경</span><span class="sxs-lookup"><span data-stu-id="ad731-103">SQL Database -  Downlevel clients support and IP endpoint changes for Table Auditing</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad731-104">이 문서는 **이제는 사용되지 않는** 테이블 감사에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-104">This document applies only to Table Auditing, which is **now deprecated**.</span></span><br>
> <span data-ttu-id="ad731-105">하위 클라이언트 연결 문자열을 수정할 필요가 **없는** 새 [Blob 감사](sql-database-auditing.md) 메서드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ad731-105">Please use the new [Blob Auditing](sql-database-auditing.md) method, which **does not** require downlevel client connection string modifications.</span></span> <span data-ttu-id="ad731-106">Blob 감사에 대한 추가 정보는 [SQL 데이터베이스 감사 시작](sql-database-auditing.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-106">Additional info on Blob Auditing can be found in [Get started with SQL database auditing](sql-database-auditing.md).</span></span>

<span data-ttu-id="ad731-107">[데이터베이스 감사](sql-database-auditing.md)는 TDS 리디렉션을 지원하는 SQL 클라이언트와 함께 자동으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-107">[Database Auditing](sql-database-auditing.md) works automatically with SQL clients that support TDS redirection.</span></span> <span data-ttu-id="ad731-108">BLOB 감사 메서드를 사용하는 경우에는 해당 리디렉션이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-108">Note that redirection does not apply when using the Blob Auditing method.</span></span>

## <span data-ttu-id="ad731-109"><a id="subheading-1"></a>하위 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="ad731-109"><a id="subheading-1"></a>Downlevel clients support</span></span>
<span data-ttu-id="ad731-110">TDS 7.4를 구현하는 모든 클라이언트는 리디렉션도 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-110">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="ad731-111">이에 대한 예외에는 리디렉션 기능이 완전히 지원되지 않는 JDBC 4.0 및 리디렉션이 구현되지 않은 Node.JS용 Tedious가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-111">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="ad731-112">TDS 버전 7.3 이하를 지원하는 "하위 클라이언트"의 경우, 연결 문자열에서 서버 FQDN을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-112">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="ad731-113">연결 문자열에서 원래 서버 FQDN: <*서버 이름*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="ad731-113">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="ad731-114">연결 문자열에서 수정된 서버 FQDN: <*서버 이름*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="ad731-114">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="ad731-115">"하위 클라이언트"의 일부 목록에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-115">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="ad731-116">.NET 4.0 이하</span><span class="sxs-lookup"><span data-stu-id="ad731-116">.NET 4.0 and below,</span></span>
* <span data-ttu-id="ad731-117">ODBC 10.0 이하</span><span class="sxs-lookup"><span data-stu-id="ad731-117">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="ad731-118">JDBC(JDBC는 TDS 7.4를 지원하지만 TDS 리디렉션 기능은 완전히 지원되지 않음)</span><span class="sxs-lookup"><span data-stu-id="ad731-118">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="ad731-119">Tedious(Node.JS용)</span><span class="sxs-lookup"><span data-stu-id="ad731-119">Tedious (for Node.JS)</span></span>

<span data-ttu-id="ad731-120">**주석:** 위의 서버 FDQN 수정은 각 데이터베이스에서 구성 단계에 대한 요구 없이 SQL 서버 수준 감사 정책의 적용에도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-120">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>

## <span data-ttu-id="ad731-121"><a id="subheading-2"></a>감사를 사용하도록 설정할 때 IP 끝점 변경</span><span class="sxs-lookup"><span data-stu-id="ad731-121"><a id="subheading-2"></a>IP endpoint changes when enabling Auditing</span></span>
<span data-ttu-id="ad731-122">테이블 감사를 사용하도록 설정하면 데이터베이스의 IP 끝점이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-122">Please note that when you enable Table Auditing, the IP endpoint of your database will change.</span></span> <span data-ttu-id="ad731-123">엄격한 방화벽 설정이 있으면 해당 방화벽 설정을 적절하게 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="ad731-123">If you have strict firewall settings, please update those firewall settings accordingly.</span></span>

<span data-ttu-id="ad731-124">새 데이터베이스 IP 끝점은 데이터베이스 지역에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ad731-124">The new database IP endpoint will depend on the database region:</span></span>

| <span data-ttu-id="ad731-125">데이터베이스 지역</span><span class="sxs-lookup"><span data-stu-id="ad731-125">Database Region</span></span> | <span data-ttu-id="ad731-126">가능한 IP 끝점</span><span class="sxs-lookup"><span data-stu-id="ad731-126">Possible IP endpoints</span></span> |
| --- | --- |
| <span data-ttu-id="ad731-127">중국 북부</span><span class="sxs-lookup"><span data-stu-id="ad731-127">China North</span></span> |<span data-ttu-id="ad731-128">139.217.29.176, 139.217.28.254</span><span class="sxs-lookup"><span data-stu-id="ad731-128">139.217.29.176, 139.217.28.254</span></span> |
| <span data-ttu-id="ad731-129">중국 동부</span><span class="sxs-lookup"><span data-stu-id="ad731-129">China East</span></span> |<span data-ttu-id="ad731-130">42.159.245.65, 42.159.246.245</span><span class="sxs-lookup"><span data-stu-id="ad731-130">42.159.245.65, 42.159.246.245</span></span> |
| <span data-ttu-id="ad731-131">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="ad731-131">Australia East</span></span> |<span data-ttu-id="ad731-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span><span class="sxs-lookup"><span data-stu-id="ad731-132">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span></span> |
| <span data-ttu-id="ad731-133">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="ad731-133">Australia Southeast</span></span> |<span data-ttu-id="ad731-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span><span class="sxs-lookup"><span data-stu-id="ad731-134">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span></span> |
| <span data-ttu-id="ad731-135">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="ad731-135">Brazil South</span></span> |<span data-ttu-id="ad731-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span><span class="sxs-lookup"><span data-stu-id="ad731-136">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span></span> |
| <span data-ttu-id="ad731-137">미국 중부</span><span class="sxs-lookup"><span data-stu-id="ad731-137">Central US</span></span> |<span data-ttu-id="ad731-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span><span class="sxs-lookup"><span data-stu-id="ad731-138">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span></span> |
| <span data-ttu-id="ad731-139">미국 중부 EUAP</span><span class="sxs-lookup"><span data-stu-id="ad731-139">Central US EUAP</span></span> |<span data-ttu-id="ad731-140">52.180.178.16, 52.180.176.190</span><span class="sxs-lookup"><span data-stu-id="ad731-140">52.180.178.16, 52.180.176.190</span></span> |
| <span data-ttu-id="ad731-141">동아시아</span><span class="sxs-lookup"><span data-stu-id="ad731-141">East Asia</span></span> |<span data-ttu-id="ad731-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span><span class="sxs-lookup"><span data-stu-id="ad731-142">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span></span> |
| <span data-ttu-id="ad731-143">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="ad731-143">East US 2</span></span> |<span data-ttu-id="ad731-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span><span class="sxs-lookup"><span data-stu-id="ad731-144">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span></span> |
| <span data-ttu-id="ad731-145">미국 동부</span><span class="sxs-lookup"><span data-stu-id="ad731-145">East US</span></span> |<span data-ttu-id="ad731-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span><span class="sxs-lookup"><span data-stu-id="ad731-146">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span></span> |
| <span data-ttu-id="ad731-147">미국 동부 EUAP</span><span class="sxs-lookup"><span data-stu-id="ad731-147">East US EUAP</span></span> |<span data-ttu-id="ad731-148">52.225.190.86, 52.225.191.187</span><span class="sxs-lookup"><span data-stu-id="ad731-148">52.225.190.86, 52.225.191.187</span></span> |
| <span data-ttu-id="ad731-149">인도 중부</span><span class="sxs-lookup"><span data-stu-id="ad731-149">Central India</span></span> |<span data-ttu-id="ad731-150">104.211.98.219, 104.211.103.71</span><span class="sxs-lookup"><span data-stu-id="ad731-150">104.211.98.219, 104.211.103.71</span></span> |
| <span data-ttu-id="ad731-151">인도 남부</span><span class="sxs-lookup"><span data-stu-id="ad731-151">South India</span></span> |<span data-ttu-id="ad731-152">104.211.227.102, 104.211.225.157</span><span class="sxs-lookup"><span data-stu-id="ad731-152">104.211.227.102, 104.211.225.157</span></span> |
| <span data-ttu-id="ad731-153">인도 서부</span><span class="sxs-lookup"><span data-stu-id="ad731-153">West India</span></span> |<span data-ttu-id="ad731-154">104.211.161.152, 104.211.162.21</span><span class="sxs-lookup"><span data-stu-id="ad731-154">104.211.161.152, 104.211.162.21</span></span> |
| <span data-ttu-id="ad731-155">일본 동부</span><span class="sxs-lookup"><span data-stu-id="ad731-155">Japan East</span></span> |<span data-ttu-id="ad731-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span><span class="sxs-lookup"><span data-stu-id="ad731-156">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span></span> |
| <span data-ttu-id="ad731-157">일본 서부</span><span class="sxs-lookup"><span data-stu-id="ad731-157">Japan West</span></span> |<span data-ttu-id="ad731-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span><span class="sxs-lookup"><span data-stu-id="ad731-158">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span></span> |
| <span data-ttu-id="ad731-159">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="ad731-159">North Central US</span></span> |<span data-ttu-id="ad731-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span><span class="sxs-lookup"><span data-stu-id="ad731-160">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span></span> |
| <span data-ttu-id="ad731-161">북유럽</span><span class="sxs-lookup"><span data-stu-id="ad731-161">North Europe</span></span> |<span data-ttu-id="ad731-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span><span class="sxs-lookup"><span data-stu-id="ad731-162">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span></span> |
| <span data-ttu-id="ad731-163">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="ad731-163">South Central US</span></span> |<span data-ttu-id="ad731-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span><span class="sxs-lookup"><span data-stu-id="ad731-164">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span></span> |
| <span data-ttu-id="ad731-165">동남아시아</span><span class="sxs-lookup"><span data-stu-id="ad731-165">Southeast Asia</span></span> |<span data-ttu-id="ad731-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span><span class="sxs-lookup"><span data-stu-id="ad731-166">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span></span> |
| <span data-ttu-id="ad731-167">서유럽</span><span class="sxs-lookup"><span data-stu-id="ad731-167">West Europe</span></span> |<span data-ttu-id="ad731-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span><span class="sxs-lookup"><span data-stu-id="ad731-168">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span></span> |
| <span data-ttu-id="ad731-169">미국 서부</span><span class="sxs-lookup"><span data-stu-id="ad731-169">West US</span></span> |<span data-ttu-id="ad731-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span><span class="sxs-lookup"><span data-stu-id="ad731-170">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span></span> |
| <span data-ttu-id="ad731-171">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="ad731-171">West US 2</span></span> |<span data-ttu-id="ad731-172">13.66.224.156, 13.66.227.8</span><span class="sxs-lookup"><span data-stu-id="ad731-172">13.66.224.156, 13.66.227.8</span></span> |
| <span data-ttu-id="ad731-173">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="ad731-173">West Central US</span></span> |<span data-ttu-id="ad731-174">52.161.29.186, 52.161.27.213</span><span class="sxs-lookup"><span data-stu-id="ad731-174">52.161.29.186, 52.161.27.213</span></span> |
| <span data-ttu-id="ad731-175">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="ad731-175">Canada Central</span></span> |<span data-ttu-id="ad731-176">13.88.248.106, 13.88.248.110</span><span class="sxs-lookup"><span data-stu-id="ad731-176">13.88.248.106, 13.88.248.110</span></span> |
| <span data-ttu-id="ad731-177">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="ad731-177">Canada East</span></span> |<span data-ttu-id="ad731-178">40.86.227.82, 40.86.225.194</span><span class="sxs-lookup"><span data-stu-id="ad731-178">40.86.227.82, 40.86.225.194</span></span> |
| <span data-ttu-id="ad731-179">영국 북부</span><span class="sxs-lookup"><span data-stu-id="ad731-179">UK North</span></span> |<span data-ttu-id="ad731-180">13.87.101.18, 13.87.100.232</span><span class="sxs-lookup"><span data-stu-id="ad731-180">13.87.101.18, 13.87.100.232</span></span> |
| <span data-ttu-id="ad731-181">영국 남부 2</span><span class="sxs-lookup"><span data-stu-id="ad731-181">UK South 2</span></span> |<span data-ttu-id="ad731-182">13.87.32.202, 13.87.32.226</span><span class="sxs-lookup"><span data-stu-id="ad731-182">13.87.32.202, 13.87.32.226</span></span> |
