# GitRepositoryAnalysisSystem
Angular + Java Servlet

## Angular建置文件

### 崴崴版
1. replace "~{PathToProject}" under "outputPath" in frontEnd/src/angular.json (ex:F:\\workspace\\)
2. cd frontEnd
3. ng build --watch --base-href /GitRepositoryAnalysisSystem/frontEnd/
    The output will be in the following location:
    GitRepositoryAnalysisSystem\src\main\webapp\frontEnd\
4. ng add @angular/material  to use Angular material
5. npm install @angular/cdk --save
6. 使用連結 http://localhost:8080/GitRepositoryAnalysisSystem/frontEnd/userLogin 即可進入GRAS魔幻世界，HAVE FUN

PS: 如果build完發現頁面均無變化，加入--outputHashing=all <br>
`ng build --watch --outputHashing=all --base-href /GitRepositoryAnalysisSystem/frontEnd/`

### 大U版(2024/03/11)
依下列步驟執行
1. 安裝node.js(14.17.3) 、 Angular(10.1.7) (`npm install -g @angular/cli@10.1.7`)
2. `cd frontEnd`
3. `npm install @angular/cdk --save`
4. run tomcat
5. `ng build --watch --base-href /GitRepositoryAnalysisSystem/frontEnd/`

## SonarQube建置文件
參考以下網頁
https://blog.51cto.com/huny/3263674

- 版本
    - Java：12以上
    - PostgreSQL：15
    - SonarQube：10.4.1.88267
- conf/sonar.properties設定
  ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/5afb9ddd-a9d5-454f-b0f1-931748eab619)
  ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/6b1a0d2a-d420-4d24-aba9-5f8b0a72684d)
  ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/54056845-8305-45e6-876b-bfd71b33620c)
- cmd執行bin/windows-x86-64/StartSonar.bat
- 若無法正常執行，則將sonar使用者權限開到admin等級
    1. 將PostgreSQL UserName切回root
    2. 將postgre user的Priviledges SuperUser設為Yes
- 執行成功後，使用連結
    http://localhost:9000
    即可進入SonarQube登入畫面，首次登入帳號密碼皆為admin
    
## SonarQube掃描專案
參考以下網頁
https://www.cnblogs.com/Uni-Hoang/p/15207178.html

- conf/sonar-scanner.properties
    ```
    #----- Default SonarQube server
    sonar.host.url=http://localhost:9000/sonarqube

    #----- Default source code encoding
    sonar.sourceEncoding=UTF-8

    sonar.jdbc.url=jdbc:postgresql://localhost/sonar?currentSchema=public
    sonar.jdbc.username=sonar
    sonar.jdbc.password=*****
    ```
- sonar-project.properties
    ```
    sonar.projectKey=GRAS
    
    # 欲掃描的資料夾
    sonar.sources=src
    
    # Java產生的class檔的資料夾位置
    sonar.java.binaries=C:/Project/GitRepositoryAnalysisSystem/build/classes
    ```
