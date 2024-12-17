#include<iostream>
using namespace std;

const int V=8;

int MinimumKey(int key[], bool visited[])  
{ 
    int min = 999, min_index;  // Infinite value

    for (int v = 0; v < V; v++) { 
        if (visited[v] == false && key[v] < min) { 
        
            min = key[v];
			min_index = v;  
        }
    }    
    return min_index;  
}  


int printMST(int parent[], int cost[V][V])  
{  
    string dept [8] = {"CS","IT","ENTC","Mech.","Auto","Civil","FE","MBA"};
    int minCost=0;
	cout<<"Department\t----->   Distance\n"; 
	cout<<"====================================="<<endl;
    for (int i = 1; i< V; i++) 
    {
		cout<<"A--B : "<<dept[parent[i]]<<" --> "<<dept[i]<<" \t Dist ="<<cost[i][parent[i]]<<" m"<<" \n";  
		minCost+=cost[i][parent[i]];
    }
    cout<<"====================================="<<endl;
	cout<<"Distance of Mininimum Spanning Tree is : "<<minCost<<" m";
	
	return minCost;
}  


void findMST(int cost[V][V])  
{  
    int parent[V], key[V];
    bool visited[V];

    for (int i = 0; i< V; i++) 
    { 
        key[i] = 999;   
        visited[i] = false;
        parent[i]=-1;
    }    

    key[0] = 0;  
    parent[0] = -1; 

    for (int x = 0; x < V - 1; x++) 
    {  
       
        int u = MinimumKey(key, visited);  

        visited[u] = true;  

        
        for (int v = 0; v < V; v++)  
        {
             
            if (cost[u][v]!=0 && visited[v] == false && cost[u][v] < key[v])
            {  
                parent[v] = u;
                key[v] = cost[u][v];  
            }        
        }
    }

    
	printMST(parent, cost);  
}  


int main()  
{  
    cout<<"\n*************************************"<<endl;
	cout<<"\tPrim's Algorithm";
	cout<<"\n*************************************"<<endl;
    
    int graph[V][V] = { {0,90,60,0,0,0,0,50},
                        {90,0,60,300,90,0,40,0},
	                    {60,60,0,100,80,0,40,40},
	                    {0,300,100,0,200,300,0,0},
	                    {0,90,80,200,0,70,38,81},
	                    {0,0,0,300,70,0,0,90}, 
                        {0,45,86,101,0,0,0,0},
                        {40,60,30,0,0,51,0,0} };
	findMST(graph);  

    return 0;  
}  













    #define INFINITY 9999 
#include<iostream> 
#define MAX 10
using namespace std;
class graph
{ int G[MAX][MAX];
  int n;
  public:
  graph()
  {
    n=0;
  }
void readgraph();
void printgraph();
void dijkstra(int startnode);
};

void graph::readgraph()
{ int i,j;
  cout<<"\nEnter No.of vertices:";
  cin>>n;
  cout<<"\nEnter the adjacency matrix :"; 
  for(i=0;i<n;i++)
   { for(j=0;j<n;j++)
     { cin>>G[i][j];
     }
   }  
 }
void graph::printgraph()
{ int i,j;
  for(i=0;i<n;i++)
  { cout<<'\n';
    for(j=0;j<n;j++)
     { cout<<G[i][j];
     }
   }  
 }
int main()
{
graph g;
int u;
g.readgraph(); 
cout<<"\nEnter the starting node: ";
cin>>u;
g.dijkstra(u);
return 0;
}
void graph::dijkstra(int startnode)
{
 int cost[MAX][MAX],distance[MAX],pred[MAX]; 
 int visited[MAX],count,mindistance,nextnode,i,j;
 for(i=0;i<n;i++)
  for(j=0;j<n;j++)
     if(G[i][j]==0)
      cost[i][j]=INFINITY;
      else
      cost[i][j]=G[i][j];
   for(i=0;i<n;i++)
   {
     distance[i]=cost[startnode][i]; 
     pred[i]=startnode; 
     visited[i]=0;
   } 
distance[startnode]=0; 
visited[startnode]=1;
count=1;
while(count<n-1)
{
  mindistance=INFINITY; //nextnode gives the node at minimum distance 
  for(i=0;i<n;i++) 
   if(distance[i]<mindistance &&!visited[i])
    {
      mindistance-distance[i]; 
      nextnode=i;
    }
visited[nextnode]-1;
for(i=0;i<n;i++)
 if(!visited[i])
   if(mindistance+cost[nextnode][i]<distance[i])
     { distance[i]=mindistance+cost[nextnode][i];
       pred[i]=nextnode;
     }
count++;
}
//print the path & distance of each node
for(i=0;i<n;i++)
 if(i!=startnode)
  { cout<<"\n Distance of node"<<i<<"="<<distance[i];
    cout<<"\n path="<<i;
do
{
 j=pred[j];
 cout<<"<-"<<j;
}
while(j!=startnode);
}
}
