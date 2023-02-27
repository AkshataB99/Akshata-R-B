# Akshata-R-B
Programming round
import java.util.*;

public class Main{
   
    static class Job {
        int start, finish, profit;
        Job(int start, int finish, int profit)
        {
            this.start = start;
            this.finish = finish;
            this.profit = profit;
        }
    }
 

    static int latestNonConflict(Job arr[], int i)
    {
        for (int j = i - 1; j >= 0; j--) {
            // finish before next is started
            if (arr[j].finish <= arr[i - 1].start)
                return j;
        }
        return -1;
    }
 
    static int findMaxProfitDP(Job arr[], int n)
    {
        int[] table = new int[n];
        table[0] = arr[0].profit;
 
        for (int i = 1; i < n; i++) {
            int inclProf = arr[i].profit;
            int l = latestNonConflict(arr, i);
            if (l != -1)
                inclProf += table[l];
 
         
            table[i] = Math.max(inclProf, table[i - 1]);
        }
 
       
        int result = table[n - 1];
 
        return result;
}
static int findMaxProfit(Job arr[], int n)
    {
        Arrays.sort(arr, new Comparator<Job>() {
            public int compare(Job j1, Job j2)
            {
                return j1.finish - j2.finish;
            }
        });
 
        return findMaxProfitDP(arr, n);
    }
     public static void main(String []args){
         Scanner sc=new Scanner(System.in);
         System.out.println("Enter the number of Jobs");
         int m = sc.nextInt();
       
        Job arr[] = new Job[m];
        int starttime;
        int endtime;
        int earnings;
        for(int i=0;i<m;i++)
        {
             starttime=sc.nextInt();
             endtime=sc.nextInt();
             earnings=sc.nextInt();
             arr[i] = new Job(starttime, endtime, earnings);
           
        }
        int n = arr.length;
        System.out.println("The optimal profit is "
                           + findMaxProfit(arr, n));
     }
}
