# Quantum-Distance-Estimator-for-k-means-clustering
* In this project, we built an alternate approach to calculate distance 
of a point from all centroids, for classification in the k-means algorithm.
* We built an estimator using the fundamentals of qubits and implemented
it on a quantum simulator and a real quantum device.
* Lastly, we compare the results we obtained from real quantum computer and quantum simulator with
the results from classical k-means algorithm.
****

# K-Means Algorithm
K-Means Clustering is an Unsupervised Learning algorithm, which groups the unlabeled dataset into different clusters.

Here K defines the number of pre-defined clusters that need to be created in the process, as if K=2, 
there will be two clusters, and for K=3, there will be three clusters, and so on.

**It is an iterative algorithm that divides the unlabeled dataset
into k different clusters in such a way that each dataset belongs 
only one group that has similar properties.**

![kmeans.png](images%2Fkmeans.png)

# Distance Estimation (Classical)

The algorithm classifies a new point into a specific cluster based on it's distance
from the centroid of each clusters. 

Each point is represented by their coordinates on the plane and the 
algorithm uses **Euclidean distance** to estimate it's distance from 
each centroids.

`But how is the centroid of each clusters calculated?`

The algorithm sums up the coordinates of all points belonging to a cluster
in one dimension and divide that by the number of points in the cluster. We 
do this for each dimension and get the coordinates for the centroids.

![2.png](images%2F2.png)

After calculating Euclidean distance from each centroids: 

![3.png](images%2F3.png)

# Distance Estimation (Quantum)

With a classical one we can easily compute euclidean distances, 
but trying to do so on a quantum computer would be way harder 
and would require more qubits than we can afford to spare. 

The reason for this is that due to the probabilistic nature of qubits, phase differences 
and probability amplitudes are easily measurable, but things like the distance between 
two vectors are not.

We only need to determine the distances of each points from the clusters, 
so we can assign them to a specific group. We need a parameter 
that would allow us to figure out which centroid was closest. 

`This parameter does not have to be proportional to the distance, only positively correlated with it.`

There are many distance-like parameters that are available when 
we deal with qubits, like the **inner product** between two (normalized) vectors, 
and the **probabilities of measuring a qubit** in the `|0>` or the `|1>` states.

### Calculating distance using inner products

1. We start with a zero-initialized ancillary qubit and a quantum state Ψ, 
which stores the normalized vectors we want to estimate the distance between:

    ![q1.png](images%2Fq1.png)

    |x> is the position vector of the new data point we want to classify and |y> is the centroid of one of the clusters in our data


2. Apply a Hadamard gate to the ancillary qubit and put it into a superposition state

   ![q2.png](images%2Fq2.png)


3. Apply a controlled-swap on Ψ controlled by the ancillary qubit, this 
will entangle Ψ with our ancillary qubit
![q3.png](images%2Fq3.png)

4. Apply a Hadamrad to ancillary qubit again
![q4.png](images%2Fq4.png)

5. Substituting values P0 and P1
![q5.png](images%2Fq5.png)

6. Simplifying using expectation values
![q6.png](images%2Fq6.png)

7. Now we just have to show the right hand side of the equation is 
positively correlated with the Euclidean distance
![q7.png](images%2Fq7.png)


****
# Libraries Used

### Data Analysis
`numpy`, `pandas`, `matplotlib`

### Quantum

`qiskit`, `QuantumCircuit`, `QuantumRegister`, `ClassicalRegister`,
`Aer`, `execute`

# References

1. https://www.javatpoint.com/k-means-clustering-algorithm-in-machine-learning