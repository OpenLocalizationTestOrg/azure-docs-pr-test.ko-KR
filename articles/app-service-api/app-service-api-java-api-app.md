---
title: "aaaBuild 및 Azure 앱 서비스의 Java API 앱 배포"
description: "자세한 내용은 어떻게 toocreate Java API 앱 패키지 및 tooAzure 앱 서비스를 배포 합니다."
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
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Azure 앱 서비스에서 Java API 앱 빌드 및 배포
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

이 자습서에서는 어떻게 toocreate Java 응용 프로그램을 사용 하 여 tooAzure 앱 서비스 API 앱을 배포 하 고 [Git]합니다. 이 자습서의 지침에 hello Java 실행할 수 있는 모든 운영 체제에서 수행할 수 있습니다. 이 자습서에서는 hello 코드를 사용 하 여 만들어집니다 [Maven]합니다. [잭 스 RS] 는 RESTful 서비스를 사용 하는 toocreate hello 및 hello에 따라 생성 됩니다 [Swagger] hello를 사용 하 여 메타 데이터 사양 [Swagger 편집기]합니다.

## <a name="prerequisites"></a>필수 조건
1. [Java 개발자 키트 8] \(이상)
2. [Maven] 설치됨
3. [Git] 설치됨
4. 유료 또는 [무료 평가판] 구독 너무[Microsoft Azure]
5. [우체부]

## <a name="scaffold-hello-api-using-swaggerio"></a>Swagger.IO를 사용 하 여 스 캐 폴드 hello API
Hello swagger.io 온라인 편집기를 사용 하 여 API의 hello 구조를 나타내는 JSON Swagger 또는 YAML 코드를 입력할 수 있습니다. Hello API 노출 영역 설계를 만든 후에 다양 한 플랫폼 및 프레임 워크에 대 한 코드를 내보낼 수 있습니다. Hello 다음 섹션에서 스 캐 폴드 된 hello 코드가 수정 된 tooinclude 모의 기능 됩니다. 

이 데모는 다음 사용된 toogenerate 코드 수행할 예정 잭 스 RS tooaccess의 REST API 끝점을 사용 하는 hello swagger.io 편집기에 붙여 하는 Swagger JSON 본문으로 시작 됩니다. 그런 다음 편집 합니다 스 캐 폴드 된 hello 코드 tooreturn 모의 데이터를 기반으로 데이터 지 속성 메커니즘 REST API를 시뮬레이션 합니다.  

1. 다음 JSON Swagger 코드 tooyour 클립보드 hello를 복사 합니다.
   
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
2. Toohello 이동 [온라인 Swagger 편집기]합니다. 한 번 hello, 클릭 **파일 붙여넣기 JSON->** 메뉴 항목입니다.
   
    ![JSON 메뉴 항목 붙여넣기][paste-json]
3. 연락처 목록 API Swagger JSON 앞에서 복사한 hello에 붙여 넣습니다. 
   
    ![Swagger에 JSON 코드 붙여넣기][pasted-swagger]
4. Hello 설명서 페이지 및 hello 편집기에서 렌더링 되는 API 요약을 볼 수 있습니다. 
   
    ![Swagger로 생성된 문서 보기][view-swagger-generated-docs]
5. 선택 hello **서버 생성 잭 스 RS->** 메뉴 옵션 tooscaffold hello 서버 쪽 코드 이후 tooadd 모의 구현을 편집 합니다. 
   
    ![코드 메뉴 항목 생성][generate-code-menu-item]
   
    Hello 코드 생성 되 면 ZIP 파일 toodownload를 제공 합니다. Hello Swagger 코드 생성기에서 스 캐 폴드 된 hello 코드를 포함 하는이 파일 및 관련 된 모든 스크립트를 작성 합니다. Hello 전체 라이브러리 tooa 디렉터리를 개발 워크스테이션에서 압축을 풉니다. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Hello 코드 tooadd API 구현 편집
이 섹션에서는 사용자 지정 코드로 hello Swagger에서 생성 된 코드의 서버 쪽 구현을 바꿉니다. hello 새 코드는 연락처의 ArrayList 엔터티 toohello 호출 클라이언트를 반환 합니다. 

1. 열기 hello *Contact.java* hello에 있는 모델 파일을 *src/gen/java/io/swagger/모델* 폴더를 사용 하 여 [Visual Studio Code] 또는 원하는 텍스트 편집기입니다. 
   
    ![연락처 모델 파일 열기][open-contact-model-file]
2. Hello hello 내에서 생성자를 다음 추가 **연락처** 클래스입니다. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. 열기 hello *ContactsApiServiceImpl.java* hello에 있는 서비스 구현 파일 *src/main/java/io/swagger/api/impl* 폴더를 사용 하 여 [Visual Studio Code]또는 원하는 텍스트 편집기입니다.
   
    ![연락처 서비스 코드 파일 열기][open-contact-service-code-file]
4. 이 새 코드 tooadd 모의 구현 toohello 서비스 코드도 hello 파일의 hello 코드를 덮어씁니다. 
   
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
5. 명령 프롬프트를 열고 응용 프로그램의 디렉터리 toohello 루트 폴더를 변경 합니다.
6. Maven 명령 toobuild hello 코드 다음 hello를 실행 하 고 hello Jetty 응용 프로그램 서버를 사용 하 여 로컬로 실행 합니다. 
   
        mvn package jetty:run
7. Jetty 포트 8080에서 코드가 시작 되었음을 반영 하는 hello 명령 창에 표시 됩니다. 
   
    ![연락처 서비스 코드 파일 열기][run-jetty-war]
8. 사용 하 여 [우체부] http://localhost:8080/api/연락처에서 toomake 요청 toohello "모든 연락처 가져오기" API 메서드.
   
    ![Hello 연락처 API를 호출 합니다.][calling-contacts-api]
9. 사용 하 여 [우체부] http://localhost:8080/api/연락처/2에 있는 요청 toohello "특정 연락처 가져오기" API toomake 메서드.
   
    ![Hello 연락처 API를 호출 합니다.][calling-specific-contact-api]
10. 마지막으로 hello Maven 명령 콘솔에서 다음을 실행 하 여 hello Java WAR (웹 보관) 파일을 빌드하십시오. 
    
         mvn package war:war
11. Hello에 두려는 됩니다 hello WAR 파일 작성 된 후 **대상** 폴더입니다. Hello 트리로 이동 **대상** 폴더 및 이름 바꾸기 hello WAR 파일 너무**ROOT.war**합니다. (Hello 대/소문자가 일치 해야이 형식).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. 마지막으로 hello 명령을 응용 프로그램 toocreate의 hello 루트 폴더에서 다음을 실행 한 **배포** 폴더 toouse toodeploy hello WAR 파일 tooAzure 합니다. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Hello 출력 tooAzure 앱 서비스를 게시 합니다.
어떻게 toocreate hello를 사용 하 여 새 API 앱 Azure 포털에서 Java 응용 프로그램 호스팅에 대 한 API 앱을 준비 하 고 hello 배포 새로 만든 WAR 알아봅니다이 섹션에서는 앱 서비스 toorun tooAzure 새 API 앱 파일입니다. 

1. Hello에 새 API 앱 만들기 [Azure 포털], hello를 클릭 하 여 **새로운 웹-> +-> API 앱을 모바일** 메뉴 항목, 응용 프로그램 세부 정보를 입력 하 고 클릭 한 다음 **만들기**합니다.
   
    ![새 API 앱 만들기][create-api-app]
2. API 앱을 만든 후 응용 프로그램을 열고 **설정** 블레이드에서 hello를 클릭 한 다음 **응용 프로그램 설정** 메뉴 항목입니다. 선택 hello hello 사용 가능한 옵션 중에서 최신 Java 버전 선택 hello hello에서 최신 Tomcat 다음 **웹 컨테이너** 메뉴를 차례로 클릭 **저장**합니다.
   
    ![API 앱 블레이드 hello에서 Java를 설정 합니다.][set-up-java]
3. Hello 클릭 **배포 자격 증명** 설정 메뉴 항목을 선택한 사용자 이름 및 파일 tooyour API 앱을 게시 하기 위한 toouse 원하는 암호를 제공 합니다. 
   
    ![배포 자격 증명 설정][deployment-credentials]
4. Hello 클릭 **배포 원본** 설정 메뉴 항목입니다. 한 번 hello, 클릭 **선택 소스** 단추, 선택 hello **로컬 Git 리포지토리** 옵션을 선택한 다음 클릭 **확인**합니다. API 앱을 사용하는 연결이 있는 Azure에서 실행되는 Git 리포지토리가 만들어집니다. 코드 toohello을 커밋할 때마다 *마스터* 분기의 Git 리포지토리를 코드 라이브 실행 중인 API 앱 인스턴스로 게시 됩니다. 
   
    ![새 로컬 Git 리포지토리 설정][select-git-repo]
5. Hello 새 Git 리포지토리 URL tooyour 클립보드에 복사 합니다. 잠시 후에 중요하다고 생각되면 저장합니다. 
   
    ![앱에 대한 새 Git 리포지토리 설정][copy-git-repo-url]
6. Git 푸시 hello WAR 파일 toohello 온라인 저장소입니다. toodo이 hello 트리로 이동 **배포** 앱 서비스에서 실행 되는 toohello 리포지토리를 hello 코드를 쉽게 커밋할 수 있도록 이전에 만든 폴더입니다. 한 번 hello 콘솔 창에 하 고 hello Git 명령을 toolaunch hello 프로세스를 실행 하 고 실행 하는 배포 hello webapps 폴더 위치한 hello 폴더로 이동 하 게 합니다. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Hello 발급 되 면 **푸시** 요청을 만들라는 메시지가 이전에 만든 배포 자격 증명 hello에 대 한 hello 암호에 대 한 합니다. 자격 증명을 입력 한 후 배포 된 hello 업데이트 하는 포털 디스플레이 표시 됩니다.
7. 다시 한 번에 우체부 toohit hello 새로 배포 된 Azure 앱 서비스에서 실행 되는 API 앱을 사용 하면 hello 동작은 일관 된 동작이 며 이제 반환 하는 연락처 데이터를 예상 대로 및 Java 코드 스 캐 폴드 된 간단한 코드 변경 내용을 toohello Swagger.io를 사용 하 여 표시 됩니다. 
   
    ![Azure에서 Java 연락처 REST API 라이브 사용][postman-calling-azure-contacts]

## <a name="next-steps"></a>다음 단계
이 문서에서는 JSON Swagger 파일 및 hello Swagger.io 편집기에서 가져온 일부 스 캐 폴드 Java 코드를 사용 하 여 수 toostart 있었습니다. 여기서부터 간단한 변경 내용 및 Git 배포 프로세스가 Java로 작성된 기능 API 앱을 갖게 됩니다. hello 다음 자습서에서는 어떻게 너무[CORS를 사용 하 여 JavaScript 클라이언트에서 API 앱][App Service API CORS]합니다. 이후 자습서에서이 계열 표시를 어떻게 hello tooimplement 인증 및 권한 부여 합니다.

이 샘플에서 toobuild를 학습할 수 있는 hello에 대 한 자세한 [저장소 SDK for Java] toopersist hello JSON blob입니다. Hello를 사용할 수 있습니다 또는 [문서 DB Java SDK] toosave 연락처 데이터 tooAzure 문서 DB입니다. 

<a name="see-also"></a>

## <a name="see-also"></a>참고 항목
Java에서 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure 포털]: https://portal.azure.com/
[문서 DB Java SDK]: ../documentdb/documentdb-java-application.md
[무료 평가판]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java 개발자 키트 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[잭 스 RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[온라인 Swagger 편집기]: http://editor2.swagger.io/
[우체부]: https://www.getpostman.com/
[저장소 SDK for Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
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
