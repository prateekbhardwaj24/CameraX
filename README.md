# Higher Order Function & Lambdas In Kotlin
--------

In Kotlin, **higher-order functions** are special types of functions that **can take other functions as parameters or return functions as results.** It's like treating functions as values that can be passed around and manipulated just like any other data.

-- Here we will understand the variations of higher order fucntions with simple examples.

## Example : 1
- Let's assume you are performing long running task like - Fetching api response/ doing heavy calculation and you want the the response when it's done **without using LiveData** .

  ```kotlin
        fun getCallbackAfterDelay(response: (String) -> Unit) {
            delay(2000) // will block thread for 2000 miliseconds //
            response("Time Up")
        }

#### Working ->
- **getCallbackAfterDelay** method get a parameter which of type function which returns string. Let's understand more - 

- **response: (String)** is a parameter/**lambda function** in getCallBackAfterDelay method which is referenced where this method called.

- **-> Unit** is indicating the return type of lambda function, unit will not give any value but you can use - Int,String etc.

- **Basic syntax & implementation**

  ```kotlin
       getCallbackAfterDelay { response ->
            // Here response is "Time Up" which is returned from getCallBackAfterDelay method

            Log.d(javaClass.simpleName, response)
            binding?.textLive?.text = response
        }
- If you have only 1 lambda function in method, Then yoiu do not need to specify the lambda name as **response** because by default lambda named as **it** and which also specifies the result returned from callback method like below.

  ```kotlin
       getCallbackAfterDelay { 
            // Here response is "Time Up" which is returned from getCallBackAfterDelay method

            Log.d(javaClass.simpleName, it)
            binding?.textLive?.text = it
       }


-------------------
------

## Example : 2 
- Now suppose you want to get two response from lambda function then how to achieve it,

    -- Let's make a method which returns even,odd value 

  ```kotlin
        fun getTwoParamsInCallback(response: (String,Int) -> Unit) {
                if(Random.nextInt().mod(2) == 0) {
                    response("Even",1)
                } else {
                    response("Odd",2)
                }
        }

#### Working -> 
- **Random.nextInt()**  will generate random number and mod(2) will calculate weather the number is divisible by 2 or not.

- Acc. to the above if else statements, response method is called with two parameters like : response("Even", 1) & response("Odd", 2).

- **Basic syntax & Implementation**

  ```kotlin
        getTwoParamsInCallback { stringValue, intValue ->
            // Similarly We can have multiple values in the same order described in callback
            Log.d(javaClass.simpleName, "$stringValue , $intValue")
        }

-------------------
------

## Example : 3
- Now if you want to return some value from from lambda function, suppose you have method **returnValueOfMethod(response: (Int) -> Int)**, This will retunr the response of **Int** type instead of **Unit** type.

  ```kotlin
        fun returnValueOfMethod(response: (Int) -> Int): Int {
            /* 
            - response took paramter of type Int as well as retun type Int,
            - But you can return any type like String, Float etc.
            - Hence returnValueOfMethod method will have to return Int type due to lamba function (response) Int return type.
            */

            return response(5)
        }

#### Working -> 
- **response** took paramter of type Int as well as return type Int, But you can return any type like String, Float etc.
- Hence, **returnValueOfMethod** method will **have to return Int type** due to **lamba function (response) Int return type**.

- **Basic syntax & Implementation**

  ```kotlin
        val data : Int = returnValueOfMethod { response ->

        // Here response is 5 (passed in lambda function call)
        // You can have some other calculation based on requirement here, like -

                val newResponse = response * 10
                 // Last line should only be Int type , because last line code statements will be returned to **data** varibale.
               
                newResponse // returning Int value
        }

        Log.d(javaClass.simpleName, data.toString())
        //This will print 50.

-------------------
------

## Example : 4, Pass one simple and lambda function as paramter
- Suppose, If you want to pass some simple variable paramters for calculation and a lambda function for getting response after calculation Then,

  ```kotlin
        fun printResult(number: Int, operation: (Int) -> Int) {
            val result = operation(number)
            println("The result is: $result")
        }
- Let's say you have a function called **printResult()** that takes an integer parameter **number** and a lambda function **operation** as arguments. The lambda function performs some computation on the integer parameter and returns a result.

#### Working ->
- Now, you can call the **printResult()** method and pass an integer value along with a lambda function that specifies the computation to be performed. In this example, the lambda function doubles the input number.

  ```kotlin
        printResult(5) { x -> x * 2 }

- Here, the lambda function **(x -> x * 2)** takes an input parameter x and returns x multiplied by 2.

- Hence, The after running code, **The result is:10**
  
-------------------
-------------------------
------

## Thank you for reading this article, If you found it helpful please join us on discort and youtube for more android articles and videos.
- Youtube Channel [https://youtube.com/@AndroidTechTricks_]
- Discord Channel [https://discord.gg/C7uU27wr]
