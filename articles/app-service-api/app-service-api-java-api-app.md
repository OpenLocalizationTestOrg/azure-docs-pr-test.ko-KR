---
title: "Azure 앱 서비스에서 Java API 앱 빌드 및 배포"
description: "Java API 앱 패키지를 만들고 Azure 앱 서비스에 배포하는 방법을 알아봅니다."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="0fa6a-103">Azure 앱 서비스에서 Java API 앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="0fa6a-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="0fa6a-104">이 자습서에서는 Java 응용 프로그램을 만들고 [Git]를 사용하여 Azure 앱 서비스 API 앱에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="0fa6a-105">이 자습서의 지침은 Java를 실행할 수 있는 모든 운영 체제에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="0fa6a-106">이 자습서의 코드는 [Maven]을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="0fa6a-107">[Jax-RS]는 RESTful 서비스를 만드는 데 사용되고 [Swagger 편집기]를 사용하여 [Swagger] 메타데이터 사양을 기반으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa6a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0fa6a-108">Prerequisites</span></span>
1. <span data-ttu-id="0fa6a-109">[Java 개발자 키트 8] \(이상)</span><span class="sxs-lookup"><span data-stu-id="0fa6a-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="0fa6a-110">[Maven] 설치됨</span><span class="sxs-lookup"><span data-stu-id="0fa6a-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="0fa6a-111">[Git] 설치됨</span><span class="sxs-lookup"><span data-stu-id="0fa6a-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="0fa6a-112">[Microsoft Azure]에 대한 유료 또는 [무료 평가판] 구독</span><span class="sxs-lookup"><span data-stu-id="0fa6a-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="0fa6a-113">[Postman]</span><span class="sxs-lookup"><span data-stu-id="0fa6a-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="0fa6a-114">Swagger.IO를 사용하여 API 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="0fa6a-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="0fa6a-115">swagger.io 온라인 편집기를 사용하여 API의 구조를 나타내는 Swagger JSON 또는 YAML 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="0fa6a-116">API 노출 영역이 설계되면 다양한 플랫폼 및 프레임워크에 코드를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="0fa6a-117">다음 섹션에서 스캐폴드된 코드는 모의 기능을 포함하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="0fa6a-118">이 데모는 swagger.io 편집기에 붙여 넣는 Swagger JSON 본문으로 시작되며 그런 다음 JAX-RS가 REST API 끝점에 액세스하기 위해 사용한 코드를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="0fa6a-119">그러면 스캐폴드된 코드를 편집하여 모의 데이터를 반환하며 이는 데이터 지속성 메커니즘을 기반으로 한 REST API를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="0fa6a-120">다음 Swagger JSON 코드를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="0fa6a-121">[온라인 Swagger 편집기]로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="0fa6a-122">이동하면 **파일-> JSON 붙여넣기** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![JSON 메뉴 항목 붙여넣기][paste-json]
3. <span data-ttu-id="0fa6a-124">연락처 목록에 앞에서 복사한 API Swagger JSON를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Swagger에 JSON 코드 붙여넣기][pasted-swagger]
4. <span data-ttu-id="0fa6a-126">설명서 페이지 및 편집기에서 렌더링된 API 요약을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![Swagger로 생성된 문서 보기][view-swagger-generated-docs]
5. <span data-ttu-id="0fa6a-128">**서버 생성 -> JAX-RS** 메뉴 옵션을 선택하여 모의 구현을 추가하기 위해 나중에 편집할 서버 쪽 코드를 스캐폴드합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![코드 메뉴 항목 생성][generate-code-menu-item]
   
    <span data-ttu-id="0fa6a-130">코드가 생성되면 다운로드할 ZIP 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="0fa6a-131">이 파일은 Swagger 코드 생성기 및 모든 관련된 작성 스크립트로 인해 스캐폴드된 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="0fa6a-132">개발 워크스테이션의 디렉터리에 전체 라이브러리의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="0fa6a-133">코드를 편집하여 API 구현 추가</span><span class="sxs-lookup"><span data-stu-id="0fa6a-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="0fa6a-134">이 섹션에서는 Swagger로 생성된 코드의 서버 측 구현을 사용자 지정 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="0fa6a-135">새 코드는 클라이언트를 호출하는 데 연락처의 ArrayList 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="0fa6a-136">[Visual Studio Code] 또는 원하는 텍스트 편집기를 사용하여 *src/gen/java/io/swagger/model* 폴더에 위치한 *Contact.java* 모델 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![연락처 모델 파일 열기][open-contact-model-file]
2. <span data-ttu-id="0fa6a-138">**연락처** 클래스 내에 다음 생성자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="0fa6a-139">[Visual Studio Code] 또는 원하는 텍스트 편집기를 사용하여 *src/main/java/io/swagger/api/impl* 폴더에 위치한 *ContactsApiServiceImpl.java* 서비스 구현 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![연락처 서비스 코드 파일 열기][open-contact-service-code-file]
4. <span data-ttu-id="0fa6a-141">이 새 코드를 사용하여 파일의 코드를 덮어써서 모의 구현을 서비스 코드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="0fa6a-142">명령 프롬프트를 열고 디렉터리를 응용 프로그램의 루트 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="0fa6a-143">로컬로 Jetty 앱 서버를 사용하여 코드를 작성하고 실행하려면 다음 Maven 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="0fa6a-144">Jetty가 포트 8080에서 코드를 시작했음을 반영하는 명령 창이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![연락처 서비스 코드 파일 열기][run-jetty-war]
8. <span data-ttu-id="0fa6a-146">[Postman]을 사용하여 http://localhost:8080/api/contacts에 있는 "모든 연락처 가져오기" API 메서드에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![연락처 API 호출][calling-contacts-api]
9. <span data-ttu-id="0fa6a-148">[Postman]을 사용하여 http://localhost:8080/api/contacts/2에 있는 "특정 연락처 가져오기" API 메서드에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![연락처 API 호출][calling-specific-contact-api]
10. <span data-ttu-id="0fa6a-150">마지막으로 콘솔에서 다음 Maven 명령을 실행하여 Java WAR(웹 보관) 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="0fa6a-151">WAR 파일을 작성하면 **대상** 폴더에 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="0fa6a-152">**대상** 폴더로 이동하여 WAR 파일의 이름을 **ROOT.war**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="0fa6a-153">대/소문자가 이 형식과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="0fa6a-154">마지막으로 응용 프로그램의 루트 폴더에서 다음 명령을 실행하여 WAR 파일을 Azure에 배포하는 데 사용할 **배포** 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="0fa6a-155">Azure 앱 서비스에 출력 게시</span><span class="sxs-lookup"><span data-stu-id="0fa6a-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="0fa6a-156">이 섹션에서는 Azure 포털을 사용 하여 새 API 앱을 만들고 Java 응용 프로그램을 호스팅하기 위해 해당 API 앱을 준비하며 새 API 앱을 실행하기 위해 Azure 앱 서비스에 새로 만든 WAR 파일을 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="0fa6a-157">**새로 만들기 -> 웹 + 모바일 -> API 앱** 메뉴 항목을 클릭하고 앱의 세부 정보를 입력한 다음 **만들기**를 클릭하여 [Azure Portal]에서 새 API 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![새 API 앱 만들기][create-api-app]
2. <span data-ttu-id="0fa6a-159">API 앱을 만들면 앱의 **설정** 블레이드를 열고 **응용 프로그램 설정** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="0fa6a-160">사용 가능한 옵션에서 최신 Java 버전을 선택한 다음 **웹 컨테이너** 메뉴에서 최신 Tomcat을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![API 앱 블레이드에서 Java 설정][set-up-java]
3. <span data-ttu-id="0fa6a-162">**배포 자격 증명** 설정 메뉴 항목을 클릭하고 API 앱에 파일을 게시하는 데 사용하려는 사용자 이름 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![배포 자격 증명 설정][deployment-credentials]
4. <span data-ttu-id="0fa6a-164">**배포 원본** 설정 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="0fa6a-165">일단 이동하면 **원본 선택** 단추를 클릭하고 **로컬 Git 리포지토리** 옵션을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="0fa6a-166">API 앱을 사용하는 연결이 있는 Azure에서 실행되는 Git 리포지토리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="0fa6a-167">Git 리포지토리의 *마스터* 분기로 코드를 커밋할 때마다 코드는 라이브 실행 중인 API 앱 인스턴스에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![새 로컬 Git 리포지토리 설정][select-git-repo]
5. <span data-ttu-id="0fa6a-169">새 Git 리포지토리의 URL을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="0fa6a-170">잠시 후에 중요하다고 생각되면 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-170">Save this as it will be important in a moment.</span></span> 
   
    ![앱에 대한 새 Git 리포지토리 설정][copy-git-repo-url]
6. <span data-ttu-id="0fa6a-172">Git는 온라인 리포지토리에 WAR 파일을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="0fa6a-173">이 작업을 수행하려면 앞에서 만든 **배포** 폴더로 이동하므로 코드를 앱 서비스에서 실행하는 리포지토리까지 쉽게 커밋할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="0fa6a-174">콘솔 창에 위치하고 webapps 폴더가 있는 폴더로 이동하면 다음 Git 명령을 발급하여 프로세스를 시작하고 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="0fa6a-175">**푸시** 요청을 발급하면 이전에 배포 자격 증명에 대해 만든 암호를 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="0fa6a-176">자격 증명을 입력하면 업데이트가 배포되었다는 메시지가 포털에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="0fa6a-177">다시 한 번 Postman을 사용하여 Azure 앱 서비스에서 실행되는 새로 배포된 API 앱을 누르면 동작이 일관되고 예상 대로 연락처 데이터를 반환하며 Swagger.io로 스캐폴드된 Java 코드에 간단한 코드 변경 내용을 사용하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Azure에서 Java 연락처 REST API 라이브 사용][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="0fa6a-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0fa6a-179">Next steps</span></span>
<span data-ttu-id="0fa6a-180">이 문서에서는 Swagger.io 편집기에서 가져온 Swagger JSON 파일 및 스캐폴드된 Java 코드를 시작할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="0fa6a-181">여기서부터 간단한 변경 내용 및 Git 배포 프로세스가 Java로 작성된 기능 API 앱을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="0fa6a-182">다음 자습서에서는 [CORS를 사용하여 JavaScript 클라이언트에서 API 앱을 사용][App Service API CORS]하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="0fa6a-183">시리즈의 후반부 자습서에서는 인증 및 권한 부여를 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="0fa6a-184">이 샘플을 작성하려면 JSON blob를 유지하기 위해 [Java용 저장소 SDK] 에 대한 자세한 정보를 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="0fa6a-185">또는 [Document DB Java SDK] 를 사용하여 Azure Document DB에 연락처 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="0fa6a-186">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0fa6a-186">See Also</span></span>
<span data-ttu-id="0fa6a-187">Java에서 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fa6a-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure Portal]: https://portal.azure.com/
[Document DB Java SDK]: ../documentdb/documentdb-java-application.md
[무료 평가판]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java 개발자 키트 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[온라인 Swagger 편집기]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Java용 저장소 SDK]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger 편집기]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
