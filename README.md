# Commonly used concrete5 advanced codes

### *concrete5.7.0 - concrete5.7.5.13*

### 1. Get select attribute options 
```
<?php
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
 
 ### *concrete5.8.0*
 
 ### 1. Get all files inside a file manager folder programmatically
 _For more info please refer this link  https://stackoverflow.com/questions/46924783/concrete5-cms-get-all-file-inside-a-file-manager-folder-programmatically_
```
<?php
use Concrete\Core\Tree\Node\Type\FileFolder;
use Concrete\Core\File\FolderItemList;

// First grab the folder object
$folder = FileFolder::getNodeByName('Testing Folder');

if (is_object($folder)) {
    $files = [];
    // if we have a folder we need to grab everything inside and then
    // recursively go through the folder's content
    // if what we get is a file we list it
    // otherwise if it's another folder we go through it as well
    $walk = function ($folder) use (&$files, &$walk) {
            $list = new FolderItemList();
            $list->filterByParentFolder($folder);
            $list->sortByNodeName();
            $nodes = $list->getResults();

            foreach ($nodes as $node) {
                if ($node->getTreeNodeTypeHandle() === 'file'){
                    $files[] = $node->getTreeNodeFileObject();
                } elseif ($node->getTreeNodeTypeHandle() === 'file_folder'){
                    $walk($node);
                }
            }
        };
    $walk($folder);

    // we are done going through all the folders, we now have our file nodes
    foreach ($files as $file) {
        echo sprintf('%sfile name is %s and URL is %s%s', '<p>', $file->getTitle(), $file->getURL(), '</p>');
    }
}
```
