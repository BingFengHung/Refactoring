# Preserve Whole Object
問題點：從一個物件中取得物件的屬性值，並將這些屬性值作為參數傳入到某個方法中。
解決方式：將整個物件作為參數傳入到某個方法中。

````cs
int low = daysTempRange.GetLow();
int high = daysTempRange.GetHigh();
bool withinPlan = plan.WithinRange(low, high);
````

修改為

````cs
bool withinPlan = plan.WithinRange(daysTempRange);
````

傳入整個物件的好處是，用戶端可以從物件身上取得的資料變多。

優點：
> 省去了要傳一大串參數給方法，直接一個物件傳入即可
> 當方法需要物件的其他屬性值時，很方便的就可以運用。

缺點：
> 方法變得比就沒那麼彈性，因為參數就限制在傳入的物件，沒辦法再從其他地方傳入參數


