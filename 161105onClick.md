# Button's Action (Click) #
說到Android Studio  
在UI上最常用也最基本的元件  
非按鈕莫屬  

我們在畫面佈局檔(Layout xml)上  
擺了按鈕元件，如果不加上動作程式會沒有任何效果  
所以以下簡述可以如何撰寫  

## 1.用元件onClick屬性 ##
在layout檔布局時，打上以下的宣告:  
```XML
      android:onClick="functionName"  
```
接著在activity程式碼內(java檔)，宣告該function名的函式(參數定義一個View型別的變數)即可  

## 2.用OnClickListener監聽器 ##
假設有一個Button要定義事件，它的id叫btn  
我們在activity先宣告一個Button型別的變數  
並透過findViewById取得它的元件  
就可以利用變數註冊監聽器，賦予該按鈕事件動作  
```Java
      Button _btn = (Button)findViewById(R.id.btn);
      _btn.setOnClickListener(new OnClickListener(){
      
        @override
        public void onClick(View v){
          //點擊按鈕後會執行的動作
        }
      };
```
