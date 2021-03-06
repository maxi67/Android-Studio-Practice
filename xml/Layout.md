# Layout種類(歸在ViewGroup) #
* RelativeLayout(相對布局)
* LinearLayout(線性布局)
* AbsoluteLayout(絕對布局)
* TableLayout(表格布局)
* FrameLayout(框架布局)

我比較常用的是RelativeLayout跟LinearLayout

## RelativeLayout ##
元件之間都是相對排列，所以可能發生元件重疊的問題  
很適合沒有設計圖，想到一個元件加一個的設計模式  
要注意設定屬性參考的對象不能出現晚於自己(XML很重先後順序)  
元件的預設情況(沒有特別用屬性指定位置)是主畫面的靠左上方  
元件相關屬性([ ]內是屬性值內容):
+ alignStart/End/Top/Bottom [某元件]: 與某元件的左/右/上/下對齊  
+ alignParentStart/End/Top/Bottom [true/false]: 對主畫面靠左/右/上/下對齊  
+ layout_toStartOf/toEndOf/above/below [某元件]: 在某元件之左/右/上/下方  
+ layout_centerHorizonal/centerVertical [true/false]: 對主畫面水平/垂直置中  

<hr>
## LinearLayout ##
元件的排列方向只會是由左而右(水平horizonal)或是由上而下(垂直vertical)  
所以每一個元件一定是依徐該規則排在前一個後面，不會有重疊問題  
相關屬性([ ]內是屬性值內容):
+ orientation [horizonal/vertical]: 元件的排列方向  

<hr>
## TableLayout ##
當初是要做計算機才學了這個(笑)  
它其實就是有網格、表格的概念  
在宣告TableLayout後，再接著呼叫數個TableRow元件(一個TableRow代表一個列)  
也可以把一個TableRow看成是一個水平的LinearLayout  
只是預設的寬就是match_parent(填滿畫面)  

另外，在每一個TableRow內，可以為每個元件定義layout_weight屬性指定權重值，可以幫它們的寬分配比例，以節省為每個元件分別定義的麻煩。 
像是只有兩個Button，就同時定義android:layout_weight為1，結果如下:  
![image](https://scontent-tpe1-1.xx.fbcdn.net/v/t1.0-9/15940682_1381031928583323_1945664001419339054_n.png?oh=8c5c60c91eb5c9b9ba1ec922125a82fe&oe=58E2630E)  
我加上背景顏色凸顯TableRow的範圍  
