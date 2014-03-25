JSONRulesChecker
=======================
This is small library for validation JSON objects in PHP.

INSTALLATION
------------
Please update your composer.json. Add this to your **require** section
```
"krydos/json-rules-checker":"dev-master"

```

WHY DO I NEED THIS
-------------

Very often I have a code like this:
```php
try {
    $json = getJsonFromAnyPlace();
    if(isset($json->attr1)) {
        // do something with $json->attr1
        
        if(isset($json->attr2)) {
            //do something with $json->attr2
        }
        else {
            throw new Exception('attr2 required');
        }
    }
    else {
        throw new Exception('attr1 required');
    }
}
catch(Exception $e) {
    // do something
}
```
I really don't like it. I write this library because I want to validate JSON using some rules.

Like that:
```php
try {
    $json = getJsonFromAnyPlace();
    // let's imagine that JSON looks something like this:
    // {"root":{"attr1":"value1", "attr2":"value2"}}
    
    // let's write a rules
    $rules = array(
        'root' => array(
            'attr1' => '<string>',
            'attr2' => '<string>'
        )
    );
    
    $validation_result = \JSONRulesChecker\JSONChecker::checkJSON($json, $rules); // return true
    if(!$validation_result) {
        throw new Excpetion('Please check you params');
    }
}
catch(Exception $e) {
    //do something
}
```

I like it :)
Please feel free to Pull Requests

<3
