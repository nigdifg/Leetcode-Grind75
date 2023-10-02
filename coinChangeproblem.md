    int solve(int indx , vector<int>&coins,int amount,vector<vector<int>>&dp){
        if(indx==0){
            if(amount%coins[0]==0){
                return amount/coins[0];
            }
            else{
                return 1e9;
            }
        }
        if(dp[indx][amount]!=-1)return dp[indx][amount];
        int notpick = solve(indx-1,coins,amount,dp);
        
        int pick = 1e9;

        if(coins[indx]<=amount){
            pick = 1+solve(indx,coins,amount-coins[indx],dp);
        }
        return dp[indx][amount] = min(pick,notpick);
    }
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>>dp(n,vector<int>(amount+1,-1));
        
        int ans = solve(n-1,coins,amount,dp);
        if(ans>=1e9)return -1;
        return ans;
    }