# SwiftModel
Dictionary to model. write in swift

- 一个简单的字典转模型框架（A simple framework for dictionary to model）

#目录
###[说明（explain）](#explain)
###[1.怎么使用它呢？（How to use it?）](#useit)
###[2.字典转模型的方法（The function for dictionarty to model）](#function)
* [字典转模型（dictionary to model）](#dict2model)
* [字典数组转模型数组（dictionary array to model array）](#dictarray2modelarray)

###[注意（Attention）](#attention)
* [第一个方法（The First Function）](#firstfunc)
* [第二个方法（The Second Function）](#secondfunc)
* [第三个方法（The Third Function）](#thirdfunc)

###[注意2（Attention2）](#attention2)
###[代码（The code）](#wantcode)
* [1.Person.swift](#person)
* [2.Car.swift](#car)
* [3.Computer.swift](#computer)
* [4.Factory.swift](#factory)
* [5.CPU.swift](#cpu)
* [6.ViewController.swift](#controller)

# <a id="explain"></a>说明（explain）
- 我不知道为什么我没有办法上传工程文件了，我试过了所有我知道的办法，在github网站上上传的时候，它提示我“Something went really wrong, and we can’t process that file.”，我不知道为什么，如果有谁知道怎么解决的话，请告诉我。所以，我会在末尾附上Demo的代码，[想看代码](#wantcode)
- I don't know why I can't upload any files,I've tried all ways what I know,When I upload the files on the github website,It prompted me"Something went really wrong, and we can’t process that file.",I do not know why, if anyone know how to solve it, please tell me. So, I will attach the code of Demo at the end.[want to watch the code](#wantcode)

#<a id="useit"></a>1.怎么使用它呢？（How to use it?）
- 在上传的文件中，有一个NSObject的分类“NSObject+Model”，将这个文件加入到你的工程中就可以使用了
- In the files which is upload, There is a file named "NSObject+Model", it's a categpry for "NSObject", just add it in your project,then you can use it.

#<a id="function"></a>2.字典转模型的方法（The function for dictionarty to model）
- 在这个分类中有两个方法可以用于字典转模型，一个传入一个字典来转换成模型，另一个则是传入字典数组转换成模型数组
- This category have two function for dictionary to model. The one, it needs you transfer a dictionary,then it make a model return to you.The other one, it needs you transfer a dict's array, then it make a model's array return to you

###<a id="dict2model"></a>字典转模型（dictionary to model）

```
class func objectWithDictionary(dict:[String : AnyObject]) -> NSObject
```
- 直接使用你的模型类调用这个方法，传入字典返回模型，例子在工程中。
- Use this function with your model class, transfer a dictionary return a model, the example in the project

###<a id="dictarray2modelarray"></a>字典数组转模型数组（dictionary array to model array）

```
class func objectArrayWithDictionaryArray(array:NSArray) -> [AnyObject]
```
- 用法与上一个方法类似，不同的是传入一个字典数组返回一个模型数组
- Use it like the previous function, The different is you have to transfer a dictionary's array and return a model's array to you


#<a id="attention"></a>注意（Attention）
* 在这个文件中，你需要注意这三个方法，这关系着你的转化是否成功
* In this file, you need to notice those function, because it's about your operation is success or fail

###<a id="firstfunc"></a>第一个方法（The First Function）
```
    // MARK: - 模型中有个数组属性，数组里面又要装着其他模型 (子类重写)    
    func objectClassInArray() -> [String : AnyClass]? {
        return nil
    }
```
* 如果在你的自定义类中，有一个或多个数组，并且这个数组中的元素依旧是自定义的，那么你需要使用这个方法来告诉它，你数组中的是那种自定义类，在模型类中重写这个方法
* if you have one or more array in your custom class, and the element in this array also belong a custom class, then you have to use this function to tell it which custom class in your array,override it in your custom class


###<a id="secondfunc"></a>第二个方法（The Second Function）
```

    // MARK: - 模型中的属性名和字典中的key不相同（子类重写）
    class func replacedKeyFromVariableName() -> [String : String]? {
        return nil
    }

```
* 如果在你的自定义类中，变量名和字典中的key不相同，那么使用这个方法告诉它被替换的key是什么
* if in your custom class,the variable name is different to the key in dictionary, you can use this function return the key which is replaced


###<a id="thirdfunc"></a>第三个方法（The Third Function）
```

    // MARK: - 模型中包含其他自定义模型，通过该方法返回自定义类类名（子类重写）
    class func customClassForVariableName() -> [String : AnyClass]? {
        return nil
    }

```
* 如果在你的模型类中的属性类别属于其他的模型类，那么用这个方法来告诉它其他的模型类是什么类型，因为我是使用Ivar来获取的成员变量，但是不知道怎么获取成员的类型，所以...，class_getProperty方法获取不完全，如果谁知道通过Ivar怎么获取成员变量类名，请告诉我。
* if in your custom class,there is one or more variable's class is other custom class, you need use this function return the class of "other custom class".Because I trough Ivar to get variable,but I don't know how to get the variable's class, so..., if through "class_getProperty" function, it can not get all variable.if you know, please tell me

#<a id="attention2"></a>注意2（Attention2）
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

# <a id="wantcode"></a> 代码（The code）

###<a id="person"></a>1.Person.swift

```
import UIKit

class Person: NSObject {
    
    var name:String?
    var age:NSNumber?
    var male:Bool?
    var computer:Computer?
    var cars:[Car]?
    var friends:[NSString]?
    
    
    override func objectClassInArray() -> [String : AnyClass]? {
        return ["cars":Car.classForCoder()]
    }
    
    override class func customClassForVariableName() -> [String : AnyClass]? {
        return ["computer":Computer.classForCoder()]
    }
    
    override func setValue(value: AnyObject?, forUndefinedKey key: String) {
        male = (value as! Int) != 0
    }
    
    
    override var description: String {
        return "Person:  name=\(name), age=\(age), male=\(male), computer=\(computer), cars=\(cars), friends=\(friends)"
    }
    
}
```
###<a id="car"></a>2.Car.swift

```
import UIKit

class Car: NSObject {
    
    var ID:String?
    var wheels:Int?
    var using:Bool?
    
    override class func replacedKeyFromVariableName() -> [String : String]? {
        return ["ID":"id"]
    }
    
    override func setValue(value: AnyObject?, forUndefinedKey key: String) {
        
        if key == "wheels" {
            wheels = value as? Int
        }else{
            using = (value as! Int) != 0
        }
    }
    
    override var description: String {
        return "Car:  ID=\(ID), wheels=\(wheels), using=\(using)"
    }
    
}
```
###<a id="computer"></a>3.Computer.swift
```
import UIKit

class Computer: NSObject {
    var price:NSNumber?
    var brand:String?
    
    override var description: String {
        return "Computer:  price=\(price), brand=\(brand)"
    }
    
}
```
###<a id="factory"></a>4.Factory.swift
```
import UIKit

class Factory: NSObject {
    var address:String?
    var name:String?
    
    
    override var description: String {
        return "Factory:  address=\(address), name=\(name)"
    }
}
```
###<a id="cpu"></a>5.CPU.swift

```
import UIKit

class CPU: NSObject {
    var core:NSNumber?
    var category:String?
    var version:String?
    
    
    override var description: String {
        return "CPU:  core=\(core), category=\(category), version=\(version)"
    }
}
```
###<a id="controller"></a>6.ViewController.swift

```
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        
        
        let dict = [
            "name": "张三",
            "age": 21,
            "male":true,
            "computer": [
                "factory": [
                    "address": "BeiJing",
                    "name": "Lenovo"
                ],
                "CPU": [
                    "core": 8,
                    "category": "game",
                    "version": "i5"
                ],
                "brand":"ThinkPad",
                "price":7550
            ],
            "friends":[
                "rose",
                "jack",
                "jobs",
                "cook",
                "李四"
            ],
            "cars":[
                [
                    "id": "1",
                    "wheels": 4,
                    "using":false
                ],
                [
                    "id": "2",
                    "wheels": 4,
                    "using":false
                ],
                [
                    "id": "3",
                    "wheels": 4,
                    "using":false
                ]
            ]
        ]
        
        
        
        let person = Person.objectWithDictionary(dict) as? Person
        
        print(person)
        
    }
    
}
```
- 添加NSObjec+model.swift并且拷贝这些代码到你的工程中，并运行起来，这个数据结构也不是很简单的了，绝对能够满足大家的需求
- Add the file named "NSObject+Model.swift" and copy the code to your project,and run it.The data structure in my project is not very simple,This framework is absolutely able to meet the needs of everyone.


