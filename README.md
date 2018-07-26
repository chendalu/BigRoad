# BigRoad
how to be a coder- LeetCode

####5. Longest Palindromic Substring 最长回文子串
<pre><code>class Solution {
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
}
</code></pre>
