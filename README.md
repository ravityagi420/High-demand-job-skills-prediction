# Evolutionary-Clusters-Mapping-using-DBPedia

Reference Paper: https://madoc.bib.uni-mannheim.de/35464/1/schuhmacher14a.pdf

**Flow Chart**


![alt text](https://github.com/ravikant436/Evolutionary-Clusters-Mapping-using-DBPedia/blob/main/images/flow_chart.PNG)

**Step 1:**
We consider 2 clusters consisting of n and m nodes respectively. These 2 clusters might have few common nodes. We extract all unique nodes from these 2 clusters.

**Step 2:**
Semantic Graph Construction from the unique nodes. We are constructing the semantic graph by finding all the possible paths between the nodes. We are constraining our search up to 2 intermediate nodes between the source and the target node. We are using DBpedia for this task.

![alt text](https://github.com/ravikant436/Evolutionary-Clusters-Mapping-using-DBPedia/blob/main/images/Weighted%20Graph.PNG)

**Step 3:**
Identifying all the edges present in the graph and store them in a Dataset. One row of the dataset represents one edge; 
Source_node -- Predicate -- Target_node.

**Step 4:**
Semantic relation Weighting for all the edges has been computed using 3 different techniques (we are going to use all three for the computation of similarity score for the sake of comparison).
Joint IC
Comb IC
IC+PMI
We, then append the edge set dataset with the 3 different edge weight scores.

**Step 5:**
Computing Cost for all the edges using the below expression.

**cost(edge) = w_max - w(edge)**

Please note that there will be three different costs for an edge, one from each weighting scheme.
Then we normalize the edge costs by dividing them by the maximum edge cost in the graph (for every respective weighting scheme)

**Step 6:**
Finding the cheapest path (the path with the least total cost) between all pairs of nodes of cluster 1 and cluster 2.

**Step 7:**
We build the final edit distance matrix Dm from the computed cost in step 5.
eg.
       PHP 	JS	 HTML
       
 PHP  [ 0     x	  y]
 
 ECMA [ a     b	  c]


**Step 8:**
This edit distance matrix represents a bipartite matching problem that we solve with the Hungarian method. This finds the optimal, cost-minimal assignment
in our node operations matrix while ensuring that each node will only be edited once. The final similarity score is then given by the sum of these edit costs, normalized by the number of distinct source entities of 2 clusters.

![alt text](https://github.com/ravikant436/Evolutionary-Clusters-Mapping-using-DBPedia/blob/main/images/result_matrix.PNG)
