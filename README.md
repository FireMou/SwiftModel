# SwiftModel
Dictionary to model. write in swift

- 一个简单的字典转模型框架（A simple framework for dictionary to model）

###1.怎么使用它呢？（How to use it?）
- 在上传的文件中，有一个NSObject的分类“NSObject+Model”，将这个文件加入到你的工程中就可以使用了
- In the files which is upload, There is a file named "NSObject+Model", it's a categpry for "NSObject", just add it in your project,then you can use it.

###2.字典转模型的方法（The function for dictionarty to model）
- 在这个分类中有两个方法可以用于字典转模型，一个传入一个字典来转换成模型，另一个则是传入字典数组转换成模型数组
- This category have two function for dictionary to model. The one, it needs you transfer a dictionary,then it make a model return to you.The other one, it needs you transfer a dict's array, then it make a model's array return to you

####class func objectWithDictionary(dict:[String : AnyObject]) -> NSObject
- 直接使用你的模型类调用这个方法，传入字典返回模型，例子在工程中。
- Use this function with your model class, transfer a dictionary return a model, the example in the project

####class func objectArrayWithDictionaryArray(array:NSArray) -> [AnyObject]
- 用法与上一个方法类似，不同的是传入一个字典数组返回一个模型数组
- Use it like the previous function, The different is you have to transfer a dictionary's array and return a model's array to you


##注意（Attention）
* 在这个文件中，你需要注意这三个方法，这关系着你的转化是否成功
* In this file, you need to notice those function, because it's about your operation is success or fail

####第一个方法（The First Function）
```
    // MARK: - 模型中有个数组属性，数组里面又要装着其他模型 (子类重写)    
    func objectClassInArray() -> [String : AnyClass]? {
        return nil
    }
```
* 如果在你的自定义类中，有一个或多个数组，并且这个数组中的元素依旧是自定义的，那么你需要使用这个方法来告诉它，你数组中的是那种自定义类，在模型类中重写这个方法
* if you have one or more array in your custom class, and the element in this array also belong a custom class, then you have to use this function to tell it which custom class in your array,override it in your custom class


####第二个方法（The Second Function）
```

    // MARK: - 模型中的属性名和字典中的key不相同（子类重写）
    class func replacedKeyFromVariableName() -> [String : String]? {
        return nil
    }

```
* 如果在你的自定义类中，变量名和字典中的key不相同，那么使用这个方法告诉它被替换的key是什么
* if in your custom class,the variable name is different to the key in dictionary, you can use this function return the key which is replaced


####第三个方法（The Third Function）
```

    // MARK: - 模型中包含其他自定义模型，通过该方法返回自定义类类名（子类重写）
    class func customClassForVariableName() -> [String : AnyClass]? {
        return nil
    }

```
* 如果在你的模型类中的属性类别属于其他的模型类，那么用这个方法来告诉它其他的模型类是什么类型，因为我是使用Ivar来获取的成员变量，但是不知道怎么获取成员的类型，所以...，class_getProperty方法获取不完全，如果谁知道通过Ivar怎么获取成员变量类名，请告诉我。
* if in your custom class,there is one or more variable's class is other custom class, you need use this function return the class of "other custom class".Because I trough Ivar to get variable,but I don't know how to get the variable's class, so..., if through "class_getProperty" function, it can not get all variable.if you know, please tell me

##注意2（Attention2）
* 如果你的模型类变量中，有Bool,Int,Float...基础类型,那么你需要在你的模型类中重写下面的这个方法来进行赋值，否则就会崩溃
* if those variables in your custom class,include basic type like "Bool""Int""Float"..., you need override the function under these word, otherwise, it will be crash

```

    override func setValue(value: AnyObject?, forUndefinedKey key: String) {
    	// Bool
        male = (value as! Int) != 0
    }
    
```
* 如果在自定义类中一个以上的基础类型的变量，你需要通过判断key进行赋值。最好不要使用这些基础类型
* if there have more than one variable is basic type, then you need judge through the "key" to assign. The best way is don not use these basic type
