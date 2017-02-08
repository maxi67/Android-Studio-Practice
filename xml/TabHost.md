TabHost是在App中很常見的元件，出現在當App有多個主要功能，想呈現在不同畫面並可以隨時切換時，由一列標籤區選取做切換，每一個頁面或畫面有一個TabID對應。  
![image](https://scontent-sjc2-1.xx.fbcdn.net/v/t1.0-9/16388091_1409711012382081_1540735620814958124_n.jpg?oh=a1277507216c51706b315574654a1bd8&oe=59465531)  

在xml中，原則上最基本的元件組成如下:
```XML
<TabHost
        android:id="@+id/tab_host"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <!--控制標籤列-->
        <TabWidget
            android:id="@android:id/tabs"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <!--控制標籤各頁內容-->
        <FrameLayout
            android:id="@android:id/tabcontent"
            android:layout_width="match_parent"
            android:layout_height="match_parent">
            
            <LinearLayout
                android:id="@+id/tab1"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical">
            </LinearLayout>

            <LinearLayout
                android:id="@+id/tab2"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical">
            </LinearLayout>
            
            <!--...-->
            
        </FrameLayout> 
</TabHost>
```
TabWidget就是控制標籤選取區的，FrameLayout則是畫面主要放置的地方，所有Tab都要寫在此Layout內，而且寬高要一致，不然切換起來會很奇怪。
我也習慣會在frameLayout外面加一個LinearLayout包覆，甚至再加一個LinearLayout把TabWidget與FrameLayout包著。透過分層有序的編排，整體感覺比較穩定且整齊。  

所有畫面的元件撰寫可以直接在xml中，如tab1就在tab1的Layout內(以上面的範例為例)，但全部擠在同一個檔案不免有些複雜，在Studio內的預覽也只能看到最上層的。
我們的做法是把所有的tab另外獨立寫成一個layout的.xml，然後在Activity內另外撰寫程式一一匯入。
(在宣告元件ID或物件名稱時，盡量避免跟物件類別相同，Studio有時會誤判成SDK內建的元件或其他東西，可以加個_或減號-，能簡單分辨更好)   

在Activity中(.java)，首先建立TabHost物件並連結畫面元件:
```java
TabHost _tabHost;
_tabHost = (TabHost)findViewById(R.id.tab_host);
```
初始化 (setup())，然後依序加入每個Tab(我幫每個標籤的樣式另外定義成有圖片[icon]與文字[text]的custom_tab.xml):  
```java
tabHost.setup(); //官方文件說若是用findViewById來寫，要在加入tab前呼叫此方法

//=== Each tab【標籤名label/標籤顯示文字title/顯示圖片ID iconId/標籤畫面ID contentId(每一個tab的Layout檔名R.layout.xxx)】========
View tab = LayoutInflater.from(this).inflate(R.layout.custom_tab, null);
ImageView image = (ImageView) tab.findViewById(R.id.icon); //圖片
image.setImageResource(iconId);                           //匯入圖片資源
TextView text = (TextView) tab.findViewById(R.id.text);    //文字
text.setText(title);                                      //文字標題
TabHost.TabSpec spec = _tabHost.newTabSpec(label).setIndicator(tab).setContent(contentId);
_tabHost.addTab(spec);
//===========================================================================================================================
```

custom_tab.xml的內容:  
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:paddingTop="5dp"
    android:paddingBottom="5dp"
    android:orientation="vertical" >
    <ImageView
        android:id="@+id/icon"
        android:layout_width="wrap_content"
        android:layout_height="30dp"
        android:layout_gravity="center" />
    <TextView
        android:id="@+id/text"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:layout_gravity="bottom"
        android:textSize="20sp"/>
</LinearLayout>
```
補充:我希望在標籤列呈現是有選取與未選取是不一樣的效果(顏色或其他)，以文字為例，可以在TextView加上background屬性寫上"@drawable/text_color"  

text_color.xml定義為一個drawable，範例如下:
```XML
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 點下去的時候 -->
    <item
        android:state_selected="true"
        android:color="#ffffff"/>

    <!-- 沒點下去的時候 -->
    <item android:color="#888888"/>
</selector>
```
若要針對圖片顏色、長相做變化也可用同樣方式，關鍵就是selector內要有兩個item，item的state_selected屬性決定選取與否不同的樣子，預設是false
