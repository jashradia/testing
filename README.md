# testing
asd
import java.io.BufferedReader; 
import java.io.InputStreamReader; 
import java.util.Vector; 
  
class Test 
{ 
    static final int MOD = 1000000007;
      
  
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); 
      
    
    static Vector<Integer> capList[] = new Vector[101]; 
      
       
    
    static int dp[][] = new int[1025][101]; 
       
    
    static int allmask; 
       
    
    static long countWaysUtil(int mask, int i) 
    { 
        
        if (mask == allmask) return 1; 
       
       
        if (i > 100) return 0; 
       
       
        if (dp[mask][i] != -1) return dp[mask][i]; 
       
        
        long ways = countWaysUtil(mask, i+1); 
       
        
        int size = capList[i].size(); 
       
        // So, assign one by one ith cap to all the possible persons 
        // and recur for remaining caps. 
        for (int j = 0; j < size; j++) 
        { 
            
            if ((mask & (1 << capList[i].get(j))) != 0) continue; 
       
           
            else ways += countWaysUtil(mask | (1 << capList[i].get(j)), i+1); 
            ways %= MOD; 
        } 
       
        // Save the result and return it. 
        return dp[mask][i] = (int) ways; 
    } 
       
    // Reads n lines from standard input for current test case 
    static void countWays(int n) throws Exception 
    { 
        //----------- READ INPUT -------------------------- 
        String str; 
        String split[]; 
        int x; 
                
        for (int i=0; i<n; i++) 
        { 
            str = br.readLine(); 
            split = str.split(" "); 
            
            // while there are words in the split[] 
            for (int j = 0; j < split.length; j++) { 
                 // add the ith person in the list of cap if with id x 
                x = Integer.parseInt(split[j]); 
                capList[x].add(i); 
            } 
            
        } 
        //---------------------------------------------------- 
       
        // All mask is used to check of all persons 
        // are included or not, set all n bits as 1 
        allmask = (1 << n) - 1; 
       
        // Initialize all entries in dp as -1 
        for (int[] is : dp) { 
            for (int i = 0; i < is.length; i++) { 
                is[i] = -1; 
            } 
        } 
       
        // Call recursive function count ways 
        System.out.println(countWaysUtil(0, 1)); 
    } 
  
    // Driver method 
    public static void main(String args[]) throws Exception 
    { 
        int n;   // number of persons in every test case 
          
        // initializing vector array 
        for (int i = 0; i < capList.length; i++) 
            capList[i] = new Vector<>(); 
          
          
        n = Integer.parseInt(br.readLine()); 
        countWays(n); 
    } 
}
