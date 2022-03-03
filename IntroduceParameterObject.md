# Introduce Parameter Object
在方法中的參數太多，直接使用一個參數物件來代替

透過將參數整合到單一類別中，可以將用於處裡此數據的方法
也移動到這個類別中，讓在原本類別的方法釋放出來。

````cs
class Entry
{
   public double Value {get; private set;}
   public DateTime ChargeDate {get; private set;}

   public Entry(double value, DateTime chargeDate)
   {
     Value = value;
     ChargeDate = chargeDate;
   }
}

class Account 
{
   private List<Entry> Entries {get;set;}

   public double GetFlowBetween(DateTime start, DateTime end)
   {
      double result = 0;
      foreach(var entry in Entries)
         if (start <= entry.ChargeDate && end >= entry.ChargeDate)
            result += entry.Value;
      return result;
   }
}
````

修改後

````cs
class Entry
{
   public double Value {get; private set;}
   public DateTime ChargeDate {get; private set;}

   public Entry(double value, DateTime chargeDate)
   {
     Value = value;
     ChargeDate = chargeDate;
   }
}

class Account
{
   private List<Entry> Entries {get;set;}

   public double GetFlowBetween(DateRange range) 
   {
      double result = 0;
      foreach(var entry in Entries) 
         if (range.Includes(entry.ChargeDate))
             result += entry.Value;
      return result;
   }
}

class DateRange
{
   public DateTime Start { get;set; }
   public DateTime End {get;set;}

   public bool Includes(DateTime givenDate)
   {
      return Start <= givenDate && End >= givenDate;
   }
}

````

可以看到原本比較日期範圍的判斷式，移動到參數物件裡面。

這麼做的好處是，在原本的參數情況下，可能有很多函式都使用相同的參數，
雖然這些參數在各自的函式中處理的方式不一樣，但是相同的參數就會導致
程式碼的重複，將其整理在同一個參數物件中，會比較好管理，如果遇到像
上面的比較時，也比較有相同的執行方法，不用在自己去另外實作
。


