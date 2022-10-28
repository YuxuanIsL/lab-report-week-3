# This is my week 3 lab report

## Part One - SearchEngine

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class SearchEngine{
    public static void main(String[] args) throws IOException{
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}

class Handler implements URLHandler{

    ArrayList<String> strs = new ArrayList<>();

    public String handleRequest(URI url){

        if(url.getPath().equals("/")){
            return strs.toString();
        }

        if(url.getPath().contains("/add")){
            String[] inputStrs = url.getQuery().split("=");
            if (inputStrs[0].equals("s")){
                strs.add(inputStrs[1]);
                return inputStrs[1]; 
            }
        }

        if(url.getPath().contains("/search")){
            String[] inputStrs = url.getQuery().split("=");
            ArrayList<String> result = new ArrayList<>();
            String toSearch = inputStrs[1];
            for(String str: strs){
                if(str.toLowerCase().contains(toSearch.toLowerCase())){
                    result.add(str);
                    System.out.print(str);
                }
            }
            return result.toString();

        }
        return "404 not found";
    }
}
```

Here I am adding new strings to the original arraylist of strings, so I am calling `/add`.


![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/add%20apples.png)

`strs` is defautly an empty ArrayList. 

When I type `/add?=apple` in the URL on the browser, I am calling the action in line 26 in the code. 

`/add?s=apple` what is after `?` is read as `String[] inputStrs` and will be splitted by `=`, so `inputStrs[0]` becomes `s`.

Line 28 becomes true, then strs added `apple` since it is `inputStrs[1]`.

![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/add%20pears.png)

When I type `/add?=pears` in the URL on the browser, I am calling the action in line 26 in the code. 

`/add?s=pears` what is after `?` is read as `String[] inputStrs` and will be splitted by `=`, so `inputStrs[0]` becomes `s`.

Line 28 becomes true, then strs added `pears` since it is `inputStrs[1]`.

![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/add%20pineapple.png)

When I type `/add?=pineapple` in the URL on the browser, I am calling the action in line 26 in the code. 

`/add?s=pineapple` what is after `?` is read as `String[] inputStrs` and will be splitted by `=`, so `inputStrs[0]` becomes `s`.

Line 28 becomes true, then strs added `pineapple` since it is `inputStrs[1]`.


As a result, the array list is now `{apples, pears, pineapple}`.



**Then, I am going to search for strings that have `apple`.**

![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/search%20for%20apples.png)

Here I am calling line 33 in my code by typing `/search?s=apple`, so that line 33 becomes `true` and continues the `if` statement.

What is after `?` is read as `String[] inputStrs` and will be splitted by `=`, so `inputStrs[0]` becomes `s`.

Then `inputStrs[1]` becomes `apple`.

`apple` is passed to `toSearch`

`str` loops for `apples`, `pears`, `pineapple` in `strs`

and `result` stores the answer as `{apples, pineapple}`

Finally, we make it Strings to return.

## Part Two - Debugging
**In `ArrayExample.java`, I will be writing `ReverseInPlace` method.**
Failure-inducing method is:
![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/%E5%9B%BE%E7%89%87%201.png)

The symptom is 
![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/%E5%9B%BE%E7%89%87%202.png)

The fixed code is
![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/%E5%9B%BE%E7%89%87%203.png)

Problems in code: It fails to make the correct exchange and fails to loop through every index.
So when it loops to index[1] which is 2, it fails to set the exchange.


**In ListExample.java, I will be writing `filter` method.**
Failure inducing method is:
![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/testFilter%20failure-inputting%20code.png)

The symtom is
![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/testFilter%20%20symptom%20.png)

The fixed code is
![image](https://github.com/YuxuanIsL/lab-report-week-3/blob/main/filter%20fixed.png)

It fails to do its work because if the `index 0` is deleted, it will always add `s` to `index 0`. 
