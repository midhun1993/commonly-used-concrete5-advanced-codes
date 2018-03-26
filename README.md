# commonly used concrete5 advanced codes

### *concrete5.7.0 - concrete5.7.5.13*

### 1. Get select attribute options 
```
   // Fetch attribute key object using attribute handle, you can replace "test_attribute" with your handle;
   $attibute_key = Concrete\Core\Attribute\Key\CollectionKey::getByHandle('test_attribute');

   // Fetch Attribute Type object
   $attribute_type = Concrete\Core\Attribute\Type::getByHandle("select");

   // Fetch Attribute Type controller object
   $type_controller =  new  Concrete\Attribute\Select\Controller($attribute_type);

   $type_controller->setAttributeKey($attibute_key);

   $options = $type_controller->getOptions()->getOptions();

   foreach ($options as $key => $option) {
   
     //echo ID
     echo $option->ID;
     
     //echo option value/display values
     echo $option->value;
     
   }
   ```
