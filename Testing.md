Map<String, Schema.SObjectType> schemaMap = Schema.getGlobalDescribe(); 

// Get the SObjectType for the Account (replace 'Account' with the desired object)
Schema.SObjectType sObjectType = schemaMap.get('Opportunity'); 

// Get the describe result for the sObject
Schema.DescribeSObjectResult describeResult = sObjectType.getDescribe(); 

// Iterate through the fields and check for required fields
for (Schema.SObjectField field : describeResult.fields.getMap().values()) {
    
    // Use getDescribe to retrieve the describe result for the field
    Schema.DescribeFieldResult fieldDescribe = field.getDescribe();

    // Check if the field is required (non-nillable)
    if (!fieldDescribe.isNillable()) {
        System.debug('Required Field: ' + fieldDescribe.getName()); 
    }
}

