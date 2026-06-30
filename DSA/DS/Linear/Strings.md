
1. int freq[26] = {0};  -----> a to z, {use -> freq[c-'a']}
2. int freq[128] = {0};   // for standard ASCII (includes -> English letters, digits, symbols and spaces.) ------>   use directly like => freq[c]++;
	// or
	int freq[256] = {0};   // for extended ASCII

3. int mpp[256] = {0}; -----> all ascii characters map/ vis array !   {access -> mpp[c]}
4. tolower(c);      toupper(c); ----> per character (**returns int**)
5. isalpha(c);       isdigit(c);          isalnum(c);
6. s.substr(start, ex-end)
7. reverse( s.begin(), s.begin()+i); -------> stl algo
8. s.erase(from, how many to erase);
9. s.insert(where_i , what_s);
10. s = s1 + s2;
11. s = s1 + 'a';
12. s.push_back(s1 / 'a');             s.pop_back();
13. string s = "";        <--equi-->     string s;
14. s[i] is a character
15. "hello"    -----> is a ptr, so                 cout << "hello"[1];    ----> e
16. int freq[75];         freq[c-'0'];
17.                 ans.push_back('0'+i);        (int -> char)
18. a to z (97 - 122 in ascii)
19. generate string   ---->  string(freq ,  character); 
20. gen key ---->string newStr =  to_string(x) + "_ " + to_string(y);
21. count(s.begin(),s.end(),target)


#### TOC concept -
- in strings Q
  think like TOC machine
- eg - [2840. Check if Strings Can be Made Equal With Operations II](https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-ii/)
- 