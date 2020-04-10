# Prims-and-Djkstra

This is the implementation of the two of the most popular algorithm of the graph theory first one is Prims which is used to find the minimum spanning tree and second one is the Djkstra that is used to find the shortest path from the source to every other vertices in the weighted undirected graph.

Prims implementation - 
1. Create a set mstSet that keeps track of vertices already included in MST.
2. Assign a key value to all vertices in the input graph. Initialize all key values as
INFINITE. Assign key value as 0 for the first vertex so that it is picked first.
3. While mstSet doesn't include all vertices:
o Pick a vertex u which is not there in mstSet and has minimum key
value.
o Include u to mstSet.
o Update key value of all adjacent vertices of u. To update the key
values, iterate through all adjacent vertices. For every adjacent
vertex v, if weight of edge u-v is less than the previous key value of v,
update the key value as weight of u-v.

void prims(vector<pair<int,int> > graph[],int V)
{   vector<int> dist(V,INT_MAX);
    int u = 0;
    int m = 0;
    set<int> IN_MST;
    dist[u] =0;
    int ans =0;
    while(IN_MST.size()<V)
    {   ans+=m;
        IN_MST.insert(u);
        for(auto x: graph[u])
        {
            if(IN_MST.find(x.first) == IN_MST.end() && dist[x.first] > x.second)
            {
                dist[x.first] = x.second;
            }
        }
        for(int i=0;i<V;i++)
        {
            cout<<dist[i]<<" ";
        }
        cout<<endl;
        m = INT_MAX;
        for(int i=0;i<V;i++)
        {
            if(IN_MST.find(i) == IN_MST.end() && m > dist[i])
            {
                m = dist[i];
                u = i;
            }
        }
        
    }
    cout<<ans<<" ";
    
    
}

Djkstra implementation -
1. Create a set sptSet (shortest path tree set) that keeps track of vertices
included in shortest path tree, i.e., whose minimum distance from source is
calculated and finalized. Initially, this set is empty.
2. Assign a distance value to all vertices in the input graph. Initialize all distance
values as INFINITE. Assign distance value as 0 for the source vertex so that it
is picked first.
3. While sptSet doesn't include all vertices:
o Pick a vertex u which is not there in sptSet and has minimum distance
value.
o Include u to sptSet.
o Update distance value of all adjacent vertices of u. To update the
distance values, iterate through all adjacent vertices. For every
adjacent vertex v, if sum of distance value of u (from source) and
weight of edge u-v, is less than the distance value of v, then update the
distance value of v

void djkstra(vector<pair<int,int> > graph[],int V,int s)
{
    vector<int> dist(V,INT_MAX);
    dist[s] = 0;
    priority_queue<iPair , vector<iPair > , greater<iPair > > pq;
    pq.push({0,s});
    while(pq.empty() == false)
    {
        int x = pq.top().second;
        
        pq.pop();
        for(pair<int,int> p : graph[x])
        {
            if(dist[p.first] > dist[x] + p.second)
            {
                dist[p.first] = dist[x] + p.second;
                pq.push(make_pair(dist[p.first],p.second));
            }
        }
    }
    for(int i=0;i<V;i++)
    {
        cout<<dist[i]<<" ";
    }
}
