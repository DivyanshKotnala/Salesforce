# Find all the necessary Feild

Use it in ctrl +e ;

String sObjectName = 'Appointment__c';
List<String> requiredFields = new List<String>();
Schema.SObjectType sObjectType = Schema.getGlobalDescribe().get(sObjectName);
   
if (sObjectType == null) {
    System.debug('Invalid sObject name: ' + sObjectName);
    
}

Schema.DescribeSObjectResult describeResult = sObjectType.getDescribe();
for (Schema.SObjectField field : describeResult.fields.getMap().values()) {
   Schema.DescribeFieldResult fieldDescribe = field.getDescribe();
       if (!fieldDescribe.isNillable() && !fieldDescribe.isDefaultedOnCreate()) {
                requiredFields.add(fieldDescribe.getName());
            }
        }
System.debug('Required Fields for ' + sObjectName + ': ' + requiredFields);
    
