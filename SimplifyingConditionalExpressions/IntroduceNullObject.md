# Introduce Null Object
十幾次的對 null 做檢查，讓你的程式碼變得更長更醜陋。

````cs
if (customer == null)
{
   plan = BillingPlan.Basic();
}
else 
{
   plan = customer.GetPlan();
}
````

改為

````cs
public sealed class NullCustomer: Customer
{
   public override bool IsNull
   {
      get { return true;}
   }

   public override Plan GetPlan()
   {
      return new NullPlan();
   }

   // Some other NULL functionality.
}

// Replace nul value with Null-object.
customer = order.customer ?? new NullCustomer();

// Use Null-object as if it's normal subclass.
plan = customer.GetPlan();
````
