```
- An APEX class for Project Orders:
```
public class ProjectOrderManager {
    public static ID addProjectOrder(Date DatetoInsert, String NameToInsert) {
        Project_Order__c orderToAdd = new Project_Order__c(Date_Ordered__c = DatetoInsert, Name=NameToInsert);
        insert(orderToAdd);
        System.debug('orderToAdd recordID is: ' + orderToAdd.Id);
        return orderToAdd.Id;
    }
}

```
- An APEX class for Project Order Details:
```
public class ProjectOrderDetailManager {
     public static ID addProjectOrderDetail(double costToInsert, Decimal quantityToInsert, String NameToInsert) {
        Project_Order_Detail__c orderDetailToAdd = new Project_Order_Detail__c(Total_Cost__c = costToInsert, Quantity__c = quantityToInsert, Name=NameToInsert);
        insert(orderDetailToAdd);
        System.debug('orderDetailToAdd recordID is: ' + orderDetailToAdd.Id);
        return orderDetailToAdd.Id;
    }
}

```
- An APEX class for Project Products:
```
public class ProjectProductManager {
      public static ID addProjectProduct(String DescriptionToInsert, Decimal InventoryToInsert, String NameToInsert) {
        Project_Product__c productToAdd = new Project_Product__c(Description__c = DescriptionToInsert, Inventory__c = InventoryToInsert, Name=NameToInsert);
        insert(productToAdd);
        System.debug('productToAdd recordID is: ' + productToAdd.Id);
        return productToAdd.Id;
    }
}

```
- An APEX trigger for Project Products Inventory:
```
trigger ProjectOrderDetailTrigger on Project_Order_Detail__c (before 
    insert,  before update) {
    if (trigger.isBefore) {
        if (trigger.isUpdate || trigger.isInsert) {
            for (Project_Order_Detail__c po :trigger.new) {
                if (po.Quantity__c > po.Project_Product__r.Inventory__c) {
                    po.addError('Quantity exceeds inventory');
                }
            }
        }
    }
}

```
- An APEX trigger for Project Products Inventory subtraction:

trigger InventoryTrigger on Project_Order_Detail__c (after insert,  after update) {
    if (trigger.isAfter) {
        if (trigger.isUpdate || trigger.isInsert) {
            for (Project_Order_Detail__c po :trigger.new) {
                po.Project_Product__r.Inventory__c = po.Project_Product__r.Inventory__c - po.Quantity__c;
            }
        }
    }
}
```
