---
title: "Azure Cosmos DB를 사용 하 여 aaaJava 응용 프로그램 개발 자습서 | Microsoft Docs"
description: "이 Java 웹 응용 프로그램 자습서 toouse를 Azure Cosmos DB hello 및 DocumentDB API toostore hello 및 Azure 웹 사이트에서 호스팅되는 Java 응용 프로그램에서 데이터 액세스 방법을 보여 줍니다."
keywords: "응용 프로그램 개발, 데이터베이스 자습서, java 응용 프로그램, java 웹 응용 프로그램 자습서, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Azure Cosmos DB 및 hello DocumentDB API를 사용 하는 Java 웹 응용 프로그램 빌드
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

이 Java 웹 응용 프로그램 자습서에서는 어떻게 toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) toostore 및 액세스 데이터를 Azure 앱 서비스 웹 앱에서 호스트 되는 Java 응용 프로그램에서 서비스입니다. 이 항목에서는 다음 내용을 배웁니다.

* 어떻게 toobuild Eclipse에서 기본 JavaServer 페이지 (JSP) 응용 프로그램입니다.
* Hello Azure Cosmos DB로 toowork hello를 사용 하 여 서비스 어떻게 [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java)합니다.

Java 응용 프로그램에 대해 설명 방식과 toocreate 있습니다, 검색, 및 표시 수 있는 웹 기반 toocreate 작업 관리 응용 프로그램 작업 완료 상태로 hello 다음 이미지와 같이 합니다. 각 hello 작업 hello 할 일 목록에는 Azure Cosmos DB에서 JSON 문서도 저장 됩니다.

![My ToDo List Java 응용 프로그램](./media/documentdb-java-application/image1.png)

> [!TIP]
> 이 응용 프로그램 개발 자습서에서는 이전에 Java를 사용한 경험이 있다고 가정합니다. 새 tooJava 또는 hello [필수 구성 요소 도구](#Prerequisites), 전체 hello를 다운로드 하는 것이 좋습니다 [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) 를 GitHub를 사용 하 여 프로젝트 [hello hello 끝이에 대 한 지침 문서](#GetProject)합니다. 작성 된, 일단 hello 프로젝트의 hello 컨텍스트에서 hello 코드에 hello 문서 toogain 대 한 정보를 검토할 수 있습니다.  
> 
> 

## <a id="Prerequisites"></a>이 Java 웹 응용 프로그램 자습서의 필수 구성 요소
이 응용 프로그램 개발 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

    또는

    Hello의 로컬 설치 [Azure Cosmos DB 에뮬레이터](local-emulator.md)합니다.
* [JDK(Java Development Kit) 7 이상](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Java 런타임 환경(예: Tomcat 또는 Jetty)을 사용하는 Azure 웹 사이트](../app-service-web/web-sites-java-get-started.md)

이러한 도구 hello에 대 한 처음으로 설치 하는 경우 coreservlets.com의 hello 빠른 시작 섹션에 hello 설치 프로세스의 단계를 제공 하는 해당 [자습서: TomCat7 설치 및 사용 하 여 Eclipse와](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) 문서.

## <a id="CreateDB"></a>1단계: Azure Cosmos DB 계정 만들기
Azure Cosmos DB 계정을 만들어 시작해 보겠습니다. 계정이 이미 없거나 사용 중인 경우이 자습서에 대 한 Azure Cosmos DB 에뮬레이터 hello 건너뛰어도 너무[2 단계: hello Java JSP 응용 프로그램 만들기](#CreateJSP)합니다.

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>2 단계: hello Java JSP 응용 프로그램 만들기
toocreate hello JSP 응용 프로그램:

1. 먼저, Java 프로젝트를 만듭니다. Eclipse를 시작한 후 **파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다. 표시 되지 않으면 **동적 웹 프로젝트** 다음 hello 않는 사용 가능한 프로젝트로 표시: 클릭 **파일**, 클릭 **새로**, 클릭 **프로젝트**..., 확장 **웹**, 클릭 **동적 웹 프로젝트**를 클릭 하 고 **다음**합니다.
   
    ![JSP Java 응용 프로그램 개발](./media/documentdb-java-application/image10.png)
2. Hello에 프로젝트 이름을 입력 **프로젝트 이름** 상자 및 hello **대상 런타임** 드롭 다운 메뉴에서 필요에 따라 (예:: Apache Tomcat v7.0) 값을 선택 하 고 클릭 **마침**. 대상 런타임을 선택 하면 Eclipse 통해 로컬 프로젝트 있습니다 toorun 활성화 합니다.
3. Eclipse에서 hello 프로젝트 탐색기 보기에서 프로젝트를 확장 합니다. **WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.
4. Hello에 **JSP 파일 새로** 대화 상자, 이름 hello 파일 **index.jsp**합니다. Hello 상위 폴더를 유지 **WebContent**클릭 하 고 다음 그림에서는 hello에 나타난 것 처럼 **다음**합니다.
   
    ![새 JSP 파일 만들기 - Java 웹 응용 프로그램 자습서](./media/documentdb-java-application/image11.png)
5. Hello에 **JSP 템플릿 선택** 대화 상자에서이 자습서 select hello 목적을 위해 **새 JSP 파일 (html)**, 클릭 하 고 **마침**합니다.
6. Eclipse에서 index.jsp 파일이 hello를 열면 텍스트 toodisplay 추가 **Hello World!** hello 기존 내 <body> 요소입니다. 업데이트 한 후 <body> 콘텐츠 코드 다음 hello 같아야 합니다.:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Hello index.jsp 파일을 저장 합니다.
8. 2 단계에서 대상 런타임을 설정 하는 경우 클릭할 수 있는 **프로젝트** 차례로 **실행** toorun 로컬로 JSP 응용 프로그램:
   
    ![Hello World - Java 응용 프로그램 자습서](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>3 단계: hello DocumentDB Java SDK 설치
hello hello DocumentDB Java SDK 및 해당 종속성에 가장 쉬운 방법은 toopull 방식은 [Apache Maven](http://maven.apache.org/)합니다.

toodo이 hello 다음 단계를 완료 하 여 프로젝트 tooa maven 프로젝트가 tooconvert를 해야 합니다.

1. Hello 프로젝트 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 여, **구성**, 클릭 **tooMaven 프로젝트 변환**합니다.
2. Hello에 **새 POM 만들** 창의 hello 기본값을 적용 하 고 클릭 **마침**합니다.
3. **프로젝트 탐색기**열고 hello pom.xml 파일입니다.
4. Hello에 **종속성** 탭 hello **종속성** 창에서 클릭 **추가**합니다.
5. Hello에 **선택 종속성** 창에서 다음 hello지 않습니다:
   
   * Hello에 **그룹 Id** 상자 com.microsoft.azure를 입력 합니다.
   * Hello에 **아티팩트 Id** 상자에 azure documentdb를 입력 합니다.
   * Hello에 **버전** 상자 1.5.1를 입력 합니다.
     
   ![DocumentDB Java 응용 프로그램 SDK 설치](./media/documentdb-java-application/image13.png)
     
   * 그룹 Id 및 아티팩트 Id에 대 한 hello 종속성 XML을 추가 또는 텍스트 편집기를 통해 직접 toohello pom.xml:
     
        <dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency>
6. 클릭 **확인** Maven hello DocumentDB Java SDK를 설치 합니다.
7. Hello pom.xml 파일을 저장 합니다.

## <a id="UseService"></a>4 단계: hello Azure Cosmos DB 서비스를 사용 하 여 Java 응용 프로그램에서
1. 첫째, 보겠습니다 TodoItem.java의 hello TodoItem 개체를 정의 합니다.
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    이 프로젝트를 사용 하 여 [프로젝트 Lombok](http://projectlombok.org/) toogenerate hello 생성자, getter, setter 및 작성기입니다. 이 코드를 수동으로 작성 또는 있을 수 있습니다 또는 IDE hello 생성 합니다.
2. tooinvoke hello Azure Cosmos DB 서비스를 인스턴스화해야 새 **DocumentClient**합니다. 가장 좋은 tooreuse hello 일반적으로 **DocumentClient** -대신 보다 각각의 후속 요청에 대 한 새 클라이언트를 구성 합니다. Hello 클라이언트에 래핑하여 hello 클라이언트를 다시 사용할 수 있습니다는 **DocumentClientFactory**합니다. Toopaste hello URI 및 기본 키 값 tooyour 클립보드에 저장 해야 DocumentClientFactory.java, [1 단계](#CreateDB)합니다. [YOUR\_ENDPOINT\_HERE]를 해당 URI로 바꾸고 [YOUR\_KEY\_HERE]를 해당 기본 키로 바꿉니다.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. 이제 할 일 항목 tooAzure Cosmos DB 우리의 유지 개체 DAO (Data Access) tooabstract를 만들어 보겠습니다.
   
    순서로 toosave 할 일 항목 tooa 컬렉션, hello 클라이언트 필요한 tooknow 어떤 데이터베이스 및 컬렉션 toopersist 너무 (에서 참조 하므로 자체 링크)입니다. 일반적으로 최상의 toocache hello 데이터베이스와 가능한 경우 컬렉션은 tooavoid 추가 왕복 toohello 데이터베이스입니다.
   
    hello 다음 코드에서는 어떻게 tooretrieve 우리의 데이터베이스 및 컬렉션, 존재 하거나 존재 하지 않는 경우 새 필터를 만들 경우:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. hello 다음 단계는 toowrite toohello 컬렉션에 있는 일부 코드 toopersist hello TodoItems 합니다. 이 예제에서는 사용 [Gson](https://code.google.com/p/google-gson/) tooserialize TodoItem 이전 일반 Java 개체 (POJOs) tooJSON 문서를 역직렬화 하 고 있습니다.
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Azure Cosmos DB 데이터베이스 및 컬렉션과 마찬가지로 문서도 셀프 link로 참조됩니다. 자체 링크 하지 않고 hello 도우미 함수 사용 하면 다음 us 검색 문서 다른 특성 (예: "id"):
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. 다음 tooa POJO deserialize를 id 별로 5 단계 tooretrieve TodoItem JSON 문서 hello 도우미 메서드를 사용할 수 있습니다.
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. 또한 hello DocumentClient tooget 컬렉션 또는 TodoItems DocumentDB SQL을 사용 하 여 목록을 사용할 수 있습니다.:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Hello DocumentClient 사용 하 여 문서를 여러 방법으로 tooupdate가 됩니다. 할 일 목록 응용 프로그램에서는 완료 된 TodoItem 인지 toobe 수 tootoggle를 하려고 합니다. Hello hello 문서 내에서 "전체" 특성을 업데이트 하 여이 작업을 수행할 수 있습니다.
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. 목록에서 hello 기능 toodelete a TodoItem을 마지막으로, 바랍니다. toodo이를 이전에 작성 하는 hello 도우미 메서드를 사용할 수 있습니다 tooretrieve 자체 링크 hello 고 hello 클라이언트 toodelete 하기:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>5 단계: hello hello Java 응용 프로그램 개발 프로젝트의 나머지를 함께 연결
이전 읽었으면 hello 재미 했으므로 비트-즉는 toobuild 빠른 사용자 인터페이스 및 DAO tooour를 연결 합니다.

1. 먼저,이 DAO 컨트롤러 toocall 작성 시작 하겠습니다.
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    더 복잡 한 응용 프로그램에서는 hello 컨트롤러 hello DAO 기반으로 복잡 한 비즈니스 논리를 보유할 수 있습니다.
2. 다음으로 servlet tooroute HTTP 요청 toohello 컨트롤러를 만들겠습니다.
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. 웹 사용자 인터페이스 toodisplay toohello 사용자가 필요 합니다. 다시 작성해 보겠습니다 hello index.jsp 앞에서 만든:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. 마지막으로 일부 클라이언트 쪽 JavaScript tootie hello 웹 사용자 인터페이스를 작성 하 고 함께 servlet hello:
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. 멋집니다! 이제 tootest hello 응용 프로그램은 남았습니다. Hello 응용 프로그램을 로컬로 실행 하 고 hello 항목 이름 및 범주를 입력 하 고 클릭 하 여 일부 할 일 항목 추가 **작업 추가**합니다.
6. 완료 되 면 hello 확인란을 설정/해제 하 고 클릭 하 여 여부를 업데이트할 수 hello 항목 표시 될 때 **작업 업데이트**합니다.

## <a id="Deploy"></a>6 단계: Java 응용 프로그램 tooAzure 웹 사이트 배포
Azure 웹 사이트에서는 Java 응용 프로그램을 간단히 배포할 수 있습니다. 즉, 응용 프로그램을 WAR 파일로 내보내고 소스 제어(예: Git) 또는 FTP를 통해 업로드하면 됩니다.

1. tooexport WAR 파일으로 응용 프로그램에서 프로젝트에서 마우스 오른쪽 단추로 **프로젝트 탐색기**, 클릭 **내보내기**, 클릭 하 고 **WAR 파일**합니다.
2. Hello에 **WAR 내보내기** 창에서 다음 hello지 않습니다.
   
   * Documentdb java 샘플 azure hello 웹 프로젝트 상자에 입력 합니다.
   * Hello 대상 상자 대상 toosave hello WAR 파일을 선택 합니다.
   * **마침**을 클릭합니다.
3. WAR 파일을 맡은 단순히 업로드 tooyour Azure 웹 사이트의 **webapps** 디렉터리입니다. Hello 파일 업로드에 대 한 지침을 참조 하십시오. [Java 응용 프로그램 tooAzure 앱 서비스 웹 앱 추가](../app-service-web/web-sites-java-add-app.md)합니다.
   
    Hello WAR 파일 업로드 toohello webapps 디렉터리를 추가 했으므로 하 고 자동으로 로드 합니다 hello 런타임 환경을 검색 합니다.
4. tooview 완성 된 제품을 toohttp://YOUR 이동\_사이트\_NAME.azurewebsites.net/azure-java-sample/ 및 작업 추가 시작!

## <a id="GetProject"></a>GitHub에서 hello 프로젝트 가져오기
이 자습서에서는 모든 hello 샘플 hello에 포함 된 [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) GitHub에 대 한 프로젝트입니다. Eclipse에 tooimport hello todo 프로젝트 hello 소프트웨어 및 hello에 나열 된 리소스는 확인 [필수 구성 요소](#Prerequisites) 섹션에서 다음 다음 hello지 않습니다.

1. [Project Lombok](http://projectlombok.org/)을 설치합니다. Lombok 사용 되는 toogenerate 생성자, getter, setter hello 프로젝트에서입니다. Hello lombok.jar 파일을 다운로드 한 후 두 번 클릭 tooinstall 것 하거나 hello 명령줄에서 설치 합니다.
2. Eclipse 열려 있으면 닫고 tooload Lombok 다시 시작.
3. Hello에 Eclipse에서 **파일** 메뉴를 클릭 하 여 **가져오기**합니다.
4. Hello에 **가져오기** 창 클릭 **Git**, 클릭 **프로젝트에서 Git**, 클릭 하 고 **다음**합니다.
5. Hello에 **리포지토리 원본 선택** 화면 **복제 URI**합니다.
6. Hello에 **소스 Git 리포지토리에** 화면의 hello에 **URI** 상자 https://github.com/Azure-Samples/java-todo-app.git, 입력 한 다음 클릭 **다음**합니다.
7. Hello에 **분기 선택** 화면에서 **마스터** 을 선택한 다음 클릭 **다음**합니다.
8. Hello에 **로컬 대상** 화면 **찾아보기** tooselect 여기 hello 리포지토리를 복사할 수 있습니다 하 한 다음 클릭 폴더 **다음**합니다.
9. Hello에 **프로젝트 가져오기 마법사 toouse 선택** 화면에서 **기존 프로젝트를 가져올** 을 선택한 다음 클릭 **다음**합니다.
10. Hello에 **가져오기 프로젝트** 화면, 선택을 취소 hello **DocumentDB** 프로젝트를 마우스 클릭 **마침**합니다. hello DocumentDB 프로젝트에 hello Azure Cosmos DB Java SDK 대신 종속성으로 추가 합니다.
11. **프로젝트 탐색기**tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java 이동한 hello URI 및 기본 키를 사용 하 여 hello 호스트와 MASTER_KEY 값을 대체 합니다. Cosmos DB Azure 계정, 및 다음 hello 파일을 저장 합니다. 자세한 내용은 [1단계를 참조하세요. Azure Cosmos DB 데이터베이스 계정 만들기](#CreateDB)를 참조하세요.
12. **프로젝트 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **azure documentdb-java 샘플**, 클릭 **빌드 경로**, 클릭 하 고 **빌드 경로 구성**.
13. Hello에 **Java 빌드 경로** hello 오른쪽 창에서 선택 hello 화면 **라이브러리** 탭을 클릭 한 다음 **외부 단지 추가**합니다. Toohello hello lombok.jar 파일 위치를 찾아서 클릭 **열려**, 클릭 하 고 **확인**합니다.
14. 사용 하 여 12 단계 tooopen hello **속성** 에 창 hello 왼쪽된 창에서 다음을 클릭 하 고 **대상으로 하는 런타임**합니다.
15. Hello에 **대상으로 하는 런타임** 화면에서 **새로**을 선택 **Apache Tomcat v7.0**, 클릭 하 고 **확인**합니다.
16. 사용 하 여 12 단계 tooopen hello **속성** 에 창 hello 왼쪽된 창에서 다음을 클릭 하 고 **프로젝트 패싯**합니다.
17. Hello에 **프로젝트 패싯** 화면에서 **동적 웹 모듈** 및 **Java**, 클릭 하 고 **확인**합니다.
18. Hello에 **서버** hello hello 화면 맨 아래에 탭을 마우스 오른쪽 단추로 클릭 **Tomcat 서버 로컬 호스트에 v7.0** 클릭 하 고 **추가 및 제거**합니다.
19. Hello에 **추가 및 제거** 창 이동 **azure documentdb-java 샘플** toohello **자동 구성** 상자를 선택한 다음 클릭 **마침**합니다.
20. Hello에 **서버** 탭을 마우스 오른쪽 단추로 클릭 **Tomcat 서버 로컬 호스트에 v7.0**, 클릭 하 고 **다시 시작**합니다.
21. 브라우저에서 탐색 toohttp://localhost:8080 / azure documentdb-java 샘플 / tooyour 작업 목록에 추가 하기 시작 합니다. 기본 포트 값을 변경한 경우 선택한 8080 toohello 값을 변경 하는 참고 합니다.
22. toodeploy 프로그램 프로젝트 tooan Azure 웹 사이트 참조 [6 단계. 웹 사이트에 응용 프로그램 tooAzure 배포](#Deploy)합니다.

[1]: media/documentdb-java-application/keys.png
