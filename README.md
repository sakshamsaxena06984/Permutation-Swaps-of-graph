# Permutation-Swaps-of-graph
Swap Px and Py only if (x, y) is a good pair. Help him and tell if Kevin can obtain permutation Q using such operations.


#include<bits/stdc++.h>
#include<vector>
#include<set>
using namespace std;
bool check(int *a1,int *a2,unordered_set<unordered_set<int>*>* output,int size)
{
	    unordered_set<unordered_set<int>*>:: iterator it=output->begin();
	    while(it!=output->end())
	    {
	   
	    	unordered_set<int>* component=*it;
	    	unordered_set<int>:: iterator it2=component->begin();
	    	while(it2!=component->end()){
	    	int ele=a1[*it2];
	    	unordered_set<int>:: iterator it1=component->begin();
	    	while(it1!=component->end())
	    	{
	    	     if(ele==a2[*it1])
	    	     {
	    	     	break;
				 }
				 it1++;
				
			}
			 if(it1==component->end())
				 {
				 	return false;
				 }
			it2++;
		}
		it++;
		}
		return true;
}
void dfs(vector<int>* edge,bool* &visited,int start,unordered_set<int>* &component)
{
	visited[start]=true;

	component->insert(start);
	for(int j=0;j<edge[start].size();j++)
	{
		int index=edge[start][j];
		if(visited[index]==false)
		{
			dfs(edge,visited,index,component);
		}
	}
	return;

}
unordered_set<unordered_set<int>*>* helper(vector<int>* egde,int n)
{
	bool *visited=new bool[n];
	for(int i=0;i<n;i++)
	{
		visited[i]=false;
	}

	unordered_set<unordered_set<int>*>* output=new unordered_set<unordered_set<int>*>();
	for(int i=0;i<n;i++)
	{
		
		if(visited[i]==false)
		{
	
		   unordered_set<int>* component=new unordered_set<int>();
		   dfs(egde,visited,i,component);
		   output->insert(component);

//		   delete component;	
		}
	}
	return output;
}
int main()
{
	int t;
	cin>>t;
	while(t--)
	{
		int n,m;
		cin>>n>>m;
		int arr1[n],arr2[n];
		for(int i=0;i<n;i++)
		{
			cin>>arr1[i];
		}
		for(int i=0;i<n;i++)
		{
			cin>>arr2[i];
		}
		
        
        vector<int> *edge=new vector<int>[n];
		// cout<<"Enter The Swap"<<endl;
		for(int i=0;i<m;i++)
		{
			int ele1,ele2;
			cin>>ele1>>ele2;
		      edge[ele1-1].push_back(ele2-1);
			  edge[ele2-1].push_back(ele1-1);	
	    }

	    unordered_set<unordered_set<int>*>* output=helper(edge,n);
	    //check for component
//	    unordered_set<unordered_set<int>*>:: iterator it=output->begin();
//	    while(it!=output->end())
//	    {
//	   
//	    	unordered_set<int>* component=*it;
//	    	unordered_set<int>:: iterator it1=component->begin();
//	    	while(it1!=component->end())
//	    	{
//	    		cout<<*it1+1<<" ";
//	    		it1++;
//			}
//			cout<<endl;
//			it++;
//	    	
//		}
     bool ans=check(arr1,arr2,output,n);
        if(ans==0)
        {
            cout<<"NO"<<endl;
        }
        else
        {
            cout<<"YES"<<endl;
        }
	}
}
