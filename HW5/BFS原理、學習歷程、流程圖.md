##廣度優先搜尋

BFS(Breadth-first Search):

是從根節點開始，遍歷完畢整張圖，不考慮結果所在的位置， 無論如何都要遍歷完畢整張地圖才終止。

按照就近原則進行， 距離原點相同的節點的訪問順序是相近的。

使用queue(先進先出)儲存節點

時間複雜度：O(V+E)（分別遍歷所有節點和各節點的所有鄰居）

空間複雜度：O(V)（Queue中最多可能存放所有節點）

用於有效率的迭代(traversal)

迭代的方式為鄰近的先訪問(level-ordered)

劣勢在於儲存指標記憶體空間，有時用DFS替代

![](https://i.imgur.com/X7GphFN.png)


##深度優先搜尋

DFS(Depth-first Search):

是從根節點開始， 逐個訪問每一條路徑， 對於具有多子節點的節點而言，先搜尋到某一條子路的最深處，再逐個回溯前驅節點。

使用stack(後進先出)儲存節點

時間複雜度：O(V+E)

空間複雜度：O(logV)

（訪問至末端節點後，Stack最多只會同時存在logV個節點，也就是樹的高度）

為了解Maze Problem而生的演算法

效能比BFS稍佳

![](https://i.imgur.com/3q1QZuB.png)


資料來源：https://codertw.com/程式語言/102866/
https://www.youtube.com/watch?v=bD8RT0ub--0
http://www.csie.ntnu.edu.tw/~u91029/Graph.html#6


學習歷程:
一開始看完影片寫的

    def BFS(self, s): 
        queue=[]
        queue.append(s)
        seen=[]
        while (len(queue)>0):
            vertex=queue.pop(0)
            seen.append(vertex)
            for w in self.graph[vertex]:
                if w not in seen:
                    queue.append(w)
                    seen.append(w)
            return seen


測完值後發現if 裡面有問題。

  
    def DFS(self, s):
        stack=[]
        stack.append(s)
        seen=[]
        while (len(queue)>0):
            vertex=stack.pop()
            seen.append(vertex)
            for w in self.graph[vertex]:
                if w not in seen:
                    stack.append(w)
                    seen.append(w)
            return seen
    
不用在放seen.append(w)，弄兩次。


    def BFS(self, s): 
        queue=[s]
        seen = [s]
        while (len(queue)>0):
            vertex=queue.pop()
            for w in self.graph[vertex]:
                if w not in seen:
                    queue.append(w)
                    seen.append(w)
        return seen

這樣！！！

換成DFS
接著直接把queue換成stack

     def DFS(self, s):
        stack=[]
        stack.append(s)
        seen=[]
        while stack:
            vertex=stack.pop()
            seen.append(vertex)
            for w in self.graph[vertex]:
                if w not in seen:
                    stack.append(w)
                    seen.append(w)
            return seen
        
還是一樣if有問題


改一改

     def DFS(self, s):
        stack=[s]
        seen=[]
        while stack:
            vertex=stack.pop()
            seen.append(vertex)
            for w in self.graph[vertex]:
                if w not in seen:
                    stack.append(w)
                    
        return seen
