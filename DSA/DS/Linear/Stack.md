
#### Collision type idea (like TOC Machine) -
1. Like Valid Parenthesis
2. [2751. Robot Collisions](https://leetcode.com/problems/robot-collisions/) 
3. [Remove All Adjacent Duplicates in String II - LeetCode](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/description/) 
4. 

---------------------------------


#### Monotonic stack thinking -
1. kya chahiye finally (greatest/ largest)
   
2.  ** pop el p focus (nikal greatest/ smallest) ***********  (if greater el ----> pse/nse dekh,  
	else if smaller el  ---->  pge/ nge dekh)
	
3. stack k andar el. p focus (esa koi pattern nhi dekha filhal)





- Some applications of monotone (increase/decrease) stack in leetcode: 
    [Next Greater Element II](https://leetcode.com/problems/Next-Greater-Element-II/description/) (a very basic one)  
    [Largest Rectangle in Histogram](https://leetcode.com/problems/Largest-Rectangle-in-Histogram/description/)(almost the same as this problem)  
    [Maximal Rectangle](https://leetcode.com/problems/Maximal-Rectangle/description/)(please do this problem after you solve the above one)  
    [Trapping Rain Water](https://leetcode.com/problems/Trapping-Rain-Water/description/) (challenge)  
    [Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/description/)(challenge)  
    [Remove K Digits](https://leetcode.com/problems/remove-k-digits/description/)  
    [Create Maximum Number](https://leetcode.com/problems/create-maximum-number/description/)  
    [132 Pattern](https://leetcode.com/problems/132-pattern/description/)(challenge, instead of focusing on the elements in the stack, this problem focuses on the elements poped from the monotone stack)  
    [sliding window maximum](https://leetcode.com/problems/sliding-window-maximum/description/)(challenge, monotone **queue**)  
    [Max Chunks To Make Sorted II](https://leetcode.com/problems/Max-Chunks-To-Make-Sorted-II/description/)


## Monotonic (top to bottom) Stack (nge/pge +  nse/pse)

1. [Online Stock Span - LeetCode](https://leetcode.com/problems/online-stock-span/description/) (pop p dhyan)
2. [Largest Rectangle in Histogram - LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/description/) (optimest approach bad m pdunga)
3. [Sum of Subarray Minimums - LeetCode](https://leetcode.com/problems/sum-of-subarray-minimums/description/) (think -> each el. kitne subarrays me min h)
4. [Sum of Subarray Ranges - LeetCode](https://leetcode.com/problems/sum-of-subarray-ranges/description/)
5. [Number of Visible People in a Queue - LeetCode](https://leetcode.com/problems/number-of-visible-people-in-a-queue/description/) (observe karo pattern)
6. [Remove K Digits](https://leetcode.com/problems/remove-k-digits/) (starting k greatest chahiye/ soch -> greatest kab pop honge (store krlenge tab))
   
```cpp
		vector<int>nge(nums.size(),-1);
        
        for(int i = n-1; i >= 0; i--){
            
            while(!s.empty() && s.top() <= nums[i]) s.pop();
            
            if(!s.empty()) nge[i] = s.top();
            
            s.push(nums[i]);
        }
```

2. [Trapping Rain Water - LeetCode](https://leetcode.com/problems/trapping-rain-water/)
   prefix max and suffix max concept **








saved -
[Sum of Total Strength of Wizards - LeetCode](https://leetcode.com/problems/sum-of-total-strength-of-wizards/description/)
[Find Building Where Alice and Bob Can Meet - LeetCode](https://leetcode.com/problems/find-building-where-alice-and-bob-can-meet/description/)



#### Recursion x stack -
i thought of something. anything solved with recursion can be solved iteratively with stack. is it correct

**Yes, you are 100% correct!** That is a brilliant realization to hit upon as a fresher.

In computer science, this is a fundamental law: **Any problem that can be solved using recursion can also be solved iteratively using an explicit stack.** In fact, it goes both ways—they are completely interchangeable in terms of what problems they can solve. Here is exactly why your thought is spot-on, explained simply.















anyth

dhyan s dekh y netre kya batana chahri

ek bar firse betha maa baap ko dhoka deke
in aksharoke samandar p m nauka leke
bhuchal y man ka lejara jaha p y toofan h
ab khali lautu n gahr lautunga to tofa leke

hu bhi busy
kuch bate kehni joki kehne ki ni
likhne k le betha mera thanda y kaleja pada
jab awaj koi meri sunne hi ni wala
mujhe hoti bt, esi baate soch k, bate m hazar bhi likhdu y shad khoj k
parvah kabhi hogi hi ni, kisiko bhi thodi si bhi
bhale har waqt pass rkhu m shabd kosh y

00.42
koshish hi to bs m kare jara
mere man m bhi or bas m ni h dhushmani nibhana
or koshish ki y shazish h ki trophy karu hasil m
pr isne waqt khoti kara sara

pura sukha, pani piya ni, hu pyasa
hu m bhukha, muh me ghusa ni, subah s, nivala
bs h khaya keval tana, ghr p, kya hota h khana

na kala dhaga
na kalava
bs gaane p m
bs kalam h pass is lavzo alfazo ki kala  p  m nyochavar

sadhgi s nishana sadha
nishane p y gana daga
challenge h or pehnu n m kala dhaga
koi nazar mila ni pata
kyoki kala meri bhari
kalam kagaz h hathiyar hi
tujhe agla nishana tana
beta mat kr hoshiyari
hath kya tu nazar laga k dikha
h y challenge
or hn beta kabhi pehnu n m kala dhaga

pr isne hi to sachme hi (vo) waqt khoti kara sara

kala dhaga
kalava


sehmati deta hu m sehne kele ni
kash hota bag
kash hota bag mujhe kimon ache true bande lage ajtk kisko ache
akele mera chill y heart h pr tum cool mano unko jo jake disco nache

senorita jab sehen hora ni tha
seh mat hi, de tu teri sehmati
tujhe kisne krne sehen ni kha

kisko haq h

wait us samay fekta album rags to riches
similarity

meri lipi

sochu bachpn s h bs dhoka dia
sochu ki m hu bhot bura


dikhega dola bhi
rato ko sota






















ab kya bar banau
m bar bar au
pr bhar jau

betha akela hu m
kehna chahta lekin kuch na keh pau m
sehta hu m sehta rehta betha betha lekin beta kabhi ek na asu behta esa sehma rehta hu m

kese samjhau y ghehraiyo ko
firbhi kehra hu m
firbhi kehra hu m

kya tu samjrae
meri bato ko
kya tu thoda feel kr para h in alfaso ko
khayalo n mere khud k banake rakha kedi
gidgida ke bolu khud s plz ab mujhe nikal jane do

unko khiladu kela bhi m


@githubpass123