# GitRepositoryAnalysisSystem
use angular + java servlet
# output Angular
1. replace "~{PathToProject}" under "outputPath" in frontEnd/src/angular.json  (ex:F:\\workspace\\)  
2. cd frontEnd  
3. ng build --watch --base-href /GitRepositoryAnalysisSystem/frontEnd/
The output will be in the following location:  
GitRepositoryAnalysisSystem\src\main\webapp\frontEnd\

4. ng add @angular/material  to use Angular material

5. npm install @angular/cdk --save

6. 使用連結 http://localhost:8080/GitRepositoryAnalysisSystem/frontEnd/userLogin 即可進入GRAS魔幻世界，HAVE FUN

PS: 如果build完發現頁面均無變化，加入--outputHashing=all
>>使用ng build --watch --outputHashing=all --base-href /GitRepositoryAnalysisSystem/frontEnd/

2024/03/11 build建置步驟
依下列步驟執行
1. 安裝node.js(14.17.3) 、 Angular(10.1.7) (npm install -g @angular/cli@10.1.7)
2. cd frontEnd
3. npm install @angular/cdk --save
4. run tomcat
5. ng build --watch --base-href /GitRepositoryAnalysisSystem/frontEnd/
目前dump檔需要更新
