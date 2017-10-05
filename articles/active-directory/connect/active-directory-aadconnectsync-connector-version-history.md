---
title: "커넥터 버전 릴리스 내역 | Microsoft Docs"
description: "이 항목에서는 FIM(Forefront Identity Manager) 및 MIM(Microsoft Identity Manager)에 대한 커넥터의 모든 버전을 보여 줍니다."
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="64672-103">커넥터 버전 릴리스 내역</span><span class="sxs-lookup"><span data-stu-id="64672-103">Connector Version Release History</span></span>
<span data-ttu-id="64672-104">FIM(Forefront Identity Manager) 및 MIM(Microsoft Identity Manager)의 커넥터는 자주 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="64672-105">이 항목은 FIM 및 MIM에만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="64672-106">이러한 커넥터는 Azure AD Connect에서 설치하도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="64672-107">출시된 커넥터는 지정된 빌드로 업그레이드할 때 AADConnect에 미리 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="64672-108">이 항목은 출시된 커넥터의 모든 버전을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="64672-109">관련 링크:</span><span class="sxs-lookup"><span data-stu-id="64672-109">Related links:</span></span>

* [<span data-ttu-id="64672-110">최신 커넥터 다운로드</span><span class="sxs-lookup"><span data-stu-id="64672-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="64672-111">[일반 LDAP 커넥터](active-directory-aadconnectsync-connector-genericldap.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="64672-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="64672-112">[일반 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="64672-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="64672-113">[웹 서비스 커넥터](http://go.microsoft.com/fwlink/?LinkID=226245) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="64672-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="64672-114">[PowerShell 커넥터](active-directory-aadconnectsync-connector-powershell.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="64672-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="64672-115">[Lotus Domino 커넥터](active-directory-aadconnectsync-connector-domino.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="64672-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="64672-116">1.1.604.0(AADConnect 보류 중 릴리스)</span><span class="sxs-lookup"><span data-stu-id="64672-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="64672-117">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="64672-117">Fixed issues:</span></span>

* <span data-ttu-id="64672-118">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="64672-118">Generic Web Services:</span></span>
  * <span data-ttu-id="64672-119">두 개 이상의 끝점이 있을 때 SOAP 프로젝트가 만들어지지 않도록 방지하는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="64672-120">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="64672-120">Generic SQL:</span></span>
  * <span data-ttu-id="64672-121">가져오기 작업에서 커넥터 공간에 저장할 때 GSQL이 시간을 제대로 변환하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="64672-122">GSQL의 커넥터 공간에 대한 기본 날짜 및 시간 형식이 'yyyy-MM-dd hh:mm:ssZ'에서 'yyyy-MM-dd HH:mm:ssZ'로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="64672-123">1.1.551.0(AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="64672-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="64672-124">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="64672-124">Fixed issues:</span></span>

* <span data-ttu-id="64672-125">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="64672-125">Generic Web Services:</span></span>
  * <span data-ttu-id="64672-126">Wsconfig 도구는 REST 서비스 메서드에 대한 "샘플 요청"의 Json 배열을 제대로 변환하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="64672-127">이로 인해 REST 요청에 대한 이 Json 배열의 직렬화와 관련된 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="64672-128">웹 서비스 커넥터 구성 도구는 JSON 속성 이름에 공백 기호를 사용하는 것을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="64672-129">WSConfigTool.exe.config 파일에 대체 패턴을 수동으로 추가할 수 있습니다(예: ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```).</span><span class="sxs-lookup"><span data-stu-id="64672-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="64672-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="64672-130">Lotus Notes:</span></span>
  * <span data-ttu-id="64672-131">**조직/조직 구성 단위에 대해 사용자 지정 인증자 허용** 옵션이 해제된 경우 내보내기(업데이트) 중 커넥터가 실패합니다. 내보내기 흐름 후에 모든 특성이 Domino로 내보내지지만, 내보내기 시 KeyNotFoundException이 동기화에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="64672-132">이 문제는 아래 특성 중 하나를 변경하여 DN(UserName 특성) 변경을 시도할 때 이름 바꾸기 작업이 실패하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="64672-133">LastName</span><span class="sxs-lookup"><span data-stu-id="64672-133">LastName</span></span>
      - <span data-ttu-id="64672-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="64672-134">FirstName</span></span>
      - <span data-ttu-id="64672-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="64672-135">MiddleInitial</span></span>
      - <span data-ttu-id="64672-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="64672-136">AltFullName</span></span>
      - <span data-ttu-id="64672-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="64672-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="64672-138">ou</span><span class="sxs-lookup"><span data-stu-id="64672-138">ou</span></span>
      - <span data-ttu-id="64672-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="64672-139">altcommonname</span></span>

  * <span data-ttu-id="64672-140">**조직/조직 구성 단위에 대한 사용자 지정 인증자 허용** 옵션이 설정되었지만 필수 인증자가 여전히 비어 있으면 KeyNotFoundException이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="64672-141">향상된 기능:</span><span class="sxs-lookup"><span data-stu-id="64672-141">Enhancements:</span></span>

* <span data-ttu-id="64672-142">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="64672-142">Generic SQL:</span></span>
  * <span data-ttu-id="64672-143">**시나리오: 다시 설계되고 구현됨:** "*" 기능</span><span class="sxs-lookup"><span data-stu-id="64672-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="64672-144">**솔루션 설명:** [다중 값 참조 특성 처리](active-directory-aadconnectsync-connector-genericsql.md) 접근 방식이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="64672-145">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="64672-145">Fixed issues:</span></span>

* <span data-ttu-id="64672-146">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="64672-146">Generic Web Services:</span></span>
  * <span data-ttu-id="64672-147">웹 서비스 커넥터가 있는 데도 서버 구성을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="64672-148">웹 서비스 커넥터는 여러 웹 서비스에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="64672-149">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="64672-149">Generic SQL:</span></span>
  * <span data-ttu-id="64672-150">단일 값 참조 특성에 대해 나열되는 개체 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="64672-151">변경 추적 전략에 대한 델타 가져오기는 다중 값 테이블에서 값이 제거될 때 개체를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="64672-152">AS/400의 DB2에서 GSQL 커넥터의 OverflowException</span><span class="sxs-lookup"><span data-stu-id="64672-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="64672-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="64672-153">Lotus:</span></span>
  * <span data-ttu-id="64672-154">GlobalParameters 페이지를 열기 전에 OU 검색을 설정/해제하는 옵션이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="64672-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="64672-155">1.1.443.0</span></span>

<span data-ttu-id="64672-156">출시 날짜: 2017년 3월</span><span class="sxs-lookup"><span data-stu-id="64672-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="64672-157">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="64672-157">Enhancements</span></span>

* <span data-ttu-id="64672-158">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="64672-158">Generic SQL:</span></span></br><span data-ttu-id="64672-159">
  **시나리오 증상:** 하나의 개체 형식에 대한 참조만 허용하고 멤버와 상호 참조하는 SQL 커넥터의 잘 알려진 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="64672-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="64672-160">
**솔루션 설명:** "*" 옵션을 선택한 참조를 위한 처리 단계에서 모든 개체 형식 조합은 동기화 엔진으로 다시 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="64672-161">그러면 자리 표시자가 많이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-161">This will create many placeholders</span></span>
- <span data-ttu-id="64672-162">이름이 고유한 상호 개체 형식인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="64672-163">일반 LDAP:</span><span class="sxs-lookup"><span data-stu-id="64672-163">Generic LDAP:</span></span></br><span data-ttu-id="64672-164">
 **시나리오:** 몇 가지 컨테이너만 특정 파티션에서 선택된 경우 검색은 여전히 전체 파티션에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="64672-165">특정 파티션은 성능 저하로 이어질 수 있는 MA가 아닌 Synchronization Service에서 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="64672-166">**해결 방법 설명:** 모든 컨테이너에 걸쳐 수행하고 전체 파티션에서 검색하는 대신 각 파티션에서 개체를 검색하기 위해 변경된 GLDAP 커넥터의 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="64672-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="64672-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="64672-167">Lotus Domino:</span></span>

  <span data-ttu-id="64672-168">**시나리오:** 내보내기를 수행하는 동안 사용자 제거를 위한 Domino 메일 삭제 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="64672-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="64672-169">
  **해결 방법:** 내보내기를 수행하는 동안 사용자 제거를 위한 구성 가능한 메일 삭제 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="64672-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="64672-170">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="64672-170">Fixed issues:</span></span>
* <span data-ttu-id="64672-171">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="64672-171">Generic Web Services:</span></span>
 * <span data-ttu-id="64672-172">WebService 구성 도구를 통해 기본 SAP wsconfig 프로젝트에서 서비스 URL을 변경한 후 다음과 같은 오류가 발생한 경우: 경로의 일부를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="64672-173">일반 LDAP:</span><span class="sxs-lookup"><span data-stu-id="64672-173">Generic LDAP:</span></span>
 * <span data-ttu-id="64672-174">GLDAP 커넥터에서 AD LDS의 모든 특성을 확인할 수 없음</span><span class="sxs-lookup"><span data-stu-id="64672-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="64672-175">LDAP 디렉터리 스키마에서 UPN 특성이 감지되지 않는 경우 마법사 중단</span><span class="sxs-lookup"><span data-stu-id="64672-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="64672-176">"objectclass" 특성이 선택되지 않은 경우 전체 가져오기를 수행하는 동안 검색 오류가 발생하지 않으면 델타 가져오기 실패</span><span class="sxs-lookup"><span data-stu-id="64672-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="64672-177">"파티션 및 계층 구조 구성" 구성 페이지에 일반</span><span class="sxs-lookup"><span data-stu-id="64672-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="64672-178">LDAP MA의 Novel 서버에 대한 파티션과 형식이 비슷한 개체가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-178">LDAP MA.</span></span> <span data-ttu-id="64672-179">RootDSE 파티션의 개체만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="64672-180">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="64672-180">Generic SQL:</span></span>
 * <span data-ttu-id="64672-181">일반 SQL 워터마크 델타 가져오기 다중값 특성이 버그를 가져오지 않는 문제 해결</span><span class="sxs-lookup"><span data-stu-id="64672-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="64672-182">다중값 특성의 삭제/추가된 값을 내보낼 때 데이터 원본에서 삭제/추가되지 않음.</span><span class="sxs-lookup"><span data-stu-id="64672-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="64672-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="64672-183">Lotus Notes:</span></span>
 * <span data-ttu-id="64672-184">특성에 대한 값이 Null이거나 비어있다는 알림을 내보낼 때 특정 필드 "전체 이름"이 메타버스에 올바르게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="64672-185">중복 인증자 오류 해결</span><span class="sxs-lookup"><span data-stu-id="64672-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="64672-186">데이터가 없는 개체가 다른 개체를 통해 Lotus Domino 커넥터에서 선택된 경우 전체 가져오기를 수행하는 동안 검색 오류를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="64672-187">델타 가져오기가 Lotus Domino 커넥터에서 실행 중인 경우 실행 마지막에 Microsoft.IdentityManagement.MA.LotusDomino.Service.exe 서비스가 때때로 응용 프로그램 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="64672-188">멤버 자격에서 사용자를 제거하려고 시도하기 위해 내보내기를 실행할 때 성공적으로 업데이트되었음이 표시되지만 실제로 사용자가 Lotus Notes의 멤버 자격에서 삭제되지는 않는 경우를 제외하면 전체 그룹 멤버는 정상적으로 작동하며 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="64672-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="64672-189">다중값 특성을 내보내는 동안 새 항목을 아래에 추가할 수 있도록 "아래에 항목 추가"로 내보내기 모드를 선택할 수 있는 기능이 Lotus MA의 GUI 구성에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="64672-190">커넥터는 메일 폴더 및 ID 자격 증명 모음에서 파일을 삭제하는 데 필요한 논리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="64672-191">멤버 자격 삭제는 NAB 멤버 간에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="64672-192">값은 다중값 특성에서 성공적으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="64672-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="64672-193">1.1.117.0</span></span>
<span data-ttu-id="64672-194">출시 날짜: 2016년 3월</span><span class="sxs-lookup"><span data-stu-id="64672-194">Released: 2016 March</span></span>

<span data-ttu-id="64672-195">**일반 SQL 커넥터**</span><span class="sxs-lookup"><span data-stu-id="64672-195">**New Connector**</span></span>  
<span data-ttu-id="64672-196">의 [일반 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql.md)초기 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="64672-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="64672-197">**새로운 기능:**</span><span class="sxs-lookup"><span data-stu-id="64672-197">**New features:**</span></span>

* <span data-ttu-id="64672-198">일반 LDAP 커넥터:</span><span class="sxs-lookup"><span data-stu-id="64672-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="64672-199">Isode에서 델타 가져오기에 대한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="64672-200">웹 서비스 커넥터:</span><span class="sxs-lookup"><span data-stu-id="64672-200">Web Services Connector:</span></span>
  * <span data-ttu-id="64672-201">개체 수준 오류가 동기화 엔진으로 다시 반환될 수 있도록 csEntryChangeResult 작업 및 setImportErrorCode 작업을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="64672-202">새 개체 수준 오류 기능을 사용하도록 SAP6 및 SAP6User 템플릿을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="64672-203">Lotus Domino 커넥터:</span><span class="sxs-lookup"><span data-stu-id="64672-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="64672-204">내보내는 경우 주소록당 하나의 인증자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="64672-205">이제 관리를 쉽게 수행할 수 있도록 모든 인증자에 대해 동일한 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="64672-206">**수정된 문제:**</span><span class="sxs-lookup"><span data-stu-id="64672-206">**Fixed issues:**</span></span>

* <span data-ttu-id="64672-207">일반 LDAP 커넥터:</span><span class="sxs-lookup"><span data-stu-id="64672-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="64672-208">IBM Tivoli DS의 경우 일부 참조 특성이 제대로 검색되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="64672-209">델타 가져오기 동안 열린 LDAP의 경우 문자열의 시작과 끝에 있는 공백이 잘렸습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="64672-210">Novell과 NetIQ의 경우 OU/컨테이너 사이의 개체를 이동하고 동시에 개체의 이름도 바꾼 내보내기가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="64672-211">웹 서비스 커넥터:</span><span class="sxs-lookup"><span data-stu-id="64672-211">Web Services Connector:</span></span>
  * <span data-ttu-id="64672-212">웹 서비스에 동일한 바인딩에 대한 여러 개의 끝점이 있으면 커넥터에서 이러한 끝점을 올바르게 검색하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="64672-213">Lotus Domino 커넥터:</span><span class="sxs-lookup"><span data-stu-id="64672-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="64672-214">fullName 특성을 메일 내 데이터베이스에 내보내지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="64672-215">그룹에서 멤버를 추가하고 제거한 내보내기에서 추가된 멤버만 내보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="64672-216">Notes Document가 잘못된 경우(isValid 특성이 false로 설정) 커넥터가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="64672-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="64672-217">이전 릴리스</span><span class="sxs-lookup"><span data-stu-id="64672-217">Older releases</span></span>
<span data-ttu-id="64672-218">2016년 3월 이전에 커넥터가 지원 항목으로 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64672-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="64672-219">**일반 LDAP**</span><span class="sxs-lookup"><span data-stu-id="64672-219">**Generic LDAP**</span></span>

* <span data-ttu-id="64672-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015년 9월</span><span class="sxs-lookup"><span data-stu-id="64672-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="64672-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015년 3월</span><span class="sxs-lookup"><span data-stu-id="64672-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="64672-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015년 1월</span><span class="sxs-lookup"><span data-stu-id="64672-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="64672-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014년 9월</span><span class="sxs-lookup"><span data-stu-id="64672-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="64672-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014년 3월</span><span class="sxs-lookup"><span data-stu-id="64672-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="64672-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="64672-225">**WebServices**</span></span>

* <span data-ttu-id="64672-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014년 9월</span><span class="sxs-lookup"><span data-stu-id="64672-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="64672-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="64672-227">**PowerShell**</span></span>

* <span data-ttu-id="64672-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014년 9월</span><span class="sxs-lookup"><span data-stu-id="64672-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="64672-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="64672-229">**Lotus Domino**</span></span>

* <span data-ttu-id="64672-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015년 9월</span><span class="sxs-lookup"><span data-stu-id="64672-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="64672-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015년 3월</span><span class="sxs-lookup"><span data-stu-id="64672-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="64672-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014년 8월</span><span class="sxs-lookup"><span data-stu-id="64672-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="64672-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014년 2월</span><span class="sxs-lookup"><span data-stu-id="64672-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="64672-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013년 10월</span><span class="sxs-lookup"><span data-stu-id="64672-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="64672-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013년 8월</span><span class="sxs-lookup"><span data-stu-id="64672-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="64672-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64672-236">Next steps</span></span>
<span data-ttu-id="64672-237">[Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="64672-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="64672-238">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="64672-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
