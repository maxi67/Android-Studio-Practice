# Button's Action (Click) #
說到Android Studio，在UI上最常用也最基本的元件，絕對非按鈕莫屬  

我們在畫面佈局檔(Layout xml)上擺了按鈕元件，如果不加上動作程式會沒有任何效果  
而以點擊事件(Click)為例的動作程式，撰寫方式最基本有兩種 

## 1.用元件onClick屬性 ##
在layout檔布局時，打上以下的宣告:  
```XML
      android:onClick="functionName"  
```
接著在activity內(.java)，宣告該function名的函式(參數:View型別的變數)即可，如:  
```Java
      public void functionName(View view){
        //點擊按鈕後會執行的動作
      }
```

## 2.用OnClickListener監聽器 ##
假設有一個Button要定義事件，它的id叫btn，我們在activity先宣告一個Button型別的變數，並透過findViewById取得它的元件，
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
除了點擊事件以外，還有諸如長按(LongClick)、碰觸(OnTouch元件被點擊或放開都會觸發)，也都可以用這種方式宣告
