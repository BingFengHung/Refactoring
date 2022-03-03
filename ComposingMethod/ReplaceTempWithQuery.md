# Replace Temp with Query
將函式中的區域變數變成一個查詢函式

````cs
double CalculateTotal() {
   double basePrice = quantity * itemPrice;

   if (basePrice > 1000) {
      return basePrice * 0.95;
   } else {
      return basePrice * 0.98;
   }
}
````

改為

````cs
double BasePrice() {
   return quantity * itemPrice;
}
double CalculateTotal() {
   if (BasePrice() > 1000) {
      return BasePrice() * 0.95;
   } else {
      return BasePrice() * 0.98;
   }
}
````

如果在一個類別中，有很多地方重複使用到相同的臨時變數，會導致
類別中的函式每一個有用到的地方，都會多一行臨時變數的表達式，
將導致類別的程式碼會變長。

因此，將臨時變數的表達式抽離出來為獨立的方法，只在有需要使用到的地方
呼叫查詢方法，可以有效的簡短類別的長度；也可以後續如果有需要修改，查詢
函式的邏輯時，只需要改其方法邏輯即可，不需要在每一段有使用到臨時變數
的地方都去修改。
