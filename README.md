此版本為CYeh與我 重現此系統之步驟紀錄。
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

以下為SCYeh提供，非常感謝
## SonarScanner掃描專案
1. 下載SonarScanner (https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/3d45ece9-bf6d-4838-9f25-6b5b66bf9aa5)
   
2. 將下載完成的SonarScanner解壓至任意位置 <br>
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/0133adf1-b437-4283-b694-c52ab0879008)
   
3. 將 {~path_to_SonarScanner}/bin 加入path系統變數
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/56df68f1-25d3-4298-8eb8-ce5308e306d0)
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/461d80d7-a75e-4601-aad1-e3acf04e1516)

4. 開啟cmd，輸入 `sonar-scanner --version`，若出現下圖資訊代表設定成功
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/dba7bffc-103e-42e1-bacd-8067cc4572ff)

5. 修改 {~path_to_SonarScanner}/conf/sonar-scanner.properties 檔案
     ```
    #----- Default SonarQube server
    sonar.host.url=http://localhost:9000/sonarqube

    #----- Default source code encoding
    sonar.sourceEncoding=UTF-8

    sonar.jdbc.url=jdbc:postgresql://localhost/sonar?currentSchema=public
    sonar.jdbc.username=sonar
    sonar.jdbc.password=*****
    ```

6. 在欲掃描的專案根目錄新增 sonar-project.properties 檔案
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/79de1e46-da58-47f7-bf8f-884f60a814a8)

    ```
    sonar.projectKey=GRAS
    
    # 欲掃描的資料夾
    sonar.sources=src
    
    # Java產生的class檔的資料夾位置
    sonar.java.binaries=C:/Project/GitRepositoryAnalysisSystem/build/classes
    ```

8. 進入SonarQube頁面，選擇Create Local Project
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/b56f0955-3a82-4503-b41e-9b9b20adf0c9)

9. 輸入Project Display Name和Project Key
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/96f8a4ac-f71d-4dee-956f-ca9a3c4abe1d)

10. 選擇Use the Global Settings
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/5532a5cf-c135-4d2a-8039-c0e124003185)

11. 選擇分析本地專案
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/29cee81d-8481-43a8-853b-e0121c630f59)

12. 點選右上角Account圖示，點選My Account
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/118acba7-a463-4351-979f-4df902db9a8b)

13. 點選Security Tab，輸入Token Name，Type選擇User Token，Expires選擇無期限，最後點擊Generate
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/ff142e6f-728e-46aa-a0b1-3d4b64429bca)

14. 複製Token並保存起來
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/75cde8dd-9e75-41c6-a497-070b4d1a3c92)

15. 點選Using existing Token並輸入剛剛複製的Token
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/d33f924d-a84b-4f65-829e-1df4cf05c7fa)

16. 選擇Others及Windows，並複製下方掃描指令
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/66e169f9-b329-4df2-9d3f-2648212c91a8)

17. 開啟cmd並cd至欲掃描專案的根目錄，執行剛剛複製的指令
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/0487331c-0610-4c30-a6fb-422bea94be63)

18. 若出現下方資訊則表示已掃描完成
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/6ab31762-31fe-4b2f-8dc8-fa78130286ab)

19. 回到SonarQube頁面可看到掃描結果
    ![image](https://github.com/liyo2686/GitRepositoryAnalysisSystem/assets/88961674/b3d9f0bc-d43b-4078-9147-3846363796e9)
