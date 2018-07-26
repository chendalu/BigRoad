## 5.Longest Palindromic Substring
方法一：暴力求解O(n<sup>3</sup>) 这部分代码就不放了，没必要

方法二：DP   

O(n<sup>2</sup>)

<pre><code>
class Solution {
    public String longestPalindrome(String s) {
        if (s == null) {
            return null;
        }
        String ret = null;
        
        int len = s.length();
        int max = 0;
        
        boolean[][] D = new boolean[len][len];
        
        for (int j = 0; j < len; j++) {
            for (int i = 0; i <= j; i++) {
		//关键点
                D[i][j] = s.charAt(i) == s.charAt(j) && (j - i <= 2 || D[i + 1][j - 1]);
                if (D[i][j]) {
                    if (j - i + 1 > max) {
                        max = j - i + 1;
                        ret = s.substring(i, j + 1);
                    }
                }
            }
        }
        
        return ret;
    }
}</code></pre>

方法三：中心扩散

O(n<sup>3</sup>)

<pre><code>class Solution {
    public String longestPalindrome(String s) {
        int start=0;
        int end=0;
        for(int i=0;i < s.length();i++){
            int len1 = expandAroundCentor(s,i,i);
            int len2 = expandAroundCentor(s,i,i+1);
            int len = Math.max(len1,len2);
            if(len > end-start){
                //这里举个例子就明白，要考虑到aba和abba这2种情况
                start = i-(len-1)/2;
                //当len是偶数时，也就是abba情况。所以不能len-1
                end = i + len/2;
            }
        }
        //beginIndex -- 起始索引（包括）。endIndex -- 结束索引（不包括）。    
        return s.substring(start,end+1);
            
        
    }
    private int expandAroundCentor(String s,int left,int right){
        int L=left;
        int R=right;
        while(L >=0 &&R< s.length()&& s.charAt(L)==s.charAt(R)){
            L--;
            R++;
        }
        return R-L-1;
    }
}</code></pre>


方法四：马拉车O(n)
<pre><code>class Solution {
    // 马拉车
    public String longestPalindrome(String s) {
        String t="&#";
        for(int i=0;i < s.length();i++){
            t+=s.charAt(i);
            t+="#";
        }
        t+="@";
        int n =t.length();
        int mx=0,id=0,maxLen=0,maxCent=0;
        int[] p=new int[n];
        for(int i=1;i < n-1;i++){
            p[i] =mx > i?Math.min(p[2*id-i],mx-i):1;
            
            while(t.charAt(i-p[i])==t.charAt(i+p[i])){
                p[i]++;
            }
            if(p[i]+i > mx){
                mx=p[i]+i;
                id=i;
            }
            if(maxLen < p[i]){
                maxLen=p[i];
                maxCent=i;
            }
        }
        return s.substring((maxCent-maxLen)/2,(maxCent-maxLen)/2+maxLen-1);
        
    }
}</code></pre>

