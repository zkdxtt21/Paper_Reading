# Basic Information
Graph Attention Networks (Veličković et al., ICLR 2018): https://arxiv.org/abs/1710.10903
## Git Repo
https://github.com/PetarV-/GAT
## Reference
If you make advantage of the GAT model in your research, please cite the following in your manuscript:
```
@article{
  velickovic2018graph,
  title="{Graph Attention Networks}",
  author={Veli{\v{c}}kovi{\'{c}}, Petar and Cucurull, Guillem and Casanova, Arantxa and Romero, Adriana and Li{\`{o}}, Pietro and Bengio, Yoshua},
  journal={International Conference on Learning Representations},
  year={2018},
  url={https://openreview.net/forum?id=rJXMpikCZ},
  note={accepted as poster},
}
```

# Reading Notes
## Idea
Attention mechanisms allow for dealing with variable sized inputs, focusing on the most relevant part of the input to make decisions. When an attention mechanism is used to compute a representation of a single sequence, it is commonly referred to as self-attention or intra-attention.

Inspired by the success of attention mechanisms in many sequence-based tasks, they introduced this attention-based architechture to perform node classification of graph-structured data.

The idea is to compute the hidden representations of each node in the graph, by attending over its neighbors, following a self-attention strategy.

## Properties of attention architecture
1. the operation is efficient, since it is parallelizable across node-neighbor pairs
2. it can be applied to graph nodes having different degrees by specifying arbitrary weights to the neighbors.
3. the model is directly applicable to inductive learning problems, including tasks where the model has to generalize to completely unseen graphs.

## Validation on chanlleging benchmarks
- Cora
- Citesser
- Pubmed citation networks
- Protein-protein interaction dataset

## GAT Architechture
- Graph Attentional Layer
    - perform self-attention on nodes - a shared attentional mechanism a, which computes attention coefficients:  
        ![eq1](images/eq1.png)
    - normalize the coefficients using the softmax function to makethem easily comparable across different nodes:  
        ![eq2](images/eq2.png)
    - In their experiments, the structure they use:  
        ![eq3](images/eq3.png)  
    Here || is the concatenation operation.
    - Once obtained, compute a linear combination using these normalized attention coefficients to sever as the final output features for every node (after potentially applying a nonlinearity, $\sigma$):  
        ![eq4](images/eq4.png)
    - multi-head attention:  
        ![eq5](images/eq5.png)  
    It implies K independent attention mechanisms execute the tranforamtion of last equation, and then their features are concatenated.
    - Specially, we employ averaging, and delay applying the final nonlineariry:  
        ![eq6](images/eq6.png)
## Pros compared with other methods:
- Computationally, it is highly efficient.   
Time complexity of a single GAT: O(|V|FF' + |E|F'), where F is the number of input features, and |V| and |E| are the numbers of nodes and edges in the graph, respectively.
- As opposed to GCNs, allows for (implicitly) assigning different importances to nodes of a same neighborhodd, enabling a leap in model capacity. Furthermore, leads to a benefits in interpretability.
- Does not depend on upfront access to the global graph structure or (features of) all of its nodes. It also means:  
    - the graph is not required to be undirected
    - directly applicable to inductive learning
- Compared with method of Hamilton et al. (2017), this model works with the entirety of the neighborhood, and does not assume any ordering within it.
- GAT can be reformulated as a particular instance of MoNet (Monti et al., 2016). Difference is our model uses node features for similarity computations, rather than the node’s structural properties.

## Evaluation
How to show result?

# Reference Papers Interested
- William L Hamilton, Rex Ying, and Jure Leskovec. Inductive representation learning on large graphs. Neural Information Processing Systems (NIPS), 2017. (https://arxiv.org/abs/1706.02216)

- Dzmitry Bahdanau, Kyunghyun Cho, and Yoshua Bengio. Neural machine translation by jointly
learning to align and translate. International Conference on Learning Representations (ICLR), 2015. (https://arxiv.org/pdf/1409.0473.pdf)

