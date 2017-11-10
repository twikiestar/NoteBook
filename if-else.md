Linux if..else..优化措施



2017年10月13日

14:07







1.条件表达式通常有两种表现形式,第一种:所有分支都是属于正常行为;第二种:条件表达式提供的答案只有一种是正常的行为.其他都是不常见的情况.如果两条分支都是正常行为,就应该使用if…else的条件表达式;如果某个条件极其罕见,就应该单独检查该条件,并在该条件为真时立刻从函数中返回.



Function getPayAmount\(\){

	Var resault;

	If\(isDead\) result = deadAmount\(\);

	Else{

		If\(isSerarated\) result = separatedAmount \(\);

		Else{

			If\(isRetired\) resault retiredAmount \(\);

			Else resault = normalPayAmount \(\);

		}

	}

	Return result;

}



可以省略为

Function getPayAmount\(\)

{

	If\(isDead\) Return deadAmount\(\);

	If\(isSeparated\) Return serparatedAmount\(\);

	If\(isRedired\) Return retiredAmount \(\);

	Return normalAmount\(\);

}



	2. 在条件表达式的每个分支上有着相同的一段执行代码,这段代码跟分支的逻辑无关的时候,将这段重复代码搬移到条件表达式之外.



If \( isSpecialDeal\(\) \){

	Total = price \* 0.95 ;

	Send \(\) ;

	

	}else{

	Total =price \*  0.98 ;

	Send \(\);

}

可以转化为:



If\(isSpecialDeal \(\) \){

	Total = price \* 0.95 ;

}else{

	Total =price \* 0.95 ;

}

Send\(\);







3.如果分支条件过于复杂,可以将分支条件提炼出来作为一个独立函数,并且提供一个语义化更好的名称用于分支判断中.使用它的优势是使得在分支中的代码可读性更好,以至于我不需要知道具体的分支判断条件,就可以理解代码的意图





If\(date.before\(SUMMER\_START\) \|\| date.after\(SUMMER\_END\) \){

	Charge = quantity \* \_winterRate \* \_winterServiceCharge;

}else{

	Charge = quantity \* \_summerRate;

}



可以转化为:



If\(notSummer\(date\)\){

	Charge =winterCharge\(quantity\);

}else{

	Charge = summerCharge\(quantity\);

}



Function notsummer \(date\){

	Return date.before\(SUMMER\_START\) \|\| date.after\(SUMMER\_END\) ;

}

Function summerCharge\(quantity\){

	Return quantity \* \_summerRate;

}

Function weinterCharge\(quantity\){

	Return quantity \* \_weinterRate \* \_winterRate \* \_winterServiceCharge;

}

4.合并表达式,如果有一系列的条件判断,都得到相同的结果,或者壳套的条件判断.那么将这些条件合并为一个条件的表达式,可能的话将这个合并的表达式提炼为一个独立的函数



Fucniton disabilityAmount\(\) {

	If \(\_seniority &lt; 2\) return 0 ;

	If \(\_monthsDisabled\) retun 0 ;

	If \(\(\_isPartTime\) return 0;

	Return 1;

}





可以转化为

Function disabilityAmount \(\){

	If\(\_seniority &lt; 2 \|\| \_monthsDisabled \|\| \_isPartTime\) return 0;

	Return 1;

}



还可以转化为:

Function disabilityAmount\(\){

	If\(isNotEligibleForDisability\(\) \) return 0;

	Return 1;

}



Function isNotEligibleForDisability \(\){

	Return \_seniority &lt; 2 \|\| \_monthsDisabled \|\| \_isPartTime;

}



5.将条件逻辑反转.有时候使用条件反转的方式,可以很大程度上简化if判断逻辑,特别是在嵌套if判断的时候



Function getAjustedCapital \(\) {

	Var resault = 0;

	If\(\_capital &gt; 0\){

		If\(\_intRate &gt; 0 $amp;$amp \_duration &gt; 0\){

			Resault = \(\_income / \_duration \) \* ADJ\_FACTOR;

		}

	}

	Return result;

}



可以简化为:



Function getAdjustedCapital\(\) {

	If \(\_capital &lt; =0\) return 0;

	If \(\_inRate &lt; = 0 \|\| \_duration &lt;=0\) return 0;

	Return \(\_income / \_duration \) \* ADJ\_FACTOR;

}





再简化为:



Function get AdjustedCapital \(\) {

	If\(\_capital &lt\); =0 \|\| \_inRate &lt; =0 \|\| \_duration & lt; =0\) return 0 ;

	Return \(\_income / \_duration \) \* ADJ\_FACTOR;

}



