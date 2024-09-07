public class RequiredFieldsHelper {

    // Method to find required fields for a given sObject type (e.g., 'Account')
    public static List<String> getRequiredFields(String sObjectName) {
        List<String> requiredFields = new List<String>();
        
        // Get global describe for all objects and retrieve the specific object type
        Schema.SObjectType sObjectType = Schema.getGlobalDescribe().get(sObjectName);
        
        // Check if the object exists
        if (sObjectType == null) {
            System.debug('Invalid sObject name: ' + sObjectName);
            return requiredFields;
        }

        // Get the describe result for the object
        Schema.DescribeSObjectResult describeResult = sObjectType.getDescribe();
        
        // Loop through each field
        for (Schema.SObjectField field : describeResult.fields.getMap().values()) {
            
            // Get the describe result for the field
            Schema.DescribeFieldResult fieldDescribe = field.getDescribe();
            
            // Check if the field is required (non-nillable and not defaulted on create)
            if (!fieldDescribe.isNillable() && !fieldDescribe.isDefaultedOnCreate()) {
                requiredFields.add(fieldDescribe.getName());
            }
        }

        return requiredFields;
    }
    
    // Helper method to log required fields
    public static void logRequiredFields(String sObjectName) {
        List<String> requiredFields = getRequiredFields(sObjectName);
        System.debug('Required Fields for ' + sObjectName + ': ' + requiredFields);
    }
}







requiredfieldshelper.logrequiredfields('account');
