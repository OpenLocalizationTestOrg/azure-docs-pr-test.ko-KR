---
title: "aaaConnector 버전 릴리스 기록 | Microsoft Docs"
description: "이 항목에서는 Forefront Identity Manager (FIM) 및 MIM Microsoft Identity Manager ()에 대 한 모든 버전의 hello 커넥터를 보여 줍니다."
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
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="a39fd-103">커넥터 버전 릴리스 내역</span><span class="sxs-lookup"><span data-stu-id="a39fd-103">Connector Version Release History</span></span>
<span data-ttu-id="a39fd-104">Forefront Identity Manager (FIM) 및 MIM Microsoft Identity Manager ()에 대 한 hello 커넥터 지속적으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="a39fd-105">이 항목은 FIM 및 MIM에만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="a39fd-106">이러한 커넥터는 Azure AD Connect에서 설치하도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="a39fd-107">출시 된 커넥터 toospecified 빌드를 업그레이드 하는 경우 AADConnect에 미리 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="a39fd-108">이 항목의 hello 출시 된 커넥터의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="a39fd-109">관련 링크:</span><span class="sxs-lookup"><span data-stu-id="a39fd-109">Related links:</span></span>

* [<span data-ttu-id="a39fd-110">최신 커넥터 다운로드</span><span class="sxs-lookup"><span data-stu-id="a39fd-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="a39fd-111">[일반 LDAP 커넥터](active-directory-aadconnectsync-connector-genericldap.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a39fd-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="a39fd-112">[일반 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a39fd-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="a39fd-113">[웹 서비스 커넥터](http://go.microsoft.com/fwlink/?LinkID=226245) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a39fd-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="a39fd-114">[PowerShell 커넥터](active-directory-aadconnectsync-connector-powershell.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a39fd-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="a39fd-115">[Lotus Domino 커넥터](active-directory-aadconnectsync-connector-domino.md) 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a39fd-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="a39fd-116">1.1.604.0(AADConnect 보류 중 릴리스)</span><span class="sxs-lookup"><span data-stu-id="a39fd-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="a39fd-117">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="a39fd-117">Fixed issues:</span></span>

* <span data-ttu-id="a39fd-118">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="a39fd-118">Generic Web Services:</span></span>
  * <span data-ttu-id="a39fd-119">두 개 이상의 끝점이 있을 때 SOAP 프로젝트가 만들어지지 않도록 방지하는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="a39fd-120">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="a39fd-120">Generic SQL:</span></span>
  * <span data-ttu-id="a39fd-121">Hello 가져오기 작업에서 hello GSQL가 변환 되지 않으면 시간 올바르게 저장 될 때 tooconnector 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="a39fd-122">hello hello GSQL의 커넥터 공간에 대 한 기본 날짜 및 시간 형식에서에서 변경 되었습니다. 'yyyy-월-일 hh:mm:ssZ' too'yyyy-월-일 HH:mm:ssZ'.</span><span class="sxs-lookup"><span data-stu-id="a39fd-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="a39fd-123">1.1.551.0(AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="a39fd-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="a39fd-124">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="a39fd-124">Fixed issues:</span></span>

* <span data-ttu-id="a39fd-125">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="a39fd-125">Generic Web Services:</span></span>
  * <span data-ttu-id="a39fd-126">hello Wsconfig 도구 않았습니다 hello REST 서비스 메서드에 대 한 "예제 요청"에서 Json 배열 hello를 올바르게 변환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="a39fd-127">이 문제가 발생 하 serialization hello REST 요청에 대 한이 Json 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="a39fd-128">웹 서비스 커넥터 구성 도구는 JSON 속성 이름에 공백 기호를 사용하는 것을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="a39fd-129">대체 패턴을 수동으로 추가할 수 있습니다 toohello WSConfigTool.exe.config 파일 예:```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="a39fd-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="a39fd-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="a39fd-130">Lotus Notes:</span></span>
  * <span data-ttu-id="a39fd-131">경우 옵션을 hello **조직/조직 구성 단위에 대 한 사용자 지정 certifiers 허용** hello 커넥터 없음 내보내는 hello 내보내기는 모든 특성 흐름이 후 (업데이트) 중 내보낸된 tooDomino 권한은 있지만 hello 시점에 사용할 수 없습니다 내보내기는 KeyNotFoundException tooSync 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="a39fd-132">이 다음 hello 특성 중 하나를 변경 하 여 hello toochange DN (사용자 이름 특성)를 읽으려고 할 때 작업이 실패 하면 이름 바꾸기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="a39fd-133">LastName</span><span class="sxs-lookup"><span data-stu-id="a39fd-133">LastName</span></span>
      - <span data-ttu-id="a39fd-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="a39fd-134">FirstName</span></span>
      - <span data-ttu-id="a39fd-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="a39fd-135">MiddleInitial</span></span>
      - <span data-ttu-id="a39fd-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="a39fd-136">AltFullName</span></span>
      - <span data-ttu-id="a39fd-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="a39fd-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="a39fd-138">ou</span><span class="sxs-lookup"><span data-stu-id="a39fd-138">ou</span></span>
      - <span data-ttu-id="a39fd-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="a39fd-139">altcommonname</span></span>

  * <span data-ttu-id="a39fd-140">**조직/조직 구성 단위에 대한 사용자 지정 인증자 허용** 옵션이 설정되었지만 필수 인증자가 여전히 비어 있으면 KeyNotFoundException이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="a39fd-141">향상된 기능:</span><span class="sxs-lookup"><span data-stu-id="a39fd-141">Enhancements:</span></span>

* <span data-ttu-id="a39fd-142">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="a39fd-142">Generic SQL:</span></span>
  * <span data-ttu-id="a39fd-143">**시나리오: 다시 설계되고 구현됨:** "*" 기능</span><span class="sxs-lookup"><span data-stu-id="a39fd-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="a39fd-144">**솔루션 설명:** [다중 값 참조 특성 처리](active-directory-aadconnectsync-connector-genericsql.md) 접근 방식이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="a39fd-145">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="a39fd-145">Fixed issues:</span></span>

* <span data-ttu-id="a39fd-146">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="a39fd-146">Generic Web Services:</span></span>
  * <span data-ttu-id="a39fd-147">웹 서비스 커넥터가 있는 데도 서버 구성을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="a39fd-148">웹 서비스 커넥터는 여러 웹 서비스에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="a39fd-149">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="a39fd-149">Generic SQL:</span></span>
  * <span data-ttu-id="a39fd-150">단일 값 참조 특성에 대해 나열되는 개체 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="a39fd-151">변경 추적 전략에 대한 델타 가져오기는 다중 값 테이블에서 값이 제거될 때 개체를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="a39fd-152">AS/400의 DB2에서 GSQL 커넥터의 OverflowException</span><span class="sxs-lookup"><span data-stu-id="a39fd-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="a39fd-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="a39fd-153">Lotus:</span></span>
  * <span data-ttu-id="a39fd-154">추가 옵션 tooenable\disable Ou GlobalParameters 페이지 열기 전에 검색</span><span class="sxs-lookup"><span data-stu-id="a39fd-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="a39fd-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="a39fd-155">1.1.443.0</span></span>

<span data-ttu-id="a39fd-156">출시 날짜: 2017년 3월</span><span class="sxs-lookup"><span data-stu-id="a39fd-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="a39fd-157">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="a39fd-157">Enhancements</span></span>

* <span data-ttu-id="a39fd-158">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="a39fd-158">Generic SQL:</span></span></br><span data-ttu-id="a39fd-159">
  **시나리오 증상:** 는 잘 알려진 제한 사항으로 hello SQL 커넥터 여기서 म만 참조 tooone 개체 유형을 허용 하 고 멤버와 교차 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="a39fd-160">
**솔루션 설명:** 된 참조에 대 한 hello 처리 단계에서 "*" 옵션이 선택 된 경우 백 toohello 동기화 엔진 개체 유형의 모든 조합을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="a39fd-161">그러면 자리 표시자가 많이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-161">This will create many placeholders</span></span>
- <span data-ttu-id="a39fd-162">것이 필수 toomake hello 명명 고유한 지 개체 유형을 교차 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="a39fd-163">일반 LDAP:</span><span class="sxs-lookup"><span data-stu-id="a39fd-163">Generic LDAP:</span></span></br><span data-ttu-id="a39fd-164">
 **시나리오:** 몇 컨테이너만 특정 파티션에 선택 되 면 다음 hello 검색 여전히에서 수행 됩니다 전체 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="a39fd-165">특정 파티션은 성능 저하로 이어질 수 있는 MA가 아닌 Synchronization Service에서 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="a39fd-166">**솔루션 설명:** 변경 GLDAP 커넥터의 코드 toomake 수 모든 컨테이너를 모두 이동해 고 hello 전체 파티션에서 검색 하는 대신 각 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="a39fd-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="a39fd-167">Lotus Domino:</span></span>

  <span data-ttu-id="a39fd-168">**시나리오:** 내보내기를 수행하는 동안 사용자 제거를 위한 Domino 메일 삭제 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="a39fd-169">
  **해결 방법:** 내보내기를 수행하는 동안 사용자 제거를 위한 구성 가능한 메일 삭제 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="a39fd-170">수정된 문제:</span><span class="sxs-lookup"><span data-stu-id="a39fd-170">Fixed issues:</span></span>
* <span data-ttu-id="a39fd-171">일반 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="a39fd-171">Generic Web Services:</span></span>
 * <span data-ttu-id="a39fd-172">Hello 다음 오류가 발생 한 후 웹 서비스 구성 도구를 통해 SAP wsconfig 프로젝트 기본 hello 서비스 URL을 변경 하는 경우: hello 경로의 일부를 찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="a39fd-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="a39fd-173">일반 LDAP:</span><span class="sxs-lookup"><span data-stu-id="a39fd-173">Generic LDAP:</span></span>
 * <span data-ttu-id="a39fd-174">GLDAP 커넥터에서 AD LDS의 모든 특성을 확인할 수 없음</span><span class="sxs-lookup"><span data-stu-id="a39fd-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="a39fd-175">마법사 나누기 hello LDAP 디렉터리 스키마에서 검색 되는 UPN 특성이 없는 경우</span><span class="sxs-lookup"><span data-stu-id="a39fd-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="a39fd-176">"objectclass" 특성이 선택되지 않은 경우 전체 가져오기를 수행하는 동안 검색 오류가 발생하지 않으면 델타 가져오기 실패</span><span class="sxs-lookup"><span data-stu-id="a39fd-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="a39fd-177">"파티션 및 계층 구성" 구성 페이지에서 모든 개체는 같은 toohello 파티션 Novel 서버 hello 제네릭에에서 대 한 유형을 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="a39fd-178">LDAP MA의 Novel 서버에 대한 파티션과 형식이 비슷한 개체가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-178">LDAP MA.</span></span> <span data-ttu-id="a39fd-179">RootDSE 파티션의 개체만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="a39fd-180">일반 SQL:</span><span class="sxs-lookup"><span data-stu-id="a39fd-180">Generic SQL:</span></span>
 * <span data-ttu-id="a39fd-181">일반 SQL 워터마크 델타 가져오기 다중값 특성이 버그를 가져오지 않는 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a39fd-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="a39fd-182">다중값 특성의 삭제/추가된 값을 내보낼 때 데이터 원본에서 삭제/추가되지 않음.</span><span class="sxs-lookup"><span data-stu-id="a39fd-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="a39fd-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="a39fd-183">Lotus Notes:</span></span>
 * <span data-ttu-id="a39fd-184">그러나 특정 필드 "전체" 상응 이름은 hello 메타 버스 올바르게 때 내보내기 tooNotes hello에 대 한 값 hello 특성은 Null 이거나 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="a39fd-185">중복 인증자 오류 해결</span><span class="sxs-lookup"><span data-stu-id="a39fd-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="a39fd-186">다른 개체와 hello Lotus Domino 커넥터에서 데이터 없이도 hello 개체를 선택한 경우 다음 म 오류가 hello 검색 전체 가져오기를 수행 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="a39fd-187">델타 가져오기는 되 고 서비스를 실행 hello Lotus Domino 커넥터에서 해당 실행된을 hello hello 끝나기 전에 Microsoft.IdentityManagement.MA.LotusDomino.Service.exe 경우에 따라 응용 프로그램 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="a39fd-188">전체 그룹 멤버 자격에서 제대로 작동 하 고 hello 내보내기 tootry tooremove 사용자를 실행 하는 경우 멤버 자격에서 업데이트를 성공으로 표시 되지만 hello 사용자 Lotus Notes의 멤버 자격에서 실제로 제거 하지 않는 점을 제외 하 고 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="a39fd-189">"추가 항목 맨 아래에"으로 내보내기의 기회 toochoose 모드는에서 추가 되었습니다 구성 Lotus GUI MA tooappend 새 항목 맨 아래에 다중 값된 특성에 대 한 hello 내보내기 중.</span><span class="sxs-lookup"><span data-stu-id="a39fd-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="a39fd-190">커넥터는 hello 필요한 hello 메일 폴더에서에서 논리 toodelete hello 파일 및 ID 자격 증명 모음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="a39fd-191">멤버 자격 삭제는 NAB 멤버 간에 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="a39fd-192">값은 다중값 특성에서 성공적으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="a39fd-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="a39fd-193">1.1.117.0</span></span>
<span data-ttu-id="a39fd-194">출시 날짜: 2016년 3월</span><span class="sxs-lookup"><span data-stu-id="a39fd-194">Released: 2016 March</span></span>

<span data-ttu-id="a39fd-195">**일반 SQL 커넥터**</span><span class="sxs-lookup"><span data-stu-id="a39fd-195">**New Connector**</span></span>  
<span data-ttu-id="a39fd-196">초기 버전의 hello [제네릭 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="a39fd-197">**새로운 기능:**</span><span class="sxs-lookup"><span data-stu-id="a39fd-197">**New features:**</span></span>

* <span data-ttu-id="a39fd-198">일반 LDAP 커넥터:</span><span class="sxs-lookup"><span data-stu-id="a39fd-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="a39fd-199">Isode에서 델타 가져오기에 대한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="a39fd-200">웹 서비스 커넥터:</span><span class="sxs-lookup"><span data-stu-id="a39fd-200">Web Services Connector:</span></span>
  * <span data-ttu-id="a39fd-201">업데이트 된 hello csEntryChangeResult 활동과 setImportErrorCode 활동 tooallow 개체 수준 오류 toobe 반환 된 뒤로 toohello 동기화 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="a39fd-202">업데이트 된 hello SAP6 및 SAP6User 템플릿 toouse hello 새 개체 수준의 오류 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="a39fd-203">Lotus Domino 커넥터:</span><span class="sxs-lookup"><span data-stu-id="a39fd-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="a39fd-204">내보내는 경우 주소록당 하나의 인증자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="a39fd-205">사용 하 여 hello 동일 이제 수 모든 certifiers hello 관리 toomake 템플릿 쉽게에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="a39fd-206">**수정된 문제:**</span><span class="sxs-lookup"><span data-stu-id="a39fd-206">**Fixed issues:**</span></span>

* <span data-ttu-id="a39fd-207">일반 LDAP 커넥터:</span><span class="sxs-lookup"><span data-stu-id="a39fd-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="a39fd-208">IBM Tivoli DS의 경우 일부 참조 특성이 제대로 검색되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="a39fd-209">델타 가져오기 중 Open LDAP에 대 한 문자열의 hello 시작 및 끝에 있는 공백은 잘리지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="a39fd-210">Novell 및 NetIQ에 대 한 hello 및 Ou/컨테이너 간에 개체를 이동 하는 내보내기 시간이 이름이 바뀐된 hello 개체 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="a39fd-211">웹 서비스 커넥터:</span><span class="sxs-lookup"><span data-stu-id="a39fd-211">Web Services Connector:</span></span>
  * <span data-ttu-id="a39fd-212">Hello 웹 서비스에 여러 개의 끝점이 모두 동일한 바인딩에 대 한이 있으면 다음 hello 커넥터 않았습니다 올바르게 검색 하지 이러한 끝점.</span><span class="sxs-lookup"><span data-stu-id="a39fd-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="a39fd-213">Lotus Domino 커넥터:</span><span class="sxs-lookup"><span data-stu-id="a39fd-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="a39fd-214">데이터베이스 메일에서 hello fullName 특성 tooa의 내보내기를 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="a39fd-215">그룹에서 추가 및 제거 멤버만 hello를 내보낼 내보내기 구성원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="a39fd-216">정보 문서에 유효 하지 않을 경우 (특성 isValid hello toofalse 설정), 다음 커넥터 없음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="a39fd-217">이전 릴리스</span><span class="sxs-lookup"><span data-stu-id="a39fd-217">Older releases</span></span>
<span data-ttu-id="a39fd-218">2016 년 3 월 하기 전에 hello 커넥터 지원 항목으로 릴리스 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="a39fd-219">**일반 LDAP**</span><span class="sxs-lookup"><span data-stu-id="a39fd-219">**Generic LDAP**</span></span>

* <span data-ttu-id="a39fd-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015년 9월</span><span class="sxs-lookup"><span data-stu-id="a39fd-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="a39fd-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015년 3월</span><span class="sxs-lookup"><span data-stu-id="a39fd-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="a39fd-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015년 1월</span><span class="sxs-lookup"><span data-stu-id="a39fd-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="a39fd-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014년 9월</span><span class="sxs-lookup"><span data-stu-id="a39fd-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="a39fd-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014년 3월</span><span class="sxs-lookup"><span data-stu-id="a39fd-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="a39fd-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="a39fd-225">**WebServices**</span></span>

* <span data-ttu-id="a39fd-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014년 9월</span><span class="sxs-lookup"><span data-stu-id="a39fd-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="a39fd-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a39fd-227">**PowerShell**</span></span>

* <span data-ttu-id="a39fd-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014년 9월</span><span class="sxs-lookup"><span data-stu-id="a39fd-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="a39fd-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="a39fd-229">**Lotus Domino**</span></span>

* <span data-ttu-id="a39fd-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015년 9월</span><span class="sxs-lookup"><span data-stu-id="a39fd-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="a39fd-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015년 3월</span><span class="sxs-lookup"><span data-stu-id="a39fd-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="a39fd-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014년 8월</span><span class="sxs-lookup"><span data-stu-id="a39fd-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="a39fd-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014년 2월</span><span class="sxs-lookup"><span data-stu-id="a39fd-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="a39fd-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013년 10월</span><span class="sxs-lookup"><span data-stu-id="a39fd-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="a39fd-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013년 8월</span><span class="sxs-lookup"><span data-stu-id="a39fd-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="a39fd-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a39fd-236">Next steps</span></span>
<span data-ttu-id="a39fd-237">Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="a39fd-238">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a39fd-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
