[To Index](/index.md)
    ---
# 面试题 16.18
难度:Medium
> 你有两个字符串，即pattern和value。 pattern字符串由字母"a"和"b"组成，用于描述字符串中的模式。例如，字符串"catcatgocatgo"匹配模式"aabab"（其中"cat"是"a"，"go"是"b"），该字符串也匹配像"a"、"ab"和"b"这样的模式。但需注意"a"和"b"不能同时表示相同的字符串。编写一个方法判断value字符串是否匹配pattern字符串。

    ```
    示例 1：

    输入： pattern = "abba", value = "dogcatcatdog"
    输出： true
    示例 2：

    输入： pattern = "abba", value = "dogcatcatfish"
    输出： false
    示例 3：

    输入： pattern = "aaaa", value = "dogcatcatdog"
    输出： false
    示例 4：

    输入： pattern = "abba", value = "dogdogdogdog"
    输出： true
    解释： "a"="dogdog",b=""，反之也符合规则
    提示：

    0 <= len(pattern) <= 1000
    0 <= len(value) <= 1000
    你可以假设pattern只包含字母"a"和"b"，value仅包含小写字母。
    ```

可以通过一个二元一次方程来逐个判断每个pattern出现的次数，即numA*lenA+numB*lenB=lenValue;

    ```
    class Solution {
	string pattern;
	inline string patternString(string a, string b)
	{
	    string res;
	    for(auto c: pattern)
	    {
		if(c=='a') res+=a;
		else res+=b;
	    }
	    return res;
	}
	public:
	bool patternMatching(string pattern, string value) {

	    int sizeA=0;
	    int sizeB=0;

	    if(pattern[0]=='b') 
	    {
		string tmp;
		for(auto c:pattern)
		    tmp+= c=='a' ? 'b' :'a';
		this->pattern=tmp;
	    }
	    else 
		this->pattern=pattern;

	    for(auto c:this->pattern)
	    {
		if(c=='a') sizeA++;
		else sizeB++;
	    }

	    if(sizeA ==0 && sizeB ==0) return value=="";
	    if(sizeA==0) 
	    {
		int cntB=value.length()/sizeB;
		return patternString("",value.substr(0,cntB)) ==value;
	    }
	    if(sizeB==0) 
	    {
		int cntA=value.length()/sizeA;
		return patternString(value.substr(0,cntA),"") ==value;
	    }
	    int startB=0;
	    for(auto c:this->pattern)
	    {
		if(c=='a') {
		    startB++;
		}
		else 
		    break;
	    }
	    //cout<<startB<<endl;
	    //cout<<sizeA<<endl;
	    int cntA=value.length()/sizeA;
	    //     cout<<cntA<<endl;
	    for(int i=0; i<=cntA;i++)
	    {
		int cntB=(value.length()-sizeA*i)/sizeB;

		string a=value.substr(0,i);
		//      cout<<i*startB<<endl;
		string b =value.substr(i*startB,cntB);
		//       cout<<a<<"  "<<b<<endl;
		if(a==b) continue;
		//    cout<<patternString(a,b) <<endl;
		if(patternString(a,b) == value) return true;

	    }
	    return false;
	}
    };
```

> 执行用时 :4 ms, 在所有 C++ 提交中击败了63.82%的用户   
内存消耗 :10.1 MB, 在所有 C++ 提交中击败了100.00%的用户
