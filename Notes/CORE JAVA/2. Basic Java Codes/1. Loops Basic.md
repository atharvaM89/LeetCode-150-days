# Basic

## 1. Day On Number

```java
package dayonnumber;
import java.util.*;
public class DayOnNumber 
{
    public static void main(String[] args) 
    {
      int y;
      System.out.println("Enter the no of Day-");
      Scanner sc=new Scanner(System.in);
      y=sc.nextInt();
      
      if(y==1)
      {
          System.out.println("The Day is Monday");
      }
      else if(y==2)
      {
          
          System.out.println("The Day is Tuesday");
      }
      else if(y==3)
      {
          System.out.println("The Day is Wednesday");
      }
      else if(y==4)
      {
          System.out.println("The Day is Thrusday");
      }
      else if(y==5)
      {
          System.out.println("The Day is Friday ");
      }
      else if(y==6)
      {
          System.out.println("The Day is Saturday");
      }
      else if(y==7)
      {
          System.out.println("The Day is Sunday");
      }
      else if(y>7)
      {
          System.out.println("Enter a Vaild no Between 1 to 7");
      }
    }
    
}

```

## 2. Day Switch

```java
package dayswitch;
import java.util.*;
public class DaySwitch
{
    public static void main(String[] args)
    {
        int Day;
        System.out.println("Enter the Number of Day-");
        Scanner sc=new Scanner(System.in);
        Day=sc.nextInt();
        
        switch(Day)
                {
            case 1: System.out.println("monday");
            break;
            case 2: System.out.println("Tues");
            break;
            case 3: System.out.println("Wed");
            break;
            case 4: System.out.println("Thursday");
            break;
            case 5: System.out.println("Friday");
            break;
            case 6: System.out.println("Sat");
            break;
            case 7: System.out.println("Sun");
            break;
            default: System.out.println("Enter the valid no");
            break;
        }
    }
    
}

```

## 3. Grade For Marks

```java
package gradesformarks;
import java.util.*;
public class GradesForMarks 
{
    public static void main(String[] args)
    {
        int Math,Chem,Phy;
        
        System.out.println("Enter the marks of Maths");
        Scanner m=new Scanner(System.in);
        Math=m.nextInt();
        
        System.out.println("Enter the marks of Chemistry");
        Scanner c=new Scanner(System.in);
        Chem=c.nextInt();
        
        System.out.println("Enter the marks of Physics");
        Scanner p=new Scanner(System.in);
        Phy=p.nextInt();
        
        int total=(Math+Chem+Phy);
        float avg=(total/3);
        
        if(avg>=70)
        {
            System.out.println("Grade is A");
        }
        else if (avg>=45 && avg<=69)
        {
            System.out.println("Grade is B");
        }
        else if(avg>=30 && avg<=44)
        {
            System.out.println("Grade is C");
        }
        else if(avg>=20 && avg<=29)
        {
            System.out.println("Grade is D");
        }
        else if(avg<=20)
        {
            System.out.println("Grade is F");
        }
    }
    
}

```

## 4. Leap Year

```java
package leapyear;
import java.util.*;
public class LeapYear 
{
    public static void main(String[] args) 
    {
        int y;
        System.out.println("Enter the Year Number-");
        Scanner sc=new Scanner(System.in);
        y=sc.nextInt();
        
        if(y%4==0)
        {
            if(y%100==0)
            {
              
                if(y%400==0)
                {
                  System.out.println("The Entered year is an Leap Year");  
                }
                else
                {
                    System.out.println("The Entered Year is not an Leap year");
                }
                
            }
            else
            {
                System.out.println("The Entered Year is not an Leap year");
            }
        }    
        else
        {
            System.out.println("The Entered Year is not an Leap year");
        }
        
    }
    
}

```

## 5. Max of Three Numbers

```java
package maxofthreeno;
public class MaxOfThreeNo 
{
    public static void main(String[] args)
    {
        int a=15,b=25,c=10;
        if(a>b && a>c)
        {
            System.out.println("A is the max no Among all");
        }
        else
        {
        if(b>c)
        {
           System.out.println("B is the Max no among all the no");
        }
        else
        {
           System.out.println("C is the max no mong all the no");
        }
        }
    }
    
}

```

## 6. Menu Sums

```java
package menusums;
import java.util.*;
public class MenuSums 
{
    public static void main(String[] args) 
    {
        System.out.println("Menu");
        System.out.println("=======");
        System.out.println("ADD");
        System.out.println("SUB");
        System.out.println("MUL");
        System.out.println("DIV");
        
        int sum1,sum2;
        String oper;
        System.out.println("Enter Two numbers-");
        Scanner sc=new Scanner(System.in);
        sum1=sc.nextInt();
        sum2=sc.nextInt();
        System.out.println("Enter Option in word");
        Scanner sd=new Scanner(System.in);
        oper=sd.nextLine();
        
        switch(oper)
        {
            case "ADD": System.out.println("Sum is="+sum1+sum2);
            break;
            case "SUB": System.out.println("Difference is="+(sum1-sum2));
            break;
            case "MUL": System.out.println("Product is="+(sum1*sum2));
            break;
            case "DIV": System.out.println("Difference is="+(sum1/sum2));
            break;
            default :System.out.println("Enter the Valid Option");
            break;
        }
        
        
    }
    
}

```

## 7. Month Number

```java
package monthnumber;
import java.util.*;
public class MonthNumber 
{
    public static void main(String[] args) 
    {
        int month;
        System.out.println("Enter the number of month -");
        Scanner sc=new Scanner(System.in);
        month=sc.nextInt();
        
        switch(month)
        {
            case 1: System.out.println("Jan");
            break;
            case 2: System.out.println("Feb");
            break;
            case 3: System.out.println("Mar");
            break;
            case 4: System.out.println("April");
            break;
            case 5: System.out.println("May");
            break;
            case 6: System.out.println("June");
            break;
            case 7: System.out.println("Jully");
            break;
            case 8: System.out.println("August");
            break;
            case 9: System.out.println("September");
            break;
            case 10: System.out.println("Octomber");
            break;
            case 11: System.out.println("November");
            break;
            case 12: System.out.println("December");
            break;
            default: System.out.println("Enter the Valid Month Number");
            break;
        }
    }
    
}

```

## 8. Odd Even

```java
package oddeven;
import java.util.*;
public class OddEven 
{
    public static void main(String[] args) 
    {
        int n;
        Scanner sc=new Scanner(System.in);
        System.out.println("Enter the number- ");
        n=sc.nextInt();
        
        if(n%2==0)
        {
          System.out.println("The Entered value is even");
        }
        else
        {
           System.out.println("Entered no is odd");
        }
        
        
    }
    
}

```

## 9. Radix

```java
package radix;
import java.util.*;
public class Radix 
{
    public static void main(String[] args)
    {
        
            String num;
        System.out.println("Enter the Number -");
        Scanner sc=new Scanner(System.in);
        num=sc.nextLine();
        
        if(num.matches("[01]+"));
        {
            System.out.println("The Entered no is Binary");
        }
        
        else if(num.matches("[0-7]+"))
                {
                System.out.println("The Entered no is octal");
                }
        else if(num.matches("[0-9]+"))
                {
                System.out.println("The Entered no is Decimal");
                }
        else if(num.matches("[0-1A-F]+"))
                {
                System.out.println("The Entered no is Hexadecimal");
                }
        
                
              
     
        
        
    }
    
}

```

## 10. Website urls

```java
package website;
import java.util.*;
public class Website 
{
    public static void main(String[] args) 
    {
        String url;
        System.out.println("Enter the url of the Website-");
        Scanner sc=new Scanner(System.in);
        url=sc.nextLine();
        
        String protocol;
        protocol=url.substring(0,url.indexOf(":"));
        
        if(protocol.equals("http"))
        {
            System.out.println("Hyper Text Transfer Protocol");
        }
        else if(protocol.equals("ftp"))
        {
            System.out.println("File Transfer Protocol");
        }
        
        String ext;
        ext=url.substring(url.lastIndexOf(".")+1);
        
        if(ext.equals("com"))
        {
            System.out.println("It is an commercial website");
        }
        else if(ext.equals("org"))
        {
            System.out.println("It is an Organizational website");
        }
    }
    
}

```

## 11. Website Type

```java
package websitetype;
import java.util.*;
public class WebsiteType 
{
    public static void main(String[] args) 
    {
        String url,ext;
        System.out.println("Enter the url of Website-");
        Scanner sc=new Scanner(System.in);
        url=sc.nextLine();
        
        ext=url.substring(url.lastIndexOf(".")+1);
        
        switch(ext)
        {
            case "com": System.out.println("It is an Commercial website");
            break;
            case "org": System.out.println("It is an Organizational website");
            break;
            case "net": System.out.println("It is an Network website");
            break;
            case "gov": System.out.println("It is an Goverment website");
            break;
            default : System.out.println("Enter the valid website");
            break;
        }
    }
    
}
```

## 12. Young or Old

```java
package youngorold;
import java.util.*;
public class YoungOrOld 
{
    public static void main(String[] args) 
    {
     int a;
     System.out.println("Enter the Age of Person-");
     Scanner sc=new Scanner(System.in);
     a=sc.nextInt();
     
     if(a<=50)
     {
         System.out.println("The person is Young");
     }
     else{
         System.out.println("The Person is Old");
     }
     
    }
    
}

```

# Loops

## 1. AP

```java
package a.p;
import java.util.*;
public class AP 
{
    public static void main(String[] args) 
    {
        System.out.println("Program to Print A.P Seires");
        System.out.println("--------------------------------------");
        System.out.println("Enter the Value of a=");
        Scanner sc=new Scanner(System.in);
        int a=sc.nextInt();
        System.out.println("Enter the Difference d=");
        Scanner sd=new Scanner(System.in);
        int d=sd.nextInt();
        System.out.println("Enter the Value of n=");
        Scanner sn=new Scanner(System.in);
        int n=sn.nextInt();
        
        int term=a;
        
        for(int i=0; i<n;i++ )
        {
            term=term+d;
            System.out.print(term+",");
            
        }
        
    }
    
}

```

## 2. Amstrong Number

```java
package amstrong.number;
import java.util.*;
public class AmstrongNumber 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter a number");
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int m=n;
        int r;
        int sum=0;
        while(n>0)
        {
            r=n%10;
            n=n/10;
            sum=sum+(r*r*r);
        }
        System.out.println(sum);
        if(sum==m)
        {
            System.out.println("It is an Amstrong Number");
        }    
        else
        {
            System.out.println("It s not an amstrong number");
        }
        
    }
}    
        
```

## 3. Count Digit On Numbers

```java
package count.digit.of.number;
import java.util.*;
public class CountDigitOfNumber 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter the Number");
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int count=0;
        
        while(n>0)
        {
            n=n/10;
            count++;
        }
        System.out.println(count);
    }
          
}

```

## 4. Display Number in Word

```java
package displaty.number.sin.words;
import java.util.*;
public class DisplatyNumberSinWords 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter the number");
        Scanner sc=new Scanner(System.in);
        int i=sc.nextInt();
        int m=i;
        String rev="";
        int r;
        
        while(i>0)
        {
            r=i%10;
            i=i/10;
            rev=rev+r;
        }
        char c;
        for(int n=rev.length()-1; i>=0; i--)
        {
            c=rev.charAt(i);
            switch('c')
            {
                                     
                case '0': System.out.println("Zero ");
                break;
                case '1': System.out.println("One ");
                break;
                case '2': System.out.println("Two ");
                break;
                case '3': System.out.println("Three ");
                break;
                case '4': System.out.println("Four ");
                break;
                case '5': System.out.println("Five ");
                break;
                case '6': System.out.println("Six ");
                break;
                case '7': System.out.println("Seven ");
                break;
                case '8': System.out.println("Eight ");
                break;
                case '9': System.out.println("Nine ");
                break;
                default: System.out.println("Enter the vaid no");
                break;
                
                
            }
        }
        
    }
    
}

```

## 5. Display Digit of Numbers

```java
package display.digit.of.number;
import java.util.*;
public class DisplayDigitOfNumber 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter the Number");
        Scanner sc=new Scanner(System.in);
        int i=sc.nextInt();
        int r;
        while(i>0)
        {
            r=i%10;
            System.out.println(r);
            i=i/10;
        }
    }
    
}

```

## 6. Factorial of Number

```java
package factorila.of.number;
import java.util.*;
public class FactorilaOfNumber 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter a Number");
        Scanner sc=new Scanner(System.in);
        int i=sc.nextInt();
        long fact=1;
        
        for(int n=1; n<=i; n++)
        {
            fact=fact*n;
        }
        System.out.println("The Factorial is ="+fact);
    }
    
}

```

## 7. Fib series

```java
package fibonaci.series;
import java.util.*;
public class FibonaciSeries 
{
    public static void main(String[] args) 
    {
        System.out.println("Program for FIbonaciss Series");
        Scanner sc=new Scanner(System.in);
        System.out.println("Enter number of Terms n=");
        int n=sc.nextInt();
        
        int a=0, b=1,c;
        System.out.println(a+","+b+",");
        
        for(int i=0;i<n-2; i++)
        {
            c=a+b;
            System.out.print(c+",");
            a=b;
            b=c;
        }
        
        
    }
    
}

```

## 8. GP Series

```java
package g.p.series;
import java.util.*;
public class GPSeries 
{
    public static void main(String[] args) 
    {
        System.out.println("Program for G.P Series");
        System.out.println("--------------------------------");
        System.out.println("Enter the value of a=");
        Scanner sc=new Scanner(System.in);
        int a=sc.nextInt();
        System.out.println("Enter the Common Ratio r=");
        Scanner sr=new Scanner(System.in);
        int r=sr.nextInt();
        System.out.println("Enter the No of terems n=");
        Scanner sn=new Scanner(System.in);
        int n=sn.nextInt();
        
        int term=a;
        for (int i=0; i<n; i++)
        {
            term=term*r;
            System.out.print(term+",");
        }
    }
    
}

```

## 9. Multiplication Table

```java
package multiplication.table;
import java.util.*;
public class MultiplicationTable 
{
    public static void main(String[] args) 
    {
        int i,n;
        System.out.println("Enter the Number for which table is required");
        Scanner sc=new Scanner(System.in);
        i=sc.nextInt();
        
         for(n=1; n<=10; n++)
         {
             System.out.println(i+"*"+n+"="+i*n);
         }
    }
    
}

```

## 10. Nested Loop Example

```java
package nested.loop.example;
public class NestedLoopExample 
{
    public static void main(String[] args) 
    {
        for(int i=1; i<=5; i++)
        {
            for(int j=1; j<=5; j++)
            {
                System.out.println("("+i+","+j+")");
            }
        } 
    }
    
}

```

## 11. Palindrome

```java
package palindrome;
import java.util.*;
public class Palindrome 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter the Number");
        Scanner sc=new Scanner(System.in);
        int i=sc.nextInt();
        int rev=0,r;
        int m=i;
        while(i>0)
        {
            r=i%10;
            i=i/10;
            rev=(rev*10)+(r);
        }
        System.out.println(rev);
        if(m==rev)
        {
            System.out.println("It is an Plaindrome");
        }
        else
        {
            System.out.println("It is not an Palindrome");
        }
    }
    
}

```

## 12. Reverse the Number

```java
package reverse.the.number;
import java.util.*;
public class ReverseTheNumber 
{
    public static void main(String[] args) 
    {
        System.out.println("Enter the Number");
        Scanner sc=new Scanner(System.in);
        int i=sc.nextInt();
        int n;
        int rev=0;
        while(i>0)
        {
            n=i%10;
            i=i/10;
            rev=(rev*10)+(n);
        }
        System.out.println(rev);
    }
    
}

```

## 13. Sum of Naturals Numbers

```java
package sumofnnaturals.number;
import java.util.*;
public class SumOfnNaturalsNumber 
{
    public static void main(String[] args) 
    {
        int i;
        
        System.out.println("Enter the nth term up to whic you need to perform adition");
        Scanner sc=new Scanner(System.in);
        i=sc.nextInt();
        
        int sum=0;
        for(int n=0; n<=i; n++)
        {
            sum=sum+n;
            
        }
        System.out.println("sum of"+i+"Natural number is-"+sum);
    }
    
}

```